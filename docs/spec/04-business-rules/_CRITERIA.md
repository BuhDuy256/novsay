# Gate: Quy tắc nghiệp vụ

Template: `_TEMPLATE.md`. Phong cách: `../_STYLE.md`. Được trích dẫn bởi: `../02-use-cases/`, `../03-requirements/fr/`, `../03-requirements/nfr/`, `../01-product-vision/`.

## 1. BR là gì, và không là gì

**BR định nghĩa giá trị mà hành vi sản phẩm phụ thuộc.** Giá trị là tập cho phép, giới hạn, ngưỡng, quota, thời gian giữ, hay danh sách định nghĩa "cái gì tính". Hành vi áp dụng giá trị là FR. BR nói giá trị là gì.

> FR: "Hệ thống từ chối link không khớp quy tắc nguồn [BR-xxx]."
> BR-xxx: các nguồn được chấp nhận, và dạng link của mỗi nguồn.

| Nếu nội dung là... | Thì nó thuộc |
|---|---|
| Hệ thống hiện, giữ, đổi, tạo hay từ chối gì, và khi nào | `../03-requirements/fr/`. FR trích dẫn BR này |
| Quy tắc không có giá trị riêng, như "không thể bắt đầu phiên mới khi đang nghe" | `../03-requirements/fr/` |
| Phán đoán của model không có giá trị viết ra được | `../03-requirements/fr/`, với điều kiện đánh giá |
| Thời gian chờ, mục tiêu tin cậy, bảo mật, riêng tư, dễ tiếp cận | `../03-requirements/nfr/` |
| Mục tiêu, hành trình, bước, ý định người dùng | `../02-use-cases/` |
| Hệ thống giữ hay kiểm giá trị thế nào: code, storage, cấu hình | ADR hoặc công việc kiến trúc |
| Sản phẩm trông thế nào hay người dùng vận hành thế nào | Công việc thiết kế UI (chưa có folder) |

Marker `[BR-?: chủ đề]` gọi tên một chủ đề, không phải quyết định. Viết quy tắc có thể cho thấy chủ đề đó không có giá trị riêng. Marker chỉ được thay bằng BR phủ trọn nghĩa; phủ một phần thì marker giữ nguyên và báo phần thiếu.

### Độ hạt và giá trị

- **Một BR** là một quy tắc gắn kết. Giá trị của nó quản một quyết định và đổi vì lý do liên quan.
- **Nhiều giá trị** có thể chung một BR. Không tách quy tắc gắn kết chỉ vì nhiều giá trị; không gộp quy tắc không liên quan để ít file.
- **Không trùng.** Trước khi viết, tìm các phát biểu và giá trị trong folder.

Mỗi giá trị là block `### V-n · Tên` với trường Giá trị. Giá trị chính xác: số có đơn vị; cận nói gồm hay không giới hạn; danh sách nói đóng hay mở. Giá trị đủ chính xác để điều kiện FR test tại và vượt giá trị. Giá trị không chứa hành vi — hệ thống làm gì tại giới hạn thì viết ở FR.

### ID và file

- Một BR mỗi file: `BR-xxx.md`. `xxx` ba chữ số. `id` bằng tên file.
- ID mới theo ID cao nhất hiện có hoặc đã bỏ. ID không đổi khi tiêu đề, lời văn hay giá trị đổi; không dùng lại, không đánh lại số.
- ID chỉ bỏ khi quy tắc rời mô hình hành vi hoặc gộp vào BR khác. ID bỏ ghi ở dưới kèm ngày và BR nó gộp vào.
- ID giá trị là `V-1`, `V-2` trong một BR, không đánh lại số.

ID BR đã loại bỏ: không có.

### Liên kết

Liên kết chỉ từ trên xuống. Use case (Hệ thống hoặc Khi), FR, NFR hoặc tầm nhìn trích dẫn BR bằng `[BR-xxx]`.

- BR không gọi tên use case, bước, nhánh, FR hay NFR. Nó không trích dẫn BR khác.
- Để tìm thứ trích dẫn BR, tìm ID của nó trong các file spec.

### Một nguồn chân lý

