# Onboard your agent to Akapulu Labs

> Official Akapulu Labs instructions that install the Akapulu skills and the docs MCP server into your coding agent in one shot.

These are official instructions from Akapulu Labs to set up a good AI development environment for building live avatar conversations and scripted clips. They are published at `https://docs.akapulu.com/agent-setup.md`, so you can verify their origin before following them. The same file lives in this repo for editing.

Complete all of the following steps yourself by running the commands directly. The only exceptions are steps explicitly marked **User step** — creating an API key and in-session MCP approval happen in the agent UI or the dashboard, so you cannot perform them. Never run a command that blocks on an interactive prompt.

Every command below is safe to re-run on a machine where setup already happened.

Do **not** stand up a hosted Akapulu account MCP or OAuth in this file. There is not one. The live plug for product knowledge is the **docs MCP**. Account actions use the customer’s **API key** on their server (REST + `@akapulu/server`), never in the browser and never pasted into chat.

---

## Install Akapulu skills and docs MCP

Every route installs the `akapulu` skill and wires the hosted docs MCP. Use the correct section for your agent below.

### Claude Code

```
npx -y skills add william-akapulu/akapulu-plugins --skill '*' --yes --global
```

Docs MCP:

```
claude mcp add --transport http akapulu-docs -s user https://docs.akapulu.com/mcp
```

> **User step.** Ask the user to reload plugins/skills if they do not appear, then confirm the `akapulu-docs` MCP shows as connected.

### Codex

```
npx -y skills add william-akapulu/akapulu-plugins --skill '*' --yes --global
```

Docs MCP:

```
codex mcp add akapulu-docs --url https://docs.akapulu.com/mcp
```

> **User step.** Ask the user to reload if prompted, then confirm the MCP is connected.

### Cursor, GitHub Copilot, Windsurf, Cline, opencode, Gemini, and all other agents

```
npx -y skills add william-akapulu/akapulu-plugins --skill '*' --yes --global
```

Docs MCP — add to `~/.cursor/mcp.json` (Cursor global) or `.cursor/mcp.json` (this project). Other clients: the equivalent MCP config file, same URL.

```json
{
  "mcpServers": {
    "akapulu-docs": {
      "url": "https://docs.akapulu.com/mcp"
    }
  }
}
```

If that file already has other servers, merge `akapulu-docs` into `mcpServers`. Do not overwrite unrelated servers.

> **User step.** Ask the user to reload or restart the agent so skills and MCP load. In Cursor, enable `akapulu-docs` if it appears in Settings → MCP.

---

## API key (User step)

Hosted links (`https://live.akapulu.com/session/{token}/`) do **not** need an API key. Embedding a conversation in the user’s app **does**.

If the user is embedding (SDK / connect route):

1. They create a key at https://akapulu.com/api-keys (dashboard, logged in).
2. They put it in **server** env (`AKAPULU_API_KEY` in `.env` / `.env.local` on the backend). Never in frontend code, never in chat.
3. They need a **scenario** at https://akapulu.com/scenarios.

Do not mint, guess, or paste a key yourself. Wait until they confirm the key is in server env before scaffolding a connect route.

If they only want a hosted link: skip the key. Point them at the dashboard scenario + hosted link, then stop.

---

## Report the result

Report what you actually verified. Do not print a checkmark for anything you could not confirm.

```
┌─ Akapulu Labs Agent Setup ───────────────────────────┐
│  skills         akapulu                              │
│  akapulu-docs   https://docs.akapulu.com/mcp         │
│  API key        server .env only (embed path)        │
│                                                      │
│  Reload or restart the agent to load the skills      │
└──────────────────────────────────────────────────────┘
```

Use `✓` verified, `⚠` needs a user action, `✗` failed. Follow the banner with the specific next action for every non-`✓` line.

Once the docs MCP is connected, verify with a cheap read: search for conversation connect, or confirm OpenAPI includes `POST /api/conversations/connect/`. Empty or thin search hits still count if the tool ran.

Do not install extra CLIs or SDKs in this file. After setup, the `akapulu` skill and the docs MCP are how you build (prebuilt UI, connect route, clips).

---

## Resources

- This repo: https://github.com/william-akapulu/akapulu-plugins
- Docs: https://docs.akapulu.com
- Docs MCP: https://docs.akapulu.com/mcp
- API keys: https://akapulu.com/api-keys
- Scenarios: https://akapulu.com/scenarios
- Prebuilt UI example: https://github.com/Akapulu/prebuilt-ui
- Cursor MCP: https://cursor.com/docs/mcp
- Claude Code MCP: https://docs.anthropic.com/en/docs/claude-code/mcp
