# Prompt 03 — Rewriting skill.md Aligned with Spec

**Context:** The original skill.md had Telegram Bot API, database.py, web_scraper.py — all out of scope. This prompt produced the clean rewrite.

---

## Problem identified

Original skill.md referenced:
- `database.py` — persistent storage (out of scope per spec)
- `web_scraper.py` — custom scraping code (out of scope)
- Telegram Bot API / Telethon — this is a Claude Skill, not a bot
- `/send_message`, `/sync_sheet` slash commands — out of scope
- Wrapped in ` ```markdown ``` ` — Claude can't read it properly

---

## Prompt

```
Tôi có spec.md (product spec) và skill.md (Claude Skill instruction file).

skill.md hiện tại có vấn đề:
- Reference database.py, web_scraper.py, Telegram Bot API — những thứ này OUT OF SCOPE theo spec
- Có /send_message, /sync_sheet commands — out of scope
- Bị wrap trong ```markdown``` block — sai format

Hãy viết lại skill.md từ đầu, aligned 100% với spec.md:
- 6-step linear flow: Parse Brief → Clarifying Questions → Discover → Score → Draft → Report
- Scoring rubric mirror 1:1 với spec (Influence brackets, Relevance brackets, Fit brackets)
- DM guardrails: ≤ 300 chars hard limit, no invented evidence, [GENERIC] label
- Edge cases table
- "What This Skill Does NOT Do" section để ngăn scope creep
- Không có database, không có Telegram API, không có /commands

skill.md là file mà Claude đọc khi skill được kích hoạt — nó phải là instructions, không phải architecture doc.
```

---

## Key distinction learned

**spec.md** = product specification (what & why, for humans and AI)
**skill.md / SKILL.md** = runtime instruction file (how to behave, for Claude only)

These serve different purposes. spec.md can be detailed and explanatory. SKILL.md must be precise and action-oriented — every sentence should tell Claude what to DO, not what something IS.

---

## Key insight

"Constraint as guardrails" — the "What This Skill Does NOT Do" section is as important as what it does. Without explicit negative constraints, AI will try to be helpful in ways that are out of scope (e.g., offering to send the Telegram messages directly).