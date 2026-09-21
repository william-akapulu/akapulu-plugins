---
name: akapulu
description: >-
  Build on Akapulu Labs — live talking-avatar conversations and scripted
  clips. Use when embedding a conversation in a web app, creating a hosted
  link, calling POST /api/conversations/connect/, using @akapulu/server or
  @akapulu/react-ui, or generating talking-avatar video clips.
metadata:
  author: akapulu
license: Apache-2.0
---

# Akapulu Labs

Start here for customer integrations. Prefer the **docs MCP** (`akapulu-docs`, `https://docs.akapulu.com/mcp`) and OpenAPI over memory. Do not invent scenario ids, avatar ids, or API keys.

## Two products (do not mix)

| Path | What it is | API key? |
| --- | --- | --- |
| **Hosted link** | Share `https://live.akapulu.com/session/<token>/`. Visitor hits Akapulu’s page. Create the link in the dashboard on a scenario. | No |
| **Embed in their app** | Their server calls connect; browser mounts `@akapulu/react` / `@akapulu/react-ui`. | Yes — **server only** (`AKAPULU_API_KEY`) |

If they only want a URL, stop after the dashboard hosted-link flow. Do not scaffold an SDK app.

## Embed path (golden)

1. **User step:** key at https://akapulu.com/api-keys → `AKAPULU_API_KEY` in **backend** `.env`. Scenario at https://akapulu.com/scenarios. Never put the key in the client or in chat.
2. Clone [prebuilt-ui](https://github.com/Akapulu/prebuilt-ui) (Express connect + Vite `AkapuluConversation`) unless they already have an app — then add a server connect route with `@akapulu/server` and the React UI in the browser.
3. Docs: [Prebuilt UI](https://docs.akapulu.com/examples/web-sdk/prebuilt-ui), [connect](https://docs.akapulu.com/api-reference/conversations/connect). Confirm shapes with docs MCP / OpenAPI.

`@akapulu/server` stays on the server. `@akapulu/react` / `@akapulu/react-ui` stay in the browser. Connect returns Daily room + token; the client does not call Akapulu with the secret key.

## Source of truth

- Docs MCP search + filesystem (pages as `.mdx`, OpenAPI under `/openapi/`).
- REST: `https://akapulu.com/api/` with `Authorization: Bearer <key>` for list/create scenarios, connect, updates, clips, knowledge bases. Avatars and billing are dashboard / session-auth today — do not pretend they are on the public API unless OpenAPI says so.
- Never claim an endpoint cannot do something without checking OpenAPI or the docs MCP first.

## Clips

Scripted talking-avatar video is a separate API (`/api/clips/`). No Web SDK. See docs clips guides.
