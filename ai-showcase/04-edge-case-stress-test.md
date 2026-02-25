# Prompt 04 — Edge Case Stress Testing

**Context:** After writing the initial spec, this prompt was used to find gaps in edge case handling.

---

## Prompt

```
Đóng vai BGK đang đánh giá spec của tôi. Tìm tất cả edge cases mà spec chưa xử lý:

Spec hiện tại cover: too few leads, conflicting data, language mismatch.

Hãy tìm thêm các edge cases quan trọng bị thiếu, đặc biệt:
1. Khi tất cả leads đều score Tier C
2. Khi web_search không trả về đủ kết quả
3. Khi follower data không có
4. Khi AI có thể bịa data để fill score
5. Khi brief thiếu nhiều fields quan trọng

Với mỗi edge case: mô tả situation + hướng xử lý cụ thể mà skill nên làm.
```

---

## Gaps found

| Edge Case | Gap before | Fix applied |
|---|---|---|
| All leads Tier C | Spec said nothing — skill would output empty DM section silently | Added explicit flag + actionable guidance to broaden criteria |
| Fabricated follower counts | No rule against it — AI might estimate to complete the score | Added "Never fabricate" rule in both spec and SKILL.md |
| Influence "estimated" with no score | Spec said mark as estimated but no number | Added: assign bracket floor score (1), never guess |
| web_search discovery failure | No smoke test before demo | Added Section 11.1 pre-demo validation gate |

---

## Stress test questions used

1. "What happens if I give the skill a very obscure niche with no web results?"
2. "What if the only leads found are all meme-coin shillers I've already filtered out?"
3. "What if Claude can't tell if someone has 5K or 500K followers?"
4. "What if I never answer Q3 (hard filters) — does the skill proceed anyway?"
5. "What if all my 'must-include' manual leads are clearly Tier C by the rubric?"

---

## Key insight

The best way to find spec gaps is to ask "what's the worst case scenario for each step?" and trace through what the skill would do. If the answer is "nothing / unclear / hallucinate" — that's a missing edge case.

Running this stress test caught 4 significant gaps that would have caused bad outputs in production.