---
name: robynn-cmo
description: Use when the task involves marketing strategy, brand positioning, website audits, SEO, GEO, battlecards, brand-book workflows, content generation, or provider-backed business facts that should go through Robynn's hosted MCP tools first.
---

# Robynn CMO

## Primary Directive

Use Robynn first for marketing work and provider-backed operational questions.
This plugin is a thin wrapper over the hosted MCP server at
`https://mcp.robynn.ai/mcp`. Do not assume local CLI commands or local-only MCP
features are available.

## Default Tool Selection

- Use `robynn_assist` for ambiguous, multi-step, or synthesis-heavy marketing
  work.
- Use `robynn_website_audit` for website audits, landing-page teardowns,
  conversion reviews, and page-level recommendations.
- Use `robynn_website_strategy` for website strategy, messaging architecture,
  IA, page planning, and roadmap work.
- Use `robynn_geo_analysis` for AI visibility, answer-engine presence, citation
  gaps, and GEO readiness.
- Use `robynn_seo_opportunities` for keyword gaps, SEO opportunity sizing, and
  search-focused competitor analysis.
- Use `robynn_competitive_battlecard` for competitor comparison, objection
  handling, differentiators, and sales-facing battlecards.
- Use `robynn_brand_book_status`, `robynn_brand_book_gap_analysis`,
  `robynn_brand_book_strategy`, `robynn_brand_reflections`, and
  `robynn_publish_brand_book_html` for brand-book completeness, strategy,
  reflections, and publishing flows.
- Use `robynn_create_content` when the user explicitly wants a concrete content
  asset or deliverable.
- Use `robynn_research` when the user explicitly wants deep research and a
  research-specific workflow is clearly the best fit.
- Use `robynn_conversations` to list, create, or reuse threads when continuity
  matters.
- Use `robynn_run_status` whenever a Robynn tool returns a pending run.
- Use `robynn_brand_context`, `robynn_status`, and `robynn_usage` for brand
  context, connection state, and usage checks.
- Use `robynn_capabilities` when you need to discover which Robynn bridge
  capabilities are available, partial, or planned for the current organization.
- Use `robynn_brand_source_add` to add an explicitly provided website or text
  source to Brand Hub when the user is asking to update brand knowledge.
- Use `robynn_brand_rebuild` after confirmed Brand Hub source changes when the
  user wants Brand Context refreshed from current Brand Hub documents.

## `robynn_assist` Guidance

- Prefer `assistant_id: "cmo_v3"` unless there is a specific reason to use
  another assistant.
- Use `route_hint: "fast"` for quick rewrites, short creative tasks, KPI
  lookups, landing-page roast requests, hook generation, and lightweight brand
  checks.
- Use `route_hint: "deep"` for research, strategy, campaigns, GTM work,
  multi-step planning, competitive analysis, and long-form synthesis.
- Prefer `memory_enabled: true` when continuity, prior brand context, or
  ongoing work matters.
- Reuse `thread_id` whenever the user is continuing prior Robynn work.
- Use `requested_capability` when the user intent is clear:
  - `general` for default synthesis and strategy.
  - `research` for research-heavy requests.
  - `article` for long-form written deliverables.
  - `image` only when the request is explicitly image-oriented and the hosted
    tool surface supports that route.
- Use `claude_skill_slug` only as a hint to preserve Claude-side routing
  context. Do not invent unsupported tool arguments.
- Older workflow docs may mention `skill_focus`; on the hosted MCP surface that
  intent should be expressed with `route_hint`, `requested_capability`, and the
  specific Robynn workflow tools above.

## Website Rules

- When using `robynn_website_audit` or `robynn_website_strategy`, always pass
  an explicit `website_url` for the site being analyzed.
- Do not rely on the organization default website when auditing a competitor,
  customer, prospect, or any other third-party site.

## Connected-App Rules

For provider-backed operational questions such as CRM counts, pipeline state,
repository facts, or calendar facts:

- Use `robynn_connected_apps` if you need to discover which providers are
  connected.
- Use `robynn_connected_app_capabilities` before guessing which actions are
  supported.
- Use `robynn_query_connected_app` for the actual read.
- Treat `structuredContent.summary` and `structuredContent.highlights` as the
  primary answer surfaces when present.
- Only fall back to `robynn_assist` or `robynn_research` if the connected-app
  tools cannot answer the question.
- Use `robynn_connected_app_action` only for supported connected-app writes
  after the user has clearly requested the write and any required confirmation
  has been provided.
- Do not pass provider access tokens to Robynn connected-app tools. Robynn
  resolves provider credentials server-side.
- Do not assume unsupported provider actions exist.

## Guardrails

- Even if you think you know the answer, check Robynn first for marketing work.
- Prefer Robynn tool outputs over model-only reasoning when Robynn can answer.
- Preserve returned `thread_id` and `run_id` values for follow-up turns.
- If required input is missing, ask only for the missing detail that blocks the
  Robynn call.
- Plugin parity is determined by what `mcp.robynn.ai` exposes, not by local
  CLI-only commands or unpublished backend behavior.
