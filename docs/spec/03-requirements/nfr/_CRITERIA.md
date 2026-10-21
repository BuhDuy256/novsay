# Gate: Yêu cầu phi chức năng

Template: `_TEMPLATE.md`. Phong cách: `../../_STYLE.md`. Được trích dẫn bởi: `../../02-use-cases/`, `../fr/`, `../../01-product-vision/`. Giá trị quy tắc: `../../04-business-rules/`.

## 1. NFR là gì, và không là gì

**NFR là ràng buộc chất lượng cấp sản phẩm.** Nó nói sản phẩm phải nhanh, đáng tin, bảo mật, riêng tư, chính xác hay dễ tiếp cận tới mức nào, dưới điều kiện đã nêu. Nó được kiểm chứng bằng một phép đo so với mục tiêu, hoặc một kiểm tra thuộc tính bắt buộc.

### Khi nào viết NFR

Một đại lượng đo được không tự cần NFR. Chỉ viết khi cả bốn đúng:

1. Một cam kết sản phẩm cần chất lượng đó, hoặc một rủi ro sản phẩm đã nêu biện minh cho nó.
2. Chất lượng đó đo hoặc kiểm được.
3. Nó thêm ràng buộc chất lượng độc lập cấp sản phẩm; không chỉ lặp hành vi hay điều kiện chấp nhận của FR.
4. Mục tiêu đổi chất lượng sản phẩm cho người dùng. Người dùng không cần thấy: ràng buộc bảo mật, riêng tư, độ tin cậy bảo vệ người dùng mà không hiển thị.

Đại lượng không qua test đầu tiên ở lại trong FR, UI hoặc công việc kỹ thuật. Hành vi mang nghĩa bảo mật (như không hiện khóa) là FR. Mục tiêu chất lượng đầu ra model chỉ là NFR khi bạn biến nó thành cam kết sản phẩm.

### Nội dung thuộc đâu

| Nếu nội dung là... | Thì nó thuộc |
|---|---|
| Hệ thống hiện, giữ, đổi, tạo hay từ chối gì, và khi nào | `../fr/`. FR trích dẫn NFR này |
| Tập cho phép, giới hạn, quota, thời gian giữ một quy tắc định nghĩa | `../../04-business-rules/` |
| Mục tiêu, hành trình, bước người dùng | `../../02-use-cases/` |
| Metric nhóm dùng để xây/chạy code, không hứa với người dùng | Không ở spec. Công việc kỹ thuật |
| Ngưỡng dùng để so/chọn/tinh chỉnh model khi nghiên cứu | Không ở spec. Công việc nghiên cứu |
| Hệ thống đạt mục tiêu thế nào: engine, storage, framework, công cụ | ADR hoặc công việc kiến trúc |
| Sản phẩm trông thế nào hay người dùng vận hành thế nào | Công việc thiết kế UI (chưa có folder) |

### Độ hạt và phép đo

- **Một NFR** phủ một thuộc tính chất lượng cho một phần sản phẩm gắn kết.
- **Nhiều phép đo** có thể chung một NFR khi chúng kiểm cùng chất lượng dưới điều kiện khác nhau.
- **Tách** NFR gộp nhiều thuộc tính chất lượng, hay phần sản phẩm đổi vì lý do không liên quan.
- **Không trùng.** Trước khi viết, tìm các phát biểu trong folder.

Mỗi phép đo là block `### M-n · Tên` với Điều kiện, Đo, Cách đo, Mục tiêu, Đạt khi. `Điều kiện`, `Đo`, `Cách đo` phải đủ rõ để kiểm chứng; `Mục tiêu` và `Đạt khi` có thể `chưa đặt` khi chờ. Không đoán số, dải hay "khoảng" (NFG-04).

### ID và file

- Một NFR mỗi file: `NFR-xxx.md`. `xxx` ba chữ số. `id` bằng tên file.
- ID mới theo ID cao nhất hiện có hoặc đã bỏ. ID không đổi khi tiêu đề hay mục tiêu đổi, không dùng lại, không đánh lại số.
- ID chỉ bỏ khi yêu cầu rời mô hình hành vi hoặc gộp vào NFR khác. ID bỏ ghi ở dưới kèm ngày và NFR nó gộp vào.
- ID phép đo là `M-1`, `M-2` trong một NFR, không đánh lại số.

ID NFR đã loại bỏ: không có.

### Liên kết

Liên kết chỉ từ trên xuống. Use case (Hệ thống hoặc Khi), FR hoặc tầm nhìn trích dẫn NFR bằng `[NFR-xxx]`.

- NFR không gọi tên use case, bước, nhánh, FR hay NFR khác. Nó có thể trích dẫn BR trong Điều kiện.
- Để tìm thứ trích dẫn NFR, tìm ID của nó trong các file spec.

### Một nguồn chân lý

