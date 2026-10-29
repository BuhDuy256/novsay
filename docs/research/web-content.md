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
* **Trạng thái:** answered

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

1. Thấy truyện trên Chrome != Server Novsay cũng lấy được nội dung. Website có thể triển khai các cơ chế blocker:

| Cơ chế | Ý nghĩa | Ảnh hưởng tới Novsay |
|---|---|---|
| CAPTCHA | Yêu cầu người truy cập hoàn thành bước xác minh | Request lấy chương thông thường không tự hoàn thành được |
| JavaScript challenge | Yêu cầu trình duyệt chạy JavaScript để xác minh | Gửi HTTP GET đơn thuần có thể chưa lấy được chương |
| Rate limit | Giới hạn số request trong một khoảng thời gian | Gửi quá nhiều có thể bị từ chối tạm thời |
| Chặn theo IP hoặc dấu hiệu request | Từ chối một số nguồn hoặc kiểu truy cập | Request từ môi trường hosting có thể bị chặn |

2. Fetch thử bằng Node.js có lấy được truyện không?
   - Môi trường: Node.js v22.19.0, Windows 11, local machine, kết nối internet thông thường.
   - URL đã thử:

   | URL | Status | `cf-mitigated` | `server` | `cf-ray` | Title trong response |
   |---|---|---|---|---|---|
   | `https://www.novel543.com/` | 403 | `challenge` | `cloudflare` | `a521aa9098509212-HKG` | "Just a moment..." |
   | `https://www.novel543.com/0327629882/8096_1.html` | 403 | `challenge` | `cloudflare` | `a521aaa58cb6d76d-HKG` | "Just a moment..." |
   | `https://novel543.com/` | 403 | `challenge` | `cloudflare` | `a521aabb7e3fe2f0-HKG` | "Just a moment..." |

   - Thời điểm: 2026-10-29T10:58 UTC. Gửi tuần tự, cách nhau 3 giây. Dùng `fetch()` có browser User-Agent, timeout 15 giây, follow redirect, không cookie.
   - URL chương `0327629882/8096_1.html` lấy từ issue trên GitHub của WebToEpub, là URL chương công khai từng hoạt động trên novel543.com. Không tự đoán URL.
   - Cả 3 request đều trả 403. Response body dài khoảng 5600–5800 bytes, không chứa văn bản truyện.
=> Node.js fetch không lấy được nội dung chương trong điều kiện đã thử. Cả homepage, chapter URL và bare domain đều bị chặn giống nhau.

3. Response 403 này cho thấy cơ chế gì?
   - Header `cf-mitigated: challenge` có nghĩa Cloudflare đã chủ động chặn request và trả trang challenge thay vì nội dung thật. Đây không phải 403 từ origin server mà từ Cloudflare proxy.
   - Response body chứa `<title>Just a moment...</title>` — trang chờ xác minh của Cloudflare. HTML chứa JavaScript tải từ `challenges.cloudflare.com` để chạy challenge phía client.
   - Trong HTML, trường `cType: 'non-interactive'` cho thấy đây là Cloudflare Managed Challenge dạng non-interactive. Nghĩa là nếu client chạy được JavaScript và pass challenge tự động, sẽ nhận được cookie `cf_clearance` rồi truy cập bình thường. Nhưng Node.js fetch không chạy JavaScript nên không hoàn thành được challenge.
   - `cf-ray` kết thúc bằng `-HKG` cho thấy request được route qua Cloudflare PoP tại Hong Kong. Điều này xác nhận request đã tới được Cloudflare, không phải lỗi DNS hay TLS.
=> Cơ chế quan sát được là Cloudflare Managed Challenge (non-interactive JS challenge). Không phải CAPTCHA, không phải rate limit, không phải chặn IP cụ thể.

4. Đối chiếu bằng curl cho kết quả gì?
   - `curl.exe` với browser User-Agent: cùng kết quả 403, `cf-mitigated: challenge`.
   - `curl.exe` không có browser User-Agent (UA mặc định `curl/8.23.0`): cùng kết quả 403, `cf-mitigated: challenge`.
