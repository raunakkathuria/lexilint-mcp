# LexiLint MCP

Spell and grammar checking for AI assistants via [Model Context Protocol (MCP)](https://modelcontextprotocol.io/).

Works with **Claude Desktop**, **Cursor**, **ChatGPT**, and other MCP-compatible clients.

[![npm version](https://badge.fury.io/js/lexilint-mcp.svg)](https://www.npmjs.com/package/lexilint-mcp)
[![MCP Registry](https://img.shields.io/badge/MCP-Registry-blue)](https://registry.modelcontextprotocol.io/v0.1/servers?search=io.github.raunakkathuria/lexilint)

## Features

- **Offline spell checking** — en-US and en-GB are free, local, unlimited, and make no API calls.
- **BYOK grammar checking** — use Gemini, OpenAI, or Anthropic with your own provider key.
- **Eight supported dictionaries** — two free English variants plus six Premium languages: Spanish, French, German, Polish, Russian, and Turkish.
- **Combined checking** — run spelling and optional grammar together with `check_text`.
- **Private provider transport** — grammar text goes directly to the selected provider; LexiLint does not proxy it.

## Install and configure

### Claude Desktop and other JSON-configured clients

Configure one provider key as an environment variable. This keeps the key out of tool calls and conversation context.

```json
{
  "mcpServers": {
    "lexilint": {
      "command": "npx",
      "args": ["-y", "lexilint-mcp"],
      "env": {
        "GEMINI_API_KEY": "your-gemini-api-key"
      }
    }
  }
}
```

Provider environment variables:

| Provider argument | Environment variable | Access |
|---|---|---|
| `gemini` | `GEMINI_API_KEY` | Free for English grammar |
| `openai` | `OPENAI_API_KEY` | LexiLint Premium |
| `anthropic` | `ANTHROPIC_API_KEY` | LexiLint Premium |

Common Claude Desktop config locations:

- macOS: `~/Library/Application Support/Claude/claude_desktop_config.json`
- Windows: `%APPDATA%\Claude\claude_desktop_config.json`

Restart the client after changing its MCP configuration.

### Run directly

```bash
npx -y lexilint-mcp
```

You can also install it globally with `npm install -g lexilint-mcp`.

## Tools

### `spell_check` — free and offline

Checks spelling without an API key or network request.

```text
text      string   Text to spell-check
language  string   "en-US" or "en-GB" (default: "en-US")
```

### `grammar_check` — BYOK grammar, style, and clarity

```text
text        string   Text to grammar-check
provider    string   "gemini" | "openai" | "anthropic"
api_key     string   Optional per-call override for the provider environment variable
model       string   Optional provider model ID (Premium when custom)
license_key string   LexiLint licence key for Premium providers/languages/models
language    string   Language code (default: "en-US")
```

With `GEMINI_API_KEY` configured, a client can call the tool without putting the provider key in its arguments:

```json
{
  "text": "This are a test.",
  "provider": "gemini",
  "language": "en-US"
}
```

A non-empty per-call `api_key` remains supported as an explicit override and takes precedence over the selected provider environment variable:

```json
{
  "text": "This are a test.",
  "provider": "gemini",
  "api_key": "temporary-override-key",
  "language": "en-US"
}
```

Get a free Gemini key from [Google AI Studio](https://aistudio.google.com). Do not paste real keys into chat messages; prefer your MCP client's local environment configuration.

### `check_text` — combined spelling and optional grammar

Always runs the available spelling check. Add `provider` to request grammar; omit it to skip grammar without requiring a provider key.

```text
text        string   Text to check
language    string   Language code (default: "en-US")
provider    string   Optional; omit to skip grammar
api_key     string   Optional per-call override for the provider environment variable
model       string   Optional provider model ID (Premium when custom)
license_key string   LexiLint licence key for Premium providers/languages/models
```

## Models and Premium access

Default models are `gemini-3.8-flash`, `gpt-5.6-terra`, and `claude-sonnet-5`. A custom model requires LexiLint Premium:

```json
{
  "text": "This are a test.",
  "provider": "gemini",
  "model": "gemini-3.7-flash",
  "license_key": "your-lexilint-license-key"
}
```

| Feature | Free | Premium ($2.99/mo or $29.99 lifetime) |
|---|---|---|
| Spell check | en-US and en-GB, offline | Plus es, fr, de, pl, ru, tr |
| Gemini grammar | English, BYOK | All supported languages and custom models |
| OpenAI grammar | — | BYOK |
| Anthropic grammar | — | BYOK |

Get Premium: https://igniteapp.net/lexilint#premium

Customers provide only their provider key and, for Premium features, their LexiLint licence key. The runtime already contains the public application configuration needed to validate a licence with Polar; customers do not configure a LexiLint signing secret or organisation ID.

## Privacy and repository boundary

- Spell checking is local and sends no text anywhere.
- Grammar text goes directly to Google, OpenAI, or Anthropic according to the provider you select.
- LexiLint does not receive provider keys or grammar text.
- The public `raunakkathuria/lexilint-mcp` repository is a metadata-only registry mirror containing exactly `LICENSE`, `README.md`, `glama.json`, and `server.json`. Private source, builds, tests, source maps, and standalone prompt documentation are not published there.

## Links

- [npm package](https://www.npmjs.com/package/lexilint-mcp)
- [Website and docs](https://igniteapp.net/lexilint/mcp-spell-checker-claude-desktop)
- [Chrome Extension](https://igniteapp.net/lexilint/)
- [MCP Registry](https://registry.modelcontextprotocol.io/v0.1/servers?search=io.github.raunakkathuria/lexilint)

## Licence

LexiLint MCP is proprietary software distributed under the terms in [`LICENSE`](LICENSE). Installing the package does not open-source the private monorepo or grant redistribution rights.
