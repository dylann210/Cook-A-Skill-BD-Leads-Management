# Prompt 01 — Cooking the Spec Structure

**Context:** Initial prompt used to design the BD Agent spec from scratch.

---

## Prompt

```
Tôi muốn build một Claude Skill cho BD automation. Cụ thể:

- Input: campaign brief (1 đoạn text mô tả product, target, goal)
- Output: danh sách leads đã research + scored + Telegram DM drafts

Hãy viết một spec.md đầy đủ bao gồm:
1. Objective và Problem Statement
2. Input contract (fields extract từ brief)
3. Quy trình discovery (dùng web_search)
4. Scoring rubric (Relevance / Influence / Fit, 0-30 tổng)
5. DM drafting rules (Telegram style, ngắn gọn)
6. Output structure (Markdown report)
7. Edge cases
8. MVP Success Criteria

Primary users: BD / Partnerships / Founder
Constraint: chạy như single Claude Skill, không dùng database hay Telegram API
```

---

## Why this prompt worked

- Đặt constraint rõ ràng ngay từ đầu: "no database, no Telegram API" → Claude không hallucinate infra không cần thiết
- Liệt kê đủ 7 sections cần có → output có cấu trúc hoàn chỉnh ngay lần đầu
- Specify "Primary users" → Claude hiểu context để viết spec đúng audience
- "Single Claude Skill" → frame đúng paradigm, tránh Claude đề xuất custom code

---

## Key insight

Spec tốt nhất được cook khi bạn biết constraint trước. Nếu không nói "no database", Claude sẽ tự thêm database layer vào design. Constraint là input quan trọng nhất khi cook spec.