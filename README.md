# humanizer

<p>
  <a href="README.md"><b>English</b></a> |
  <a href="README.zh.md">繁體中文</a>
</p>

Cannibalized from [blader/humanizer](https://github.com/blader/humanizer) v2.11.1 (MIT), 2026-08-18.

Removes AI-writing tells from English prose, based on Wikipedia WikiProject AI Cleanup's "Signs of AI writing" (35 patterns).

## Why this one

The zh-Hant side is covered by `_ref-writing-structure` (sentence-structure rules) plus blog-writer's strict self-check. The English side had no voice QA at all: the translation service runs a flash-tier model, and flash-tier MT carries heavier AI tells than a Sonnet rewrite.

Scope: English prose. Does not overlap the zh-Hant rules.

## Local adaptation (2026-08-19)

Upstream ships this as a single 456-line SKILL.md. **Not one word of the 35 patterns changed** — every adjustment is structural or packaging.

| Change | Why |
|---|---|
| The 35 patterns moved to `references/PATTERNS.md` | Body drops from 6608 to 2194 tokens. It was over the 5000-token compaction boundary, so the tail was being dropped silently — and the tail is exactly *Check for false positives*, *What not to flag*, *How to return the result* and *Rewrite process*. What survived was 35 entries on what to flag. That leaves a tool that only accuses, never acquits, and does not know what to hand back. |
| Body keeps a numbered index of the 35 | `§7`, `§14` and friends have to resolve, and an agent needs to see the reach before it can decide whether to open the file. |
| `description` compressed to keywords plus zh-Hant triggers | Every skill's description is resident in the system prompt and shares one listing budget. |
| Added `LICENSE` | Upstream is MIT, and the attribution lived at SKILL.md line 452 — past the truncation point. A licence notice should not live only where it can be cut. |
| Added `.gitignore` | Matches the other skills: excludes `__pycache__` and local trails like `lessons.md`. |

**Unchanged**: the patterns themselves, the voice, the judgement calls, the three modes in *How to return the result*, and the four steps of *Rewrite process*. The upstream style is why this skill got adopted; it stays.

**No `disable-model-invocation`**: this is a "check what I just wrote" tool, and it earns its keep by the model reaching for it at the right moment.

## Upstream

- Source: https://github.com/blader/humanizer (MIT)
- Vendored version: 2.11.1
- Upstream also ships `agents/openai.yaml` for Codex; not vendored (Claude Code is the primary harness).
- The pattern catalogue derives from Wikipedia's "Signs of AI writing", CC BY-SA 4.0.
