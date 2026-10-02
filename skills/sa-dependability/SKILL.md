---
name: sa-dependability
description: Phân tích độ tin cậy, an toàn và hành vi lỗi ở mức kiến trúc cho hệ thống nhúng khi sự cố có hậu quả đáng kể.
---

# Thiết kế cho lỗi và an toàn

## Đầu vào

Kịch bản vận hành/lỗi từ `sa-requirements`, đường đi và giao diện từ `sa-architecture`, phân bổ và ràng buộc thời gian từ hai skill tiếp theo. Chỉ dùng mức chi tiết tương xứng hậu quả lỗi của sản phẩm.

## Các bước suy luận

| Bước | Input | Phân tích và câu hỏi dẫn dắt | Vì sao | Output → bước sau |
| --- | --- | --- | --- | --- |
| 1. Xác định điều không được xảy ra | Bối cảnh, người dùng, cơ cấu chấp hành | Hậu quả nào gây hại, mất dịch vụ hoặc mất dữ liệu? Trạng thái an toàn là gì và ai xác nhận? | Không thể chọn biện pháp nếu chưa biết cần tránh hậu quả nào | Danh sách nguy cơ/hậu quả → bước 2 |
| 2. Tìm đường gây lỗi | Sơ đồ chức năng, giao diện, nguồn lỗi | Lỗi cảm biến, tính toán, bộ nhớ, nguồn, giao tiếp, thao tác hoặc tấn công có thể lan tới đâu? Có lỗi chung không? | Biện pháp cục bộ có thể không chặn được lan truyền | Chuỗi lỗi–hậu quả → bước 3 |
| 3. Chọn biện pháp | Chuỗi lỗi, ràng buộc | Phát hiện bằng gì, trong bao lâu? Cô lập, dự phòng, timeout/watchdog, suy giảm hay dừng an toàn? Tác động lên thời gian, nguồn và chi phí? | Biện pháp phải giải quyết lỗi cụ thể và không làm vỡ yêu cầu khác | Phương án giảm thiểu và trade-off → bước 4 |
| 4. Định nghĩa hành vi lỗi | Biện pháp và trạng thái | Khi phát hiện lỗi, đầu ra, log, phục hồi và quyền điều khiển thay đổi ra sao? | Người triển khai và kiểm thử cần hành vi không mơ hồ | Yêu cầu lỗi/giao diện bổ sung → kiến trúc và phép thử |
| 5. Đánh giá rủi ro còn lại | Phương án, bằng chứng | Lỗi nào vẫn có thể lọt, mức hậu quả và giả định nào chưa được chứng minh? Ai chấp nhận? | Không thể suy ra an toàn tuyệt đối từ việc thêm một pattern | Rủi ro/phép thử lỗi → `sa-verification`; thiếu đáp ứng → quay lại kiến trúc |

## Đầu ra tối thiểu

Bảng `nguy cơ | nguyên nhân/đường lỗi | hậu quả | phát hiện | phản ứng | giới hạn thời gian | bài kiểm | rủi ro còn lại`, định nghĩa trạng thái an toàn và giả định được người có trách nhiệm xác nhận.

## Kiểm tra chất lượng

Biện pháp gắn với lỗi cụ thể, có cách kích lỗi và quan sát phản ứng; phân biệt reliability, safety và security theo hậu quả cần bảo vệ. Không tuyên bố tuân thủ chuẩn nếu chưa có quy trình và chứng cứ theo chuẩn áp dụng.

## Nguồn

Marwedel, Ch. 5.6 *Dependability and Risk Analysis*; Douglass, Ch. 6 *Safety and Reliability Patterns*; Noergaard, Ch. 11.1 về kịch bản thuộc tính chất lượng.
