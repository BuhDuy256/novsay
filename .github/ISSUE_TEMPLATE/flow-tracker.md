---
name: Flow tracker
about: Root tracking issue for a build scope. One per scoped build.
title: "Flow tracker — "
labels: flow-tracker
---

## Phạm vi

- **Use case:** UC-XXX
- **Các bước:** (ví dụ: S1-S2, hoặc "tất cả")
- **Nhánh thay thế:** (ví dụ: A1, A3, hoặc "tất cả")
- **FR liên quan:** FR-NNN, FR-NNN
- **NFR liên quan:** NFR-NNN
- **Plans:** plans/UC-XXX-short-label/

## Phase 1: Nghiên cứu
<!-- Gate: tất cả ticket nghiên cứu trong phạm vi đã đóng -->

_Ticket sẽ được thêm khi danh sách câu hỏi nghiên cứu được tạo._

## Phase 2: Kế hoạch kiểm thử
<!-- Gate: tất cả ticket test stub đã đóng -->
<!-- Blocked by: Phase 1 hoàn tất -->

_Ticket sẽ được thêm khi kế hoạch kiểm thử được tạo._

## Phase 3: Kế hoạch implementation
<!-- Gate: kế hoạch đã review và chấp nhận -->
<!-- Blocked by: Phase 2 hoàn tất -->

- [ ] Kế hoạch implementation đã review và chấp nhận

## Phase 4: Implementation
<!-- Gate: tất cả ticket impl đã đóng, test xanh -->

_Ticket sẽ được thêm khi kế hoạch implementation được chấp nhận._

## Phase 5: Kiểm thử sau implementation
<!-- Gate: tất cả ticket post-impl đã đóng -->

_Ticket sẽ được thêm cùng lúc với ticket implementation._

## Phase 6: Xác nhận
<!-- Gate: issue này đóng -->
<!-- Blocked by: Phase 5 hoàn tất -->

- [ ] Toàn bộ test suite pass
- [ ] Điều kiện chấp nhận đã xác nhận
- [ ] Smoke tests pass
