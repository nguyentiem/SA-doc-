---
name: sa-architecture
description: Thiết kế và tài liệu hóa kiến trúc hệ thống nhúng khi cần phân rã thành phần, giao diện, luồng dữ liệu và quyết định kiến trúc có truy vết.
---

# Thiết kế kiến trúc hệ thống nhúng

## Đầu vào

Baseline yêu cầu, kịch bản chất lượng, sơ đồ ngữ cảnh và các ràng buộc từ `sa-requirements`. Nếu thiếu ngưỡng cần để so sánh, phản hồi về skill đó.

## Các bước suy luận

| Bước | Input | Phân tích và câu hỏi dẫn dắt | Vì sao | Output → bước sau |
| --- | --- | --- | --- | --- |
| 1. Rút chức năng/hành vi | Yêu cầu và kịch bản | Những biến đổi dữ liệu, quyết định, trạng thái và phản ứng nào bắt buộc? Đường đi đầu-cuối là gì? | Tránh chọn khối theo tên công nghệ trước khi hiểu trách nhiệm | Mô hình chức năng/luồng/trạng thái → bước 2 |
| 2. Tìm ranh giới khối | Mô hình hành vi | Khối nào cần sở hữu trạng thái/tài nguyên? Chức năng nào phải ở gần cảm biến/đầu ra? Thay đổi nào cần cô lập? | Ranh giới quyết định khả năng tích hợp, kiểm thử và thay đổi | 2–3 cách phân nhóm khả thi → bước 3 |
| 3. Định giao diện | Các nhóm chức năng | Dữ liệu, đơn vị, tốc độ, thời điểm, lỗi, thứ tự và quyền truy cập là gì? | Phần lớn sai lệch phát sinh tại chỗ nối giữa các khối | Bảng hợp đồng giao diện → phân bổ và phân tích thời gian/lỗi |
| 4. So sánh phương án | Yêu cầu đo được, phương án, giao diện | Phương án nào đạt tiêu chí nào; trade-off CPU/RAM/năng lượng/chi phí/lỗi ra sao? Giả định nào còn yếu? | Chọn phương án có lý do kiểm chứng được | Quyết định kiến trúc, rủi ro → `sa-hw-sw-partition` |
| 5. Tài liệu hóa góc nhìn | Quyết định và cấu trúc | Vẽ góc nhìn logic, luồng chạy/đồng thời, triển khai và ngữ cảnh theo câu hỏi cần trả lời; kiểm tra cùng một thành phần được mô tả nhất quán | Một sơ đồ không thể hiện đủ hành vi, cấu trúc và triển khai | Bộ sơ đồ, truy vết → các skill phân tích và đội triển khai |

## Đầu ra tối thiểu

Sơ đồ ngữ cảnh, thành phần/giao diện, luồng sự kiện quan trọng, ánh xạ yêu cầu–thành phần, nhật ký quyết định (`vấn đề | phương án | tiêu chí | quyết định | giả định | điều kiện xem lại`).

## Kiểm tra chất lượng

Mỗi chức năng quan trọng có nơi chịu trách nhiệm; giao diện đủ để hai nhóm triển khai độc lập; góc nhìn khác nhau không mâu thuẫn. Nếu phương án không có cách kiểm chứng, gửi giả thuyết sang `sa-verification`.

## Nguồn

Noergaard, Ch. 11.1 giai đoạn 3–6 (tr. 523–537); Marwedel, Ch. 2 *Specifications and Modeling*, đặc biệt mô hình trạng thái, luồng dữ liệu và đồng thời.
