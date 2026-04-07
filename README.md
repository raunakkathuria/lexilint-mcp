# LexiLint MCP

Spell and grammar checking for AI assistants via [Model Context Protocol (MCP)](https://modelcontextprotocol.io/).

Works with **Claude Desktop**, **Cursor**, **ChatGPT**, and any MCP-compatible tool.

[![npm version](https://badge.fury.io/js/lexilint-mcp.svg)](https://www.npmjs.com/package/lexilint-mcp)
[![MCP Registry](https://img.shields.io/badge/MCP-Registry-blue)](https://registry.modelcontextprotocol.io/v0.1/servers?search=io.github.raunakkathuria/lexilint)

## Features

- 🔒 **100% offline spell check** — uses nspell with local dictionaries. Zero tokens consumed. Zero API calls. Works without internet.
- 🤖 **BYOK grammar check** — bring your own Gemini (free tier), OpenAI, or Claude API key. Your text goes directly to your chosen provider.
- 💰 **Zero token cost for spell check** — stop wasting AI tokens on typo detection
- 🌍 **8 languages** — English (US/UK), Spanish, French, German, Polish, Russian, Turkish
- ⚡ **Instant results** — no latency, no rate limits, unlimited usage

## Installation

### Claude Desktop / Cursor / ChatGPT

Add to your MCP config:

```json
{
  "mcpServers": {
    "lexilint": {
      "command": "npx",
      "args": ["-y", "lexilint-mcp"]
    }
  }
}
```

### npm

```bash
npm install -g lexilint-mcp
```

## Usage

Once installed, your AI assistant can use these tools:

- `spell_check` — check text for spelling errors (100% offline)
- `grammar_check` — check text for grammar issues (requires API key)

### Example

> "Use the spell_check tool to check this text: 'Ths is a tset'"

The spell check runs locally — no tokens consumed.

## Token Cost Comparison

| Method | Cost per 500-word check |
|--------|------------------------|
| Ask AI directly ("fix typos in this") | ~$0.02 (GPT-4) / ~$0.015 (Claude) |
| **LexiLint MCP spell_check** | **$0.00** |

## Grammar Check Setup

Grammar checking uses your own API key (BYOK):

1. Get a free [Google Gemini API key](https://aistudio.google.com)
2. Set the environment variable:

```json
{
  "mcpServers": {
    "lexilint": {
      "command": "npx",
      "args": ["-y", "lexilint-mcp"],
      "env": {
        "GEMINI_API_KEY": "your-key-here"
      }
    }
  }
}
```

Supported providers: `GEMINI_API_KEY`, `OPENAI_API_KEY`, `ANTHROPIC_API_KEY`

## Links

- 📦 [npm package](https://www.npmjs.com/package/lexilint-mcp)
- 🌐 [Website & docs](https://igniteapp.net/lexilint/mcp-spell-checker-claude-desktop)
- 🧩 [Chrome Extension](https://igniteapp.net/lexilint/)
- 📋 [MCP Registry](https://registry.modelcontextprotocol.io/v0.1/servers?search=io.github.raunakkathuria/lexilint)

## License

MIT
