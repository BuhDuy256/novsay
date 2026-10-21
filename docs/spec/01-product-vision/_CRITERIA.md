# Gate: Tầm nhìn sản phẩm

Template: `_TEMPLATE.md`. Phong cách: `../_STYLE.md`. Con: `../02-use-cases/`, `../03-requirements/`, `../04-business-rules/`.

## 1. Tầm nhìn là gì, và không là gì

**Tầm nhìn định nghĩa sản phẩm là gì, trước khi bất kỳ file spec nào khác mô tả nó làm gì.** Nó trả lời năm câu hỏi: (1) Sản phẩm là gì? (2) Nó giải quyết vấn đề gì? (3) Nó mang giá trị chính gì? (4) Nguyên tắc nào dẫn lựa chọn? (5) Ranh giới nào thuộc bản chất sản phẩm?

**Tầm nhìn không phải nhật ký quyết định, danh sách tính năng hay phạm vi.** Nó chỉ giữ điều vẫn đúng khi phạm vi, giao diện hay kiến trúc thay đổi (VG-01).

**Tầm nhìn không lớn lên bằng suy diễn.** Chỉ bạn chốt một phát biểu. Mọi thứ khác là đề xuất hoặc câu hỏi mở (VG-13). Một lỗ hổng được viết thành lỗ hổng (VG-14).

### Nội dung thuộc đâu

| Nếu nội dung là... | Thì nó thuộc |
|---|---|
| Sản phẩm là gì, vì sao tồn tại, giá trị, nguyên tắc, ranh giới bền | Ở đây |
| Một khả năng sản phẩm cung cấp | `../02-use-cases/`. Chỉ vào đây khi bạn nói nó là một phần bản chất sản phẩm |
| Một bước, một phản hồi hay một nhánh của một mục tiêu | `../02-use-cases/` |
| Phát biểu kiểm thử được của một phản hồi hệ thống | `../03-requirements/fr/` |
| Thời gian chờ, mục tiêu kích thước hay chất lượng khác | `../03-requirements/nfr/`. Tầm nhìn trích dẫn `[NFR-?: chủ đề]` |
| Giới hạn, danh sách cho phép, loại file hay giá trị khác một quy tắc định nghĩa | `../04-business-rules/`. Tầm nhìn trích dẫn `[BR-?: chủ đề]` |
| Code đạt được điều gì đó thế nào: engine, storage, framework, giao thức | ADR trong `docs/adr/` |
| Sản phẩm được vận hành hay trông thế nào | Công việc thiết kế UI (chưa có folder) |
| Quy tắc viết file spec, hay thuật ngữ dùng chung | `../_STYLE.md` hoặc `AGENTS.md` |
| Quan sát thô một sản phẩm khác | `docs/research/` |

### Ranh giới không phải giới hạn phạm vi

Ranh giới nói sản phẩm KHÔNG là gì, do bản chất. Nó đúng ở mọi bản phát hành. Giới hạn phạm vi nói một bản phát hành bỏ điều gì. Chỉ cái đầu thuộc đây.

> Giới hạn phạm vi (không ở đây): "V1 chỉ có giao diện web."
> Ranh giới (ở đây): "Sản phẩm không tự sinh nội dung truyện; nó chỉ đọc nội dung có sẵn."

Phép thử: nếu có thời gian vô hạn, phát biểu có còn đúng không? Không thì là giới hạn phạm vi.

### Chốt, đề xuất, mở

Mỗi phát biểu có một trong hai trạng thái.

| Trạng thái | Nghĩa | Spec bậc dưới được dựa vào |
|---|---|---|
| `chốt` | Bạn đã nói điều đó | Có |
| `đề xuất` | AI gợi ý, bạn chưa quyết | Không |

Câu hỏi mở là trạng thái thứ ba: chưa đủ biết để quyết.

### Hướng liên kết: chỉ từ trên xuống

Tầm nhìn là đỉnh của chuỗi. File spec bậc dưới không bao giờ gọi tên một block tầm nhìn. Để kiểm tra file so với tầm nhìn, đọc tầm nhìn.

### Một nguồn chân lý

Một dữ kiện viết ở đúng một block. Block khác trỏ tới bằng ID. Một thuật ngữ hay vùng mà `../_STYLE.md` định nghĩa thì dùng ở đây, không định nghĩa lại (VG-06).

## 2. Phần, block và ID

| Phần | Trả lời | ID block | Trường |
|---|---|---|---|
| Sản phẩm là gì | Câu hỏi 1 | `I-x` | Phát biểu, Trạng thái, Nguồn, Hệ quả cho spec |
| Vì sao tồn tại | Câu hỏi 2 và 3 | `W-x` | Phát biểu, Trạng thái, Nguồn, Bằng chứng, Hệ quả cho spec |
| Nguyên tắc | Câu hỏi 4 | `P-x` | Phát biểu, Trạng thái, Nguồn, Vì sao, Hệ quả cho spec |
| Ranh giới | Câu hỏi 5 | `B-x` | Phát biểu, Trạng thái, Nguồn, Vì sao, Hệ quả cho spec |
| Câu hỏi mở | Lỗ hổng bất kỳ | `Q-x` | Câu hỏi, Ảnh hưởng |
| Đã loại bỏ | ID đã gỡ | không | Một dòng mỗi ID |

- `Trạng thái` là `chốt` hoặc `đề xuất`. Luôn có.
- `Nguồn` chỉ có khi `đề xuất` — nói ai đề xuất và suy ra từ đâu.
- `Vì sao` nêu lý do, hoặc bỏ dòng. Đừng bịa lý do.
- `Hệ quả cho spec` chỉ có ở block `chốt`, và chỉ điều suy trực tiếp từ phát biểu.
- ID không bao giờ đánh lại số hay dùng lại. Block bị gỡ ghi ở `Đã loại bỏ` (VG-05).

