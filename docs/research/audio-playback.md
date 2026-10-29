---
id: TF-003
title: "Phát audio"
created-at: "21-10-2026"
updated-at: "29-10-2026"
---

# Phát audio

## UC-001/RQ-7: Định dạng audio tương thích cross-platform

> MP3, OGG, WAV, AAC — định dạng nào, kể cả khi phát nền?

- **Phục vụ:** FR-004, NFR-001
- **Ticket:** [#8](https://github.com/BuhDuy256/novsay/issues/8)
- **Trạng thái:** open

<!-- Điền kết quả nghiên cứu ở đây. Bao gồm:
- Bảng tương thích định dạng: MP3, OGG, WAV, AAC, OPUS trên Windows Chrome và iPhone Safari
- Kiểm tra phát nền với từng định dạng
- Kích thước file tương đối (cùng nội dung, khác codec)
- Đề xuất định dạng cho Novsay
-->

---

## UC-001/RQ-13: Phát audio nền trên iPhone Safari và Windows Chrome

> Trên iPhone Safari và Windows Chrome.

- **Phục vụ:** NFR-001 M-1
- **Ticket:** [#14](https://github.com/BuhDuy256/novsay/issues/14)
- **Trạng thái:** open
- **Blocked by:** [#8](https://github.com/BuhDuy256/novsay/issues/8) (RQ-7: cần biết định dạng audio trước)

<!-- Điền kết quả nghiên cứu ở đây. Bao gồm:
- Media Session API: có cần không, cách dùng
- HTMLAudioElement vs Web Audio API cho background playback
- iPhone Safari: hạn chế autoplay, lock screen controls, audio interruption
- Windows Chrome: behavior khi minimize, tắt màn hình
- Service Worker: có giúp gì cho background audio không
- Kết quả test thực tế trên cả hai platform
-->
