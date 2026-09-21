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

Akapulu Labs is a platform for AI avatars. Docs: https://docs.akapulu.com. Docs MCP: `akapulu-docs` (`https://docs.akapulu.com/mcp`). REST: `https://akapulu.com/api/` with Bearer `AKAPULU_API_KEY`.

**Live conversations.** A talking avatar joins a video call. A **scenario** is the behavior (persona, stages, tools). An **avatar** is the face and voice — public catalog at https://akapulu.com/catalog.

**Hosted link.** A public URL for a scenario. Anyone opens it and clicks Start Call.

**Embed.** Web SDK in their app: `@akapulu/server` on the backend, `@akapulu/react` or `@akapulu/react-ui` in the browser. https://docs.akapulu.com/web-sdk/overview

**Scenarios.** One `role_instruction` plus **nodes** (stages) with `task_instruction`. Tools on a node: **transition** (move to another node), **HTTP endpoint**, **knowledge base**, **vision**. https://docs.akapulu.com/guides/scenarios/overview

**Endpoints.** Saved HTTP calls the avatar can make during a live call. https://docs.akapulu.com/guides/endpoints/create-endpoint

**Knowledge bases.** Documents the avatar can search during a call. https://docs.akapulu.com/guides/knowledge-bases/overview

**Clips.** Talking-avatar video from a script. Offline, not a live call. https://docs.akapulu.com/guides/clips/overview

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
