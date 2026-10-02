---
name: sa-requirements
description: Phân tích và đặc tả yêu cầu cho hệ thống nhúng khi cần biến nhu cầu sản phẩm, ràng buộc và thuộc tính chất lượng thành tiêu chí kiến trúc đo được.
---

# Phân tích yêu cầu hệ thống nhúng

## Đầu vào và mục đích

Nhận mục tiêu sản phẩm, mô tả môi trường sử dụng, phản hồi của bên liên quan, hệ thống hiện hữu và các ràng buộc đã biết. Dùng khi bắt đầu dự án hoặc khi thay đổi yêu cầu. Xem [luồng SA](../../SA_CAN_LAM_GI.md) để biết vị trí của skill.

## Các bước suy luận

| Bước | Input | Phân tích và câu hỏi dẫn dắt | Vì sao | Output → bước sau |
| --- | --- | --- | --- | --- |
| 1. Vẽ ngữ cảnh | Mục tiêu, bên liên quan, môi trường | Ranh giới hệ thống ở đâu? Ai/thiết bị nào cấp tín hiệu, nhận đầu ra? Nguồn điện, mạng và con người có vai trò gì? | Không biết ranh giới sẽ bỏ sót giao diện hoặc giao sai trách nhiệm | Sơ đồ ngữ cảnh → tìm kịch bản ở bước 2 |
| 2. Thu kịch bản | Ngữ cảnh | Với mỗi tác nhân: sự kiện bình thường, khởi động, tắt, mất kết nối, lỗi, quá tải và bảo trì dẫn đến phản ứng nào? | Danh sách tính năng không nêu đủ hành vi theo trạng thái và điều kiện | Bảng kích thích–phản ứng → bước 3 |
| 3. Định lượng | Kịch bản, giới hạn sản phẩm | Chuyển “nhanh/tiết kiệm/an toàn” thành số đo, đơn vị, điều kiện và ngưỡng; phân biệt bắt buộc với mục tiêu | Có thể so sánh và kiểm chứng các phương án kiến trúc | Yêu cầu có tiêu chí chấp nhận → mô hình chức năng và phép kiểm |
| 4. Giải xung đột | Yêu cầu sơ bộ | Yêu cầu nào mâu thuẫn về chi phí, điện năng, thời gian, bảo mật? Nguồn nào quyết định? Ghi giả định và câu hỏi mở | Tránh chọn công nghệ dựa trên yêu cầu tự mâu thuẫn | Bảng ưu tiên, quyết định/chưa rõ → bước 5 |
| 5. Lập truy vết | Yêu cầu đã làm rõ | Gắn ID, nguồn, mức ưu tiên, cách xác minh và trạng thái; liên hệ chức năng/thành phần khi chúng được thiết kế | Thay đổi về sau phải tìm được phạm vi ảnh hưởng | Baseline yêu cầu → `sa-architecture` và `sa-verification` |

## Đầu ra tối thiểu

`ID | phát biểu | nguồn | ưu tiên | kịch bản/điều kiện | ngưỡng chấp nhận | cách xác minh | trạng thái`, kèm sơ đồ ngữ cảnh, giả định và câu hỏi mở. Chưa có giá trị đo thì ghi `TBD` cùng người/việc để xác định, không bịa số.

## Kiểm tra chất lượng

Mỗi yêu cầu quan trọng chỉ mô tả một nghĩa có thể kiểm tra; tiêu chí hiệu năng có đơn vị và điều kiện đo; kịch bản lỗi quan trọng có phản ứng rõ. Nếu không thể thiết kế phép kiểm, quay lại bước 2–3.

## Nguồn

Noergaard, Ch. 11.1 giai đoạn 2 (tr. 512–522) về ảnh hưởng, bên liên quan và kịch bản chất lượng. Marwedel, Ch. 2.1 (tr. 29–34) về năng lực cần có của **kỹ thuật đặc tả/mô hình hóa**, như thời gian, đồng thời, lỗi và tính đọc được; không coi mục đó là quy trình thu thập yêu cầu sản phẩm.
