---
title: "Worklog Tuần 11"
date: 2026-03-23
weight: 11
chapter: false
pre: " <b> 1.11. </b> "
---

### Mục tiêu tuần 11:

* **Backend**: Review API lần cuối, hoàn thiện Docker Compose sẵn sàng production, tài liệu biến môi trường.
* **Frontend**: Xây dựng `HomeScreen` dashboard trung tâm, sửa bug còn tồn, polish UX toàn ứng dụng.
* Đạt được ứng dụng hoàn chỉnh, tích hợp đầy đủ, sẵn sàng test cuối.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --------- | ------------ | --------------- | -------------- |
| 2   | - Xây dựng **HomeScreen** (Frontend) — 5 API song song khi mount <br>&emsp; + Bữa ăn hôm nay: tổng calo → progress bar vs. 2500 kcal <br>&emsp; + BMI từ `HealthCalculation` mới nhất <br>&emsp; + Chiều cao/cân nặng từ `BodyMetric` mới nhất <br>&emsp; + Tên kế hoạch tập active + link nhanh đến PlanDetail <br>&emsp; + Số buổi tập tuần này vs. mục tiêu 4 buổi | 24/03/2026 | 24/03/2026 | |
| 3   | - Hoàn thiện **Docker Compose** <br>&emsp; + Thêm `healthcheck` trên service `postgres` (`pg_isready`) <br>&emsp; + `depends_on.db.condition: service_healthy` cho service API <br>&emsp; + Xác nhận `GET /actuator/health` hoạt động <br>&emsp; + Hoàn chỉnh `.env.example` với mô tả tất cả biến | 25/03/2026 | 25/03/2026 | |
| 4   | - **Sửa bug** toàn diện Frontend <br>&emsp; + `WorkoutSessionScreen`: edge case hoàn thành bài tập cuối <br>&emsp; + `DietScreen`: `ensureDailyMeals` chỉ gọi 1 lần khi mount <br>&emsp; + `HealthDashboardScreen`: hiển loading khi gọi `calculateMetrics` <br>&emsp; + `BMITrendChart`: empty state khi dưới 2 điểm dữ liệu | 26/03/2026 | 26/03/2026 | |
| 5   | - Cải thiện **Response Interceptor** (Axios `client.ts`) <br>&emsp; + Hàng đợi refresh token: nhiều request `401` cùng lúc → chỉ refresh 1 lần duy nhất <br>&emsp; + Nếu refresh thất bại: `forceLogout` xóa token + logout Redux + về Login <br>&emsp; + Xử lý `code === 4040` "user not found" → tự động `forceLogout` | 27/03/2026 | 27/03/2026 | |
| 6   | - **Polish UX** toàn ứng dụng <br>&emsp; + Thêm `NotificationBox` thay thế native `Alert.alert` qua `installAlertProxy` <br>&emsp; + Thêm pull-to-refresh cho `HomeScreen` <br>&emsp; + Chuẩn hóa loading spinner và error state trên tất cả màn hình <br>&emsp; + Kiểm tra nhãn tiếng Việt nhất quán | 28/03/2026 | 28/03/2026 | |

### Kết quả đạt được tuần 11:

* **Backend — Docker Compose**:
  * Health check PostgreSQL đảm bảo API container chờ DB sẵn sàng hoàn toàn.
  * `.env.example` tài liệu đầy đủ 10+ biến môi trường cần thiết.
* **Frontend — HomeScreen**:
  * 5 API song song hoàn thành trong dưới 1.5s trên localhost.
  * Người dùng thấy rõ tiến độ calo và buổi tập ngày/tuần ngay khi mở app.
* **Frontend — Sửa Bug & Polish**:
  * Các bug quan trọng được xử lý; token refresh hoạt động ổn định.
  * `NotificationBox` tạo trải nghiệm thông báo đồng nhất toàn ứng dụng.
  * Nhãn tiếng Việt nhất quán trên tất cả màn hình.

### Kế hoạch tuần tiếp theo:

* Chạy kiểm thử tích hợp end-to-end toàn bộ ứng dụng.
* Viết tài liệu dự án (README, API reference, sơ đồ kiến trúc).
* Chuẩn bị demo và dọn dẹp code cho bàn giao.


### Mục tiêu tuần 11:

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


### Kết quả đạt được tuần 11:

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


