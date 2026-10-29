---
scope: ""
title: ""
created: DD-MM-YYYY
---

# Kế hoạch kiểm thử — {scope}

## Phạm vi

- **Use case:** UC-XXX
- **Các bước:** S1-S2 (hoặc "tất cả")
- **Nhánh thay thế:** A1, A3 (hoặc "tất cả")
- **FR liên quan:** FR-NNN, FR-NNN
- **NFR liên quan:** NFR-NNN

## Loại kiểm thử

| Loại | Mục đích | Thời điểm |
|---|---|---|
| Acceptance | Kiểm tra trực tiếp điều kiện chấp nhận của FR | Trước implementation |
| Security | Kiểm tra các AC liên quan bảo mật và mô hình mối đe dọa | Trước implementation |
| Unit | Kiểm tra từng hàm/module riêng lẻ | Cùng lúc implementation |
| Integration | Kiểm tra các module làm việc với nhau | Sau implementation |
| E2E | Kiểm tra toàn bộ luồng UC từ đầu tới cuối | Sau implementation |
| Smoke | Tập kiểm tra tối thiểu chứng minh build không hỏng | Sau implementation |
| Recovery / Resilience | Kiểm tra hành vi khi gặp lỗi | Sau implementation |
| Regression | Ngăn lỗi đã sửa xuất hiện lại | Sau implementation (liên tục) |
| Performance | Kiểm tra mục tiêu hiệu năng của NFR | Sau implementation |

## Kiểm thử trước implementation

### Acceptance tests

| AC | FR | Mô tả kiểm thử | Ticket | Trạng thái |
|---|---|---|---|---|
| AC-1 | FR-NNN | | #N | open |

### Security tests

| Mối đe dọa / AC | FR | Mô tả kiểm thử | Ticket | Trạng thái |
|---|---|---|---|---|
| | FR-NNN | | #N | open |

## Kiểm thử cùng implementation (gộp vào ticket impl)

| Module / hàm | FR | Mô tả kiểm thử | Ticket impl |
|---|---|---|---|
| | FR-NNN | | #N |

## Kiểm thử sau implementation

### E2E tests

| Luồng | Bước UC | Mô tả kiểm thử | Ticket | Trạng thái |
|---|---|---|---|---|
| Luồng chính | S1-S6 | | #N | open |

### Smoke tests

| Kiểm tra | Mô tả | Ticket | Trạng thái |
|---|---|---|---|
| | | #N | open |

### Recovery / Resilience tests

| Tình huống lỗi | Nhánh thay thế UC | Mô tả kiểm thử | Ticket | Trạng thái |
|---|---|---|---|---|
| | A-N | | #N | open |

### Performance tests

| Chỉ số | NFR | Mục tiêu | Mô tả kiểm thử | Ticket | Trạng thái |
|---|---|---|---|---|---|
| | NFR-NNN | | | #N | open |

### Regression tests

Thêm khi phát hiện và sửa bug. Không lên kế hoạch trước.
