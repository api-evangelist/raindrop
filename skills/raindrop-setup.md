---
name: raindrop-setup
description: Instrument an app so its AI agent runs are tracked in Raindrop — find AI call sites, pick the right SDK/integration, and wire up event tracking.
api: Raindrop Ingest API
generated: '2026-07-20'
method: generated
source: https://www.raindrop.ai/docs/integrations/skills (published skill: raindrop-setup)
operations:
- 'POST https://api.raindrop.ai/v1/events/track'
- 'POST https://api.raindrop.ai/v1/signals/track'
- 'POST https://api.raindrop.ai/v1/users/identify'
---

# Raindrop Setup

Instrument an application so its AI agent activity is observable in Raindrop. Raindrop's own open-source `raindrop-setup` skill (github.com/raindrop-ai/skills) automates this; the steps below mirror it.

## Steps

1. Get a **write key** from app.raindrop.ai and export it (e.g. `RAINDROP_WRITE_KEY`).
2. Choose the integration: a first-party SDK (`raindrop-ai` on npm or PyPI, Go, Rust beta, Java beta, browser) or a framework auto-tracer (LangChain, CrewAI, Vercel AI SDK, OpenAI Agents SDK, Claude Agent SDK, etc.), or the raw HTTP API.
3. Locate every AI call site (model calls, tool calls, agent turns).
4. Track interactions: `POST /v1/events/track` with a JSON array of events (`user_id`, `event`, `ai_data.model/input/output`). Keep each event under 1 MB.
5. Attach feedback via `POST /v1/signals/track` (e.g. `thumbs_up`/`thumbs_down`, edits) and user context via `POST /v1/users/identify`.
6. Confirm ingest: authorized requests return **204**. Send `Authorization: Bearer <write key>`; optionally scope with `X-Raindrop-Project-Id`.

## Conventions

- Auth: bearer write key. Errors: `{ "error": { "code", "message" } }` (not RFC 9457).
- See `conventions/raindrop-conventions.yml`, `authentication/raindrop-authentication.yml`, `errors/raindrop-problem-types.yml`.
