---
title: "Worklog Tuần 5"
date: 2026-02-02
weight: 5
chapter: false
pre: " <b> 1.5. </b> "
---

### Mục tiêu tuần 5:

* **Backend**: Xây dựng module `UserWorkoutPlan` — kế hoạch cá nhân với clone từ system template, soft-delete, và logic chỉ một kế hoạch active.
* **Frontend**: Xây dựng các màn hình quản lý kế hoạch — `MyPlansScreen`, `CreatePlanScreen`, `PlanEditScreen` với tab chỉnh sửa theo ngày.
* Cho phép user tự quản lý lịch tập cá nhân linh hoạt.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --------- | ------------ | --------------- | -------------- |
| 2   | - Xây dựng **UserWorkoutPlan** entity <br>&emsp; + Trường: `user (@ManyToOne)`, `name (≤150)`, `description`, `goalTypeId (UUID)`, `isActive`, `isDeleted` <br>&emsp; + Soft-delete qua `@SQLRestriction("is_deleted = false")` <br>&emsp; + Viết Flyway **V1**: tạo bảng `user_workout_plan`, `user_workout_plan_exercises` | 03/02/2026 | 03/02/2026 | |
| 2   | - Viết Flyway **V2**: thêm cột `is_deleted BOOLEAN DEFAULT FALSE` | 03/02/2026 | 03/02/2026 | |
| 3   | - Xây dựng **UserWorkoutPlanExercise** entity <br>&emsp; + `dayOfWeek`, `sets`, `reps`, `restSeconds`, `dayIndex`, `weekIndex`, `orderIndex` <br>&emsp; + Reference `Exercise` và `UserWorkoutPlan` | 04/02/2026 | 04/02/2026 | |
| 3   | - Triển khai business logic trong **UserWorkoutPlanService** <br>&emsp; + `userId` luôn lấy từ `Jwt.getSubject()` — ngăn chặn IDOR <br>&emsp; + **Clone**: sao chép sâu toàn bộ `WorkoutPlanExercise` — không giữ FK về kế hoạch gốc <br>&emsp; + **Activate**: đặt `isActive=true` cho plan mục tiêu, `isActive=false` cho tất cả plan khác | 04/02/2026 | 04/02/2026 | |
| 4   | - Xây dựng **UserWorkoutPlanController** (`/api/user-workout-plans`) <br>&emsp; + `POST /me` (tạo kế hoạch), `POST /me/clone/{systemPlanId}` (clone) <br>&emsp; + `GET /me`, `GET /me/active`, `GET /{id}` <br>&emsp; + `PUT /{id}`, `PUT /{id}/activate`, `DELETE /{id}` (soft) <br>&emsp; + CRUD bài tập trong kế hoạch | 05/02/2026 | 05/02/2026 | |
| 5   | - Xây dựng **MyPlansScreen** (Frontend) <br>&emsp; + Liệt kê tất cả kế hoạch với badge trạng thái active <br>&emsp; + Toggle kích hoạt; xóa với `ConfirmModal` <br> - Xây dựng **CreatePlanScreen** (Frontend) <br>&emsp; + Form: tên, mô tả, dropdown goal type | 06/02/2026 | 06/02/2026 | |
| 6   | - Xây dựng **PlanEditScreen** (Frontend) <br>&emsp; + Tab bar theo ngày (Thứ 2 - Chủ nhật) để xem bài tập từng ngày <br>&emsp; + Reorder (lên/xuống), xóa bài tập <br>&emsp; + Điến `PlanExercisePicker` để thêm bài tập | 07/02/2026 | 07/02/2026 | |

### Kết quả đạt được tuần 5:

* **Backend — Module UserWorkoutPlan**:
  * Flyway V1 + V2 migrations được apply thành công.
  * Soft-delete với `@SQLRestriction` hoạt động — kế hoạch đã xóa không bao giờ xuất hiện trong query.
  * Clone tạo bản sao độc lập — xem xét xác nhận không có FK về source.
  * Quy tắc một plan active được thực thi tại service layer.
  * `userId` luôn lấy từ JWT — bảo mật IDOR hoàn toàn.
* **Frontend — Quản lý kế hoạch**:
  * `MyPlansScreen` hiển thị đồng bộ trạng thái active/inactive.
  * `CreatePlanScreen` validate trước khi submit.
  * `PlanEditScreen` theo ngày dễ dùng, sử dụng `uiSlice` để sync trạng thái.

### Kiến thức AWS đã học và giả sử áp dụng cho project:

* Hiểu mô hình vận hành PostgreSQL trên Amazon RDS (single AZ) cho môi trường production cơ bản.
* Nắm cách dùng Security Group và subnet để giới hạn truy cập DB chỉ từ service backend.
* Biết chiến lược backup snapshot tự động và khôi phục dữ liệu cho user-owned data quan trọng.
* Hiểu vì sao migration phải idempotent để deploy an toàn qua nhiều môi trường.
### Kế hoạch tuần tiếp theo:

* **Backend**: Xây dựng module `UserWorkoutSession` và `WorkoutLog` để theo dõi buổi tập thực tế.
* **Frontend**: Xây dựng `PlanDetailScreen` (dashboard kế hoạch active) và `WorkoutSessionScreen` (màn hình tập thực tế với Redux session state).


### Mục tiêu tuần 5:

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


### Kết quả đạt được tuần 5:

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


