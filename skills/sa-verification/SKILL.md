---
name: sa-verification
description: Đánh giá và xác minh kiến trúc hệ thống nhúng bằng phân tích, mô phỏng, nguyên mẫu và phép đo có truy vết về yêu cầu.
---

# Xác minh kiến trúc hệ thống nhúng

## Đầu vào

Yêu cầu có ngưỡng từ `sa-requirements`, quyết định/giả định từ `sa-architecture`, ngân sách HW/SW và kết quả phân tích thời gian/lỗi. Dùng cả trước khi triển khai đầy đủ để giảm rủi ro sớm.

## Các bước suy luận

| Bước | Input | Phân tích và câu hỏi dẫn dắt | Vì sao | Output → bước sau |
| --- | --- | --- | --- | --- |
| 1. Lập truy vết | Yêu cầu, quyết định, thành phần | Yêu cầu nào được khối/quyết định nào đáp ứng? Bằng chứng nào sẽ kiểm tra? | Tránh yêu cầu không ai thực hiện hoặc không ai kiểm | Ma trận yêu cầu–quyết định–phép kiểm → bước 2 |
| 2. Chọn rủi ro để thử | Giả định, mức tác động, độ bất định | Nếu giả định sai thì ảnh hưởng lớn đến đâu, sửa muộn tốn bao nhiêu? | Nguồn lực kiểm chứng cần dồn vào điều có thể làm hỏng kiến trúc | Danh sách giả thuyết ưu tiên → bước 3 |
| 3. Thiết kế bằng chứng | Giả thuyết và ngưỡng | Phân tích, mô phỏng, nguyên mẫu hay đo trên đích? Điều kiện, dữ liệu, độ chính xác và ngưỡng là gì? | Một phép đo thiếu điều kiện không chứng minh được kết luận | Kế hoạch kiểm chứng tái lập → bước 4 |
| 4. Thực hiện và kết luận | Kế hoạch, hệ thống/mô hình | Ghi cấu hình, công cụ, tải, số đo, sai số; so với ngưỡng. Phân biệt đạt, không đạt, chưa đủ bằng chứng | Quyết định phải dựa trên kết quả chứ không trên kỳ vọng | Báo cáo bằng chứng/sai lệch → bước 5 |
| 5. Đóng vòng lặp | Sai lệch và quyết định | Sửa yêu cầu, mô hình, phân bổ hay biện pháp? Thành phần và bài kiểm nào bị ảnh hưởng? | Thay đổi một chỗ có thể làm hỏng tính chất khác | Quyết định cập nhật và kiểm thử hồi quy → các skill trước |

## Đầu ra tối thiểu

Ma trận `yêu cầu | quyết định/thành phần | giả thuyết | phương pháp | điều kiện | ngưỡng | kết quả | trạng thái`, báo cáo đo và danh sách sai lệch có người xử lý.

## Kiểm tra chất lượng

Mỗi kết luận “đạt” có dữ liệu và điều kiện tái lập; không coi kết quả trên nguyên mẫu là kết quả trên sản phẩm nếu cấu hình khác. Khi chưa có bằng chứng đủ mạnh, ghi “chưa xác minh” và việc cần làm tiếp.

## Nguồn

Noergaard, Ch. 11.1 giai đoạn 6 (tr. 535–537) và Ch. 12; Marwedel, Ch. 5 *Evaluation and Validation* và Ch. 8 *Test*.
