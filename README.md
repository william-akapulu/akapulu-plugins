# Akapulu Labs agent plugins

Public skills for coding agents building on [Akapulu Labs](https://akapulu.com) (live avatar conversations and scripted clips).

## For humans

Paste this into Cursor, Claude Code, or Codex:

```text
Set up Akapulu Labs for me: fetch https://docs.akapulu.com/agent-setup.md and follow it.
```

That installs the `akapulu` skill and the [docs MCP](https://docs.akapulu.com/mcp). The agent sends you to https://akapulu.com/api-keys to create a key, then you activate it in your **terminal** with `export AKAPULU_API_KEY=...` (type the key there, not in chat). After that it creates a Clara hosted link you can try, then shares docs for a custom UI and the rest of the product.

## For agents

`agent-setup.md` is the installer. Skills live under `skills/`.
