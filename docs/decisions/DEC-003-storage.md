---
id: DEC-003
title: "Storage cho transcript, audio và metadata"
date: DD-MM-YYYY
status: decided
research: "RQ-10 in plans/UC-001/research-checklist.md"
affects: "FR-008, BR-003, FR-006, FR-012, FR-013"
---

## Câu hỏi

Transcript, audio file, metadata bản đã lưu và tiến độ nên được lưu ở đâu? Database nào cho metadata, blob storage nào cho audio? (RQ-10, ticket [#11](https://github.com/BuhDuy256/novsay/issues/11))

Cần lưu không thời hạn (BR-003), hỗ trợ nhiều bản cùng link, query audio tương thích (FR-008).

## Các lựa chọn đã xem xét

| Lựa chọn | Mô tả | Đáp ứng yêu cầu nào | Đánh đổi |
|---|---|---|---|
| Supabase (Postgres + Storage) | Managed Postgres cho metadata, S3-compatible storage cho audio | BR-003 (durable), FR-008 (SQL query), FR-006 (realtime) | Free tier có giới hạn |
| SQLite + local filesystem | SQLite cho metadata, filesystem cho audio | BR-003, FR-008 | Không scale, cần VPS |
| PlanetScale/Turso + R2 | Managed DB + Cloudflare R2 | BR-003, FR-008, R2 free egress | Nhiều service |
| Firebase (Firestore + Storage) | NoSQL + GCS storage | FR-006 (realtime), generous free tier | Vendor lock-in, NoSQL query limits cho FR-008 |

## Chọn

<!-- Chọn lựa chọn nào. Một câu. -->

## Vì sao

<!-- Vì sao chọn lựa chọn này. Trích dẫn FR, NFR hoặc ràng buộc cụ thể. -->

## Các lựa chọn bị loại và lý do

<!-- Với mỗi lựa chọn bị loại, một câu nói vì sao. -->

## Hệ quả

<!-- Quyết định này mở ra hoặc ràng buộc gì cho implementation.
Ví dụ:
- Database: [Postgres/SQLite/Firestore] → schema design
- Blob storage: [S3/R2/GCS/filesystem] → upload/download API
- Audio tương thích query: → RQ-11 approach
- Tiến độ storage: → RQ-8 mechanism
- Request state: → RQ-12 design
-->
