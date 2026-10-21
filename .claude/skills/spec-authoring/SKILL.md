---
name: spec-authoring
description: Viết hoặc viết lại một file use case (docs/spec/02-use-cases) sao cho theo đúng template, criteria và style tiếng Việt của folder. Dùng khi tạo file spec, chuyển file cũ sang template mới, hoặc sửa lỗi style. Không dùng để quyết phạm vi hay bịa hành vi sản phẩm.
---

# Spec authoring

Quy tắc nằm ở ba file. Đọc trước khi viết; đừng viết lại chúng trong spec hay trong skill này.

- `docs/spec/<folder>/_TEMPLATE.md`: cấu trúc và tên trường cố định.
- `docs/spec/<folder>/_CRITERIA.md`: tiêu chí file phải đạt.
- `docs/spec/_STYLE.md`: quy tắc tiếng Việt, thẻ bằng chứng, bảng thuật ngữ, và kiểm giao diện (quy tắc 11).

## Nguồn nội dung

Chỉ viết điều đến từ người dùng, từ file đang viết lại, hoặc từ thẻ nghiên cứu trong `docs/research/`. Nếu một bước cần hành vi không từ nguồn nào, đánh dấu `[assumed]` và nói trong báo cáo. Đừng bịa.

Use case khám phá hành vi sản phẩm có thể làm. Flow lấy từ thẻ nghiên cứu hay sản phẩm tham chiếu được phép; bằng chứng nói nó đến từ đâu; nó không phải cam kết xây.

Đừng viết FR hay thay `FR-?` bằng ID thật trừ khi việc yêu cầu. Use case không có trường trạng thái, không tiến độ cài đặt.

## File mới

1. Copy `_TEMPLATE.md` của folder. ID use case: lấy số sau ID cao nhất trong `02-use-cases/` và trong ID đã loại bỏ (`02-use-cases/_CRITERIA.md`). Không dùng lại, chuyển hay đánh lại số.
2. Điền mọi phần. Viết yêu cầu/quy tắc/mục tiêu chưa viết thành marker `?`. Bỏ phần template đánh dấu bỏ được khi trống.
3. Chạy các kiểm style bên dưới.

## Viết lại file có sẵn

1. Giữ mọi ID, mọi trích dẫn (`FR-`, `[BR-`, `[NFR-`), frontmatter, nội dung bằng chứng và logic. Nếu quy tắc style buộc đổi nghĩa, đừng chọn lặng lẽ: đổi nhỏ nhất và ghi vào báo cáo.
2. Chuyển nội dung vào block và trường của template.
3. Chạy các kiểm style.
4. So trước/sau: cùng ID, cùng trích dẫn, cùng liên kết nghiên cứu.
5. Một cụm giao diện có thể mang yêu cầu. Dịch nó, đừng chỉ xóa. Hỏi điều gì vẫn đúng khi giao diện đổi: "một nút Phát ở góc dưới" thành "người dùng yêu cầu phát; hệ thống phát audio từ tiến độ đã lưu". Cụm chỉ là thiết kế (vị trí, màu, nhãn) thì xóa và ghi vào báo cáo như quyết định UI không chỗ.

## Kiểm style

- Tìm trong `Hệ thống`, `Khi` và `Tình huống và mục tiêu` mẫu từ cấm trong `_STYLE.md`. Sửa hoặc ghi lý do.
- Tách câu dài thành một hành động một câu.
- Kiểm mỗi thuật ngữ trong văn bản có trong bảng thuật ngữ; mỗi trường tối đa 7 dòng.
- Kiểm thẻ bằng chứng ở dòng riêng.
- Use case: chạy kiểm giao diện trong `_STYLE.md` (quy tắc 11, UCG-09) trên toàn file trừ frontmatter và khối sinh tự động. Viết lại mỗi kết quả thành ý định hoặc phản hồi, rồi áp dụng phép thử hoán đổi cho mọi câu Người dùng, Khi, Hệ thống.

## Use case: kết thúc bằng sơ đồ

Sau lần sửa cuối một use case, chạy [use-case-sequence](../use-case-sequence/SKILL.md) trên file. Đừng sửa khối sinh tự động bằng tay.

## Báo cáo

Liệt kê: file đã đổi, kiểm đã chạy và kết quả, mỗi chỗ quy tắc style đổi nghĩa, mỗi cụm UI mang yêu cầu và cách viết lại, mỗi quyết định UI bị xóa không chỗ, mỗi `[assumed]` thêm, mỗi tham chiếu đã xem sau khi đổi Hệ thống.
