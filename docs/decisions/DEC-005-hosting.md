---
id: DEC-005
title: "Hosting và chi phí vận hành"
date: DD-MM-YYYY
status: decided
research: "RQ-16 in plans/UC-001/research-checklist.md"
affects: "cross-cutting, DEC-002 execution model, DEC-003 storage"
---

## Câu hỏi

Hosting nào đáp ứng yêu cầu? Chi phí dự kiến? (RQ-16, ticket #17)

Ảnh hưởng execution model (DEC-002), storage (DEC-003), deployment pipeline.

## Các lựa chọn đã xem xét

| Lựa chọn | Mô tả | Đáp ứng yêu cầu nào | Đánh đổi |
|---|---|---|---|
| Vercel | Serverless, tích hợp Next.js | DX tốt nhất cho Next.js | Function timeout ngắn, giá scale |
| Railway | Container-based, managed | Long-running OK, đơn giản | Ít free tier |
| Fly.io | Container edge deployment | Long-running, global | Phức tạp hơn |
| Cloudflare (Pages + Workers + R2) | Edge-first, R2 free egress | Rẻ nhất | Workers runtime limits |
| VPS (Hetzner/DigitalOcean) | Full control | Rẻ, không giới hạn | Tự quản lý |

## Chọn

<!-- Chọn lựa chọn nào. Một câu. -->

## Vì sao

<!-- Vì sao chọn lựa chọn này. Trích dẫn FR, NFR hoặc ràng buộc cụ thể.
Cân nhắc:
- Execution model từ DEC-002 (long-running? serverless?)
- Storage từ DEC-003 (managed DB? blob storage?)
- Stack từ DEC-004 (Next.js → Vercel? Express → VPS?)
- Chi phí cho 1 user (owner) ban đầu
- Độ phức tạp deploy và maintain
-->

## Các lựa chọn bị loại và lý do

<!-- Với mỗi lựa chọn bị loại, một câu nói vì sao. -->

## Hệ quả

<!-- Quyết định này mở ra hoặc ràng buộc gì cho implementation.
Ví dụ:
- Platform: [Vercel/Railway/VPS/...]
- Chi phí ước tính: $X/tháng
- Deployment: [git push / CI / manual]
- Domain: [custom / platform subdomain]
- SSL: [automatic / manual]
- Monitoring: [platform built-in / external]
-->
