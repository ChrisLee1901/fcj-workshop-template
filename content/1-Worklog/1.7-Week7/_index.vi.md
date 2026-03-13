---
title: "Worklog Tuần 7"
date: 2026-02-23
weight: 7
chapter: false
pre: " <b> 1.7. </b> "
---

### Mục tiêu tuần 7:

* **Backend**: Xây dựng module Media — entity `Image` với polymorphic association, tích hợp AWS S3.
* **Frontend**: Xây dựng `SessionDetailScreen`, `SessionCalendarScreen`, và `mediaService` với image caching.
* Hiển thị hình ảnh cho bài tập và kế hoạch tập luyện trong toàn ứng dụng.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --------- | ------------ | --------------- | -------------- |
| 2   | - Xây dựng entity **Image** (`module/media`) <br>&emsp; + `url (≤500)`, `isThumbnail`, `food (nullable)`, `workoutPlan (nullable)`, `exercise (nullable)` <br>&emsp; + Constraint `chk_image_exclusive`: chính xác 1 trong 3 FK có giá trị (polymorphic association) <br>&emsp; + Flyway **V3**: tạo bảng `image` với constraint | 24/02/2026 | 24/02/2026 | |
| 3   | - Xây dựng **ImageController** (`/api/images`) <br>&emsp; + `POST /` (register URL), `GET /{id}` <br>&emsp; + `GET /food/{foodId}`, `GET /workout-plan/{id}`, `GET /exercise/{id}` <br>&emsp; + `PUT /{id}`, `DELETE /{id}` <br> - Cấu hình **AWS S3** (`AwsS3Config.java`): `AmazonS3` bean, region `ap-southeast-1`, bucket từ env | 25/02/2026 | 25/02/2026 | <https://docs.aws.amazon.com/sdk-for-java/> |
| 4   | - Xây dựng **mediaService** (Frontend) <br>&emsp; + `getImageUrl(owner, id)` — gọi `GET /api/images/{owner}/{id}` <br>&emsp; + Cache URL trong bộ nhớ + deduplication in-flight <br>&emsp; + Bulk helpers: `getFoodImageUrlMap`, `getWorkoutPlanImageUrlMap`, `getExerciseImageUrlMap` | 26/02/2026 | 26/02/2026 | |
| 5   | - Xây dựng **SessionDetailScreen** (Frontend) <br>&emsp; + Tóm tắt buổi tập: nhóm bài tập theo `exerciseId` <br>&emsp; + Hiển thị set × rep × cân nặng cho từng bài <br>&emsp; + Format ngày giờ qua `utils/date.ts` | 27/02/2026 | 27/02/2026 | |
| 6   | - Xây dựng **SessionCalendarScreen** (Frontend) <br>&emsp; + Lịch tháng với chấm trên ngày có buổi tập <br>&emsp; + Di chuyển tháng (mũi tên trái/phải) <br>&emsp; + Nhấn ngày để hiển thị log buổi tập bên dưới <br>&emsp; + Nhãn tiếng Việt (Thứ 2–CN, Tháng 1–12) | 28/02/2026 | 28/02/2026 | |

### Kết quả đạt được tuần 7:

* **Backend — Module Media**:
  * Flyway V3 được apply với exclusive FK constraint — toàn vẹn dữ liệu polymorphic ở cấp DB.
  * `ImageController` đăng ký URL hình ảnh và trả về đúng theo entity sở hữu.
  * AWS S3 bean cấu hình local qua biến môi trường.
* **Frontend — Lịch sử buổi tập**:
  * `SessionDetailScreen` nhóm log bài tập đúng và hiển thị rõ ràng.
  * `SessionCalendarScreen` đánh dấu ngày tập; nhấn ngày hiển log chi tiết.
* **Frontend — Media Service**:
  * URL hình ảnh được cache trong bộ nhớ — không gọi API trung lặp.
  * Tile kế hoạch và danh sách bài tập hiển thị hình ảnh từ S3.

### Kiến thức AWS đã học và giả sử áp dụng cho project:

* Hiểu cơ chế presigned URL trong S3 để upload/download an toàn mà không lộ AWS credentials.
* Biết áp dụng nguyên tắc thời hạn URL ngắn để giảm rủi ro truy cập trái phép.
* Nắm lifecycle policy (transition/expiration) để tối ưu chi phí ảnh cũ hoặc dữ liệu ít truy cập.
* Hiểu kiến trúc media service tách biệt giúp scale độc lập với business API.
### Kế hoạch tuần tiếp theo:

* **Backend**: Xây dựng module Food & Nutrition — `Food`, `Meal`, `MealFood`, `DailyNutrition` với CRUD đầy đủ và tính toán dinh dưỡng.
* **Frontend**: Xây dựng `DietScreen` với quản lý bữa ăn, tìm kiếm thực phẩm, thêm thực phẩm vào bữa.


### Mục tiêu tuần 7:

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


### Kết quả đạt được tuần 7:

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


