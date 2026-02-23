BD Agent — Lead Research & Telegram Outreach Skill
BD Agent is a Claude Skill that turns a campaign brief into an auto‑researched, qualified lead list plus personalized Telegram outreach drafts. It’s built for BD / Partnerships who want to go from idea → people → messages in a single run, without writing code or setting up infrastructure.

🔍 What It Does
BD Agent runs a deterministic pipeline:

Understand the campaign

Parses your brief to extract ICP, key topics (e.g., Polymarket / prediction markets), tone, languages, and goals.

Auto‑discover leads (default path)

Uses web search to find relevant KOLs / founders / partners around the specified niche.

Extracts topics, language, and personality from public bios and content.

Score & tier leads

Scores each lead on:

Relevance (topic match)

Influence (reach / role)

Fit (tone & angle alignment)

Assigns Tier A / B / C with short evidence‑based notes.

Draft Telegram DMs

Generates per‑lead DM drafts for Tier A/B:

References real topics they talk about.

Adapts tone to your campaign + their style.

Aligns CTA with your stated goal (call, feedback, post…).

Return one Markdown report

Campaign summary

Lead scorecard table

DM drafts grouped by tier

All logic is specified in spec.md.

🧑‍💼 Who It’s For
BD / Partnerships / Founders running GTM or collab campaigns.

Non‑technical teammates who want a reusable research + outreach workflow inside Claude Projects.

No setup of React, Node, DB, or Telegram bots is required; everything runs as a single skill.

📁 Project Structure
text
.
├── spec.md        # Full skill specification: problem, rubric, workflow, outputs
└── README.md      # High-level overview (this file)
If you later add implementation files (prompt, examples, etc.), you can extend this tree, but spec.md stays the canonical design doc.

⚙️ How to Use (Conceptual)
Open the skill in Claude Projects / Custom GPT.

Paste your campaign brief when prompted.

Answer 3 clarifying questions (goal, tone, hard filters).

Optionally provide a few “must‑include” leads.

Run the skill and review the Markdown report:

Pick Tier A/B leads you like.

Copy Telegram DMs, edit if needed, and send.

Implementation details (clarifying questions, scoring rubric, DM rules, edge cases) are all defined in spec.md so devs or prompt‑engineers can follow exactly.

🔮 Future Directions (High Level)
Add multi‑channel drafting (X / LinkedIn / email) on top of the same lead scoring.

Allow saving previous runs into a lightweight lead history.

Plug into automation tools/bots to actually send messages once the skill is stable.

For all behavior, constraints, and acceptance criteria, see spec.md.
