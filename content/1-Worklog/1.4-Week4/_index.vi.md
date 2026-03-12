---
title: "Worklog Tuần 4"
date: 2026-01-26
weight: 4
chapter: false
pre: " <b> 1.4. </b> "
---

### Mục tiêu tuần 4:

* **Backend**: Xây dựng module System Workout — dữ liệu bài tập và kế hoạch mẫu do admin quản lý.
* **Frontend**: Xây dựng các màn hình duyệt bài tập — wizard gợi ý kế hoạch và bộ chọn bài tập.
* Thiết lập mối quan hệ `GoalType` ↔ `WorkoutPlan` ↔ `Exercise` cho tính năng gợi ý kế hoạch.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --------- | ------------ | --------------- | -------------- |
| 2   | - Xây dựng **MuscleGroup** entity & admin CRUD <br>&emsp; + Entity: `name (UNIQUE, ≤100)`, `description (≤500)` <br>&emsp; + `AdminMuscleGroupController` với `@PreAuthorize("hasRole('ADMIN')")` <br>&emsp; + CRUD đầy đủ: `POST`, `GET /`, `GET /{id}`, `PUT /{id}`, `DELETE /{id}` | 27/01/2026 | 27/01/2026 | |
| 3   | - Xây dựng **Exercise** entity & admin CRUD <br>&emsp; + Entity: `name (≤150)`, `description`, `equipment`, `muscleGroup (@ManyToOne)` <br>&emsp; + `AdminExerciseController`: full CRUD + filter by muscle group <br>&emsp; + Public: `GET /api/workouts/exercises`, `GET /{id}`, `GET /by-muscle-group/{id}`, `POST /custom` | 28/01/2026 | 28/01/2026 | |
| 4   | - Xây dựng **WorkoutPlan** & **WorkoutPlanExercise** <br>&emsp; + `WorkoutPlan`: `name`, `description`, `goalType (@ManyToOne)`, `difficultyLevel`, `estimatedDurationMinutes`, `isSystemPlan` <br>&emsp; + `WorkoutPlanExercise`: lịch theo `dayOfWeek (1-7)`, `sets`, `reps`, `restSeconds`, `dayIndex`, `weekIndex`, `orderIndex` <br>&emsp; + `AdminWorkoutPlanController`: CRUD đầy đủ + filter theo goal type | 29/01/2026 | 29/01/2026 | |
| 4   | - Mở các **public workout endpoints** qua `WorkoutController` (`/api/workouts`) <br>&emsp; + `GET /muscle-groups`, `GET /muscle-groups/{id}` <br>&emsp; + `GET /exercises`, `GET /exercises/{id}`, `GET /exercises/by-muscle-group/{id}` <br>&emsp; + `GET /plans`, `GET /plans/{id}`, `GET /plans/by-goal-type/{id}` | 29/01/2026 | 29/01/2026 | |
| 5   | - Xây dựng **SuggestedPlanScreen** (Frontend) — wizard 3 bước <br>&emsp; + Bước 1: Chọn loại mục tiêu (gọi `GET /api/goal-types`) <br>&emsp; + Bước 2: Duyệt kế hoạch mẫu với hình ảnh và độ khó <br>&emsp; + Bước 3: Xem chi tiết kế hoạch theo ngày → clone qua `cloneFromSystemPlan` | 30/01/2026 | 30/01/2026 | |
| 6   | - Xây dựng **PlanExercisePicker** screen (Frontend) <br>&emsp; + Liệt kê tất cả bài tập hệ thống với hình ảnh và nhóm cơ <br>&emsp; + Tìm kiếm theo tên <br>&emsp; + Khi chọn: gọi `addExerciseToPlan(planId, dayOfWeek, exerciseId)` <br> - Seed dữ liệu bài tập và nhóm cơ ban đầu qua `DatabaseSeeder` | 31/01/2026 | 31/01/2026 | |

### Kết quả đạt được tuần 4:

* **Backend — System Workout**:
  * Entity `MuscleGroup` + admin CRUD hoạt động; đã seed: Ngực, Lưng, Chân, Vai, Tay, Cơ bụng.
  * `Exercise` + admin CRUD + public read endpoints hoạt động.
  * `WorkoutPlan` với `WorkoutPlanExercise` (lịch theo ngày, hỗ trợ multi-week qua `weekIndex`) triển khai xong.
  * Admin endpoints được bảo vệ bởi `ROLE_ADMIN`; public read truy cập không cần auth.
* **Frontend — Duyệt bài tập**:
  * `SuggestedPlanScreen` hướng dẫn user qua mục tiêu → chọn kế hoạch trong 3 bước rõ ràng.
  * `PlanExercisePicker` liệt kê bài tập với context nhóm cơ; chọn bài tập thêm vào kế hoạch user.
* `DatabaseSeeder` seed dữ liệu nhóm cơ + bài tập ban đầu khi khởi động ứng dụng.

### Kế hoạch tuần tiếp theo:

* **Backend**: Xây dựng module `UserWorkoutPlan` với clone kế hoạch từ system template, soft-delete, và logic kích hoạt.
* **Frontend**: Xây dựng `MyPlansScreen`, `CreatePlanScreen`, và `PlanEditScreen` (trình chỉnh sửa theo ngày).


### Mục tiêu tuần 4:

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


### Kết quả đạt được tuần 4:

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


