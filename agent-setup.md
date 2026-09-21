# Onboard your agent to Akapulu Labs

> Official Akapulu Labs instructions that install the Akapulu skills and the docs MCP, then create a first scenario and hosted link.

These are official instructions from Akapulu Labs, published at `https://docs.akapulu.com/agent-setup.md`.

Run the commands in this file. **User step** means ask the human to do it.

## 1. Install skills and docs MCP

### Claude Code

```
npx -y skills add william-akapulu/akapulu-plugins --skill '*' --yes --global
```

```
claude mcp add --transport http akapulu-docs -s user https://docs.akapulu.com/mcp
```

> **User step.** Reload skills if they do not appear. Confirm `akapulu-docs` is connected.

### Codex

```
npx -y skills add william-akapulu/akapulu-plugins --skill '*' --yes --global
```

```
codex mcp add akapulu-docs --url https://docs.akapulu.com/mcp
```

> **User step.** Reload if prompted. Confirm the MCP is connected.

### Cursor and other agents

```
npx -y skills add william-akapulu/akapulu-plugins --skill '*' --yes --global
```

Add the docs MCP to `~/.cursor/mcp.json` (or this project's `.cursor/mcp.json`). Merge into `mcpServers` if the file already exists:

```json
{
  "mcpServers": {
    "akapulu-docs": {
      "url": "https://docs.akapulu.com/mcp"
    }
  }
}
```

> **User step.** Reload the agent. In Cursor, enable `akapulu-docs` under Settings → MCP.

## 2. API key

> **User step.** Open https://akapulu.com/api-keys and create a key.

The env var name is `AKAPULU_API_KEY`. Put it in this project however env vars are already loaded.

Wait until `AKAPULU_API_KEY` is set, then continue.

## 3. First scenario and hosted link

Create a live Clara conversation (greeting, then a short wrap-up) with catalog avatar Clara (`1f777f64-3758-4a7d-9cbc-c64ae654f7d1`).

```
curl -sS https://akapulu.com/api/scenarios/create/ \
  -H "Authorization: Bearer $AKAPULU_API_KEY" \
  -H "Content-Type: application/json" \
  -d @- <<'EOF'
{
  "name": "Chat with Clara",
  "nodes_json": {
    "initial_node": "greeting",
    "role_instruction": "You are Clara, a friendly guide from Akapulu Labs. Speak in short natural sentences that will be read aloud. Do not use symbols, abbreviations, digits, URLs, markdown, or lists. Spell out any numbers as words. Keep each reply to one or two sentences. The visitor's first name is {{runtime.first_name}}. Use that first name only in the very first line of your first greeting, and only if it is not blank and you are confident how to pronounce it. If it is blank, unusual, or you are unsure of the pronunciation, skip the name. After that first line, never use their name again.",
    "nodes": {
      "greeting": {
        "task_instruction": "Greet the visitor warmly and introduce yourself as Clara from Akapulu Labs. If you can use their first name, use it only in the first line of this first greeting, then never use it again. Ask what they want to build with Akapulu Labs. Keep replies brief. Ask follow-up questions about their use case and stay in this conversation. Do not call wrap_up after the first couple of replies. After about five of their replies, once you have a sense of what they want, call wrap_up.",
        "respond_immediately": true,
        "functions": [
          {
            "name": "wrap_up",
            "type": "transition",
            "description": "Move to the short closing message after about five visitor replies, once you have a sense of what they want to build. Do not call this after only one or two replies.",
            "transition_to": "close"
          }
        ]
      },
      "close": {
        "task_instruction": "Acknowledge what they just said in one short sentence. Then wrap up the call: say you have to end the call now, and if they want more conversations like this they can start building today or get in touch. End with a warm goodbye. Keep the whole reply to two or three short sentences.",
        "respond_immediately": true,
        "end_after_bot_response": true
      }
    }
  },
  "hosted_links": [
    {
      "avatar_id": "1f777f64-3758-4a7d-9cbc-c64ae654f7d1",
      "label": "Chat with Clara",
      "runtime_vars": { "first_name": "" },
      "stt_keywords": ["Akapulu", "Akapulu Labs", "Clara"]
    }
  ]
}
EOF
```

Read `hosted_links[0].url` from the response (a `https://live.akapulu.com/session/...` link).

> **User step.** Ask them to open that URL and click **Start Call**. That is a live talking-avatar conversation on their account.

## 4. After they try the link

Send them these docs:

- Custom UI: https://docs.akapulu.com/examples/web-sdk/customized-ui
- Web SDK: https://docs.akapulu.com/web-sdk/overview
- Prebuilt UI: https://docs.akapulu.com/examples/web-sdk/prebuilt-ui
- Knowledge bases: https://docs.akapulu.com/guides/knowledge-bases/overview
- HTTP endpoints: https://docs.akapulu.com/guides/endpoints/create-endpoint
- Scenarios: https://docs.akapulu.com/guides/scenarios/overview
- Clips: https://docs.akapulu.com/guides/clips/overview

When you finish, give them the hosted link URL.
