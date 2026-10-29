---
scope: ""
title: ""
created: DD-MM-YYYY
---

# Theo dõi tiến độ — {scope}

Bản sao cục bộ của GitHub flow tracker issue. Cập nhật file này khi issue được
cập nhật.

## Phạm vi

- **Use case:** UC-XXX
- **Các bước:** S1-S2 (hoặc "tất cả")
- **Nhánh thay thế:** A1, A3 (hoặc "tất cả")
- **FR liên quan:** FR-NNN, FR-NNN

<!-- Mọi tham chiếu #N phải là link clickable: [#N](https://github.com/{owner}/{repo}/issues/N)
     Xem WORKFLOW.md "Linking convention". -->

## Phase 1: Nghiên cứu
<!-- Gate: tất cả ticket nghiên cứu trong phạm vi đã đóng -->

- [ ] [#N](https://github.com/{owner}/{repo}/issues/N) tên câu hỏi

## Phase 2: Kế hoạch kiểm thử
<!-- Gate: tất cả ticket test stub đã đóng -->
<!-- Blocked by: Phase 1 hoàn tất -->

- [ ] [#N](https://github.com/{owner}/{repo}/issues/N) tên test stub

## Phase 3: Kế hoạch implementation
<!-- Gate: kế hoạch đã review và chấp nhận -->
<!-- Blocked by: Phase 2 hoàn tất -->

- [ ] [#N](https://github.com/{owner}/{repo}/issues/N) review kế hoạch

## Phase 4: Implementation
<!-- Gate: tất cả ticket impl đã đóng, test xanh -->

- [ ] [#N](https://github.com/{owner}/{repo}/issues/N) tên module (Blocked by: [#N](https://github.com/{owner}/{repo}/issues/N))

## Phase 5: Kiểm thử sau implementation
<!-- Gate: tất cả ticket post-impl đã đóng -->

- [ ] [#N](https://github.com/{owner}/{repo}/issues/N) tên test (Blocked by: [#N](https://github.com/{owner}/{repo}/issues/N))

## Phase 6: Xác nhận
<!-- Gate: flow tracker issue đóng -->
<!-- Blocked by: Phase 5 hoàn tất -->

- [ ] Toàn bộ test suite pass
- [ ] Điều kiện chấp nhận của UC đã xác nhận
