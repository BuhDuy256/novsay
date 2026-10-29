---
id: DEC-002
title: "Execution model cho lấy chương và tạo audio"
date: DD-MM-YYYY
status: decided
research: "RQ-9 in plans/UC-001/research-checklist.md"
affects: "FR-007, FR-012"
---

## Câu hỏi

Việc lấy chương và tạo audio chạy ở đâu? Serverless function, long-running server, hay queue worker? (RQ-9, ticket #10)

Cần biết execution model để thiết kế retry, trạng thái yêu cầu, và khả năng resume khi owner quay lại.

## Các lựa chọn đã xem xét

| Lựa chọn | Mô tả | Đáp ứng yêu cầu nào | Đánh đổi |
|---|---|---|---|
| Serverless function | Vercel/Cloudflare function xử lý sync | Đơn giản deploy | Timeout ngắn (10-30s), không đủ cho TTS dài |
| Long-running server | Express/Fastify server xử lý async | FR-007 (không timeout), FR-012 (trạng thái) | Cần VPS hoặc container, chi phí |
| Queue + worker | Tách request thành job, worker xử lý | FR-007 (retry built-in), FR-012 (job status) | Phức tạp nhất, cần message queue |
| Serverless + polling | Function khởi tạo, client poll trạng thái | FR-012 (poll status) | Cần state store, poll logic |

## Chọn

<!-- Chọn lựa chọn nào. Một câu. -->

## Vì sao

<!-- Vì sao chọn lựa chọn này. Trích dẫn FR, NFR hoặc ràng buộc cụ thể. -->

## Các lựa chọn bị loại và lý do

<!-- Với mỗi lựa chọn bị loại, một câu nói vì sao. -->

## Hệ quả

<!-- Quyết định này mở ra hoặc ràng buộc gì cho implementation.
Ví dụ:
- Thời gian chạy tối đa: [N phút] → ảnh hưởng chunking strategy
- Retry mechanism: [built-in / manual] → FR-007
- State persistence: [database / in-memory] → FR-012, RQ-12
- Hosting requirement: → ảnh hưởng DEC-005
-->
