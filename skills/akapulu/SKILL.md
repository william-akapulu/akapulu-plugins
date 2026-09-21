---
name: akapulu
description: >-
  Build on Akapulu Labs — live talking-avatar conversations and scripted
  clips. Use when creating a first scenario or hosted link, embedding a
  conversation in a web app, using @akapulu/server or @akapulu/react-ui,
  knowledge bases, HTTP endpoints, or talking-avatar video clips.
metadata:
  author: akapulu
license: Apache-2.0
---

# Akapulu Labs

Live talking-avatar calls and scripted clips. Prefer the docs MCP (`akapulu-docs`, `https://docs.akapulu.com/mcp`) for request shapes.

## First thing to build

API key: they create it at https://akapulu.com/api-keys. The env var is `AKAPULU_API_KEY` — set it however this project already loads secrets. Then a **Chat with Clara** scenario plus a hosted link.

Catalog Clara avatar id: `1f777f64-3758-4a7d-9cbc-c64ae654f7d1`.

`POST https://akapulu.com/api/scenarios/create/` with `Authorization: Bearer $AKAPULU_API_KEY`. Payload is in https://docs.akapulu.com/agent-setup.md.

Give them `hosted_links[0].url` and ask them to open it and click **Start Call**.

## After they try the hosted link

Send docs:

- Custom UI: https://docs.akapulu.com/examples/web-sdk/customized-ui
- Web SDK: https://docs.akapulu.com/web-sdk/overview
- Prebuilt UI: https://docs.akapulu.com/examples/web-sdk/prebuilt-ui
- Knowledge bases: https://docs.akapulu.com/guides/knowledge-bases/overview
- HTTP endpoints: https://docs.akapulu.com/guides/endpoints/create-endpoint
- Scenarios: https://docs.akapulu.com/guides/scenarios/overview
- Clips: https://docs.akapulu.com/guides/clips/overview
