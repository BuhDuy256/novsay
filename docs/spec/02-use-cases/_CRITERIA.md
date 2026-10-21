# Gate: Use case

Template: `_TEMPLATE.md`. Phong cách: `../_STYLE.md`. Con: `../03-requirements/fr/`, `../03-requirements/nfr/`, `../04-business-rules/`.

## 1. Use case là gì, và không là gì

**Một use case mô hình hoá hành vi sản phẩm cho một mục tiêu người dùng đạt trong một lần ngồi.** Nó nói người dùng làm gì và sản phẩm phản hồi thấy được thế nào. Mỗi phản hồi hệ thống là một ứng viên yêu cầu chức năng. Mỗi nhánh thay thế là một ứng viên yêu cầu lỗi/biên. Mỗi quy tắc hay mục tiêu chất lượng mà một bước phụ thuộc được trích dẫn ở đây và định nghĩa ở nơi khác.

**Một flow ghi lại hành vi để cân nhắc, không phải cam kết xây nó.** Use case khám phá rộng. Bằng chứng nói ý tưởng đến từ đâu; nó không chọn gì cả.

### Nội dung thuộc đâu

| Nếu nội dung là... | Thì nó thuộc |
|---|---|
| Giới hạn, ngưỡng, quota, danh sách cho phép, thời gian giữ hay giá trị khác một quy tắc định nghĩa | `../04-business-rules/`. Use case trích dẫn ID quy tắc |
| Thời gian chờ, mục tiêu kích thước, sẵn sàng hay chất lượng khác | `../03-requirements/nfr/`. Use case trích dẫn ID NFR |
| Phát biểu kiểm thử được của một phản hồi hệ thống | `../03-requirements/fr/`. Use case trích dẫn ID yêu cầu |
| Quan sát thô từ bản ghi (sản phẩm làm gì, hiện giới hạn nào) | `docs/research/`. Use case liên kết thẻ nghiên cứu |
| Hệ thống đạt phản hồi thế nào (model, queue, storage, API) | ADR hoặc công việc kiến trúc, không ở đây |
| Người dùng vận hành sản phẩm thế nào hay nó trông thế nào: điều khiển, thao tác, vị trí, nhãn, màu, bố cục | Công việc thiết kế UI (chưa có folder). Use case chỉ viết ý định và phản hồi (UCG-09) |

### Hướng liên kết: chỉ từ trên xuống

- Tầm nhìn (`../01-product-vision/`) là cha. Nó không liệt kê use case; để tìm cha, đọc tầm nhìn.
- Use case trích dẫn ID yêu cầu, NFR và quy tắc. Yêu cầu, NFR và quy tắc không bao giờ trích dẫn use case, bước hay nhánh.
- Use case liên kết thẻ nghiên cứu hỗ trợ nó. Thẻ không gọi tên use case.

### ID use case

- Một ID (`UC-xxx`) gọi tên một file use case. ID flow (`Sx`, `Ax`) gọi tên một khối trong file.
- Không gian tên là `docs/spec/`. ID dùng trong folder `docs/specification/` cũ không thuộc nó.
- Một ID không bao giờ chuyển sang mục tiêu khác hay dùng lại, kể cả sau khi file bị xóa.
- ID mới lấy số sau ID cao nhất trong folder và trong danh sách ID đã loại bỏ. Khoảng trống giữ nguyên.
- ID không đánh lại số.

ID use case đã loại bỏ:
- UC-003 — gỡ 21-10-2026; tự chuyển chương kế bị hoãn, không thuộc scope hiện tại.

## 2. Thẻ bằng chứng

Nhận định về hành vi sản phẩm dùng thẻ trong `../_STYLE.md` (`[observed: <nguồn>]`, `[inferred: <nguồn>]`, `[assumed]`). Với mức bao phủ sản phẩm, nguồn là thẻ nghiên cứu hoặc bản ghi dưới `docs/research/`. Flow chưa ai ghi là `chưa kiểm chứng` và các bước giữ `[assumed]`.

Bằng chứng nói flow hay phản hồi đến từ đâu. Nó không phải quyết định xây nó. Thẻ nghiên cứu cho thấy hành vi ở sản phẩm khác không đưa hành vi đó vào scope.

## 3. Tiêu chí

"Kiểm" là lớp dự kiến: *Lint* = máy kiểm được, *Review* = phán đoán người, *CI* = kiểm chéo. Chưa có công cụ nên review làm cả Lint lẫn CI.

