# Request Logs

Every request made to the API is logged and viewable in the app under [Settings → API → API Logs](https://app.nusii.com/settings/api_logs), so you can see exactly what your integration is sending and debug it when something looks off.

For each request we record:

- The HTTP method and path
- The request parameters
- The response status and JSON response body
- The duration and user agent
- The API token that made the request

You can filter the list by API token (including revoked tokens), and click any request to see its full parameters and response. Response bodies are truncated at 64 KB.

Logs are kept for 30 days, or 90 days on the Business plan. Viewing them requires the "View API logs" permission, so account owners can control which team members have access.
