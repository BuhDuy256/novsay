---
id: TF-004
title: "Lưu dữ liệu"
created-at: "21-10-2026"
updated-at: "29-10-2026"
---

# Lưu dữ liệu

## **RQ-11:** Làm thế nào để xác định audio tương thích?

> Khớp transcript, cùng cấu hình tạo audio, còn dùng được. Dùng hash transcript hay so ký tự?

- **Phục vụ:** FR-008 AC-1/AC-13/AC-14/AC-15
- **Ticket:** #12
- **Trạng thái:** open
- **Blocked by:** #11 (RQ-10: cần biết storage để biết cách query)

<!-- Điền kết quả nghiên cứu ở đây. Bao gồm:
- Định nghĩa "tương thích" theo FR-008: transcript giống hệt + cùng cấu hình tạo audio + còn dùng được
- Cách so sánh transcript: hash (SHA-256) vs exact string comparison
- Cấu hình tạo audio gồm gì: provider, model, voice, parameters
- Schema fingerprint: hash(transcript + config) → lookup audio
- Xử lý edge case: cùng text khác whitespace, cùng hash khác provider version
- Đề xuất approach
-->
