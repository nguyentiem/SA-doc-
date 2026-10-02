---
name: sa-realtime
description: Phân tích kiến trúc thời gian thực của hệ thống nhúng khi có tác vụ định kỳ, sự kiện, deadline, ngắt hoặc tài nguyên dùng chung.
---

# Thiết kế và kiểm tra thời gian thực

## Đầu vào

Kịch bản có deadline từ `sa-requirements`, đường đi/giao diện từ `sa-architecture`, nền tảng và tài nguyên từ `sa-hw-sw-partition`.

## Các bước suy luận

| Bước | Input | Phân tích và câu hỏi dẫn dắt | Vì sao | Output → bước sau |
| --- | --- | --- | --- | --- |
| 1. Lập chuỗi phản ứng | Kịch bản và luồng sự kiện | Sự kiện đến lúc nào, qua những đoạn nào, deadline tính từ đâu tới đâu? | Tránh đo nhầm một tác vụ thay vì phản ứng đầu-cuối | Sơ đồ chuỗi thời gian → bước 2 |
| 2. Mô hình tải | Chuỗi, nền tảng | Chu kỳ/kiểu đến, tải đỉnh, burst, tác vụ đồng thời, thời gian thực thi tối đa ước lượng là gì? | Tải trung bình không chứng minh được deadline | Bảng tác vụ và khoảng bất định → bước 3 |
| 3. Chọn lịch biểu/giao tiếp | Bảng tác vụ, OS/RTOS | Ưu tiên, ngắt, hàng đợi, khóa, đảo ưu tiên, deadlock và mất sự kiện được xử lý thế nào? | Chờ đợi/tranh chấp thường quyết định độ trễ thực | Cấu hình lịch biểu và ngân sách chờ → bước 4 |
| 4. Kiểm tra đầu-cuối | Các đoạn thực thi và chờ | Cộng giới hạn thời gian cho cảm biến, truyền, xử lý, queue, bus, đầu ra; xét jitter và lỗi deadline | Đáp ứng cục bộ không đảm bảo đáp ứng hệ thống | Phân tích đạt/chưa đạt → bước 5; chưa đạt thì phản hồi phân bổ |
| 5. Đo và điều chỉnh | Ngân sách, phần cứng đích | Đo ở tải cao, điều kiện ngắt/cache/bus đại diện; so với ngưỡng và ghi cấu hình | Ước lượng thời gian phải được kiểm chứng | Bằng chứng → `sa-verification`; sai lệch → bước 2–4 |

## Đầu ra tối thiểu

Bảng `sự kiện | chu kỳ/kiểu đến | deadline | tác vụ | WCET/ước lượng | chờ tối đa | jitter | bằng chứng`, sơ đồ chuỗi phản ứng, ngân sách thời gian và kế hoạch đo.

## Kiểm tra chất lượng

Nêu rõ WCET là bound có cơ sở hay chỉ là số đo/ước lượng; không suy ra bảo đảm real-time từ mức sử dụng CPU trung bình hoặc một lần đo thuận lợi.

## Nguồn

Marwedel, Ch. 5 về đánh giá/WCET và Ch. 6 về lịch biểu; Douglass, Ch. 4 về đồng thời và quản lý tài nguyên, Ch. 5 về máy trạng thái; Noergaard, Ch. 9.
