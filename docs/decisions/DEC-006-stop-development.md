---
id: DEC-006
title: "Dừng phát triển Novsay"
date: 29-10-2026
status: decided
affects: "toàn bộ dự án"
---

## Quyết định

Dừng phát triển Novsay. Giữ lại tài liệu và kết quả nghiên cứu để tham khảo, không tiếp tục implementation.

## Bối cảnh

Novsay xuất phát từ nhu cầu lấy nội dung truyện trên website và chuyển thành audio để nghe thuận tiện hơn.

## Lý do dừng

1. **Giá trị chưa đủ rõ.** Chưa xác định được lợi ích đủ rõ so với các sản phẩm có sẵn như NaturalReader hoặc Speechify.

2. **Trở ngại kỹ thuật.** Việc lấy nội dung tự động gặp trở ngại từ cơ chế chống bot của website nguồn. Các thử nghiệm đã ghi nhận Node fetch bị challenge trên những nguồn đã thử. Chưa có giải pháp được kiểm chứng là đủ ổn định cho trải nghiệm mong muốn.

3. **Chi phí tiếp tục không tương xứng.** Tiếp tục sẽ cần thêm công sức nghiên cứu, triển khai và bảo trì, trong khi giá trị nhận lại chưa đủ rõ.

Quyết định này không có nghĩa Novsay không thể làm được. Hiện tại, dự án chưa đủ giá trị để tiếp tục đầu tư.

## Bài học

Kiểm tra sớm nhu cầu, giải pháp hiện có và giả định kỹ thuật có thể khiến dự án phải dừng, trước khi đầu tư sâu vào specification và implementation plan.