| ID | Tiêu chí | Ngăn chặn | Kiểm |
|---|---|---|---|
| UCG-01 | Một mục tiêu người dùng, đạt trong một lần ngồi, kết quả quan sát được có giá trị. Tiêu đề là người dùng + động từ + đối tượng cụ thể + điều phân biệt, bằng lời người dùng | Case quá to hoặc quá nhỏ; hai case không phân biệt được | Review |
| UCG-02 | Tình huống và mục tiêu mô tả người dùng muốn gì và vì sao lúc này. Không chứa tính năng hay giải pháp | Giải pháp đội lốt mục tiêu | Review |
| UCG-03 | Bảng Các bước có 3–9 dòng `Sx` theo thứ tự. Mỗi dòng có Người dùng (ý định), Hệ thống (điều quan sát được, không "nếu"), FR (ID hoặc `FR-?`). Không cài đặt, không giao diện | Phản hồi chôn trong văn xuôi; nguồn FR không rõ | Lint (dòng, cột) + Review |
| UCG-04 | Mỗi nhánh là block `### Ax · Tên` với Tại, Kết thúc, Khi, Hệ thống, FR. `Kết thúc` dùng một giá trị trong template. Mỗi bước nhận input, hủy được, phụ thuộc dịch vụ ngoài hoặc có thể lâu đều có nhánh, hoặc lý do ghi rõ | Nhánh không test tái lập được | Lint (trường) + Review |
| UCG-05 | Kết quả kiểm chứng được bằng quan sát. Đảm bảo tối thiểu nói điều vẫn đúng khi nhánh bất kỳ thất bại | Không có khẳng định cuối để test; mất dữ liệu khi lỗi | Review |
| UCG-06 | ID bước và nhánh không đánh lại số một khi đã trích dẫn; ID bỏ được liệt kê và không dùng lại. Mỗi tham chiếu tới use case hoặc block khác (một `Kết thúc`, một "như UC-xxx Sx") gọi tên ID tồn tại và chưa bỏ. `UC-?` trong `Kết thúc` được phép | Trích dẫn trỏ nhầm; tham chiếu tới block đã bỏ | CI (tham chiếu) + Review |
| UCG-07 | Use case không chứa giá trị quy tắc hay chất lượng. Nó trích dẫn bằng ID mọi yêu cầu, giới hạn, danh sách cho phép, kiểm tra hay thời gian chờ mà một bước phụ thuộc (`FR-xxx`, `[BR-xxx]`, `[NFR-xxx]`). Marker `?` được phép trên mọi flow | Cùng một quy tắc viết nhiều chỗ; giá trị đổi một nơi không đổi nơi kia | Lint (số, marker) + CI (ID tồn tại) |
| UCG-08 | Mức bao phủ sản phẩm nêu cho mỗi sản phẩm tham chiếu là `quan sát`, `không có` hoặc `chưa kiểm chứng`, kèm liên kết thẻ nghiên cứu. Khác biệt mô tả bằng lời, không giá trị quy tắc. Nhận định chưa ghi giữ `[assumed]` | Đoán bị đọc thành dữ kiện | Lint (thẻ) + Review |
| UCG-09 | Văn bản theo `../_STYLE.md`: từ trong bảng thuật ngữ, không động từ mơ hồ bị cấm, không "có thể/nên/có lẽ" trong Hệ thống, điều kiện ở Khi, một hành động một dòng, bằng chứng ở dòng riêng. Use case viết ý định và phản hồi, không widget, thao tác, vị trí, kiểu dáng hay nhãn; gọi nơi chỉ bằng vùng | Phản hồi hai người đọc hai nghĩa; spec vỡ khi thiết kế đổi | Lint (từ cấm, từ giao diện) + Review |
| UCG-10 | Sơ đồ tương tác theo `../_MERMAID.md` (MG-01..MG-10): hợp lệ, là view sinh từ bảng Các bước và Nhánh thay thế, mỗi message ánh xạ 1-1, không sửa bằng tay | Sơ đồ lệch nguồn; nhánh bị mất khi vẽ | Review (tới khi có skill), rồi CI |

## 4. Minh hoạ

**UCG-03: quan sát được, không cài đặt.**

> Không đạt: "S5: Model trả JSON chương và renderer vẽ nó."
> Đạt: "S5 · Hệ thống: phát audio của chương và hiện tiến độ đang chạy."

**UCG-04: nhánh phát hiện được.**

> Không đạt: "A1: Có lỗi. Hệ thống hiện lỗi."
> Đạt: "A1 (tại S3): mất kết nối khi đang lấy nội dung. Hệ thống giữ link người dùng đã nhập và báo lấy không được."

**UCG-09: ý định và phản hồi, không giao diện.**

> Không đạt: "Người dùng bấm nút Phát ở góc dưới."
> Đạt: "Người dùng yêu cầu phát. Hệ thống phát audio từ vị trí tiến độ đã lưu."
