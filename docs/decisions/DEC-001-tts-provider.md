---
id: DEC-001
title: "TTS provider cho tiếng Trung"
date: DD-MM-YYYY
status: decided
research: "RQ-5 in plans/UC-001/research-checklist.md"
affects: "FR-004, BR-002, FR-008"
---

## Câu hỏi

Dùng TTS provider nào cho tiếng Trung? (RQ-5, ticket [#6](https://github.com/BuhDuy256/novsay/issues/6))

Cần chọn provider và giọng đọc cố định tiếng Trung. Quyết định này ảnh hưởng:
- Cấu hình tạo audio (FR-008 AC-1 tương thích)
- Chi phí vận hành
- Định dạng audio đầu ra
- Giới hạn độ dài đầu vào (ảnh hưởng RQ-6 chunking)

## Các lựa chọn đã xem xét

| Lựa chọn | Mô tả | Đáp ứng yêu cầu nào | Đánh đổi |
|---|---|---|---|
| Google Cloud TTS | WaveNet/Neural2 voices cho zh-CN | FR-004 AC-3 (nghe rõ), nhiều giọng | Có giá, cần GCP account |
| Azure TTS | Neural voices cho zh-CN, SSML support | FR-004 AC-3, SSML cho punctuation | Có giá, cần Azure account |
| OpenAI TTS | tts-1 hoặc tts-1-hd | FR-004 AC-3, API đơn giản | Chưa rõ chất lượng tiếng Trung, giá cao |
| Edge TTS (edge-tts) | Free, dùng Microsoft Edge API | FR-004 AC-3, miễn phí | Không chính thức, có thể bị chặn |
| ElevenLabs | Multilingual v2 voices | FR-004 AC-3, chất lượng cao nhất | Giá cao nhất, có thể overkill |

## Chọn

<!-- Chọn lựa chọn nào. Một câu. -->

## Vì sao

<!-- Vì sao chọn lựa chọn này. Trích dẫn FR, NFR hoặc ràng buộc cụ thể. -->

## Các lựa chọn bị loại và lý do

<!-- Với mỗi lựa chọn bị loại, một câu nói vì sao. -->

## Hệ quả

<!-- Quyết định này mở ra hoặc ràng buộc gì cho implementation.
Ví dụ:
- Giọng đọc cố định: [tên giọng] → BR-002 V-1
- Định dạng output: [MP3/OGG/...] → ảnh hưởng RQ-7
- Giới hạn input: [N ký tự] → ảnh hưởng RQ-6 chunking
- Cấu hình tạo audio: provider + model + voice + params → FR-008 AC-1 fingerprint
-->