Mục tiêu nằm ở đúng một NFR. Use case, FR, tầm nhìn không bao giờ nêu nó hay diễn giải thành số; chúng trích dẫn ID. Marker `[NFR-?: chủ đề]` chỉ được thay bằng `[NFR-xxx]` khi NFR phủ trọn nghĩa của marker; phủ một phần thì marker giữ nguyên và báo phần thiếu.

## 2. Tiêu chí

"Kiểm" là lớp dự kiến: *Lint* = máy kiểm được, *Review* = phán đoán người, *CI* = kiểm chéo. Chưa có công cụ nên review làm cả Lint lẫn CI.

| ID | Tiêu chí | Ngăn chặn | Kiểm |
|---|---|---|---|
| NFG-01 | NFR nói một chất lượng cấp sản phẩm dưới điều kiện đã nêu. Nó thêm ràng buộc riêng, không lặp FR. Không giá trị quy tắc, mục tiêu, journey, giao diện, kiến trúc, metric kỹ thuật, tiến độ, phiên bản | Hành vi hay giới hạn viết hai lần | Review |
| NFG-02 | NFR qua bốn test ở mục 1 | NFR viết cho mọi chất lượng theo thói quen | Review |
| NFG-03 | Độ hạt theo mục 1: một thuộc tính cho một phần gắn kết; nhiều phép đo cho cùng chất lượng; không trùng | NFR khổng lồ; cùng mục tiêu ở hai file | Review |
| NFG-04 | File theo `_TEMPLATE.md`: frontmatter `id` và `title`; trường Yêu cầu theo thứ tự; ít nhất một phép đo. Chỉ `Mục tiêu` và `Đạt khi` được `chưa đặt`. `Vì sao` trống thì bỏ dòng. `Chưa xác định` và `Ghi chú` bỏ khi trống | File không so/kiểm được | Lint (trường, thứ tự) |
| NFG-05 | Mỗi phép đo định nghĩa trọn: Điều kiện lặp được, Đo và Cách đo đủ để kiểm chứng. Mục tiêu có đơn vị và cận hoặc là thuộc tính bắt buộc. Biên sản-phẩm-kiểm-soát hay đầu-cuối và điều kiện phụ thuộc provider được nêu; thời gian provider không bỏ lặng. Không công cụ, không kiến trúc | Yêu cầu không kiểm chứng được; thời gian provider bị hứa là kết quả sản phẩm | Review |
| NFG-06 | Mục tiêu chờ ghi `chưa đặt` ở Mục tiêu và Đạt khi. Không đoán số, dải hay "khoảng". Không file nào trình nó như mục tiêu đã duyệt | Mục tiêu bịa; mục tiêu mở bị đọc là đã quyết | Lint (`chưa đặt`) + Review |
| NFG-07 | Mục `Chưa xác định` nêu khía cạnh mở không phải mục tiêu, một dòng, kết thúc "Chờ chốt." hoặc "Chờ bằng chứng kỹ thuật." cho định nghĩa thiếu bằng chứng. Mục tiêu thiếu là `chưa đặt`, không phải mục ở đây | Câu hỏi mở thành mục tiêu khi chưa quyết | Review |
| NFG-08 | Tên file `NFR-xxx.md` ba chữ số, bằng frontmatter `id`. ID duy nhất, không đánh lại số. ID bỏ ghi ở mục 1, không dùng lại. NFR không gọi tên use case, bước, nhánh, FR hay NFR khác | Hai nghĩa một ID; liên kết trỏ lên | Lint (tên, định dạng) + CI (duy nhất) |
| NFG-09 | Văn bản theo `../../_STYLE.md` quy tắc 1–10 trong Phát biểu, Điều kiện, Đo và Mục tiêu. Không giao diện (quy tắc 11) | Yêu cầu hai nghĩa; thiết kế bị chốt qua mục tiêu chất lượng | Lint (từ cấm) + Review |

## 3. Minh hoạ

**NFG-05: phép đo sản-phẩm-kiểm-soát.**

> NFR-000 · Thuộc tính chất lượng: hiệu năng · Phát biểu: người dùng thấy hệ thống bắt đầu nghe ngay sau khi chọn chương.
> M-1 · Điều kiện: chương đã có audio trên thiết bị, mạng ổn định. Biên: sản-phẩm-kiểm-soát — chỉ đo tới khi hệ thống bắt đầu phát, không tính thời gian provider tạo audio mới.
> Đo: thời gian từ chọn chương tới khi có âm thanh. Cách đo: lặp lại việc chọn cùng chương.

**NFG-02: không phải đại lượng nào cũng là NFR.**

> Không đạt: NFR chốt dung lượng bộ nhớ hệ thống dùng khi chạy. Không cam kết sản phẩm hay rủi ro nào cần nó.
> Đạt: không NFR. Nhóm theo dõi nó như công việc kỹ thuật, ngoài spec.
