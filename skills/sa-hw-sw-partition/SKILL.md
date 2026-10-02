---
name: sa-hw-sw-partition
description: Phân chia chức năng giữa phần cứng, firmware và phần mềm hệ thống; so sánh bộ xử lý, bộ nhớ, I/O, driver và OS/RTOS theo yêu cầu hệ thống nhúng.
---

# Phân chia phần cứng và phần mềm

## Đầu vào

Chức năng, luồng dữ liệu, giao diện và phương án từ `sa-architecture`; ngưỡng thời gian/tài nguyên/chi phí từ `sa-requirements`; dữ liệu nền tảng có nguồn và điều kiện đo.

## Các bước suy luận

| Bước | Input | Phân tích và câu hỏi dẫn dắt | Vì sao | Output → bước sau |
| --- | --- | --- | --- | --- |
| 1. Liệt kê tải | Chức năng và kịch bản | Mỗi chức năng cần tính toán, lưu trữ, I/O, độ trễ, cập nhật và độ tin cậy mức nào? | Tránh chọn nền tảng theo cảm tính | Hồ sơ tải/chức năng → bước 2 |
| 2. Tạo cách phân bổ | Hồ sơ tải, cấu trúc logic | Làm trong ngoại vi/mạch, firmware, driver, OS/middleware hay ứng dụng? Giao tiếp qua đâu? | Cùng chức năng có thể có nhiều cách triển khai với trade-off khác nhau | Các phương án HW/SW → bước 3 |
| 3. Lập ngân sách | Phương án, datasheet, phép đo | Tính CPU, RAM, flash, bus, I/O, điện năng, nhiệt, chi phí; ghi tải đỉnh, overhead, dự phòng và độ bất định | Phương án logic phải khả thi trên giới hạn vật lý | Bảng ngân sách → bước 4 và `sa-realtime` |
| 4. So khớp nền tảng | Ngân sách, yêu cầu, thị trường linh kiện | Processor/board, OS/RTOS, BSP/driver, công cụ debug, vòng đời và tích hợp có đáp ứng không? | Chọn thành phần kéo theo phụ thuộc kỹ thuật và bảo trì | Ma trận lựa chọn → bước 5 |
| 5. Chốt giả thuyết | Ma trận và rủi ro | Ghi lựa chọn, phương án thay thế, giả định cần thử, điều kiện phải xem lại | Ước lượng chưa đủ để chứng minh đạt | Quyết định/phép thử → `sa-verification`; lỗi ngân sách → `sa-architecture` |

## Đầu ra tối thiểu

Ánh xạ chức năng–nơi thực thi, sơ đồ triển khai, bảng tài nguyên theo tải đỉnh, ma trận phương án, quyết định và rủi ro tích hợp.

## Kiểm tra chất lượng

Mọi chức năng có nơi chạy và giao diện; tổng ngân sách có overhead/dự phòng, không cộng số đo ở các điều kiện không tương đương; datasheet và ước lượng được phân biệt với số đo trên đích.

## Nguồn

Noergaard, Ch. 3–10 và Ch. 11.1 giai đoạn 3 (tr. 523–530); Marwedel, Ch. 3–4 và Ch. 6–7; Douglass, Ch. 3.
