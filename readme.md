
# BD Agent

**AI Business Development Agent for Lead Research, CRM & Outreach**

BD Agent helps you:

1. **Research** leads and enrich them with insights.  
2. **Manage** leads in a lightweight, insight‑driven CRM.  
3. **Reach out** automatically with personalized messages (Telegram in MVP, multi‑platform later). [crmchat](https://crmchat.ai)

> **MVP:** Telegram‑only outreach, orchestrated by **OpenClaw** agents  
> **Future:** Multi‑platform (Telegram, X, LinkedIn, Email, …) [techcrunch](https://techcrunch.com/2026/01/30/openclaws-ai-assistants-are-now-building-their-own-social-network/)

***

## Features

### 1. Research: Lead Discovery & Insights

- Create **research tasks** describing what kind of leads you want (e.g. “50 crypto KOLs talking about Polymarket”).  
- Provide candidate profiles/handles; an OpenClaw‑powered agent:
  - Reads public info (bio / sample posts).  
  - Generates topics of interest, tone/personality, and a short insight summary for each lead.  
  - Suggests tags like `["KOL", "Crypto", "Polymarket"]`. [crawleyagent](https://crawleyagent.com)

### 2. Lead Management: Insight‑Driven Mini CRM

- Central **Lead Database** with:
  - Name, Telegram handle, source (research/manual).  
  - Status: `NEW`, `RESEARCHED`, `CONTACTED`, `REPLIED`, `QUALIFIED`, `CLOSED`.  
  - Topics & interests.  
  - Personality notes and free‑form internal notes. [themindreader](https://themindreader.ai/blog-insights/ai-in-customer-relationship-management)
- **Lead list view** with filters (status, topic, source) and last contacted/replied.  
- **Lead detail view** with profile, insight summary, notes, and Telegram message timeline.

### 3. Outreach: Personalized Messaging Agent (Telegram MVP)

- Connect your **Telegram** account/bot.  
- Use an OpenClaw agent to run **outreach campaigns** for segments from your lead DB:
  - One‑off broadcasts (e.g. New Year greetings).  
  - Simple 2‑step sequences (initial + follow‑up). [crmchat](https://crmchat.ai/telegram-outreach)
- AI‑assisted templates:
  - Variables: `{first_name}`, `{topics}`, `{personality}`, `{custom_note}`.  
  - Tone adaptation based on personality (casual vs formal). [leadspicker](https://www.leadspicker.com/ai-sales-tools/humanatic)
- Safe sending:
  - Daily send limit, time windows, random delays.  
- Automatic updates:
  - Sent → status to `CONTACTED`.  
  - Reply detected → status to `REPLIED` and logged in the timeline.

***

## Tech Stack (MVP)

- **Agent Orchestration:** OpenClaw (AI agent framework to run research & outreach workflows) [en.wikipedia](https://en.wikipedia.org/wiki/OpenClaw)
- **Frontend:** React, TypeScript, Tailwind CSS  
- **Backend:** Node.js, Express  
- **Database:** PostgreSQL or SQLite  
- **Messaging:** Telegram Bot API  
- **LLM Provider:** Claude/OpenAI (called from OpenClaw tools for insights & personalization)

> Next versions reuse the same OpenClaw agent layer to add X, LinkedIn and email channels.

***

## Project Structure

```text
├── client/                         # Frontend (React + TypeScript + Tailwind)
│   └── src/
│       ├── components/
│       ├── pages/
│       ├── features/
│       │   ├── research/           # Research tasks & enrichment UI
│       │   ├── leads/              # Lead list, detail, notes
│       │   └── campaigns/          # Telegram campaigns & stats
│       └── utils/
│
├── server/                         # Backend (Node.js + Express + OpenClaw)
│   └── src/
│       ├── routes/
│       ├── controllers/
│       ├── services/
│       │   ├── researchAgent/      # OpenClaw workflows for research
│       │   ├── leadService/        # Lead CRUD & pipeline logic
│       │   └── telegramOutreach/   # OpenClaw workflows for campaigns
│       ├── integrations/           # Telegram, LLM, future X/LinkedIn
│       ├── jobs/                   # Background workers (campaign queues)
│       ├── models/                 # DB schemas
│       └── utils/
│
└── README.md
```

***

## Core Data Models (Conceptual)

```ts
Lead {
  id: string;
  name?: string;
  telegramHandle: string;
  source: 'RESEARCH_TASK' | 'MANUAL';

  status: 'NEW' | 'RESEARCHED' | 'CONTACTED' | 'REPLIED' | 'QUALIFIED' | 'CLOSED';

  topics: string[];
  personality?: string;
  notes?: string;

  createdAt: Date;
  updatedAt: Date;
  lastContactedAt?: Date;
  lastRepliedAt?: Date;
}
```

```ts
Campaign {
  id: string;
  name: string;
  channel: 'TELEGRAM';
  type: 'BROADCAST' | 'SEQUENCE_2_STEP';

  segmentFilter: any;
  step1Template: string;
  step2Template?: string;

  sendWindowStart: string;
  sendWindowEnd: string;
  dailyLimit: number;

  status: 'DRAFT' | 'RUNNING' | 'PAUSED' | 'COMPLETED';
  createdAt: Date;
}
```

```ts
Message {
  id: string;
  leadId: string;
  campaignId?: string;
  channel: 'TELEGRAM';
  direction: 'OUTBOUND' | 'INBOUND';
  content: string;
  sentAt: Date;
  telegramMessageId?: string;
}
```

```ts
ResearchTask {
  id: string;
  name: string;
  description: string;
  status: 'RUNNING' | 'DONE';
  createdAt: Date;
}
```

Bạn có thể copy block này làm README, chỉ cần chỉnh lại tên repo / logo / link OpenClaw theo setup cụ thể của bạn.
