---
title: "Worklog Tuần 10"
date: 2026-03-16
weight: 10
chapter: false
pre: " <b> 1.10. </b> "
---

### Mục tiêu tuần 10:

* **Backend**: Hoàn thiện endpoint — cải thiện validation, pagination, viết unit test cho service chính.
* **Frontend**: Xây dựng `ChatScreen` với AWS Bedrock AI và `ProfileScreen` quản lý tài khoản.
* Cung cấp trợ lý AI tư vấn fitness — tính năng khác biệt của ứng dụng.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --------- | ------------ | --------------- | -------------- |
| 2   | - Hoàn thiện endpoint backend <br>&emsp; + Thêm `@Valid` và custom constraint validator cho tất cả request DTO <br>&emsp; + Chuẩn hóa `PageResponse<T>` cho tất cả paginated endpoint <br>&emsp; + Thêm filter ngày chạy `?startDate=&endDate=` cho session history | 13/10/2025 | 13/10/2025 | |
| 3   | - Viết **unit test** (JUnit 5 + Mockito) <br>&emsp; + `UserWorkoutPlanServiceTest`: clone, activate, IDOR prevention <br>&emsp; + `HealthCalculationServiceTest`: BMI/BMR/TDEE cho nhiều trường hợp <br>&emsp; + `UserWorkoutSessionServiceTest`: active session query, deactivate | 14/10/2025 | 14/10/2025 | |
| 4   | - Xây dựng **chatService** (Frontend) <br>&emsp; + Gọi trực tiếp AWS Bedrock Runtime API <br>&emsp; + Model: `anthropic.claude-3-5-haiku-20241022-v1:0` <br>&emsp; + System prompt tiếng Việt: persona huấn luyện viên thể dục <br>&emsp; + Gửi 12 lượt hội thoại gần nhất (sliding window) | 15/10/2025 | 15/10/2025 | <https://docs.aws.amazon.com/bedrock/> |
| 5   | - Xây dựng **ChatScreen** (Frontend) <br>&emsp; + Giao diện chat toàn màn hình với bừa chat user/bot <br>&emsp; + Hiệu ứng "đang gõ" (3 chấm nẩy) khi chờ phản hồi <br>&emsp; + 4 chip gợi ý nhanh: "Gợi ý bài tập", "Thực đơn hôm nay", "Mục tiêu calo", "Tư vấn giảm cân" <br>&emsp; + Lời chào của bot bằng tiếng Việt <br>&emsp; + Keyboard avoidance animation | 16/10/2025 | 16/10/2025 | |
| 6   | - Xây dựng **ProfileScreen** (Frontend) <br>&emsp; + Hiển thị avatar, tên, email, username, ngày sinh, giới tính <br>&emsp; + Modal chỉnh sửa ngày sinh và giới tính <br>&emsp; + Đăng xuất: `signOut` + `dispatch(logout)` + xóa secure storage <br>&emsp; + Xóa tài khoản: `deleteUserProfile` + `signOut` — đều có `ConfirmModal` xác nhận | 17/10/2025 | 17/10/2025 | |

### Kết quả đạt được tuần 10:

* **Backend — Hoàn thiện & Testing**:
  * Tất cả DTO có `@Valid` — lỗi validation trả về cấu trúc `ApiResponse` theo field.
  * `PageResponse<T>` được chuẩn hóa cho tất cả paginated endpoint.
  * Unit test pass cho `UserWorkoutPlanService`, `HealthCalculationService`, `UserWorkoutSessionService`.
* **Frontend — AI Chat**:
  * `chatService` gọi Bedrock thành công, chat có context vai trò tiếng Việt.
  * Quick-option chip cho phép tương tác ngay không cần tự gõ.
* **Frontend — Profile**:
  * Load profile từ Redux — không tốn thêm API call.
  * Đăng xuất và xóa tài khoản đều có xác nhận an toàn.

### Kế hoạch tuần tiếp theo:

* **Backend**: Review lần cuối API, hoàn thiện Docker Compose với health check và tài liệu biến môi trường.
* **Frontend**: Xây dựng `HomeScreen` dashboard với 5 API song song, sửa bug còn tồn, polish UX toàn ứng dụng.


### Mục tiêu tuần 10:

* Kết nối, làm quen với các thành viên trong First Cloud Journey.
* Hiểu dịch vụ AWS cơ bản, cách dùng console & CLI.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc                                                                                                                                                                                   | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu                            |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | ----------------------------------------- |
| 2   | - Làm quen với các thành viên FCJ <br> - Đọc và lưu ý các nội quy, quy định tại đơn vị thực tập                                                                                             | 11/08/2025   | 11/08/2025      |
| 3   | - Tìm hiểu AWS và các loại dịch vụ <br>&emsp; + Compute <br>&emsp; + Storage <br>&emsp; + Networking <br>&emsp; + Database <br>&emsp; + ... <br>                                            | 12/08/2025   | 12/08/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 4   | - Tạo AWS Free Tier account <br> - Tìm hiểu AWS Console & AWS CLI <br> - **Thực hành:** <br>&emsp; + Tạo AWS account <br>&emsp; + Cài AWS CLI & cấu hình <br> &emsp; + Cách sử dụng AWS CLI | 13/08/2025   | 13/08/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 5   | - Tìm hiểu EC2 cơ bản: <br>&emsp; + Instance types <br>&emsp; + AMI <br>&emsp; + EBS <br>&emsp; + ... <br> - Các cách remote SSH vào EC2 <br> - Tìm hiểu Elastic IP   <br>                  | 14/08/2025   | 15/08/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 6   | - **Thực hành:** <br>&emsp; + Tạo EC2 instance <br>&emsp; + Kết nối SSH <br>&emsp; + Gắn EBS volume                                                                                         | 15/08/2025   | 15/08/2025      | <https://cloudjourney.awsstudygroup.com/> |


### Kết quả đạt được tuần 10:

* Hiểu AWS là gì và nắm được các nhóm dịch vụ cơ bản: 
  * Compute
  * Storage
  * Networking 
  * Database
  * ...

* Đã tạo và cấu hình AWS Free Tier account thành công.

* Làm quen với AWS Management Console và biết cách tìm, truy cập, sử dụng dịch vụ từ giao diện web.

* Cài đặt và cấu hình AWS CLI trên máy tính bao gồm:
  * Access Key
  * Secret Key
  * Region mặc định
  * ...

* Sử dụng AWS CLI để thực hiện các thao tác cơ bản như:

  * Kiểm tra thông tin tài khoản & cấu hình
  * Lấy danh sách region
  * Xem dịch vụ EC2
  * Tạo và quản lý key pair
  * Kiểm tra thông tin dịch vụ đang chạy
  * ...

* Có khả năng kết nối giữa giao diện web và CLI để quản lý tài nguyên AWS song song.
* ...


