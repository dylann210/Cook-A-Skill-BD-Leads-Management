# Prompt 02 — Iterating the Scoring Rubric

**Context:** The initial spec had a vague Influence score: "Follower hints / role prominence (coarse brackets)". This prompt made it specific.

---

## Problem identified

The original rubric said:

> Influence 0–10: Follower hints / role prominence (coarse brackets)

This is too vague — "coarse brackets" is not actionable. Claude (or a human) scoring a lead would still guess.

---

## Prompt

```
Trong spec.md hiện tại, Influence score chỉ nói "coarse brackets" mà không có con số cụ thể.

Hãy cải thiện:
1. Thêm follower brackets cụ thể cho Influence (giống engagement table style):
   - Mỗi bracket range → score cụ thể
   - Ít nhất 5-6 levels từ < 1K đến > 500K
2. Thêm rule cho role prominence (VC, co-founder, etc.)
3. Xử lý case khi không có follower data
4. Làm tương tự cho Relevance và Fit — thêm brackets vào spec

Mục tiêu: AI đọc spec phải cho điểm nhất quán, không cảm tính.
```

---

## Result

Spec được cập nhật với 3 bảng brackets đầy đủ:

**Influence:** 6 levels (< 1K → > 500K) + role prominence +1 rule + estimated case
**Relevance:** 4 levels (no mention → deep expert)
**Fit:** 3 levels (mismatch → perfect match)

---

## Why this matters

Scoring rubric là core logic của skill. Nếu rubric vague, AI sẽ cho điểm khác nhau mỗi lần chạy → tier assignment không reliable → DM drafting target sai people. Đây là điểm quan trọng nhất cần nail đúng trong spec.

---

## Key insight

Khi iterate rubric, hỏi "nếu tôi là AI mới đọc spec lần đầu, tôi có biết assign 7 hay 8 không?" — nếu không → rubric chưa đủ cụ thể.