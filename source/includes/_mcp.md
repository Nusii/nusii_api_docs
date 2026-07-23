# MCP Server

> The server URL is the same for every assistant:

```
https://app.nusii.com/mcp
```

Nusii has a built-in MCP ([Model Context Protocol](https://modelcontextprotocol.io)) server, so AI assistants like Claude, ChatGPT, and Gemini (and agent platforms like Microsoft Copilot Studio) can work with your Nusii account: summarize your proposals, draft new ones from your templates, and update pricing, straight from a chat.

The MCP server is the assistant-facing sibling of the REST API. It speaks MCP over Streamable HTTP, authenticates with the same OAuth tokens as the v2 API, and enforces the same permissions: an assistant can only see and do what the connected user can see and do in the app.

If you just want to connect an assistant, follow the step-by-step guides in [Connect AI assistants to Nusii](https://nusii.com/docs/integrations/ai-assistants/). This section documents the server itself: authentication, the available tools, write safety, rate limits, and logging.

## Connecting a client

> Add Nusii to Claude Code, for example:

```
claude mcp add --transport http nusii https://app.nusii.com/mcp
```

Any MCP client that supports remote servers (Streamable HTTP) with OAuth can connect. There is nothing to install and no API key to paste: on first use the client discovers Nusii's OAuth server, registers itself, and opens a browser window where you sign in with your normal Nusii login, pick an account, and approve access.

Setup guides for Claude, ChatGPT, Codex, and other assistants live in the [help center](https://nusii.com/docs/integrations/ai-assistants/). A client that only supports local servers can bridge to Nusii with [mcp-remote](https://www.npmjs.com/package/mcp-remote).

## MCP Authentication

> An unauthenticated request returns `401` with a pointer to the discovery document:

```
WWW-Authenticate: Bearer resource_metadata=
  "https://app.nusii.com/.well-known/oauth-protected-resource/mcp"
```

The server implements the standard MCP authorization flow, so clients connect without any manual OAuth setup:

- **Discovery.** Resource metadata at `/.well-known/oauth-protected-resource/mcp` (RFC 9728) points to the authorization server metadata at `/.well-known/oauth-authorization-server` (RFC 8414).
- **Dynamic client registration.** Clients register themselves at `/oauth/register` (RFC 7591). You don't need to create an OAuth app first.
- **Authorization code + PKCE.** The same flow described under [OAuth Authentication](#oauth-authentication). The user signs in, picks one of their accounts, and approves the requested scopes. The token is scoped to that account.

Endpoint | Purpose
-------- | -------
`POST /mcp` | The MCP endpoint (JSON-RPC over Streamable HTTP, Bearer token required)
`GET /.well-known/oauth-protected-resource/mcp` | Resource metadata (RFC 9728)
`GET /.well-known/oauth-authorization-server` | Authorization server metadata (RFC 8414)
`POST /oauth/register` | Dynamic client registration (RFC 7591)

The tokens are the same personal OAuth tokens the v2 API accepts: access tokens expire after 24 hours and MCP clients refresh them automatically. If you're building your own agent, any access token from the OAuth flow above works against `POST /mcp` as a Bearer header, no dynamic registration required.

### MCP Scopes

Scope | What it allows
----- | --------------
`read` | Required. The reporting and lookup tools.
`write` | Optional. The drafting and editing tools. Write tools are only advertised in `tools/list` when the token carries this scope.

Scopes are fixed at the moment the user approves the connection. To move an assistant from read-only to read/write, disconnect it and connect again, approving write access this time.

### 401 versus 403

A `401` means the token is missing, expired, or revoked; MCP clients react by (re)running the OAuth flow. A `403` means the token is valid but MCP access is switched off: either the MCP server isn't enabled for the account, or the team member's MCP access is disabled under [Settings → Team Members](https://app.nusii.com/settings/memberships). That's deliberately not a 401, so clients don't loop back into OAuth when re-authorizing won't help.

## MCP Tools

MCP tools are self-describing: `tools/list` returns each tool's name, description, and full input schema at runtime, so your client always sees the current contract. The tables below are an overview; the schemas your client fetches are the authoritative reference.

### Read tools

Available to every connection (the `read` scope):

Tool | Description
---- | -----------
`proposals_summary` | Proposal counts by status and the conversion rate over a period (a preset like `last_30_days`, or explicit `from`/`to` dates).
`templates_list` | The account's templates (id, name, dates), optionally filtered by name, with cursor pagination.
`template_details` | One template's full content: text sections, cost sections with line items, and the template total.
`clients_search` | Case-insensitive client lookup by name, company, or email.
`proposal_details` | A whole proposal for review: metadata, client, and every section in order.
`proposal_pricing` | A proposal's cost sections, line items, and totals, including per-unit, recurring, and range items.
`section_body` | One section's raw editor HTML, so rewrites can round-trip without destroying formatting.

### Write tools

Require the `write` scope, and only ever work on drafts and other unaccepted proposals:

Tool | Description
---- | -----------
`create_proposal_from_template` | Create a draft proposal from a template, optionally attaching a client by id or email (creating the client if needed).
`create_proposal` | Create a draft proposal from scratch, with optional sections and pricing built in a single transaction.
`create_section` | Add a text or cost section to a proposal, at an optional position.
`update_section` | Replace a section's title or body.
`update_line_items` | Batch-update line item names, amounts, and quantities. Atomic: one invalid item rolls back the whole batch.
`remove_line_items` | Delete line items from a proposal. Totals recalculate automatically.
`attach_client_to_proposal` | Set or replace a proposal's client, with the same id/email resolution as create.

### Tool limits

A few caps to know about when building on the write tools:

- 20 sections per `create_proposal` call, and 100 sections per proposal overall
- 50 line items per section
- 50,000 characters per section body
- `clients_search` returns at most 20 matches; `templates_list` pages 50 at a time
- Amounts are decimal strings (`"1250.00"`), never integers

## Drafts only, never sent

The write tools create and edit drafts. By design, there is no send tool: sending a proposal, and anything else a client sees, always happens in the app, by a person. Accepted proposals are locked to MCP entirely, just as they are in the editor.

Permissions mirror the app and the API. Every request resolves the token to its user, account, and role, so for example a team member on the Sales role only ever sees proposals they created, sent, or prepared. Removing a user from the account, or revoking the connection under [Settings → API](https://app.nusii.com/settings/api), cuts MCP access immediately.

<aside class="notice">
If you're building an autonomous agent on the MCP server, keep a human in the loop for write tools. Proposal, template, and client content returned by the read tools is data authored in the account (sometimes pasted from client emails): your agent should treat it as material to report on or edit, never as instructions to follow.
</aside>

## MCP Rate Limiting

The MCP endpoint is rate limited to 60 requests per minute per IP. If the limit is exceeded you will receive a response `HTTP 429 (Too Many Requests)`. Client registration is throttled separately.

## MCP Logs

Every authenticated MCP request is logged and viewable in the app under [Settings → API → MCP Logs](https://app.nusii.com/settings/mcp_logs), so you can see exactly what a connected assistant looked up or changed, and when.

For each request we record:

- The MCP method and tool name
- The tool arguments (filtered, never the response payload)
- The outcome and duration
- The connected client and user

Logs follow the same retention as API logs: 30 days, or 90 days on the Business plan. Owners and administrators see the whole account's requests; other roles see their own, or none, depending on their log permissions.
