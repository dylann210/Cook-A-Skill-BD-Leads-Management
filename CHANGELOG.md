# Changelog

All notable changes to the BD Agent Spec are documented here.

Format: `[version] YYYY-MM-DD — description`

---

## [1.1.1] 2026-02-25

### Rewritten — `skill.md`

Complete rewrite of the Claude Skill instruction file to align with `spec.md` v1.1.0.

**Removed (were out of scope per spec):**
- Outer ` ```markdown ``` ` wrapper — file is now clean Markdown.
- References to `database.py`, `web_scraper.py`, `main.py` — spec explicitly excludes persistent storage and custom code.
- Telegram Bot API / Telethon integration — the skill is a Claude Skill, not a bot.
- `/send_message` and `/sync_sheet` slash commands — out of scope.
- Google Sheets sync — out of scope.

**Added / Aligned:**
- 6-step linear flow matching spec: Parse Brief → Clarifying Questions → Discover → Score → Draft → Report.
- Scoring rubric updated to spec v1.1.0 brackets (Relevance, Influence with 6-level follower table, Fit).
- Role prominence +1 adjustment rule for Influence score.
- Hard ≤ 300-character limit on all DMs with trimming instruction.
- Edge cases table (too few leads, no follower data, conflicts, language mismatch, DM over limit).
- Explicit "What This Skill Does NOT Do" section to prevent scope creep.
- DM draft output format with character count annotation and `[GENERIC]` label pattern.

---

## [1.1.0] 2026-02-25

### Changed — `spec.md`

**Section 7.2 — Scoring Rubric: Influence score brackets added**
- Replaced vague "coarse brackets" description with a concrete 6-level follower bracket table (< 1K → > 500K), each mapped to a specific score range.
- Added role-prominence adjustment rule: confirmed prominent roles (VC partner, protocol co-founder, known CT figure) grant +1 to bracket score, max 10.
- Added `Influence: estimated` label when no follower data is available.

**Section 8 — DM Guardrails: hard character limit added**
- Added hard limit of **≤ 300 characters** per Telegram DM.
- Rationale: Telegram DMs beyond this length have significantly lower read rates; the skill must trim aggressively.
- Updated Section 11 success criteria to reflect the 300-char requirement.

**Section 11.1 — Pre-Demo web_search Discovery Validation (new)**
- Added a Day 2 smoke-test gate for `web_search` discovery across 3 different niches.
- Each niche must return ≥ 5 scoreable profiles to pass.
- Failure condition triggers immediate query construction review before demo day.

**Section 12 — Full Sample Output (new)**
- Added a complete end-to-end output example using a PredictDAO beta outreach campaign.
- Includes: Executive Summary, Lead Scorecard (5 leads across all tiers), and Telegram DM Drafts (Tier A × 2, Tier B × 2 including one GENERIC-flagged draft).
- All DMs in the sample are within the 300-char limit with character counts noted.

---

## [1.0.0] 2026-02-24

### Added — `spec.md`

- Initial spec created.
- Sections: Objective, Problem Statement, Business Value, Scope, Input Contract, Clarifying Questions, Lead Discovery & Scoring, Outreach Drafting, Output Structure, Edge Cases, MVP Success Criteria.
- Scoring rubric: 3 dimensions (Relevance / Influence / Fit), 0–30 total, Tier A/B/C mapping.
- Telegram DM format: Hook → Bridge → Soft CTA, 2–4 sentence guardrail.
- Output: Markdown report with Executive Summary, Lead Scorecard, and DM Drafts sections.