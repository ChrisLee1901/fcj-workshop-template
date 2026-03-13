---
title: "Worklog Tuần 12"
date: 2026-03-30
weight: 12
chapter: false
pre: " <b> 1.12 </b> "
---

### Mục tiêu tuần 12:

* Thực hiện kiểm thử tích hợp end-to-end toàn bộ ứng dụng myFit (tất cả tính năng, tất cả màn hình).
* Viết tài liệu dự án đầy đủ — README, API reference, tổng quan kiến trúc.
* Dọn dẹp code, xóa debug artifacts, chuẩn bị bàn giao dự án.
* Nhìn lại 12 tuần thực tập: bài học kinh nghiệm, điểm mạnh và hướng cải thiện tương lai.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --------- | ------------ | --------------- | -------------- |
| 2   | - **Kiểm thử tích hợp** — Backend <br>&emsp; + Kiểm tra tất cả API endpoint với input hợp lệ + không hợp lệ <br>&emsp; + Xác nhận Flyway V1/V2/V3 migration chạy trên DB mới <br>&emsp; + Docker Compose cold start: `db` + `api` healthy dưới 30 giây <br>&emsp; + Rà soát `application.properties` — không có giá trị dev nào lọt sang production | 31/03/2026 | 31/03/2026 | |
| 3   | - **Kiểm thử tích hợp** — Frontend (6 hành trình người dùng) <br>&emsp; + Hành trình 1: Đăng ký → Onboarding → Trang chủ <br>&emsp; + Hành trình 2: Tạo kế hoạch → Clone kế hoạch system → Kích hoạt <br>&emsp; + Hành trình 3: Bắt đầu buổi tập → Log set → Timer nghỉ → Kết thúc → Màn hình Thành công <br>&emsp; + Hành trình 4: Thêm thực phẩm vào 4 bữa → Kiểm tra tổng calo <br>&emsp; + Hành trình 5: Nhập chỉ số cơ thể → BMI/BMR/TDEE tính đúng → Chart hiển thị <br>&emsp; + Hành trình 6: Chat AI → Bedrock phản hồi tiếng Việt | 01/04/2026 | 01/04/2026 | |
| 4   | - Viết **Backend README** (`myFit-api/README.md`) <br>&emsp; + Tổng quan dự án & sơ đồ kiến trúc (API ↔ PostgreSQL ↔ Cognito ↔ S3) <br>&emsp; + Tài liệu từng module: Auth, Food, SystemWorkout, UserWorkoutPlan, Session, UserMetric, Media, GoalType <br>&emsp; + Hướng dẫn cài đặt: prerequisites, biến `.env`, lệnh Docker Compose <br>&emsp; + Bảng API endpoint reference | 02/04/2026 | 02/04/2026 | |
| 4   | - Cập nhật **Frontend** `guide.md` <br>&emsp; + Bảng tech stack <br>&emsp; + Sơ đồ cấu trúc navigation <br>&emsp; + Hướng dẫn cài đặt: `npm install`, biến `.env`, `npx expo start` <br>&emsp; + Danh sách màn hình với mô tả tính năng <br>&emsp; + Ghi chú cấu hình AWS Cognito + Bedrock | 02/04/2026 | 02/04/2026 | |
| 5   | - **Dọn dẹp code** — Backend <br>&emsp; + Xóa `TODO`, `FIXME`, `System.out.println` debug <br>&emsp; + Thêm Javadoc cho method public không hiển nhiên <br>&emsp; + Rà soát security config không để lộ route không mong muốn <br>&emsp; + Build cuối: `mvn clean package -DskipTests` → JAR build thành công | 03/04/2026 | 03/04/2026 | |
| 6   | - **Dọn dẹp code** — Frontend <br>&emsp; + Xóa tất cả `console.log` <br>&emsp; + Chạy `eslint` và sửa cảnh báo lint còn lại <br>&emsp; + Xóa import không dùng <br>&emsp; + Build cuối: `npx expo export` → zero TypeScript error <br> - **Tổng kết dự án**: tài liệu bài học kinh nghiệm, quyết định kỹ thuật và hướng cải thiện tương lai | 04/04/2026 | 04/04/2026 | |

### Kết quả đạt được tuần 12:

* **Kiểm thử tích hợp**:
  * Tất cả API endpoint backend vượt qua test thủ công với input hợp lệ và không hợp lệ.
  * Docker Compose cold start đáng tin cậy — API healthy trong 25 giây sau `docker-compose up`.
  * Flyway V1, V2, V3 migration chạy sạch trên PostgreSQL mới.
  * Tất cả 6 hành trình người dùng test end-to-end không có lỗi nghiêm trọng.
* **Tài liệu**:
  * `myFit-api/README.md` bao gồm hướng dẫn cài đặt đầy đủ, bảng biến môi trường, và mô tả endpoint.
  * Frontend `guide.md` cập nhật sơ đồ navigation, danh sách màn hình, và cấu hình AWS.
  * Tổng quan kiến trúc: Spring Boot API ↔ PostgreSQL ↔ AWS Cognito ↔ AWS S3 ↔ React Native ↔ AWS Bedrock.
* **Chất lượng Code**:
  * Zero `console.log` hay `System.out.println` còn lại trong production code.
  * TypeScript build (`npx expo export`) không có lỗi.
  * Maven `mvn clean package` build JAR thành công.
* **Tổng kết dự án — Bài học kinh nghiệm**:
  * **Ngăn chặn IDOR** qua trích xuất `sub` từ JWT là pattern bảo mật quan trọng phải áp dụng nhất quán trong REST API phân quyền theo user.
  * **Soft delete** với `@SQLRestriction` linh hoạt hơn hard delete cho dữ liệu thuộc sở hữu người dùng — cho phép khôi phục tiềm năng.
  * **JWT Stateless** loại bỏ phức tạp quản lý session phía server, đánh đổi bằng độ phức tạp của token revocation (giải quyết bằng forced logout + refresh queue).
  * **React Native + NativeWind** là bộ đôi mạnh mẽ — cú pháp TailwindCSS quen thuộc tăng tốc đáng kể phát triển UI mobile.
  * **Redux + React Query** phân tách rõ ràng: Redux quản lý auth/session state; React Query quản lý server cache và background refetch.
  * **Hướng cải thiện tương lai**: Deploy Backend lên AWS ECS (Fargate) + ALB HTTPS; Frontend bundle lên CloudFront + S3; CI/CD qua GitHub Actions (đã scaffolded trong `.github/workflows/`).

### Kiến thức AWS đã học và giả sử áp dụng cho project:

* Nắm 5 trụ cột AWS Well-Architected và cách đối chiếu kiến trúc hiện tại của dự án.
* Hiểu phương pháp tối ưu chi phí: right-sizing, lifecycle policy, budget alert, tắt tài nguyên không dùng.
* Biết xây dựng kế hoạch backup/DR cơ bản (RPO/RTO) cho dữ liệu quan trọng.
* Hiểu quy trình handover vận hành cloud: tài liệu runbook, checklist release, và incident playbook.

### Mục tiêu tuần 12:

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


### Kết quả đạt được tuần 12:

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


