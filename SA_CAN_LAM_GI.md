# SA cần làm gì và tư duy ra kiến trúc như thế nào

**Phạm vi:** SA là *System Architect* của hệ thống nhúng. Đây là quy trình thực hành tổng hợp từ ba đầu sách trong thư mục, không phải quy trình nguyên văn. Hai file *Embedded Systems Architecture* có cùng nội dung nên chỉ tính một nguồn.

## Câu hỏi trung tâm

> Trong bối cảnh vận hành đã biết, hệ thống phải phản ứng ra sao, giao trách nhiệm cho phần nào, các phần trao đổi thế nào, và bằng chứng nào chứng tỏ kiến trúc đáp ứng yêu cầu?

Chuỗi tư duy là **nhu cầu → hành vi quan sát được → ngưỡng đo → chức năng → thành phần/giao diện → phân bổ tài nguyên → bằng chứng**. Đi thẳng từ nhu cầu tới tên MCU, RTOS hoặc pattern sẽ bỏ qua các mắt xích cần để kiểm tra quyết định.

SA chịu trách nhiệm về tính nhất quán và lý do của quyết định kiến trúc; SA phối hợp với sản phẩm, phần cứng, firmware, phần mềm và kiểm thử, không nhất thiết tự triển khai mọi phần.

## Những gì cần phân tích

| Lớp | Câu hỏi chính | Kết quả |
| --- | --- | --- |
| Bối cảnh và ranh giới | Ai dùng? Hệ thống nhận và tác động gì lên thế giới thật? Thiết bị, hệ thống ngoài và vòng đời ra sao? | Sơ đồ ngữ cảnh, bên liên quan |
| Hành vi | Ở trạng thái nào, sự kiện nào xảy ra, phản ứng gì phải thấy được? Khởi động, dừng, lỗi, cập nhật và quá tải ra sao? | Kịch bản, luồng sự kiện, trạng thái |
| Ràng buộc | Deadline, thông lượng, RAM/flash, điện năng, nhiệt, giá, kích thước, chuẩn nào là bắt buộc? Đo ở điều kiện nào? | Yêu cầu và tiêu chí chấp nhận |
| Cấu trúc | Khối nào giữ trạng thái, xử lý dữ liệu, sở hữu thiết bị/tài nguyên và giao tiếp với khối khác? | Các góc nhìn kiến trúc, hợp đồng giao diện |
| Phương án | Phân bổ HW/SW, bộ xử lý, bus, bộ nhớ, OS/RTOS, driver và chiến lược lỗi nào khả thi? | Ma trận so sánh, trade-off, quyết định |
| Bằng chứng | Phân tích, mô phỏng, nguyên mẫu hay đo trên đích nào có thể bác bỏ giả định? | Ma trận truy vết, kết quả xác minh |

## Các bước làm và mối nối

