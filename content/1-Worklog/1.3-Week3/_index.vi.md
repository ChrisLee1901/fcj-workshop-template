---
title: "Worklog Tuần 3"
date: 2026-01-19
weight: 3
chapter: false
pre: " <b> 1.3. </b> "
---

### Mục tiêu tuần 3:

* **Backend**: Xây dựng lớp cơ sở hạ tầng chung — xử lý exception, CORS, và module `GoalType`.
* **Frontend**: Dựng toàn bộ cấu trúc navigation và triển khai luồng Onboarding đa bước.
* Đảm bảo luồng từ đăng nhập → onboarding → ứng dụng chính hoạt động trước khi thêm tính năng sâu hơn.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --------- | ------------ | --------------- | -------------- |
| 2   | - Triển khai **GlobalExceptionHandler** (`@RestControllerAdvice`) <br>&emsp; + Xử lý `MethodArgumentNotValidException` → lỗi validation theo field <br>&emsp; + Xử lý `EntityNotFoundException`, các business exception tùy chỉnh <br>&emsp; + Tất cả lỗi trả về qua `ApiResponse` envelope | 25/08/2025 | 25/08/2025 | |
| 2   | - Cấu hình **CorsConfig** toàn cục <br>&emsp; + Cho phép origin local dev và production frontend <br>&emsp; + Allow headers: `Authorization`, `Content-Type` <br>&emsp; + Cho phép tất cả HTTP methods | 25/08/2025 | 25/08/2025 | |
| 3   | - Xây dựng module **GoalType** <br>&emsp; + Entity: `name (UNIQUE)`, `description` <br>&emsp; + Repository, Service, Controller <br>&emsp; + Endpoints (tất cả **public**): `POST /api/goal-types`, `GET /api/goal-types`, `GET /api/goal-types/{id}`, `GET /api/goal-types/by-name/{name}` | 26/08/2025 | 26/08/2025 | |
| 4   | - Xây dựng **RootNavigator** cho Frontend <br>&emsp; + Đọc Redux `isAuthenticated` + `hasCompletedOnboarding` từ `authSlice` <br>&emsp; + Điều hướng đến `AuthStack` / `OnboardingStack` / `MainTabs` <br> - Xây dựng **AuthStack**: `WelcomeScreen` + `LoginScreen` <br> - Xây dựng **MainTabs** với `CustomTabBar` <br>&emsp; + 4 tab: Trang chủ, Tập luyện, Dinh dưỡng, Sức khỏe <br>&emsp; + Nút Chat nổi trung tâm chia đôi tab trái/phải | 27/08/2025 | 27/08/2025 | <https://reactnavigation.org/> |
| 5   | - Xây dựng **OnboardingStack** (5 bước) <br>&emsp; + Bước 1: Giới tính + Ngày sinh + Chiều cao + Cân nặng <br>&emsp; + Bước 2: Mức hoạt động + Loại công việc <br>&emsp; + Bước 3: Mục tiêu tập luyện + Cân nặng mục tiêu + Vùng cơ thể cần cải thiện <br>&emsp; + Bước 4: Sở thích ăn uống + Dị ứng + Số bữa/ngày + Lượng nước <br>&emsp; + Bước 5: Kinh nghiệm + Địa điểm tập + Tần suất + Thời gian/buổi | 28/08/2025 | 28/08/2025 | |
| 6   | - Thêm **CaloriesScreen** và **TrainingScreen** vào onboarding preview <br> - Kết nối hoàn thành onboarding: `dispatch(completeOnboarding())` → sync user profile qua `POST /user/sync` | 29/08/2025 | 29/08/2025 | |

### Kết quả đạt được tuần 3:

* **Backend — Common Layer**:
  * `GlobalExceptionHandler` bắt tất cả exception; trả về `ApiResponse` nhất quán cho client.
  * CORS cấu hình toàn cục — frontend chạy trên `localhost:8081` giao tiếp API trên `localhost:8080`.
* **Backend — Module GoalType**:
  * Entity `GoalType` lưu thành công; hỗ trợ các loại: **Giảm mỡ**, **Tăng cơ**, **Duy trì cân nặng**.
  * Tất cả 4 public endpoint hoạt động: tạo, liệt kê, lấy theo ID, lấy theo tên.
  * GoalType là nền tảng để liên kết workout plans với mục tiêu thể dục.
* **Frontend — Navigation**:
  * `RootNavigator` điều hướng đúng theo trạng thái auth + onboarding.
  * `MainTabs` hiển thị `CustomTabBar` với nút Chat trung tâm nổi bật.
  * Tất cả stacks được đăng ký: `AuthStack`, `OnboardingStack`, `WorkoutStack`, `DietStack`, `HealthStack`.
* **Frontend — Onboarding**:
  * Wizard 5 bước hoàn chỉnh với hiệu ứng slide animation.
  * Dữ liệu user được thu thập đầy đủ (giới tính, ngày sinh, chiều cao, cân nặng, mục tiêu, sở thích)
  * Hoàn thành onboarding dispatch `completeOnboarding()` và gọi API sync.

### Kế hoạch tuần tiếp theo:

* **Backend**: Xây dựng module System Workout — `MuscleGroup`, `Exercise`, `WorkoutPlan`, `WorkoutPlanExercise` với admin CRUD và public read endpoints.
* **Frontend**: Triển khai `SuggestedPlanScreen` (wizard 3 bước chọn kế hoạch) và `PlanExercisePicker`.


### Mục tiêu tuần 3:

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


### Kết quả đạt được tuần 3:

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


