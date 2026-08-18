# humanizer

Cannibalized from [blader/humanizer](https://github.com/blader/humanizer) v2.11.1 (MIT), 2026-08-18.

Removes AI-writing tells from English prose, based on Wikipedia WikiProject AI Cleanup's "Signs of AI writing" (35 patterns).

## Why this one

The zh-Hant side is covered by `_ref-writing-structure` (sentence-structure rules) plus blog-writer's strict self-check. The English side had no voice QA at all: `stations/translate/config.yaml:19` runs `gemini-3.5-flash`, and flash-tier MT carries heavier AI tells than a Sonnet rewrite.

Scope: English prose. Does not overlap the zh-Hant rules.

## Upstream

- Source: https://github.com/blader/humanizer (MIT)
- Vendored version: 2.11.1
- Upstream also ships `agents/openai.yaml` for Codex; not vendored (Claude Code is the primary harness).