=> Cloudflare challenge áp dụng cho mọi request chưa có `cf_clearance` cookie, không phân biệt User-Agent. Thay đổi UA không giúp vượt qua.

5. HTTP 200 có nghĩa là lấy được truyện chưa?
=> Câu hỏi này chưa kiểm chứng được vì không request nào trả 200. Nếu sau này tìm cách qua được challenge, vẫn cần kiểm tra response body có chứa văn bản truyện hay là trang xác minh hoặc trang lỗi. Status 200 chỉ cho biết HTTP thành công, không đảm bảo nội dung là chương truyện.

6. Có header `cf-ray` thì kết luận bị Cloudflare chặn được không?
=> Chưa đủ. `cf-ray` chỉ cho thấy request đi qua Cloudflare CDN. Nhiều website dùng Cloudflare nhưng không bật challenge. Bằng chứng chặn thực sự là header `cf-mitigated: challenge` kết hợp với status 403 và response body chứa trang challenge.

7. Kết quả này có ý nghĩa gì với Novsay?
   - Node.js `fetch()` từ backend không thể lấy nội dung chương từ novel543.com trong trạng thái hiện tại của website. Cloudflare chặn ở tầng proxy trước khi request tới origin server.
   - Đây là giới hạn kiến trúc: HTTP client đơn thuần (fetch, axios, got, curl) không chạy JavaScript nên không hoàn thành challenge. Thay đổi header hay User-Agent không giúp vượt qua.
   - Các hướng xử lý có thể xem xét:
     - Dùng headless browser (Playwright, Puppeteer) để chạy JS challenge và lấy `cf_clearance` cookie. Tăng độ phức tạp triển khai và tài nguyên server.
     - Chấp nhận giới hạn: khi gặp challenge, báo lỗi cho user và không thử lại tự động vì retry không giải quyết được challenge.
     - Tìm website nguồn khác không có Cloudflare challenge làm nguồn thay thế hoặc nguồn đầu tiên.
   - Về retry (FR-007): retry chỉ có ý nghĩa khi lỗi là tạm thời (timeout, 429, 5xx). Challenge 403 từ Cloudflare không phải lỗi tạm thời — gửi lại cùng request sẽ nhận cùng kết quả. Novsay nên phân biệt loại lỗi: nếu response có `cf-mitigated: challenge` thì dừng và báo "website yêu cầu xác minh, không thể lấy tự động", không thử lại.

8. Giới hạn của kết quả nghiên cứu:
   - Chỉ thử từ một máy local tại một thời điểm, một vị trí mạng. Kết quả từ hosting (VPS, cloud function) có thể khác — Cloudflare có thể áp dụng mức challenge khác nhau theo IP range hoặc ASN.
   - Chỉ thử 3 URL, cách nhau 3 giây. Chưa có thông tin về rate limit vì chưa request nào vượt qua challenge.
   - Cloudflare có thể thay đổi mức bảo vệ theo thời gian. Website owner có thể tắt hoặc điều chỉnh challenge bất kỳ lúc nào.
   - URL chương lấy từ issue cũ trên GitHub, có thể không còn hợp lệ trên website hiện tại, nhưng không ảnh hưởng kết luận vì challenge chặn ở mọi URL.
   - Chưa thử headless browser hoặc bất kỳ phương pháp nào khác ngoài HTTP GET đơn thuần.

9. Tái hiện:

```
node "C:\Users\Duy\AppData\Local\Temp\claude\C--Users-Duy-Desktop-novsay\a4d93404-4a6d-4fe9-9cf0-40653c36bc51\scratchpad\rq4-fetch-test.mjs"
```

   Hoặc curl nhanh:

```
curl.exe -s -D - -o NUL "https://www.novel543.com/" -H "User-Agent: Mozilla/5.0"
```

   Kết quả mong đợi: 403, `cf-mitigated: challenge`, body chứa "Just a moment...".

