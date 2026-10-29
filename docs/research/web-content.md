---
id: TF-001
title: "Lấy nội dung website"
created-at: "21-10-2026"
updated-at: "29-10-2026"
---

# Lấy nội dung website

## UC-001/RQ-1: Cấu trúc URL chương trên Novel543 như thế nào?

> Quy tắc nào phân biệt link chương với link trang chủ, thư mục truyện hoặc trang khác?

- **Phục vụ:** FR-001 AC-1/AC-2, BR-001 V-2
- **Ticket:** #2
- **Trạng thái:** open

<!-- Điền kết quả nghiên cứu ở đây. -->

---

## UC-001/RQ-2: SSRF prevention cho link nguồn

> Làm thế nào để ngăn link hoặc chuyển hướng truy cập vào mạng riêng của server?
> Cần biết cách kiểm tra IP sau DNS resolution, chặn private/loopback ranges, và xử lý redirect chains.

- **Phục vụ:** FR-001 AC-3
- **Ticket:** #3
- **Trạng thái:** open

<!-- Điền kết quả nghiên cứu ở đây. -->

---

## UC-001/RQ-3: Cấu trúc HTML trang chương Novel543

> Novel543 trả nội dung chương bằng HTML tĩnh, JavaScript render hay API riêng?
> Cấu trúc HTML của trang chương (selector cho tiêu đề và vùng truyện) là gì?

- **Phục vụ:** FR-002 AC-1
- **Ticket:** #4
- **Trạng thái:** open

<!-- Điền kết quả nghiên cứu ở đây. Bao gồm:
- Kết quả fetch thử trang chương thực tế
- CSS selector cho vùng tiêu đề
- CSS selector cho vùng văn bản truyện
- Các element cần loại bỏ (quảng cáo, điều hướng, bình luận)
-->

---

## UC-001/RQ-4: Cơ chế chống bot của Novel543

> Fetch từ backend Node có bị chặn không? Có Cloudflare, CAPTCHA, rate limit không?

- **Phục vụ:** FR-002 AC-1/AC-3, FR-007
- **Ticket:** #5
- **Trạng thái:** open

<!-- Điền kết quả nghiên cứu ở đây. Bao gồm:
- Kết quả fetch thử từ backend (curl hoặc Node fetch)
- Response headers đáng chú ý (cf-ray, server, etc.)
- Status code nhận được
- Có bị chặn không, cơ chế gì
-->
