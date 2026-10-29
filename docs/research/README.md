# Research

Technical research for Novsay. Each file covers a **topic area** and accumulates
questions from any UC build over time.

## Quy ước

- **Một file mỗi topic** — không tạo file mới khi UC mới có câu hỏi cùng topic.
- **Heading format:** `## UC-XXX/RQ-N: Tiêu đề ngắn` — scope rõ ràng, nhiều UC
  cùng tồn tại trong một file.
- Khi UC-002 tạo câu hỏi về web content → thêm section vào `web-content.md`,
  không tạo `web-content-2.md`.
- Decision records (`docs/decisions/DEC-NNN-*.md`) dành cho câu hỏi cần chọn
  giữa nhiều lựa chọn. Research files dành cho câu hỏi cần tìm hiểu sự thật.

## Topics

| File | Nội dung | UC-001 questions |
|---|---|---|
| [web-content.md](web-content.md) | Fetching, extracting, validating chapter content | RQ-1, RQ-2, RQ-3, RQ-4 |
| [audio-generation.md](audio-generation.md) | TTS, chunking, audio preparation | RQ-6 |
| [audio-playback.md](audio-playback.md) | Playback, background audio, format | RQ-7, RQ-13 |
| [data-storage.md](data-storage.md) | Storing transcripts, audio, compatibility | RQ-11 |
| [listening-progress.md](listening-progress.md) | Tracking and restoring play position | RQ-8 |
| [preparation-and-recovery.md](preparation-and-recovery.md) | Request states, failure handling | RQ-12 |
| [authentication.md](authentication.md) | Secrets, access control | RQ-14 |

## Decision records

| RQ | Decision | File |
|---|---|---|
| UC-001/RQ-5 | TTS provider | [DEC-001](../decisions/DEC-001-tts-provider.md) |
| UC-001/RQ-9 | Execution model | [DEC-002](../decisions/DEC-002-execution-model.md) |
| UC-001/RQ-10 | Storage | [DEC-003](../decisions/DEC-003-storage.md) |
| UC-001/RQ-15 | Stack choice | [DEC-004](../decisions/DEC-004-stack.md) |
| UC-001/RQ-16 | Hosting | [DEC-005](../decisions/DEC-005-hosting.md) |

## Question status

- `open` — not started
- `researching` — in progress
- `answered` — answer written in this file
- `decided → DEC-NNN` — answer led to a decision record in `docs/decisions/`