10. Thử website nguồn thay thế thì sao? Thử nhiều site tiểu thuyết tiếng Trung khác để xem chặn Cloudflare có phải là vấn đề riêng của novel543 hay phổ biến cả thể loại.
   - Môi trường: cùng máy local, cùng thời điểm (2026-10-29T11:08–11:14 UTC). Dùng `curl.exe` (Schannel TLS trên Windows) với browser UA, sau đó đối chiếu bằng Node.js `fetch()`.
   - Kết quả homepage:

   | Website | curl status | Cơ chế chặn | Ghi chú |
   |---|---|---|---|
   | `www.69shu.com` | 301 → `69shuba.com` | Cloudflare | Redirect sang domain khác |
   | `www.69shuba.com` | 403 | Cloudflare challenge | `cf-mitigated: challenge` |
   | `www.biquge.com.cn` | TLS error (exit 35) | — | Không kết nối được |
   | `www.xbiquge.so` | 403 | FEICDN | CDN khác, cũng chặn |
   | `www.ddyueshu.com` | 403 | CDN | Tương tự |
   | `www.uukanshu.cc` | 301 → Cloudflare challenge | Cloudflare | |
   | `www.qidian.com` | 202 | WAF captcha riêng | `x-waf-captcha-referer` cookie, không phải Cloudflare |
   | `www.hetushu.com` | 403 | Cloudflare challenge | `cf-mitigated: challenge` |
   | `www.bqg225.com` | 301 → `bqgen.cc` | Cloudflare | Redirect |
   | `www.bqgen.cc` | 200 | Không chặn homepage | Nhưng chapter page redirect sang verify |
   | `www.trxs.cc` | 200 | Không chặn homepage | Chapter page: phụ thuộc TLS client |

=> Đa số site tiểu thuyết tiếng Trung đều dùng Cloudflare hoặc CDN tương đương có cơ chế chặn. Đây không phải vấn đề riêng của novel543.

11. bqgen.cc (笔趣阁) có lấy được chương không?
   - Homepage trả 200 với 29KB HTML, chứa danh sách truyện và link thật.
   - Nhưng khi fetch chapter page (ví dụ `/html/104815/1.html`), site redirect sang `/user/verify.html` — trang xác minh riêng của site (không phải Cloudflare). Trang này dùng JavaScript đặt cookie `getsite` rồi redirect tiếp sang `/userverify`.
=> Node fetch không lấy được chương trên bqgen.cc. Site có cơ chế chặn bot riêng ở tầng ứng dụng, tách biệt với Cloudflare.

12. trxs.cc (同人小说网) có lấy được chương không? Đây là phát hiện quan trọng nhất.
   - Homepage: `www.trxs.cc` trả 200. Bare domain `trxs.cc` trả 403 Cloudflare challenge.
   - Chapter URL pattern: `/tongren/{novel_id}/{chapter}.html`
   - Kết quả fetch chapter `/tongren/6201/1.html`:

   | Client | Status | Nội dung | `cf-mitigated` |
   |---|---|---|---|
   | `curl.exe` (Schannel TLS) | 200 | Có văn bản truyện tiếng Trung | Không có |
   | `curl.exe` với UA `NovayScraper/0.1` | 200 | Có văn bản truyện tiếng Trung | Không có |
   | Node.js `fetch()` (OpenSSL TLS) | 403 | Cloudflare challenge | `challenge` |

   - curl lấy được chapter hoàn chỉnh: title "人在木叶，战场收尸十年 第1章", content div `class="read_chapterDetail"`, nhiều `<p>` chứa cốt truyện tiếng Trung, 9599 bytes. Encoding `gb2312`.
   - Node.js fetch cùng URL, cùng thời điểm, cùng máy: 403 Cloudflare challenge "Just a moment...".

13. Tại sao curl lấy được nhưng Node.js không?
   - Thay đổi User-Agent không ảnh hưởng: curl với UA `NovayScraper/0.1` (hoàn toàn không giống browser) vẫn trả 200.