## 3. Tiêu chí

"Kiểm" là lớp dự kiến: *Lint* = máy kiểm được, *Review* = phán đoán người, *CI* = kiểm chéo. Chưa có công cụ nên review làm cả Lint lẫn CI.

| ID | Tiêu chí | Ngăn chặn | Kiểm |
|---|---|---|---|
| VG-01 | Mỗi block nói sản phẩm là gì, vì sao tồn tại, giá trị, nguyên tắc hoặc ranh giới bền. Nó vẫn đúng khi phạm vi, giao diện hay kiến trúc thay đổi. Dữ kiện chỉ một tính năng hay một use case phụ thuộc thì về use case đó | Tầm nhìn thành danh sách tính năng | Review |
| VG-02 | Block nói điều đúng của sản phẩm hoặc cho người dùng. Nó không bao giờ nói code đạt được thế nào. `Vì sao` nêu lý do của bạn, hoặc bỏ dòng | Kiến trúc được chọn tình cờ | Review |
| VG-03 | Ranh giới nói sản phẩm KHÔNG là gì do bản chất, qua phép thử ở mục 1. Tính năng thiếu hay giới hạn phạm vi không phải ranh giới | Giới hạn V1 biến thành giới hạn vĩnh viễn | Review |
| VG-04 | Câu hỏi mở có `Câu hỏi` và `Ảnh hưởng`. `Ảnh hưởng` liệt kê mục spec chờ câu trả lời theo ID, hoặc "chưa thấy". Không block nào khác trả lời câu hỏi | Lỗ hổng giấu trong phát biểu | Lint (trường) + Review |
| VG-05 | ID `I-x`, `W-x`, `P-x`, `B-x`, `Q-x` không đánh lại số hay dùng lại. Block gỡ ghi ở `Đã loại bỏ` kèm nội dung đi đâu | Trích dẫn trỏ nhầm block | Review |
| VG-06 | Mỗi dữ kiện viết một lần. Block khác trỏ bằng ID. File không định nghĩa lại thuật ngữ, vùng hay quy tắc mà `../_STYLE.md` định nghĩa | Hai nguồn cho một dữ kiện lệch nhau | Review |
| VG-07 | Mỗi block có `Trạng thái: chốt` hoặc `đề xuất`. Block `đề xuất` có `Nguồn` và không có `Hệ quả cho spec`. Spec bậc dưới không dựa vào block `đề xuất` | Đề xuất bị đọc thành quy tắc | Lint (trường) + Review |
| VG-08 | File không chứa phạm vi, thứ tự hay ưu tiên. Không dùng từ MVP, V1, phase, roadmap | Quyết định phạm vi đặt sai chỗ | Lint (từ) + Review |
| VG-09 | File không chứa quy tắc hay giá trị chất lượng. Nó trích dẫn `[BR-?: chủ đề]` hoặc `[NFR-?: chủ đề]` cho mọi giới hạn hay mục tiêu | Cùng một quy tắc viết nhiều chỗ khác nhau | Lint (số, marker) + CI (ID tồn tại) |
| VG-10 | Liên kết chỉ từ trên xuống. Chỉ `Ảnh hưởng` gọi tên mục spec bậc dưới, và mỗi ID tồn tại hoặc đã loại bỏ | Liên kết trỏ lên; ID treo | CI (tham chiếu tồn tại) |
| VG-11 | Văn bản theo `../_STYLE.md`: từ trong bảng thuật ngữ, không động từ mơ hồ bị cấm, một dữ kiện một dòng, bằng chứng ở dòng riêng | Văn bản người đọc hiểu hai nghĩa | Lint (từ cấm) + Review |
| VG-12 | File không có câu quảng cáo. Không từ ca ngợi như mạnh mẽ, mượt, trực quan, thông minh, tốt nhất, dễ | Văn quảng cáo bị đọc thành cam kết | Lint (từ) + Review |
| VG-13 | Chỉ bạn chốt một phát biểu. AI chỉ viết nội dung mới thành block `đề xuất` hoặc câu hỏi mở. Nội dung tìm thấy ở use case, thẻ nghiên cứu hay sản phẩm tham chiếu không vì thế mà được chốt | Suy diễn và tính năng vay mượn thành chân lý sản phẩm | Review |
| VG-14 | Block `W-x` nói vấn đề, nhu cầu hay giá trị cho con người có `Bằng chứng` với thẻ trong `../_STYLE.md`. Nó không nói quá bằng chứng. Chỉ có `[assumed]` thì viết thành niềm tin ("Tôi tin rằng..."). Phần chưa có gì ghi "Chưa viết. Xem Q-x." | Vấn đề người dùng bịa ra; tầm nhìn nhìn có vẻ đầy đủ nhưng là đoán | Lint (trường, thẻ) + Review |

## 4. Minh hoạ

**VG-01: bản chất, không phải tính năng.**

> Không đạt: "Sản phẩm đọc một chương truyện thành audio." Đó là khả năng, thuộc use case.
> Đạt: "Sản phẩm là app nghe tiểu thuyết cá nhân, host trên Internet, có tài khoản."

**VG-03: ranh giới, không phải giới hạn V1.**

> Không đạt: "Ranh giới: không tự chuyển chương." V1 chọn chưa làm, đó là phạm vi.
> Đạt: "Ranh giới: sản phẩm không tự sinh hay sở hữu nội dung truyện; nó đọc nội dung từ nguồn."