| Bước | Input | Phân tích/hành động | Vì sao cần | Output và mối nối |
| --- | --- | --- | --- | --- |
| 0. Chốt bối cảnh | Mục tiêu sản phẩm, bên liên quan, hệ thống hiện hữu | Vẽ tác nhân, thiết bị ngoài, môi trường, ranh giới trách nhiệm | Tránh gán nhầm hoặc bỏ sót giao diện | Ngữ cảnh → nhận diện kịch bản ở bước 1 |
| 1. Đặc tả yêu cầu | Ngữ cảnh, nhu cầu, ràng buộc | Viết kịch bản bình thường/bất thường; chuyển thuộc tính chất lượng thành kích thích, điều kiện, phản ứng và ngưỡng; gắn nguồn/ưu tiên | Tạo tiêu chí độc lập để đánh giá phương án | Yêu cầu đo được → phân rã ở bước 2 và phép xác minh ở bước 6 |
| 2. Mô hình chức năng/hành vi | Yêu cầu, tín hiệu vào/ra | Xác định chức năng, trạng thái, luồng dữ liệu, sự kiện, đồng thời và phụ thuộc | Phải biết hệ thống làm gì trước khi chọn cấu trúc | Mô hình hành vi → phương án kiến trúc ở bước 3 |
| 3. Tạo phương án kiến trúc | Mô hình hành vi, thuộc tính chất lượng | Đề xuất cách nhóm chức năng, nơi giữ trạng thái, giao diện và chiến lược xử lý; so sánh cùng tiêu chí | Một phương án đơn lẻ không bộc lộ trade-off | Phương án ứng viên → phân bổ ở bước 4 |
| 4. Phân bổ và lập ngân sách | Phương án, datasheet/ước lượng, giới hạn | Ánh xạ HW, firmware, OS/RTOS và ứng dụng; tính CPU, RAM, flash, bus, nguồn, nhiệt, chi phí | Kiến trúc logic có thể không khả thi trên vật lý | Sơ đồ triển khai/ngân sách → phân tích chéo ở bước 5 |
| 5. Phân tích thời gian và lỗi | Cấu trúc, giao diện, ngân sách, kịch bản lỗi/tải cao | Kiểm tra đường đi đầu-cuối, lịch biểu, tranh chấp, lỗi, phục hồi, bảo mật, test/debug | Thuộc tính chất lượng thường hỏng ở giao diện giữa các khối | Rủi ro/giả thuyết → bước 6; có thể quay lại bước 3–4 |
| 6. Xác minh | Yêu cầu đo được, giả thuyết, cấu hình thử | Phân tích, mô phỏng, nguyên mẫu hoặc đo trên đích; so với ngưỡng và ghi sai lệch | Sơ đồ và ước lượng chưa phải bằng chứng | Kết quả → chốt hoặc sửa yêu cầu, cấu trúc, phân bổ |
| 7. Bàn giao/duy trì | Kiến trúc đã đánh giá, quyết định, kết quả | Tài liệu hóa góc nhìn, giao diện, quyết định, truy vết; rà thay đổi/hồi quy | Đội triển khai và kiểm thử cần cùng một bản hiểu | Baseline kiến trúc → đầu vào cho thay đổi tiếp theo |

Đây là vòng lặp: số đo ở bước 6 có thể bác bỏ giả định của bước 4, dẫn tới phương án mới ở bước 3 hoặc làm rõ lại yêu cầu ở bước 1. Mỗi lần lặp cần ghi giả định nào thay đổi và phép kiểm nào chạy lại.

## Làm sao tự tư duy ra kiến trúc

Với mỗi yêu cầu quan trọng, hỏi theo thứ tự:

1. **Kích thích là gì?** Ai/thiết bị nào tạo sự kiện, tần suất và biến thiên ra sao?
2. **Phản ứng nào phải quan sát được?** Đầu ra, trạng thái, deadline và điều kiện lỗi là gì?
3. **Đường đi nào tạo phản ứng?** Cảm biến → truyền nhận → xử lý → quyết định → đầu ra.
4. **Khối nào cần tồn tại?** Mỗi khối có trách nhiệm, dữ liệu và chủ sở hữu trạng thái/tài nguyên rõ không?
5. **Nút thắt ở đâu?** Tính ngân sách đầu-cuối kể cả chờ đợi, giao tiếp, ngắt và khởi động.
6. **Một khối sai/chậm thì sao?** Phát hiện, cô lập, timeout, suy giảm chức năng và trạng thái an toàn là gì?
7. **Kiểm chứng bằng gì?** Phép thử nào có thể chứng minh phương án sai, ở điều kiện nào và ngưỡng nào?

Nếu thiếu dữ liệu, ghi giả định hoặc câu hỏi mở; chọn phép đo/người cung cấp thông tin. Đừng thay khoảng trống bằng tên công nghệ. Với mỗi phương án, phát biểu giả thuyết: “Nếu dùng cấu trúc A trên nền tảng B, kịch bản K sẽ đạt ngưỡng N trong điều kiện C”, rồi tìm bằng chứng xác nhận hoặc bác bỏ. Ưu tiên giả định có tác động lớn và ít bằng chứng.

### Ví dụ minh họa

