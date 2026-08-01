---
name: raindrop-investigate
description: Diagnose and resolve issues in an AI app using Raindrop's Query API and hosted MCP tools — search events, inspect traces, quantify signals, and triage issues.
api: Raindrop Query API + MCP
generated: '2026-07-20'
method: generated
source: https://www.raindrop.ai/docs/integrations/skills (published skill: raindrop-investigate)
operations:
- 'GET https://query.raindrop.ai/v1/events/search'
- 'GET https://query.raindrop.ai/v1/traces'
- 'GET https://query.raindrop.ai/v1/signals'
- 'GET https://query.raindrop.ai/v1/conversations/{id}'
- 'MCP https://mcp.raindrop.ai/mcp (search_events, inspect_trace, triage_issue)'
---

# Raindrop Investigate

Systematically diagnose an AI agent failure with Raindrop. Raindrop's open-source `raindrop-investigate` skill drives its MCP tools; the steps below mirror it.

## Steps

1. Connect the Raindrop **MCP server** at `https://mcp.raindrop.ai/mcp` (OAuth 2.1, or `Authorization: Bearer <api-key>`), or use a Query API key.
2. Pull an activity overview: recent issues, top signals, event trends.
3. Search for the failure: `GET /v1/events/search` (semantic + keyword) to find the offending events; respect rate limits (search 50 RPM).
4. Inspect the trace: `GET /v1/traces` / MCP `inspect_trace` to walk model calls and tool spans and form a root-cause hypothesis.
5. Quantify: `GET /v1/signals` and `/v1/events/facets` to size the impact.
6. Triage: resolve, ignore, reopen, or reprioritize the issue (MCP `triage_issue`).

## Conventions

- Read-only Query API, bearer query key, `X-Raindrop-Project-Id` to scope. Limits: 200 RPM (50 RPM search, 20 RPS global).
- See `conventions/raindrop-conventions.yml`, `mcp/raindrop-mcp.yml`, `errors/raindrop-problem-types.yml`.
