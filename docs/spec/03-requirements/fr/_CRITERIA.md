# Gate: Yêu cầu chức năng

Template: `_TEMPLATE.md`. Phong cách: `../../_STYLE.md`. Được trích dẫn bởi: `../../02-use-cases/` (cột FR). Giá trị quy tắc: `../../04-business-rules/`. Mục tiêu chất lượng: `../nfr/`.

## 1. FR là gì, và không là gì

**FR là phát biểu kiểm thử được của một hành vi hệ thống dưới điều kiện đã nêu.** Nó nói hệ thống hiện, giữ, đổi, tạo hay từ chối gì. Phản hồi use case nói người dùng quan sát gì trong một hành trình; FR thêm độ chính xác mà test cần: input nào, kết quả nào, trường hợp biên nào, điều gì giữ nguyên.

| Nếu nội dung là... | Thì nó thuộc |
|---|---|
| Mục tiêu, hành trình, thứ tự bước, ý định người dùng | `../../02-use-cases/`. Use case trích dẫn FR ở cột FR |
| Giới hạn, ngưỡng, quota, danh sách cho phép, thời gian giữ | `../../04-business-rules/`. FR trích dẫn `[BR-xxx]`, hoặc `[BR-?: chủ đề]` tới khi quy tắc tồn tại |
| Thời gian chờ, mục tiêu kích thước, sẵn sàng | `../nfr/`. FR trích dẫn `[NFR-xxx]`, hoặc `[NFR-?: chủ đề]` |
| Người dùng vận hành thế nào hay nó trông thế nào | Công việc thiết kế UI (chưa có folder) |
| Hệ thống đạt hành vi thế nào (model, queue, storage, API) | ADR hoặc công việc kiến trúc |
| Việc cần xây, hay đã xây/test tới đâu | Không ở trong spec. FR không tiến độ, ưu tiên, phiên bản |

Một quy tắc không có giá trị ở lại trong FR, ví dụ "người dùng không thể bắt đầu phiên mới khi một yêu cầu đang chạy". Quy tắc có giá trị thì về `../../04-business-rules/`.

### Độ hạt và tái sử dụng

- **Một FR** có một mục đích gắn kết; kết quả thuộc về nhau và đổi vì cùng lý do.
- **Tách** FR khi: kết quả có thể tự thất bại dưới điều kiện khác nhau đáng kể; block khác chỉ cần một phần; nó gộp trách nhiệm không liên quan.
- **Tái dùng** FR khi block khác cần cùng hành vi: cùng loại điều kiện, cùng kết quả mong đợi.
- **Cùng chữ không phải cùng hành vi.** Chỉ tái dùng khi nghĩa giống nhau.
- **Không FR trùng.** Trước khi viết, tìm các phát biểu trong folder.
- **Độ chính xác.** FR có thể nhắc hành vi cốt lõi; điều kiện chấp nhận thêm ít nhất một trong: kết quả quan sát được, điều kiện input liên quan, trường hợp biên, đảm bảo giữ nguyên, hành vi lỗi. FR chỉ lặp use case thì không viết.

### ID và file

- Một FR mỗi file: `FR-xxx.md`. `xxx` là ba chữ số. `id` trong frontmatter bằng tên file.
- ID mới lấy số sau ID cao nhất trong folder và trong ID đã loại bỏ. Khoảng trống giữ nguyên.
- ID không đổi khi tiêu đề hay lời văn đổi, và không dùng lại.
- ID chỉ bỏ khi hành vi rời khỏi mô hình hành vi hoặc gộp vào FR khác. ID bỏ ghi ở dưới kèm ngày và, sau khi gộp, FR nó gộp vào.
- ID điều kiện chấp nhận là `AC-1`, `AC-2` trong một FR, không đánh lại số.

ID FR đã loại bỏ: không có.

### Liên kết

Liên kết chỉ từ trên xuống. Use case trích dẫn FR ở cột FR của bảng Các bước. Một FR có thể phục vụ nhiều block; một block có thể trích dẫn nhiều FR.

- FR không gọi tên use case, bước hay nhánh.
- Để tìm block dùng FR, tìm ID của nó trong `../../02-use-cases/`.
- FR đổi cùng các block nó phục vụ. Đổi nghĩa FR được kiểm với mọi block trích dẫn nó trong cùng một change.

## 2. Tiêu chí

