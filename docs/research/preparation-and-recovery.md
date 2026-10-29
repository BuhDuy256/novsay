---
id: TF-006
title: "Yêu cầu chuẩn bị và lỗi"
created-at: "21-10-2026"
updated-at: "29-10-2026"
---

# Yêu cầu chuẩn bị và lỗi

## UC-001/RQ-12: Thiết kế trạng thái yêu cầu chuẩn bị

> Đang chạy, xong, thất bại — mà không tạo yêu cầu trùng.

- **Phục vụ:** FR-012 AC-1/AC-4
- **Ticket:** [#13](https://github.com/BuhDuy256/novsay/issues/13)
- **Trạng thái:** open
- **Blocked by:** [#10](https://github.com/BuhDuy256/novsay/issues/10) (RQ-9: execution model ảnh hưởng cách lưu trạng thái)

<!-- Điền kết quả nghiên cứu ở đây. Bao gồm:
- State machine của yêu cầu chuẩn bị: pending → processing → ready / failed / interrupted
- Nơi lưu trạng thái: database (từ DEC-003), in-memory, hay cả hai
- Cách frontend biết trạng thái: polling, SSE, WebSocket
- Idempotency: cách tránh tạo yêu cầu trùng (unique key = owner + transcript hash?)
- Xử lý khi process bị kill giữa chừng: trạng thái "interrupted"
- Đề xuất design
-->
