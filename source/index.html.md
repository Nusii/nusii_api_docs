---
title: Nusii API Reference

language_tabs: # must be one of https://github.com/rouge-ruby/rouge/wiki/List-of-supported-languages-and-lexers
  - shell--curl: cURL
  - shell--cli: Nusii CLI
  - ruby

toc_footers:
  - <a href='https://app.nusii.com/settings/integrations'>Get your API Key</a>
  - <a href='https://github.com/Nusii/nusii-cli'>Nusii CLI on GitHub</a>

includes:
  - resources/account
  - resources/clients
  - resources/proposals
  - resources/sections
  - resources/line_items
  - resources/proposal_activities
  - resources/users
  - resources/themes
  - resources/webhooks
  - pagination
  - rate_limiting
  - errors

search: true

code_clipboard: true

meta:
  - name: description
    content: Documentation for the Nusii Proposal Software API
---

# Introduction

Welcome to the Nusii API. You can use our API to manage clients, proposals, sections, line items, and more.

We have examples in cURL, the [Nusii CLI](https://github.com/Nusii/nusii-cli), and Ruby. You can view code examples in the dark area to the right, and you can switch between them using the tabs in the top right.

# Nusii CLI

The [Nusii CLI](https://github.com/Nusii/nusii-cli) is a command-line tool for the Nusii API. It can be used standalone or with AI coding agents like Claude Code, Codex, and others.

It auto-detects piped output and returns JSON, supports `--no-input` for non-interactive use, and uses structured exit codes for automation.

```shell--cli
# Install with Homebrew
brew install nusii/tap/nusii

# Or install from source
go install github.com/nusii/nusii-cli@latest

# Login (saves your key to ~/.config/nusii/config.yaml)
nusii auth login --api-key YOUR_API_KEY

# Check auth status
nusii auth status
```

```shell--curl
# The Nusii CLI is an alternative to using cURL.
# Install: brew install nusii/tap/nusii
```

```ruby
# The Nusii CLI is an alternative to the Ruby gem.
# Install: brew install nusii/tap/nusii
```

# Authentication

> To authenticate:

```shell--curl
curl -X GET \
  -H 'User-Agent: Your App Name (www.yourapp.com)' \
  -H 'Content-Type: application/json' \
  -H "Authorization: Token token=YOUR_API_KEY" \
  "https://app.nusii.com/api/v2/account/me"
```

```shell--cli
nusii auth login --api-key YOUR_API_KEY
```

```ruby
require 'nusii-ruby'

Nusii.api_key = 'YOUR_API_KEY'
Nusii.user_agent = 'Your App Name (www.yourapp.com)'
```

> Make sure to replace `YOUR_API_KEY` with your API key.

All API requests require authentication. Include your API key in the Authorization header:

`Authorization: Token token=YOUR_API_KEY`

You can get your API key from [Settings > Integrations](https://app.nusii.com/settings/integrations).

<aside class="notice">
You must replace <code>YOUR_API_KEY</code> with your personal API key.
</aside>
