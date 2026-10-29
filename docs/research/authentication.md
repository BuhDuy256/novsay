---
id: TF-007
title: "Đăng nhập và quyền truy cập"
created-at: "21-10-2026"
updated-at: "29-10-2026"
---

# Đăng nhập và quyền truy cập

## **RQ-14:** Làm thế nào để giữ API key của TTS provider và các secret khỏi mã chạy trên trình duyệt?

- **Phục vụ:** NFR-002 M-1
- **Ticket:** #15
- **Trạng thái:** open

<!-- Điền kết quả nghiên cứu ở đây. Bao gồm:
- Kiến trúc: client không bao giờ gọi TTS trực tiếp, luôn qua backend
- Lưu secret: environment variables, secret manager (platform-specific)
- Đảm bảo: không leak trong client bundle, không trong error messages, không trong network tab
- Framework support: Next.js server-only, env prefix conventions
- Đề xuất approach cho V1
-->
