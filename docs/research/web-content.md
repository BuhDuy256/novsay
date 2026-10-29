---
id: TF-001
title: "Lấy nội dung website"
created-at: "21-10-2026"
updated-at: "29-10-2026"
---

# Lấy nội dung website

## UC-001/RQ-1: Cấu trúc URL chương trên website nguồn

> Quy tắc nào phân biệt link chương với link trang chủ, thư mục truyện hoặc trang khác trên các website tiểu thuyết?

* **Phục vụ:** FR-001 AC-1/AC-2, BR-001 V-2
* **Ticket:** [#2](https://github.com/BuhDuy256/novsay/issues/2)
* **Trạng thái:** answered

1. Một website sẽ luôn có nhiều loại trang: Homepage, Landing Page, Table of Contents, Search Page and other pages.

2. URL của 1 Page có các attributes sau cần quan tâm:
    - **Hostname**: Thuộc website nguồn nào? (ví dụ: novel543.com, www.novel543.com)
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
* **Trạng thái:** answered

1. Context ở đây là Attacker có thể lạm dụng Novsay để tổ chức tấn công tới các address của internal service mà user không truy cập được. Ví dụ:
1.1. 127.0.0.1: chính server đang chạy Novsay. Cụ thể hơn:
    - Giả sử kẻ tấn công nhập URL sau vào ô lấy chương: `http://127.0.0.1:9000/admin`
    - Nếu Novsay không kiểm tra đích truy cập:
        1. Server Novsay nhận URL.
        2. Server Novsay gửi request tới cổng 9000 trên chính nó.
        3. Trang quản trị nhận request từ nội bộ và trả nội dung.
        4. Nếu Novsay trả nội dung đó cho người nhập URL, dữ liệu quản trị có thể bị lộ.
1.2. Địa chỉ mạng riêng: có thể chứa database hoặc dịch vụ nội bộ.
1.3. Một số địa chỉ đặc biệt của môi trường hosting: có thể cung cấp thông tin của máy chủ.

2. Các vấn đề từ proposed solutions:

| Phương án | Cách làm | Điều cần xem xét |
|---|---|---|
| Dùng thư viện "ssrf-req-filter" (npm) | Nhờ thư viện thực hiện một phần kiểm tra SSRF | Phải xác minh khả năng bảo vệ và tương thích với HTTP client |
| Tự kiểm tra IP | Tự giải DNS và kiểm tra các nhóm địa chỉ | Phải xử lý IPv4, IPv6 và thay đổi DNS |
| Allowlist hostname + kiểm tra IP (Whilelist) | Chỉ nhận hostname đã cho phép, đồng thời kiểm tra đích kết nối | Cần cập nhật khi thêm nguồn truyện |

3. **Có thể triển khai Hybrid**: Library + Whitelist

---

## UC-001/RQ-3: Cấu trúc HTML trang chương website nguồn

> Website nguồn trả nội dung chương bằng HTML tĩnh, JavaScript render hay API riêng?
> Cấu trúc HTML của trang chương (selector cho tiêu đề và vùng truyện) là gì? Mỗi site có selector khác nhau thì xử lý thế nào?

* **Phục vụ:** FR-002 AC-1
* **Ticket:** [#4](https://github.com/BuhDuy256/novsay/issues/4)
* **Trạng thái:** open

<!-- Điền kết quả nghiên cứu ở đây. Bao gồm:
* Kết quả fetch thử trang chương thực tế
* CSS selector cho vùng tiêu đề
* CSS selector cho vùng văn bản truyện
* Các element cần loại bỏ (quảng cáo, điều hướng, bình luận)
-->

1. Website content có thể được hình thành theo nhiều cách khác nhau:

| Trường hợp | Website hoạt động thế nào? | Hướng lấy nội dung |
|---|---|---|
| Có sẵn trong HTML | Response HTML đã chứa văn bản chương | Phân tích HTML và lấy vùng truyện |
| Được JavaScript thêm vào | HTML ban đầu chưa có truyện; JavaScript chạy rồi thêm nội dung | Tìm cách lấy dữ liệu hoặc dùng trình duyệt tự động |
| Được lấy qua API riêng | Trang gọi một endpoint khác để lấy dữ liệu chương | Xem xét gọi endpoint đó nếu phù hợp |

2. Một content của một trang truyện có thể gồm nhiều phần: "Title", "Truyện", "Menu", "Advertisement" và "Nút chuyển trang"
=> **Làm sao xác định đúng "Title" và "Truyện"?**

3. Cần nhớ về cấu trúc của HTML để hiểu cách xử lí?

```
<h1 class="chapter-title">Chương 1</h1>

<div id="chapter-content">
  <p>Đoạn truyện thứ nhất...</p>
  <p>Đoạn truyện thứ hai...</p>
</div>

<a href="...">Chương tiếp theo</a>
```
=> Ta sẽ dựa vào "chapter-title" hay gọi là các **selector** của các HTML tag attributes như class, id, ... để xác định content nằm ở đâu?
=> Mỗi website nguồn có selector khác nhau → cần **site config** chứa selector riêng cho từng site (hostname → {titleSelector, contentSelector, removeSelectors}).

---

## UC-001/RQ-4: Cơ chế chống bot của website nguồn

> Website nguồn có cơ chế chống bot (Cloudflare, CAPTCHA, rate limit) không? Fetch từ backend Node có bị chặn không?

* **Phục vụ:** FR-002 AC-1/AC-3, FR-007
* **Ticket:** [#5](https://github.com/BuhDuy256/novsay/issues/5)
* **Trạng thái:** open

<!-- Điền kết quả nghiên cứu ở đây. Bao gồm:
* Kết quả fetch thử từ backend (curl hoặc Node fetch)
* Response headers đáng chú ý (cf-ray, server, etc.)
* Status code nhận được
* Có bị chặn không, cơ chế gì
-->
