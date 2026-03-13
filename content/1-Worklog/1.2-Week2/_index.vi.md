---
title: "Worklog Tuần 2"
date: 2026-01-12
weight: 2
chapter: false
pre: " <b> 1.2. </b> "
---

### Mục tiêu tuần 2:

* **Backend**: Tích hợp AWS Cognito vào Spring Security. Xây dựng module `UserProfile`.
* **Frontend**: Triển khai luồng xác thực hoàn chỉnh — từ màn hình đăng nhập đến lưu trữ token và quản lý trạng thái.
* Thiết lập pattern xử lý token an toàn được tái sử dụng xuyên suốt ứng dụng.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --------- | ------------ | --------------- | -------------- |
| 2   | - Nghiên cứu khái niệm AWS Cognito User Pools <br>&emsp; + Cấu hình User Pool: password policy, app clients, PKCE <br>&emsp; + Phân biệt ID Token và Access Token <br>&emsp; + JWT claims: `sub`, `cognito:groups`, `token_use` | 13/01/2026 | 13/01/2026 | <https://docs.aws.amazon.com/cognito/> |
| 3   | - Triển khai **Spring Security** cấu hình JWT <br>&emsp; + Thêm `spring-security-oauth2-resource-server` <br>&emsp; + Cấu hình `SecurityConfig`: stateless, CSRF disabled, CORS enabled <br>&emsp; + Cài đặt Cognito issuer-uri trong `application.properties` <br>&emsp; + Viết `OAuth2TokenValidator` tự định nghĩa — từ chối token có `token_use != "access"` | 14/01/2026 | 14/01/2026 | <https://docs.spring.io/spring-security/> |
| 3   | - Triển khai trích xuất role từ JWT <br>&emsp; + Đọc claim `cognito:groups` → chuyển thành `ROLE_<GROUP>` <br>&emsp; + Cấu hình `@PreAuthorize("hasRole('ADMIN')")` cho admin endpoints <br>&emsp; + Quy tắc phân quyền: public, authenticated, admin-only | 14/01/2026 | 14/01/2026 | |
| 4   | - Xây dựng **UserProfile** entity & repository <br>&emsp; + Các trường: `cognitoId (UNIQUE)`, `email (UNIQUE)`, `username`, `name`, `gender`, `birthdate`, `phoneNumber`, `picture`, `emailVerified` <br>&emsp; + `UserProfileRepository` kế thừa `JpaRepository` | 15/01/2026 | 15/01/2026 | |
| 4   | - Xây dựng **UserProfileService** & **UserProfileController** <br>&emsp; + `POST /user/sync` — upsert profile từ Cognito claims (an toàn IDOR: `cognitoSub` từ JWT `sub`) <br>&emsp; + `GET /user/{id}`, `PUT /user/{id}`, `DELETE /user/{id}` | 15/01/2026 | 15/01/2026 | |
| 5   | - Xây dựng **LoginScreen** cho Frontend <br>&emsp; + Nút "Đăng nhập với AWS Cognito" duy nhất <br>&emsp; + Khởi động PKCE flow qua `expo-auth-session` + `expo-web-browser` <br>&emsp; + Xử lý redirect callback: đổi code → tokens <br>&emsp; + Giải mã ID Token bằng `jwt-decode` để lấy thông tin user | 16/01/2026 | 16/01/2026 | <https://docs.expo.dev/guides/authentication/> |
| 6   | - Xây dựng **authSlice** (Redux) và lưu trữ token <br>&emsp; + State: `isAuthenticated`, `user`, `token`, `refreshToken`, `hasCompletedOnboarding` <br>&emsp; + Actions: `login`, `logout`, `completeOnboarding`, `updateUserProfile` <br>&emsp; + Lưu token vào `expo-secure-store` (mobile) / `localStorage` (web) qua `utils/storage.ts` <br> - Kết nối Axios **request interceptor**: tự động gắn `Authorization: Bearer <token>` | 17/01/2026 | 17/01/2026 | |

### Kết quả đạt được tuần 2:

* **Backend — Security**:
  * Spring Security cấu hình hoàn chỉnh với AWS Cognito làm JWT issuer.
  * `OAuth2TokenValidator` tự định nghĩa chặn ID token — chỉ Access Token được chấp nhận tại API.
  * Phân quyền theo role hoạt động: `ROLE_ADMIN` từ Cognito group cấp quyền admin.
  * Các quy tắc bảo mật được định nghĩa: public health check, authenticated routes, admin-only `/admin/**`.
* **Backend — Module UserProfile**:
  * `POST /user/sync` upsert user từ Cognito JWT claims an toàn, không có lỗ hổng IDOR.
  * Full CRUD (`GET`, `PUT`, `DELETE`) trên `/user/{id}` với kiểm tra phân quyền.
  * Entity `UserProfile` lưu thành công vào PostgreSQL qua JPA.
* **Frontend — Xác thực**:
  * `LoginScreen` hiển thị đúng; nhấn nút mở Cognito Hosted UI trong trình duyệt.
  * PKCE code exchange hoạt động end-to-end — tokens được trả về và lưu an toàn.
  * `authSlice` chuyển được `isAuthenticated`; `RootNavigator` điều hướng đúng stack.
  * Axios interceptor tự gắn Bearer token cho mọi API call tiếp theo.

### Kiến thức AWS đã học và giả sử áp dụng cho project:

* Nắm kiến trúc AWS Cognito User Pool và luồng OAuth2/OIDC với PKCE cho mobile app.
* Hiểu sự khác nhau giữa ID Token và Access Token, và vì sao backend chỉ nên chấp nhận Access Token.
* Biết map claim cognito:groups sang role ứng dụng để thực thi RBAC an toàn.
* Hiểu cách thiết kế token validation theo issuer/audience/expiration để giảm rủi ro giả mạo token.
### Kế hoạch tuần tiếp theo:

* **Backend**: Xây dựng lớp cơ sở hạ tầng — `GlobalExceptionHandler`, `CorsConfig`. Triển khai module `GoalType`.
* **Frontend**: Xây dựng nền tảng navigation — `RootNavigator`, `AuthStack`, `MainTabs` với custom tab bar, `OnboardingStack`.


### Mục tiêu tuần 2:

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


### Kết quả đạt được tuần 2:

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