Yêu cầu giả định: “Khi cảm biến báo nguy hiểm, đầu ra phải về trạng thái an toàn trong 20 ms, kể cả khi mất kênh truyền chính.” Từ đó cần hai kịch bản (có và mất kết nối), đường đi cảm biến–xử lý–đầu ra, ngân sách cho từng đoạn và cách phát hiện mất kết nối. Nếu thời gian lỗi của kênh truyền không có giới hạn, phương án chỉ phụ thuộc vào quyết định ở trung tâm chưa có cơ sở đạt deadline. SA so sánh xử lý cục bộ, xác nhận ý nghĩa của “an toàn” với người chịu trách nhiệm, rồi thử ngắt kết nối và đo độ trễ trên phần cứng đích ở tải cao. Con số và phương án này chỉ minh họa cách suy luận.

## Skill và luồng bàn giao

| Skill | Nhận từ | Giao cho |
| --- | --- | --- |
| [sa-requirements](skills/sa-requirements/SKILL.md) | Mục tiêu, bối cảnh, bên liên quan | Yêu cầu, kịch bản và ngưỡng cho kiến trúc/xác minh |
| [sa-architecture](skills/sa-architecture/SKILL.md) | Yêu cầu và hành vi | Chức năng, cấu trúc, giao diện cho phân bổ, thời gian và lỗi |
| [sa-hw-sw-partition](skills/sa-hw-sw-partition/SKILL.md) | Phương án và giới hạn | Nền tảng, ngân sách và giả định cho phân tích/xác minh |
| [sa-realtime](skills/sa-realtime/SKILL.md) | Luồng sự kiện và phân bổ | Deadline, ngân sách, phép đo; phản hồi nếu không đạt |
| [sa-dependability](skills/sa-dependability/SKILL.md) | Kịch bản lỗi và kiến trúc | Biện pháp, phép thử lỗi, rủi ro còn lại; phản hồi cho yêu cầu/kiến trúc |
| [sa-verification](skills/sa-verification/SKILL.md) | Yêu cầu, quyết định, giả thuyết | Bằng chứng/sai lệch để chốt hoặc lặp các bước trước |

## Điểm dừng để bàn giao

Yêu cầu chi phối kiến trúc có nguồn và ngưỡng đo; chức năng quan trọng có chủ sở hữu, giao diện và nơi thực thi; ngân sách quan trọng có giả định/bằng chứng; quyết định lớn có lý do, phương án thay thế và điều kiện xem lại; truy vết được **yêu cầu → quyết định/thành phần → phép kiểm → kết quả**. Các điểm chưa chắc chắn còn lại có người theo dõi và kế hoạch kiểm chứng.

## Nguồn và giới hạn

- Noergaard, *Embedded Systems Architecture*, Ch. 11, tr. 509–537: sáu giai đoạn tạo, tài liệu hóa, đánh giá kiến trúc; Ch. 3–10 về các lớp kỹ thuật; Ch. 12 về triển khai/kiểm thử/bảo trì. [PDF](<Embedded Systems Architecture - A Comprehensive Guide for Engineers and Programmers.pdf>).
- Marwedel, *Embedded System Design*, 4th ed. (2021), Ch. 2–8: mô hình/specification, phần cứng, phần mềm hệ thống, đánh giá, ánh xạ ứng dụng, tối ưu, kiểm thử. **Mục 2.1 nói về yêu cầu đối với kỹ thuật mô hình hóa**, không phải checklist thu thập yêu cầu sản phẩm. [PDF](2021_Book_EmbeddedSystemDesign.pdf).
- Douglass, *Design Patterns for Embedded Systems in C* (2011), Ch. 3–6: pattern truy cập phần cứng, đồng thời/tài nguyên, máy trạng thái, an toàn/độ tin cậy. Pattern là phương án để cân nhắc, không thay thế phân tích yêu cầu. [PDF](design-patterns-for-embedded-systems-in-c-an-embedded-software-engineering-t.pdf).

Các ví dụ công nghệ và chuẩn trong sách cũ cần đối chiếu với datasheet và tài liệu hiện hành khi áp dụng cho dự án thật.
