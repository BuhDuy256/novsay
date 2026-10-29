# Quy tắc viết spec

Áp dụng cho mọi file trong `docs/spec/`. Các quy tắc 5 và 7 áp dụng cho trường `Hệ thống` và `Khi` của use case. Quy tắc 11 áp dụng cho toàn bộ use case.

**Vì sao:** mỗi câu chỉ có một nghĩa, để một phản hồi của hệ thống trở thành một yêu cầu kiểm thử được. Từ ngữ thường làm được cả hai điều đó.

## Quy tắc

| # | Quy tắc | Không viết | Viết |
|---|---|---|---|
| 1 | **Một thứ, một tên.** Dùng đúng từ trong bảng thuật ngữ. Không bao giờ đổi từ đồng nghĩa. | "tiến độ" và "vị trí nghe" cho cùng một thứ | "tiến độ" mọi lúc |
| 2 | **Dùng từ thường.** hiện, giữ, dùng, bắt đầu, kết thúc, trước, sau | hiển thị, duy trì, khởi tạo, kết thúc công việc, trước đó, sau đó | "Hệ thống phát audio." |
| 3 | **Không thành ngữ hay cụm bóng bẩy.** | "bật đèn xanh", "chốt hạ", "quay xe" | "đồng ý", "kết thúc", "đổi ý" |
| 4 | **Không động từ mơ hồ.** Cấm: xử lý, quản lý, hỗ trợ, đảm bảo, thực hiện, tiến hành, phù hợp, đúng cách, mượt mà. | "Hệ thống xử lý lỗi một cách mượt mà." | "Hệ thống báo không lấy được nội dung và giữ link người dùng đã nhập." |
| 5 | **Không "có thể", "nên", "có lẽ" trong phản hồi hệ thống.** Nói điều hệ thống làm. Dùng **"được phép"** chỉ cho quyền của người dùng. | "Hệ thống có thể hiện thông báo." | "Hệ thống hiện thông báo." |
| 6 | **Câu ngắn, chủ động.** Một hành động một câu. Trích dẫn `[BR-xxx]` không tính. | "Một thông báo được hiện rằng công việc đã dừng và có bao nhiêu chương đã xong." | "Hệ thống hiện thông báo rằng nó đã dừng. Thông báo nêu số chương đã làm." |
| 7 | **Điều kiện để ở trường Khi.** Phản hồi hệ thống không có "nếu". Khi hành vi khác theo bước, mở đầu bằng nhãn: "Tại S3:", "Kết nối trở lại:". | "Nếu link không hợp lệ, hệ thống từ chối." | Khi: "Link không khớp nguồn [BR-?]." Hệ thống: "Nêu lý do." |
| 8 | **Một hành động một dòng. Tối đa 7 dòng mỗi trường.** | Một ô 110 chữ | Mỗi dòng một việc người dùng thấy được |
| 9 | **In đậm ít.** In đậm một từ trong bảng thuật ngữ ở lần dùng đầu tiên của một dòng. Tối đa 2 chỗ một dòng. | In đậm cả cụm | "Phát **audio**." |
| 10 | **Bằng chứng ở dòng riêng.** Một thẻ cho một nhận định. Không bao giờ đặt giữa câu. | "…màn hình vẫn ở chương đầu `[observed: …]`, và không đề nghị tải chương sau." | `- **Bằng chứng:** [observed: claude-report (màn hình giữ chương đầu)]` |
| 11 | **Ý định và phản hồi, không phải giao diện.** Bên người dùng nói người dùng muốn gì. Bên hệ thống nói hệ thống báo, giữ, đổi hay tạo gì. Không bao giờ gọi tên widget, thao tác, vị trí, kiểu dáng hay nhãn. Gọi tên một nơi chỉ bằng vùng (xem Vùng). Nếu một chi tiết giao diện mang yêu cầu, hãy viết yêu cầu đó. | "Người dùng mở menu và chọn một truyện." "Mở màn nghe ở góc dưới." "Hiện thẻ có nút nghe lại." | "Người dùng chọn một truyện." "Mở màn nghe. Tiến độ đã lưu và audio hiện tại giữ nguyên." "Cho người dùng nghe lại." |

Quy tắc 4 đến 7 giữ phản hồi kiểm thử được. Quy tắc 1 đến 3 và 6 giữ nó dễ đọc. Quy tắc 11 giữ spec đúng khi thiết kế thay đổi.

## Thẻ bằng chứng

Một thẻ cho một nhận định. Khóa giữ tiếng Anh để grep được; nội dung nguồn viết tiếng Việt:

- `[observed: <nguồn> (<nó cho thấy gì>)]` thấy trong bản ghi hoặc sản phẩm
- `[inferred: <nguồn>]` suy ra từ dữ kiện đã quan sát
- `[assumed]` hoặc `[assumed: <điều gì>]` chưa có bằng chứng

