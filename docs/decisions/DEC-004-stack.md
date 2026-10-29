---
id: DEC-004
title: "Stack choice (runtime, framework, language)"
date: DD-MM-YYYY
status: decided
research: "RQ-15 in plans/UC-001/research-checklist.md"
affects: "cross-cutting, all implementation tickets"
---

## Câu hỏi

Ngôn ngữ, runtime, framework frontend và backend nào dùng cho Novsay? (RQ-15, ticket #16)

Quyết định nền tảng ảnh hưởng mọi ticket implementation.

## Các lựa chọn đã xem xét

| Lựa chọn | Mô tả | Đáp ứng yêu cầu nào | Đánh đổi |
|---|---|---|---|
| Next.js (React + Node) | Full-stack framework, SSR/SSG, API routes | Frontend + backend cùng repo, ecosystem lớn | Nặng cho app nhỏ, Vercel-oriented |
| SvelteKit | Full-stack, nhẹ, SSR built-in | Nhẹ, nhanh, DX tốt | Ecosystem nhỏ hơn React |
| React SPA + Express | Tách frontend (Vite) và backend (Express) | Linh hoạt, quen thuộc | Phải tự setup SSR nếu cần |
| Vue + Nuxt | Full-stack Vue framework | Progressive, DX tốt | Ecosystem nhỏ hơn React |

## Chọn

<!-- Chọn lựa chọn nào. Một câu. -->

## Vì sao

<!-- Vì sao chọn lựa chọn này. Trích dẫn FR, NFR hoặc ràng buộc cụ thể.
Cân nhắc:
- Khả năng của team/owner
- Ecosystem cho TTS, audio playback, storage
- DX cho flash model implementers
- Hosting compatibility (DEC-005)
-->

## Các lựa chọn bị loại và lý do

<!-- Với mỗi lựa chọn bị loại, một câu nói vì sao. -->

## Hệ quả

<!-- Quyết định này mở ra hoặc ràng buộc gì cho implementation.
Ví dụ:
- Language: TypeScript
- Runtime: Node.js [version]
- Frontend: [React/Svelte/Vue]
- Backend: [Next.js API routes / Express / ...]
- Build tool: [Vite / Next.js built-in / ...]
- Package manager: [npm / pnpm / ...]
- Ảnh hưởng DEC-005 hosting choice
-->
