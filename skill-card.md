# Skill Card — BD Agent

---

## 1. Tên Skill

**BD Agent — Automated Lead Discovery & Outreach Drafting**

> From a campaign brief, automatically discover, score, and draft personalized Telegram DMs for relevant leads — all in one Claude conversation.

---

## 2. Việc gì được automate

| # | Công việc được automate |
|---|---|
| 1 | Xây dựng search queries từ campaign brief (ICP + key topics + goal) |
| 2 | Tìm kiếm 20–50 KOL / founder / partner profiles bằng web search |
| 3 | Trích xuất bio, topics, tone, ngôn ngữ của từng profile |
| 4 | Chấm điểm mỗi lead trên 3 chiều: Relevance / Influence / Fit (0–30) |
| 5 | Phân Tier A / B / C với justification cụ thể |
| 6 | Viết Telegram DM cá nhân hoá cho tất cả Tier A & B leads (≤ 300 ký tự) |
| 7 | Xuất toàn bộ thành 1 Markdown report: summary + scorecard + DM drafts |

---

## 3. TRƯỚC — Làm tay

**Quy trình BD thủ công điển hình khi tìm KOL / partner cho 1 campaign:**

| Bước | Công việc | Thời gian ước tính |
|---|---|---|
| 1 | Google / X / Telegram tìm kiếm thủ công KOLs theo niche | ~45 phút |
| 2 | Mở từng profile, đọc bio + vài bài gần đây để đánh giá | ~60 phút |
| 3 | Copy tên, handle, note vào Google Sheet / Notion | ~15 phút |
| 4 | "Cho điểm" theo cảm tính: relevant không? lớn không? | ~15 phút |
| 5 | Viết DM template (chung) rồi chỉnh tay từng người | ~45 phút |
| **Tổng** | | **~3 tiếng / campaign** |

**Kết quả thường gặp:**
- Danh sách lead không nhất quán giữa các lần campaign
- DM chung chung, không cá nhân hoá → reply rate thấp
- Không có record rõ ràng tại sao chọn ai, bỏ ai

---

## 4. SAU — Có Skill

**Quy trình với BD Agent:**

| Bước | Công việc | Thời gian |
|---|---|---|
| 1 | Paste campaign brief vào Claude | ~2 phút |
| 2 | Trả lời 3 câu hỏi (goal, tone, hard filters) | ~3 phút |
| 3 | Đợi skill chạy (discover → score → draft) | ~10 phút |
| 4 | Review Markdown report, chọn DMs muốn gửi | ~5–10 phút |
| **Tổng** | | **~15–25 phút / campaign** |

**Kết quả:**
- 20–50 leads được tìm và chấm điểm tự động với rubric nhất quán
- Mỗi DM ≤ 300 ký tự, cá nhân hoá theo signal thực của từng người
- Report có thể share ngay cho teammate mà không cần giải thích thêm
- **Tiết kiệm ~2.5 giờ** mỗi campaign cycle

---

## 5. Tool / AI đã dùng

| Tool | Mục đích |
|---|---|
| **Claude (claude-sonnet-4-6)** | Core AI engine chạy toàn bộ pipeline |
| **web_search** (built-in Claude tool) | Discovery — tìm profile KOL/founder từ public web |
| **Claude Projects / Skill system** | Deploy SKILL.md như một reusable Claude Skill |
| **Markdown output** | Format báo cáo — không cần thêm tool render |

Không dùng thêm: database, API keys, custom code, external integrations.

---

## 6. Limitation

| Limitation | Mô tả | Workaround |
|---|---|---|
| **web_search coverage** | Telegram-specific profiles khó index; X/Twitter profiles accessible hơn | Dùng query hướng về X, blog, newsletter thay vì Telegram trực tiếp |
| **Follower count accuracy** | web_search không luôn trả về con số chính xác — score Influence có thể approximate | Dùng `Influence: estimated` label, verify thủ công trước khi gửi |
| **No memory across runs** | Mỗi lần chạy là independent — không nhớ leads từ campaign trước | Export Markdown report ra Notion / Google Sheet để lưu |
| **Hallucination risk** | Nếu web_search trả về ít data, skill có thể fill gap — guardrails [GENERIC] label sẽ flag | Luôn verify trước khi gửi DM, đặc biệt Tier B |
| **Telegram profiles** | Không tìm được Telegram user trực tiếp qua web search | Focus vào public content (X, blog, newsletter), dùng manual leads cho Telegram-only contacts |
| **Single language DM per lead** | Skill draft 1 DM per lead, không tạo A/B variants | Dùng [GENERIC] draft như template, tạo variant thủ công |

---

## 7. Roadmap mở rộng

**Phase 2 — Enhanced Discovery:**
- Integrate X API để lấy follower count chính xác và recent tweet analysis
- Thêm Telegram channel search (Telemetr.io API)
- Batch processing: chạy nhiều campaigns song song

**Phase 3 — Multi-channel Outreach:**
- Thêm LinkedIn DM draft template
- Email outreach draft (cold email format)
- X / Twitter DM template variant

**Phase 4 — Memory & CRM-lite:**
- Lightweight lead history: lưu campaign runs vào Notion database
- "Already contacted" filter: skip leads đã outreach trong 30 ngày
- Reply tracking: mark leads đã reply để loại khỏi future runs

**Phase 5 — Automation Loop:**
- Kết nối với Telegram bot để send DM sau khi human approve
- Zapier / Make integration để trigger skill từ campaign brief form
- Weekly "new leads" digest: chạy lại skill mỗi tuần và diff với lần trước

---

## Pre-Demo Checklist (5 phút trước khi demo)

- [ ] Chuẩn bị sẵn 1 campaign brief all-in-one (brief + desired action + tone + hard filters trong 1 đoạn)
- [ ] Test web_search với ít nhất 1 niche trước — xem có ≥ 5 scoreable profiles không
- [ ] Có sẵn backup brief nếu niche chính trả về ít kết quả
- [ ] Mở sẵn SKILL.md để BGK thấy cấu trúc skill nếu cần
- [ ] Confirm output format trông đúng như mong đợi (scorecard + DMs)

**Demo brief template (all-in-one, không cần trả lời 3 câu riêng):**

```
Campaign brief:
Product: [product name + 1 line description]
Target: [ICP description]
Goal: [what you want leads to do]

Desired action: [e.g., try beta and post a take]
Tone: [e.g., founder-to-founder, casual]
Hard filters: [e.g., EN only, min 5K followers, no meme-coin shillers]
```