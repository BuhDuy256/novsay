---
scope: "UC-001 full"
title: "Danh sách nghiên cứu — UC-001"
created: 29-10-2026
---

# Danh sách nghiên cứu — UC-001

## Phạm vi

- **Use case:** UC-001
- **Các bước:** tất cả (S1-S6)
- **Nhánh thay thế:** tất cả (A1-A4, A6-A12)
- **FR liên quan:** FR-001, FR-002, FR-003, FR-004, FR-006, FR-007, FR-008, FR-010, FR-012, FR-013
- **NFR liên quan:** NFR-001, NFR-002, NFR-003
- **BR liên quan:** BR-001, BR-002, BR-003

## Cách dùng

Mỗi câu hỏi gắn với FR/NFR mà nó phục vụ. Trả lời bằng cách nghiên cứu
(với sự hỗ trợ của agent hoặc tự nghiên cứu). File deliverable đã được tạo sẵn —
mở file, điền nội dung vào phần `<!-- Điền kết quả -->` hoặc các mục trống.

## Deliverable map

| RQ | Loại | File |
|---|---|---|
| RQ-1 | research | [docs/research/web-content.md](https://github.com/BuhDuy256/novsay/blob/main/docs/research/web-content.md) |
| RQ-2 | research | [docs/research/web-content.md](https://github.com/BuhDuy256/novsay/blob/main/docs/research/web-content.md) |
| RQ-3 | research | [docs/research/web-content.md](https://github.com/BuhDuy256/novsay/blob/main/docs/research/web-content.md) |
| RQ-4 | research | [docs/research/web-content.md](https://github.com/BuhDuy256/novsay/blob/main/docs/research/web-content.md) |
| RQ-5 | decision | [docs/decisions/DEC-001-tts-provider.md](https://github.com/BuhDuy256/novsay/blob/main/docs/decisions/DEC-001-tts-provider.md) |
| RQ-6 | research | [docs/research/audio-generation.md](https://github.com/BuhDuy256/novsay/blob/main/docs/research/audio-generation.md) |
| RQ-7 | research | [docs/research/audio-playback.md](https://github.com/BuhDuy256/novsay/blob/main/docs/research/audio-playback.md) |
| RQ-8 | research | [docs/research/listening-progress.md](https://github.com/BuhDuy256/novsay/blob/main/docs/research/listening-progress.md) |
| RQ-9 | decision | [docs/decisions/DEC-002-execution-model.md](https://github.com/BuhDuy256/novsay/blob/main/docs/decisions/DEC-002-execution-model.md) |
| RQ-10 | decision | [docs/decisions/DEC-003-storage.md](https://github.com/BuhDuy256/novsay/blob/main/docs/decisions/DEC-003-storage.md) |
| RQ-11 | research | [docs/research/data-storage.md](https://github.com/BuhDuy256/novsay/blob/main/docs/research/data-storage.md) |
| RQ-12 | research | [docs/research/preparation-and-recovery.md](https://github.com/BuhDuy256/novsay/blob/main/docs/research/preparation-and-recovery.md) |
| RQ-13 | research | [docs/research/audio-playback.md](https://github.com/BuhDuy256/novsay/blob/main/docs/research/audio-playback.md) |
| RQ-14 | research | [docs/research/authentication.md](https://github.com/BuhDuy256/novsay/blob/main/docs/research/authentication.md) |
| RQ-15 | decision | [docs/decisions/DEC-004-stack.md](https://github.com/BuhDuy256/novsay/blob/main/docs/decisions/DEC-004-stack.md) |
| RQ-16 | decision | [docs/decisions/DEC-005-hosting.md](https://github.com/BuhDuy256/novsay/blob/main/docs/decisions/DEC-005-hosting.md) |

## Câu hỏi

### FR-001 — Kiểm tra link nguồn

| # | Câu hỏi | Vì sao quan trọng | Ticket | Trạng thái |
|---|---|---|---|---|
| RQ-1 | Cấu trúc URL chương trên website nguồn như thế nào? Quy tắc nào phân biệt link chương với link trang chủ, thư mục truyện hoặc trang khác? | FR-001 AC-1/AC-2: cần regex hoặc pattern để nhận/từ chối link. BR-001 V-2 nói link chương công khai nhưng chưa xác định pattern. | [#2](https://github.com/BuhDuy256/novsay/issues/2) | answered |
| RQ-2 | Làm thế nào để ngăn link hoặc chuyển hướng truy cập vào mạng riêng của server (SSRF prevention)? | FR-001 AC-3: phải từ chối đích không công khai. Cần biết cách kiểm tra IP sau DNS resolution. | [#3](https://github.com/BuhDuy256/novsay/issues/3) | answered |

### FR-002 — Lấy một chương

| # | Câu hỏi | Vì sao quan trọng | Ticket | Trạng thái |
|---|---|---|---|---|
| RQ-3 | Website nguồn trả nội dung chương bằng HTML tĩnh, JavaScript render hay API riêng? Cấu trúc HTML (selector tiêu đề, vùng truyện) là gì và xử lý multi-site thế nào? | FR-002 AC-1: cần biết cách tách văn bản truyện khỏi quảng cáo/điều hướng/bình luận. Quyết định dùng HTML parser hay headless browser. Cần site config cho mỗi website nguồn. | [#4](https://github.com/BuhDuy256/novsay/issues/4) | open |
| RQ-4 | Website nguồn có cơ chế chống bot (Cloudflare, CAPTCHA, rate limit) không? Fetch từ backend Node có bị chặn không? | FR-002 AC-1/AC-3, FR-007: ảnh hưởng khả năng lấy chương và chiến lược retry. Mỗi site có thể có cơ chế khác nhau. | [#5](https://github.com/BuhDuy256/novsay/issues/5) | open |

### FR-004 — Chuẩn bị audio chương

| # | Câu hỏi | Vì sao quan trọng | Ticket | Trạng thái |
|---|---|---|---|---|
| RQ-5 | Dùng TTS provider nào cho tiếng Trung? So sánh các lựa chọn (Google Cloud TTS, Azure TTS, ElevenLabs, OpenAI TTS, Edge TTS) về chất lượng, giới hạn độ dài, giá, latency và API. | FR-004 AC-1/AC-3, BR-002: cần chọn provider và giọng đọc cố định tiếng Trung. Quyết định này ảnh hưởng cấu hình tạo audio (FR-008 AC-1 tương thích). | [#6](https://github.com/BuhDuy256/novsay/issues/6) | open |
| RQ-6 | Transcript một chương dài bao nhiêu ký tự? Provider có giới hạn đầu vào không? Nếu phải chia, làm thế nào để ghép audio không thiếu/lặp/đảo? | FR-004 AC-2: audio đọc đúng nội dung và thứ tự transcript. Cần chiến lược chunking nếu vượt giới hạn. | [#7](https://github.com/BuhDuy256/novsay/issues/7) | open |
| RQ-7 | Định dạng audio đầu ra nào (MP3, OGG, WAV) dùng được trên cả Windows Chrome và iPhone Safari? | FR-004, NFR-001: audio phải phát được trên cả hai môi trường, kể cả nền. Liên quan RQ-12. | [#8](https://github.com/BuhDuy256/novsay/issues/8) | open |

### FR-006 — Lưu và khôi phục tiến độ

| # | Câu hỏi | Vì sao quan trọng | Ticket | Trạng thái |
|---|---|---|---|---|
| RQ-8 | Lưu tiến độ (vị trí phát) ở đâu và bằng cơ chế nào để đảm bảo khôi phục sau gián đoạn đột ngột trên cùng thiết bị, lùi tối đa 5 giây? | FR-006 AC-1/AC-6, NFR-003 M-1: cần cơ chế checkpoint đủ tin cậy. localStorage, IndexedDB, hay server-side? Tần suất lưu? | [#9](https://github.com/BuhDuy256/novsay/issues/9) | open |

### FR-007 — Khôi phục việc chuẩn bị thất bại

| # | Câu hỏi | Vì sao quan trọng | Ticket | Trạng thái |
|---|---|---|---|---|
| RQ-9 | Việc lấy chương và tạo audio chạy ở đâu (serverless function, long-running server, queue worker)? Thời gian chạy tối đa? | FR-007 AC-2, FR-012: cần biết execution model để thiết kế retry và trạng thái yêu cầu. Ảnh hưởng hosting (RQ-16). | [#10](https://github.com/BuhDuy256/novsay/issues/10) | open |

### FR-008 — Chọn lưu và dùng lại bản nghe

| # | Câu hỏi | Vì sao quan trọng | Ticket | Trạng thái |
|---|---|---|---|---|
| RQ-10 | Transcript, audio file, metadata bản đã lưu và tiến độ nên được lưu ở đâu? Database nào cho metadata, blob storage nào cho audio? | FR-008 AC-4/AC-6, BR-003: cần lưu không thời hạn, hỗ trợ nhiều bản cùng link, query audio tương thích. | [#11](https://github.com/BuhDuy256/novsay/issues/11) | open |
| RQ-11 | Làm thế nào để xác định audio tương thích (khớp transcript, cùng cấu hình tạo audio, còn dùng được)? Dùng hash transcript hay so ký tự? | FR-008 AC-1/AC-13/AC-14/AC-15: logic dùng lại audio phụ thuộc cách so sánh transcript và cấu hình. | [#12](https://github.com/BuhDuy256/novsay/issues/12) | open |

### FR-012 — Xem lại trạng thái chuẩn bị audio

| # | Câu hỏi | Vì sao quan trọng | Ticket | Trạng thái |
|---|---|---|---|---|
| RQ-12 | Làm thế nào để owner quay lại app và thấy trạng thái yêu cầu chuẩn bị (đang chạy, xong, thất bại) mà không tạo yêu cầu trùng? | FR-012 AC-1/AC-4: cần thiết kế trạng thái yêu cầu, cách lưu và cách frontend poll/subscribe. Liên quan RQ-9. | [#13](https://github.com/BuhDuy256/novsay/issues/13) | open |

### NFR-001 — Nghe nền

| # | Câu hỏi | Vì sao quan trọng | Ticket | Trạng thái |
|---|---|---|---|---|
| RQ-13 | Làm thế nào để audio tiếp tục phát khi chuyển app, tắt màn hình hoặc khóa máy trên iPhone Safari và Windows Chrome? | NFR-001 M-1: cần Media Session API, Web Audio API hay cách khác? Service Worker có giúp không? | [#14](https://github.com/BuhDuy256/novsay/issues/14) | open |

### NFR-002 — Bảo vệ thông tin dịch vụ

| # | Câu hỏi | Vì sao quan trọng | Ticket | Trạng thái |
|---|---|---|---|---|
| RQ-14 | Làm thế nào để giữ API key của TTS provider và các secret khỏi mã chạy trên trình duyệt? | NFR-002 M-1: TTS call phải đi qua backend; cần env vars hoặc secret manager. Ảnh hưởng kiến trúc client-server. | [#15](https://github.com/BuhDuy256/novsay/issues/15) | open |

### Cross-cutting — Stack và triển khai

| # | Câu hỏi | Vì sao quan trọng | Ticket | Trạng thái |
|---|---|---|---|---|
| RQ-15 | Ngôn ngữ, runtime, framework frontend và backend nào dùng cho Novsay? | Quyết định nền tảng ảnh hưởng mọi ticket implementation. Cần chọn trước khi lên kế hoạch. | [#16](https://github.com/BuhDuy256/novsay/issues/16) | open |
| RQ-16 | Hosting nào (Vercel, Railway, Fly.io, Cloudflare Workers, VPS) đáp ứng yêu cầu? Chi phí dự kiến? | Ảnh hưởng execution model (RQ-9), storage (RQ-10), deployment pipeline. | [#17](https://github.com/BuhDuy256/novsay/issues/17) | open |

## Trạng thái

- `open` — chưa bắt đầu
- `researching` — đang nghiên cứu
- `answered` — đã trả lời trong docs/research/
- `decided` — đã quyết định trong docs/decisions/DEC-NNN
