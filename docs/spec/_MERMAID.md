# Gate: Mermaid

Áp dụng cho mọi sơ đồ Mermaid nhúng trong `docs/spec/` (sequence diagram của use case và bất kỳ flowchart, state diagram nào khác). Sơ đồ là một **view**: nguồn chân lý là các block văn bản. Không bao giờ sửa sơ đồ bằng tay để làm nó "khớp".

"Kiểm" là lớp dự kiến: *Lint* = máy kiểm được, *Review* = phán đoán người, *CI* = kiểm chéo. Chưa có công cụ nên hiện tại review làm cả Lint lẫn CI.

| ID | Tiêu chí | Ngăn chặn | Kiểm |
|---|---|---|---|
| MG-01 | Cú pháp Mermaid hợp lệ, render được trên GitHub và VS Code (tập con bảo thủ trong skill `mermaid-markdown`) | Sơ đồ vỡ khi xem | Lint |
| MG-02 | Sơ đồ là view. Block nguồn là chân lý. Sửa nguồn thì tái sinh sơ đồ, không sửa sơ đồ để khớp nguồn | Hai nguồn lệch nhau | CI |
| MG-03 | Mỗi participant/node/message ánh xạ 1-1 với một phần tử nguồn. Không thừa, không thiếu, không trùng | Sơ đồ không còn là cái nhìn trung thực | CI |
| MG-04 | Nhãn ngắn, một nghĩa, theo chính sách ngôn ngữ (`_STYLE.md`): nhãn tiếng Việt, ID giữ tiếng Anh | Nhãn hai người đọc hai nghĩa | Review |
| MG-05 | Không hardcode màu, theme, class, HTML hay style. Đọc được trên cả nền sáng lẫn tối | Sơ đồ chỉ đẹp trên một theme | Lint |
| MG-06 | Nhánh được thể hiện bằng đúng cấu trúc Mermaid (`alt`/`opt`/`loop`), không "dẹt" làm mất ngữ nghĩa. Nhánh không diễn tả sạch được (ví dụ "Quay lại S2") ghi chú dưới sơ đồ | Nhánh bị mất khi vẽ | Review |
| MG-07 | Chiều mũi tên đúng (người dùng → hệ thống là yêu cầu, hệ thống → người dùng là phản hồi). Mỗi participant khai báo đúng một lần | Hướng sai làm hiểu sai tương tác | Review |
| MG-08 | Sơ đồ trả lời được câu hỏi chính trong một cái liếc. Chi tiết phụ để trong văn xuôi | Sơ đồ thành tường chữ | Review |
| MG-09 | Một thay đổi ở block nguồn tái sinh sơ đồ trong cùng một change | Sơ đồ tụt hậu so với nguồn | CI |
| MG-10 | Không dùng tính năng beta hay không được target renderer hỗ trợ | Sơ đồ chỉ chạy trên một renderer | Review |

## Minh hoạ

**MG-03 và MG-06: sơ đồ trung thực với nhánh.**

> Không đạt: sequence diagram chỉ vẽ main flow, bỏ nhánh "mất kết nối" vì nó là `Returns to S2`.
> Đạt: main flow vẽ tuyến tính; dưới sơ đồ ghi `*Không vẽ (nhánh quay lại bước): A3.*` và block `A3` vẫn giữ đầy đủ `Tại/Kết thúc/Khi/Hệ thống`.

**MG-04: nhãn một nghĩa, không phải giao diện.**

> Không đạt: `User->>System: nhấn nút Phát` — nhãn mô tả widget.
> Đạt: `User->>System: yêu cầu phát` — nhãn là ý định.
