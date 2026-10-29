---
id: TF-001
title: "Lấy nội dung website"
created-at: "21-10-2026"
updated-at: "29-10-2026"
---

# Lấy nội dung website

## UC-001/RQ-1: Cấu trúc URL chương trên Novel543 như thế nào?

> Quy tắc nào phân biệt link chương với link trang chủ, thư mục truyện hoặc trang khác?

* **Phục vụ:** FR-001 AC-1/AC-2, BR-001 V-2
* **Ticket:** [#2](https://github.com/BuhDuy256/novsay/issues/2)
* **Trạng thái:** answered

1. Một website sẽ luôn có nhiều loại trang: Homepage, Landing Page, Table of Contents, Search Page and other pages.

2. URL của 1 Page có các attributes sau cần quan tâm:
    - **Hostname**: Là novel543.com, hay là www.novel543.com, hay là gì khác?
    - **Cấu trúc path** của một link chương?
    - **Dấu hiệu phân biệt link** giữa nhiều loại pages của website đó?
    - **Các biến thể hợp lệ** như URL có query, có `/` cuối hoặc dạng gì đó khác?

3. **Regex Matching** là check xem các URL có match với URL template (gọi là Regex) không? (hay nói cách khác các URL phải cùng chung pattern)
=> Chỉ phù hợp với URL có cấu trúc cố định như: sau /book/ phải là số, rồi đến /chapter/ và một số khác.

4. **URL Component Validation (URL Parser)** là tách các URL ra thành các phần nhỏ hơn để check?

> Protocol : https:
> Hostname : www.example.com
> Path     : /book/123/chapter/456

5. **Regex Matching Trade-off**: Nếu chỉ dùng Regex Matching thì yêu cầu bao giờ Website URL cũng phải chung pattern
=> Không thể được.

6. **URL Component Validation Trade-off**: Nếu chỉ tách các thành phần ra mà không nghiên cứu kĩ các thành phần thì dễ nhận nhầm phần "Sau Hostname" không phải link chương mình muốn.

7. **Hybrid solution**: Dùng URL Parser để tách các thành phần ra rồi sau đó dùng regex để kiểm tra riêng từng phần.

8. Có URL là 1 chuyện, có fetch được không là vấn đề khác? Và fetch được không còn dựa vào ta có gây ra SSRF cho target website không? Rồi URL có truy cập được? Website có thông tin ta cần hay ko?
=> Dẫn tới các research questions sau này.

---

## UC-001/RQ-2: SSRF prevention cho link nguồn

> Làm thế nào để ngăn link hoặc chuyển hướng truy cập vào mạng riêng của server?
> Cần biết cách kiểm tra IP sau DNS resolution, chặn private/loopback ranges, và xử lý redirect chains.

* **Phục vụ:** FR-001 AC-3
* **Ticket:** [#3](https://github.com/BuhDuy256/novsay/issues/3)
* **Trạng thái:** open

<!-- Điền kết quả nghiên cứu ở đây. -->

---

## UC-001/RQ-3: Cấu trúc HTML trang chương Novel543

> Novel543 trả nội dung chương bằng HTML tĩnh, JavaScript render hay API riêng?
> Cấu trúc HTML của trang chương (selector cho tiêu đề và vùng truyện) là gì?

* **Phục vụ:** FR-002 AC-1
* **Ticket:** [#4](https://github.com/BuhDuy256/novsay/issues/4)
* **Trạng thái:** open

<!-- Điền kết quả nghiên cứu ở đây. Bao gồm:
* Kết quả fetch thử trang chương thực tế
* CSS selector cho vùng tiêu đề
* CSS selector cho vùng văn bản truyện
* Các element cần loại bỏ (quảng cáo, điều hướng, bình luận)
-->

---

## UC-001/RQ-4: Cơ chế chống bot của Novel543

> Fetch từ backend Node có bị chặn không? Có Cloudflare, CAPTCHA, rate limit không?

* **Phục vụ:** FR-002 AC-1/AC-3, FR-007
* **Ticket:** [#5](https://github.com/BuhDuy256/novsay/issues/5)
* **Trạng thái:** open

<!-- Điền kết quả nghiên cứu ở đây. Bao gồm:
* Kết quả fetch thử từ backend (curl hoặc Node fetch)
* Response headers đáng chú ý (cf-ray, server, etc.)
* Status code nhận được
* Có bị chặn không, cơ chế gì
-->