"Kiểm" là lớp dự kiến: *Lint* = máy kiểm được, *Review* = phán đoán người, *CI* = kiểm chéo. Chưa có công cụ nên review làm cả Lint lẫn CI.

| ID | Tiêu chí | Ngăn chặn | Kiểm |
|---|---|---|---|
| FRG-01 | FR nói một hành vi hệ thống dưới điều kiện đã nêu. Không mục tiêu, journey, giá trị quy tắc, mục tiêu chất lượng, giao diện, kiến trúc, tiến độ hay phiên bản | Yêu cầu nhắc lại hành trình; giá trị ở hai nơi | Review |
| FRG-02 | Độ hạt theo mục 1: một mục đích gắn kết; tách theo lý do; tái dùng cho cùng hành vi; không FR thứ hai cho hành vi FR đã phủ | FR khổng lồ; một FR mỗi bước theo thói quen; cùng hành vi viết hai lần | Review |
| FRG-03 | Điều kiện chấp nhận thêm độ chính xác test được vượt qua phản hồi use case: kết quả, input, biên, giữ nguyên, hành vi lỗi | FR chỉ chép use case, không thêm test | Review |
| FRG-04 | File theo `_TEMPLATE.md`: frontmatter `id` và `title`; trường Yêu cầu theo thứ tự; ít nhất một điều kiện chấp nhận. `Vì sao` trống thì bỏ dòng. `Chưa xác định` và `Ghi chú` bỏ khi trống. Không trường phiên bản, ưu tiên, tiến độ, bằng chứng, use case | File không so/kiểm được | Lint (trường, thứ tự) |
| FRG-05 | `Trạng thái` là `chốt` hoặc `đề xuất`. Block `đề xuất` có `Vì sao` | Trạng thái phê duyệt không ai định nghĩa | Lint (giá trị, trường) |
| FRG-06 | FR không chứa giá trị quy tắc hay mục tiêu chất lượng. Nó trích dẫn `[BR-xxx]`/`[NFR-xxx]`, hoặc marker `?`. Input ví dụ trong điều kiện được phép | Cùng giá trị ở nhiều file | Lint (số, marker) + CI (ID tồn tại) |
| FRG-07 | Mục `Chưa xác định` nêu hành vi bỏ ngỏ một dòng. Không phát biểu và không điều kiện nào giả định kết quả cho nó. Phản hồi phụ thuộc trọn một quyết định mở thì không viết FR; block giữ `FR-?` | Câu hỏi mở thành yêu cầu khi chưa quyết | Review |
| FRG-08 | Mỗi điều kiện là block `### AC-n · Tên` với Cho trước, Khi, Thì, Kiểm. `Kiểm` là `tất định` hoặc `đánh giá`. `Thì` là kết quả quan sát được, một dòng mỗi ý, không "nếu". Không bắt chính xác lời model | Điều kiện không test được; test gắn với lời model | Lint (trường, giá trị) + Review |
| FRG-09 | Văn bản theo `../../_STYLE.md` quy tắc 1–10 trong Phát biểu và Thì, và ý định quy tắc 11: không nhãn, vị trí, màu, biểu tượng chưa duyệt; gọi nơi bằng vùng | Yêu cầu chốt thiết kế chưa ai chọn | Lint (từ cấm, từ giao diện) + Review |
| FRG-10 | Tên file `FR-xxx.md` ba chữ số, bằng frontmatter `id`. ID duy nhất. ID mới theo ID cao nhất hiện có hoặc đã bỏ. ID bỏ ghi ở mục 1, không dùng lại | Hai nghĩa cho một ID | Lint (tên, định dạng) + CI (duy nhất) |

## 3. Minh hoạ

**FRG-02: tái dùng cho cùng hành vi.**

> Không đạt: một FR "giữ tiến độ sau khi dừng" cho lần nghe đầu, và FR thứ hai cùng nghĩa cho lần nghe tiếp.
> Đạt: một FR "khi bị gián đoạn, tiến độ đã lưu được giữ nguyên và không bị ghi đè bằng tiến độ chưa xong". Mọi block có thể bị dừng đều trích dẫn nó.

**FRG-09: hành vi, không thiết kế.**

> Không đạt: "Nút Phát bị mờ khi chưa có audio."
> Đạt: "Hệ thống không nhận yêu cầu phát khi chưa có audio."
