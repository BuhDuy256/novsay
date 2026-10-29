# Quyết định

Mỗi file ghi lại một quyết định kỹ thuật hoặc sản phẩm trong quá trình build.
Quyết định là đầu ra của câu hỏi nghiên cứu — ghi lại đã chọn gì, vì sao,
và đã loại gì.

## Danh mục

| ID | Câu hỏi | Chọn | Ngày | Trạng thái |
|---|---|---|---|---|
| DEC-001 | TTS provider cho tiếng Trung (RQ-5) | — | — | open |
| DEC-002 | Execution model (RQ-9) | — | — | open |
| DEC-003 | Storage (RQ-10) | — | — | open |
| DEC-004 | Stack choice (RQ-15) | — | — | open |
| DEC-005 | Hosting (RQ-16) | — | — | open |

## Quy ước

- Một file mỗi quyết định: `DEC-NNN-chủ-đề-ngắn.md`.
- ID tăng dần, không dùng lại.
- Trạng thái: `open` (chưa quyết), `decided` (chốt) hoặc `revisiting` (mở lại kèm lý do).
- Mỗi quyết định link tới câu hỏi nghiên cứu gốc.
- Ticket implementation trích dẫn quyết định theo ID.
