---
id: NFR-000
title: ""
updated: DD-MM-YYYY
---

<!-- NFR là ràng buộc chất lượng cấp sản phẩm dưới điều kiện đã nêu (NFG-01).
     Chỉ viết khi cả bốn đúng: có cam kết sản phẩm hoặc rủi ro cần nó; đo/kiểm được; thêm ràng buộc độc lập chứ không lặp FR; mục tiêu có ý nghĩa với người dùng (NFG-02).
     Không hành vi (đó là FR), không giá trị quy tắc (đó là BR, trích [BR-xxx]), không metric kỹ thuật, không giao diện, không kiến trúc, không tiến độ.
     File này không gọi tên use case, bước, nhánh, FR hay NFR khác. Nơi khác trích dẫn [NFR-xxx].
     Viết theo docs/spec/_STYLE.md. -->

## Yêu cầu

<!-- Thuộc tính chất lượng: một, ví dụ hiệu năng, độ tin cậy, toàn vẹn dữ liệu, bảo mật, riêng tư.
     Phát biểu: chất lượng sản phẩm phải có, không kèm mục tiêu.
     Trạng thái: chốt | đề xuất. Vì sao tuỳ chọn, bỏ dòng khi không cần. -->

- **Thuộc tính chất lượng:**
- **Phát biểu:**
- **Trạng thái:** chốt
- **Vì sao:**

## Kiểm chứng

<!-- Ít nhất một phép đo. Một block mỗi phép đo: "### M-n · Tên". ID không đánh lại số (NFG-08).
     Điều kiện: trạng thái, input và môi trường, đủ để lặp lại; nêu biên sản-phẩm-kiểm-soát hay đầu-cuối; nêu điều kiện phụ thuộc provider, không bỏ lặng thời gian provider.
     Đo: đại lượng đo hoặc thuộc tính kiểm. Cách đo: đo/kiểm thế nào bằng lời, không công cụ, không kiến trúc.
     Mục tiêu: giá trị kèm đơn vị và cận, hoặc thuộc tính bắt buộc (kiểm bảo mật/riêng tư có thể là thuộc tính không số). "chưa đặt" khi chờ; không đoán số.
     Đạt khi: điều gì tính là đạt. "chưa đặt" khi chờ. -->

### M-1 · Tên phép đo

- **Điều kiện:**
- **Đo:**
- **Cách đo:**
- **Mục tiêu:** chưa đặt
- **Đạt khi:** chưa đặt

## Chưa xác định

<!-- Khía cạnh bỏ ngỏ không phải mục tiêu, một dòng mỗi ý, kết thúc "Chờ chốt." (hoặc "Chờ bằng chứng kỹ thuật." khi thiếu bằng chứng để định nghĩa).
     Mục tiêu chưa quyết là "chưa đặt", không phải mục ở đây. Bỏ phần này nếu trống. -->

## Ghi chú

<!-- Chỉ điều không thuộc phát biểu lẫn phép đo, ví dụ tách hay gộp. Bỏ phần này nếu trống. -->
