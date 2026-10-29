# Research notes — style guide

Đọc file này trước khi viết hoặc chỉnh sửa bất kỳ file nào trong `docs/research/`.
Đọc thêm các ghi chú hiện có trong file mục tiêu để nắm giọng văn trước khi viết tiếp.

## Cấu trúc

1. Dùng numbered list làm cấu trúc chính. Mỗi số trình bày một ý hoặc một câu hỏi riêng. Tiếp tục số thứ tự đang có trong file.

2. Dùng bullet bên trong numbered item khi cần liệt kê chi tiết. Chỉ dùng bảng khi cần so sánh cùng tiêu chí (ví dụ: kết quả của nhiều URL). Dùng code block cho lệnh hoặc đoạn response ngắn.

3. Không dùng bold, italic hoặc heading con trong text thông thường. Giữ nguyên heading và metadata hiện có. Dùng inline code cho URL, lệnh, tên file, header hoặc giá trị kỹ thuật.

## Ngôn ngữ

4. Viết tiếng Việt tự nhiên, ngắn và trực tiếp. Giữ thuật ngữ kỹ thuật quen thuộc bằng tiếng Anh (request, response, headers, fetch, backend, hosting, retry...).

5. Khi đưa thuật ngữ mới, giải thích ngay bằng hành vi cụ thể. Ví dụ: "Retry là gửi lại request sau lần thất bại." Tránh cách viết chung chung như "xử lý phù hợp" hoặc "đảm bảo hoạt động ổn định".

## Lập luận

6. Giải thích theo thứ tự: vấn đề cần kiểm tra → đã thử thế nào → quan sát được gì → điều đó có nghĩa gì với Novsay.

7. Dùng câu hỏi ngắn để dẫn vào phần cần hiểu khi phù hợp. Ví dụ: "HTTP 200 có nghĩa là lấy được truyện chưa?" rồi giải thích ngay sau đó.

8. Dùng `=>` để nối quan sát với giải thích, hệ quả hoặc kết luận. Chỉ dùng khi có quan hệ rõ ràng, không thêm sau mọi câu.

9. Gắn bằng chứng với nhận định ngay trong cùng mục. Phân biệt rõ:
   - Quan sát: dữ kiện đo được (status, header, nội dung response).
   - Suy luận: kết quả đó có thể cho thấy điều gì.
   - Đề xuất: Novsay nên làm gì dựa trên kết quả.

10. Giữ cách diễn đạt gần với notes hiện có nhưng sửa thuật ngữ nếu cần để đúng kỹ thuật. Không sao chép khẳng định thiếu chính xác chỉ để giống phong cách.
