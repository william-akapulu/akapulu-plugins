---
name: akapulu
description: >-
  Build on Akapulu Labs — live talking-avatar conversations and scripted
  clips. Use when creating a first scenario or hosted link, embedding a
  conversation in a web app, calling the connect API, using @akapulu/server
  or @akapulu/react-ui, knowledge bases, HTTP endpoints, or talking-avatar
  video clips.
metadata:
  author: akapulu
license: Apache-2.0
---

# Akapulu Labs

Live talking-avatar calls and scripted clips. Prefer the docs MCP (`akapulu-docs`, `https://docs.akapulu.com/mcp`) and OpenAPI for request shapes.

## First thing to build

If they just installed: API key in `.env` as `AKAPULU_API_KEY` (https://akapulu.com/api-keys), then a **Chat with Clara** scenario plus a hosted link.

Catalog Clara avatar id: `1f777f64-3758-4a7d-9cbc-c64ae654f7d1`.

`POST https://akapulu.com/api/scenarios/create/` with `Authorization: Bearer $AKAPULU_API_KEY`:

- `name`: `Chat with Clara`
- `nodes_json`: `initial_node` `greeting`; Clara role instruction (short spoken sentences, optional `{{runtime.first_name}}` only on the first line); greeting node asks what they want to build and `wrap_up` transitions to `close` after about five replies; `close` has `end_after_bot_response: true`
- `hosted_links`: Clara `avatar_id`, `runtime_vars.first_name` `""`, `stt_keywords` `Akapulu`, `Akapulu Labs`, `Clara`

Give them `hosted_links[0].url` and ask them to open it and click **Start Call**.

Exact payload: `agent-setup.md` in this repo (also https://docs.akapulu.com/agent-setup.md).

## After they try the hosted link

Point them at what they want next:

- **Embed in their app** — [Web SDK](https://docs.akapulu.com/web-sdk/overview), [prebuilt UI](https://docs.akapulu.com/examples/web-sdk/prebuilt-ui), [customized UI](https://docs.akapulu.com/examples/web-sdk/customized-ui). `@akapulu/server` on the backend with `AKAPULU_API_KEY`; `@akapulu/react` / `@akapulu/react-ui` in the browser.
- **Knowledge bases** — [guide](https://docs.akapulu.com/guides/knowledge-bases/overview)
- **HTTP endpoints** — [guide](https://docs.akapulu.com/guides/endpoints/create-endpoint)
- **More scenario stages / tools** — [scenarios](https://docs.akapulu.com/guides/scenarios/overview)
- **Scripted clips** — [clips](https://docs.akapulu.com/guides/clips/overview)

## API

Base `https://akapulu.com/api/`. Bearer `AKAPULU_API_KEY`. Create scenarios (with `hosted_links` on the same request), connect, updates, clips, knowledge bases, endpoints. Confirm fields with OpenAPI via the docs MCP.