Giá trị nằm ở đúng một BR. File spec khác không bao giờ nêu nó, diễn giải thành số hay liệt kê mục được phép; chúng trích dẫn ID. Đổi giá trị chỉ đổi BR; cùng một change tìm các file trích dẫn BR cho văn bản dựa vào giá trị cũ, và báo từng file.

## 2. Tiêu chí

"Kiểm" là lớp dự kiến: *Lint* = máy kiểm được, *Review* = phán đoán người, *CI* = kiểm chéo. Chưa có công cụ nên review làm cả Lint lẫn CI.

| ID | Tiêu chí | Ngăn chặn | Kiểm |
|---|---|---|---|
| BRG-01 | BR định nghĩa giá trị của một quy tắc mà hành vi sản phẩm phụ thuộc. Không hành vi, mục tiêu, journey, mục tiêu chất lượng, giao diện, kiến trúc, tiến độ, phiên bản | Hành vi viết hai lần; giá trị giấu trong hành vi | Review |
| BRG-02 | Độ hạt theo mục 1: một quy tắc gắn kết; nhiều giá trị liên quan được phép; tách cho hành vi/lý do không liên quan; không giá trị định nghĩa hai lần | File quy tắc khổng lồ; cùng giá trị ở hai nơi | Review |
| BRG-03 | Mỗi giá trị chính xác: số có đơn vị; cận gồm hay không; danh sách đóng hay mở. FR test được tại và vượt giá trị | Giá trị hai người áp dụng hai cách | Review |
| BRG-04 | File theo `_TEMPLATE.md`: frontmatter `id` và `title`; trường Quy tắc theo thứ tự; ít nhất một block giá trị. `Vì sao` trống thì bỏ dòng. `Chưa xác định` và `Ghi chú` bỏ khi trống | File không so/kiểm được | Lint (trường, thứ tự) |
| BRG-05 | Giá trị chờ ghi `chưa đặt`. Không đoán số, dải hay "khoảng". Không file nào trình nó như giới hạn đã duyệt | Giới hạn bịa; giá trị mở bị đọc là đã quyết | Lint (`chưa đặt`) + Review |
| BRG-06 | Mục `Chưa xác định` nêu khía cạnh mở không phải giá trị, một dòng, kết thúc "Chờ chốt.". Giá trị chưa quyết là `chưa đặt`, không phải mục ở đây | Câu hỏi mở thành quy tắc khi chưa quyết | Review |
| BRG-07 | Giá trị nằm ở một BR. Use case, FR, NFR, tầm nhìn trích dẫn ID, không nêu lại giá trị. Marker chỉ được thay khi BR phủ trọn nghĩa | Cùng giá trị nhiều file; marker bị xóa bởi chủ đề tương tự | Lint (số ở file trích dẫn) + CI (ID tồn tại) + Review |
| BRG-08 | Tên file `BR-xxx.md` ba chữ số, bằng frontmatter `id`. ID duy nhất, không đánh lại số. ID bỏ ghi ở mục 1, không dùng lại. BR không gọi tên use case, bước, nhánh, FR, NFR hay BR khác | Hai nghĩa một ID; liên kết trỏ lên | Lint (tên, định dạng) + CI (duy nhất) |
| BRG-09 | Văn bản theo `../_STYLE.md` quy tắc 1–10 trong Phát biểu và Giá trị. Không giao diện (quy tắc 11) | Quy tắc hai nghĩa; thiết kế bị chốt qua quy tắc | Lint (từ cấm) + Review |

## 3. Minh hoạ

**BRG-01: phán đoán không phải giá trị.**

> Không đạt: BR "hệ thống hỏi khi nguồn không rõ". Đó là hành vi kèm phán đoán, là FR.
> Đạt: bạn quyết có một danh sách các loại nguồn được nhận. BR liệt kê các loại đó.

**BRG-07: một nơi cho giá trị.**

> Không đạt: use case nói "Hệ thống lùi vài giây khi gián đoạn [BR-000]."
> Đạt: "Hệ thống lùi theo giới hạn lùi [BR-000]." Con số nằm ở BR-000.