Trong một danh sách (bối cảnh sử dụng, kiến thức, …), dòng cuối có thể là một `- **Bằng chứng:** [assumed]`. Nó tính cho mọi mục phía trên chưa có dòng Bằng chứng riêng.

## Vùng

Một vùng là nơi chứa một loại thông tin. Nó được định nghĩa bởi nó chứa gì, không bao giờ bởi nó nằm ở đâu hay trông thế nào. Danh sách là đóng; mỗi sản phẩm tự khai báo vùng của nó trong bảng thuật ngữ. Với Novsay chưa có vùng nào được chốt.

Một use case có thể nói thứ gì đó được hiện, giữ hay đổi trong một vùng. Nó không được nói vùng được bố trí hay đi tới thế nào. Để thêm vùng, thêm một dòng vào bảng thuật ngữ và nói nó chứa gì.

## Thuật ngữ

Dùng những từ này cho những thứ này. Thêm dòng khi cần từ mới. Không thêm từ đồng nghĩa. Một từ không bao giờ gọi tên widget, thao tác, vị trí hay kiểu dáng. Bảng này là khởi đầu, lấy từ scope V1 đã chốt; bổ sung khi khám phá.

| Thuật ngữ | Nghĩa |
|---|---|
| **tài khoản** | Danh tính của người dùng để truy cập và giữ dữ liệu riêng |
| **truyện** | Một tác phẩm dài nhiều chương |
| **chương** | Một phần của truyện. Người dùng nhận link chương công khai |
| **nguồn** | Website tiểu thuyết được hỗ trợ, cung cấp nội dung truyện |
| **văn bản truyện** | Văn bản lấy được từ một chương, được xem trước khi nghe |
| **transcript** | Văn bản truyện đã được owner xác nhận bằng hành động nghe. Audio đọc đúng transcript này |
| **audio** | Bản đọc (TTS) của transcript, được chuẩn bị mới hoặc dùng lại |
| **yêu cầu chuẩn bị** | Việc chuẩn bị audio từ transcript đã xác nhận, có trạng thái riêng |
| **bản nghe** | Transcript đã xác nhận và audio tương ứng; chỉ dùng trong phiên hoặc được lưu vào tài khoản owner |
| **bản đã lưu** | Bản nghe đã lưu thành công cả transcript lẫn audio vào tài khoản owner |
| **tiến độ** | Vị trí nghe gắn với một bản nghe và audio tương ứng trên thiết bị hiện tại |
| **nghe nền** | Phát audio vẫn tiếp tục khi chuyển app, tắt màn hình hoặc khóa máy |
| **gián đoạn** | Sự kiện làm việc nghe dừng ngoài yêu cầu chủ động của owner. Phạm vi và giới hạn khôi phục theo NFR-003 |
| **giọng đọc** | Giọng TTS được chọn để đọc transcript |
| **ngôn ngữ gốc** | Ngôn ngữ của văn bản truyện nguồn |
| **dịch** | Việc chuyển nội dung sang ngôn ngữ đọc. Novsay đọc nguyên bản; dịch để version sau |

## Cách kiểm tra

Chưa có công cụ, nên review làm việc này. Có hai nhóm kiểm tra.

**Từ ngữ.** Chạy trên các trường `Hệ thống` và `Khi`, và trên `Tình huống và mục tiêu`. Mỗi kết quả được sửa hoặc ghi lý do. (Lưu ý: không dùng `\b` vì nó không chạy với dấu tiếng Việt.)

```
xử lý|quản lý|hỗ trợ|đảm bảo|thực hiện|tiến hành|phù hợp|đúng cách|mượt mà|có thể|có lẽ|nên
```

**Giao diện (quy tắc 11).** Chạy trên toàn use case, trừ frontmatter, khối sinh tự động và dòng `Thẻ nghiên cứu`. Mỗi kết quả được viết lại thành ý định hoặc phản hồi. Một kết quả không phải ngôn ngữ giao diện (ví dụ "phải" trong "chữ viết từ phải sang trái") có lý do ghi rõ.

```
nút|bấm|nhấn|chạm|vuốt|cuộn|menu|dropdown|hộp thoại|popup|tab|sidebar|thanh công cụ|thẻ|chip|biểu tượng|toggle|checkbox|màn hình|trang|góc|bên trên|bên dưới|trái|phải|nhãn|trường nhập
```

Sau đó áp dụng **phép thử hoán đổi** cho từng câu: hình dung cùng sản phẩm với giao diện khác, ví dụ chỉ chạm hoặc chỉ giọng nói. Nếu câu vẫn đúng, nó qua. Nếu không, nó mô tả giao diện và được viết lại.
