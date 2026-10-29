---
scope: ""
title: ""
created: DD-MM-YYYY
---

# Danh sách nghiên cứu — {scope}

## Phạm vi

<!-- Mô tả chính xác phạm vi của lần build này. -->

- **Use case:** UC-XXX
- **Các bước:** S1-S2 (hoặc "tất cả")
- **Nhánh thay thế:** A1, A3 (hoặc "tất cả")
- **FR liên quan:** FR-NNN, FR-NNN
- **NFR liên quan:** NFR-NNN

## Cách dùng

Mỗi câu hỏi gắn với FR/NFR mà nó phục vụ. Trả lời bằng cách nghiên cứu
(với sự hỗ trợ của agent hoặc tự nghiên cứu). File deliverable đã được tạo sẵn —
mở file, điền nội dung vào phần `<!-- Điền kết quả -->` hoặc các mục trống.

> **Lưu ý:** Mọi tham chiếu `#N` và đường dẫn file phải là link clickable.
> Xem WORKFLOW.md "Linking convention".

## Mô hình luồng

<!-- Mô tả từng bước kỹ thuật xảy ra khi UC chạy. Mỗi bước cho thấy
     hệ thống làm gì ở runtime. Câu hỏi nghiên cứu được gắn vào bước
     mà chúng phát sinh. -->

### {S1 — Tên bước}

1. **S1.1** — {Mô tả hành động kỹ thuật cụ thể}
2. **S1.2** — {Hành động tiếp theo} → **RQ-N** _(chưa biết cách làm)_
3. **S1.3** — {Hành động tiếp theo}

### {S2 — Tên bước}

1. **S2.1** — {Mô tả hành động kỹ thuật}
2. **S2.2** — {Hành động} → **RQ-N** _(cần quyết định)_

### Nhánh thay thế

#### {A1 — Tên nhánh} (tách từ S1.2)

1. **A1.1** — {Xử lý lỗi/ngoại lệ} → **RQ-N** _(chưa biết xử lý thế nào)_

## Deliverable map

<!-- Link mỗi RQ đến file deliverable. Dùng full Markdown link. -->

| RQ | Loại | File |
|---|---|---|
| RQ-1 | research | [docs/research/topic.md](https://github.com/{owner}/{repo}/blob/main/docs/research/topic.md) |

## Câu hỏi

### FR-NNN — Tên

| # | Câu hỏi | Vì sao quan trọng | Ticket | Trạng thái |
|---|---|---|---|---|
| RQ-1 | | | [#N](https://github.com/{owner}/{repo}/issues/N) | open |

### NFR-NNN — Tên

| # | Câu hỏi | Vì sao quan trọng | Ticket | Trạng thái |
|---|---|---|---|---|
| RQ-N | | | [#N](https://github.com/{owner}/{repo}/issues/N) | open |

## Trạng thái

- `open` — chưa bắt đầu
- `researching` — đang nghiên cứu
- `answered` — đã trả lời trong docs/research/
- `decided` — đã quyết định trong docs/decisions/DEC-NNN