=> Cloudflare không phân biệt dựa trên User-Agent header.
   - Khác biệt chính giữa hai client ở đây là TLS stack:
     - `curl.exe` trên Windows dùng Schannel (Windows native TLS). TLS fingerprint (JA3/JA4) của Schannel giống ứng dụng Windows thông thường.
     - Node.js dùng OpenSSL tích hợp. TLS fingerprint của Node.js khác biệt rõ rệt và được Cloudflare nhận diện.
   - TLS fingerprinting là kỹ thuật Cloudflare dùng để phân loại client dựa trên cách client thiết lập kết nối TLS (cipher suites, extensions, thứ tự). Mỗi TLS stack tạo ra fingerprint khác nhau mà không thể thay đổi bằng HTTP headers.
=> Suy luận: Cloudflare trên trxs.cc phân loại client bằng TLS fingerprint. Schannel (curl trên Windows) pass, OpenSSL (Node.js) bị challenge. Đây là suy luận dựa trên quan sát — chưa xác nhận trực tiếp bằng so sánh JA3 hash.

14. Kết quả bổ sung này có ý nghĩa gì với Novsay?
   - Node.js `fetch()` mặc định (dùng undici/OpenSSL) bị Cloudflare nhận diện và challenge trên hầu hết các site đã thử. Đây là giới hạn ở tầng TLS, không giải quyết được bằng thay đổi HTTP headers.
   - Có ít nhất một site (trxs.cc) mà curl trên Windows lấy được chương nhưng Node.js thì không. Nếu deploy Novsay trên hosting Linux, kết quả có thể khác nữa vì TLS fingerprint phụ thuộc OS và TLS library.
   - Về chọn website nguồn đầu tiên (BR-001 V-1): novel543.com chặn mọi client (cả curl). trxs.cc cho phép curl nhưng chặn Node.js. Cả hai đều không hoạt động với Node fetch mặc định.
   - Các hướng kiến trúc cần xem xét:
     - Dùng TLS library khác trong Node.js để thay đổi fingerprint (ví dụ `undici` với custom TLS options, hoặc binding tới BoringSSL/rustls).
     - Gọi curl subprocess từ Node.js thay vì dùng fetch trực tiếp. curl trên server Linux dùng OpenSSL nhưng tạo fingerprint khác Node.js — cần thử riêng.
     - Headless browser (Playwright/Puppeteer) giải quyết cả JS challenge lẫn TLS fingerprint vì dùng Chromium TLS stack.
     - Chọn website nguồn không dùng Cloudflare hoặc có mức bảo vệ thấp hơn. Trong số site đã thử, chưa tìm được site nào Node fetch lấy được chương.
   - Về retry (FR-007): kết luận từ mục 7 vẫn đúng — challenge 403 không phải lỗi tạm thời. Bổ sung: nếu cùng URL mà curl được nhưng Node không, retry bằng Node cũng không thay đổi kết quả.

15. Giới hạn bổ sung:
   - Chưa thử deploy trên Linux hoặc hosting thực tế. curl trên Linux dùng OpenSSL (không phải Schannel), fingerprint sẽ khác — chưa biết Cloudflare xử lý thế nào.
   - Chưa thử headless browser hoặc TLS library thay thế trong Node.js.
   - Chưa tìm được site nào Node.js `fetch()` mặc định lấy được chương thành công.
   - Kết quả trxs.cc có thể thay đổi: Cloudflare điều chỉnh policy liên tục, site owner cũng có thể thay đổi cấu hình.
   - Chưa thử tải nhiều để tìm rate limit vì vẫn chưa vượt qua challenge.

16. Tái hiện bổ sung:

```
node "C:\Users\Duy\AppData\Local\Temp\claude\C--Users-Duy-Desktop-novsay\a4d93404-4a6d-4fe9-9cf0-40653c36bc51\scratchpad\rq4-fetch-test-trxs.mjs"
```

   So sánh cùng URL bằng curl:

```
curl.exe -s -D - -o NUL "https://www.trxs.cc/tongren/6201/1.html" -H "User-Agent: NovayScraper/0.1"
```

   Kết quả mong đợi: curl trả 200, Node fetch trả 403 `cf-mitigated: challenge`.
