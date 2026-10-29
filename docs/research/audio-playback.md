---
id: TF-003
title: "Phát audio"
created-at: "21-10-2026"
updated-at: "29-10-2026"
---

# Phát audio

## **RQ-7:** Định dạng audio đầu ra nào dùng được trên cả Windows Chrome và iPhone Safari?

> MP3, OGG, WAV, AAC — định dạng nào, kể cả khi phát nền?

- **Phục vụ:** FR-004, NFR-001
- **Ticket:** #8
- **Trạng thái:** open

<!-- Điền kết quả nghiên cứu ở đây. Bao gồm:
- Bảng tương thích định dạng: MP3, OGG, WAV, AAC, OPUS trên Windows Chrome và iPhone Safari
- Kiểm tra phát nền với từng định dạng
- Kích thước file tương đối (cùng nội dung, khác codec)
- Đề xuất định dạng cho Novsay
-->

---

## **RQ-13:** Làm thế nào để audio tiếp tục phát khi chuyển app, tắt màn hình hoặc khóa máy?

> Trên iPhone Safari và Windows Chrome.

- **Phục vụ:** NFR-001 M-1
- **Ticket:** #14
- **Trạng thái:** open
- **Blocked by:** #8 (RQ-7: cần biết định dạng audio trước)

<!-- Điền kết quả nghiên cứu ở đây. Bao gồm:
- Media Session API: có cần không, cách dùng
- HTMLAudioElement vs Web Audio API cho background playback
- iPhone Safari: hạn chế autoplay, lock screen controls, audio interruption
- Windows Chrome: behavior khi minimize, tắt màn hình
- Service Worker: có giúp gì cho background audio không
- Kết quả test thực tế trên cả hai platform
-->
