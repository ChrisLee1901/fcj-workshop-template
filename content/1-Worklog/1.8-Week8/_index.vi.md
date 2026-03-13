---
title: "Worklog Tuần 8"
date: 2026-03-02
weight: 8
chapter: false
pre: " <b> 1.8. </b> "
---

### Mục tiêu tuần 8:

* **Backend**: Xây dựng module Food & Nutrition — `Food`, `Meal`, `MealFood`, `DailyNutrition` với tính toán macro tự động.
* **Frontend**: Xây dựng `DietScreen` với layout 4 bữa, tìm kiếm thực phẩm, modal thêm food; `DietHistoryScreen`.
* Cho phép user theo dõi lượng calo và macro hàng ngày.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --------- | ------------ | --------------- | -------------- |
| 2   | - Xây dựng entity **Food** (bảng `food`) <br>&emsp; + `name`, `caloriesPer100g`, `proteinPer100g`, `carbsPer100g`, `fatsPer100g`, `unit` <br>&emsp; + `FoodController`: CRUD + phân trang + tìm kiếm theo từ khóa | 03/03/2026 | 03/03/2026 | |
| 3   | - Xây dựng entity **Meal** (bảng `meal`) <br>&emsp; + `userProfile (@ManyToOne)`, `date (LocalDateTime)`, `mealType (BREAKFAST/LUNCH/SNACK/DINNER)`, `note` <br>&emsp; + `MealController`: tạo, lấy theo ID, lọc theo ngày, lọc theo loại bữa | 04/03/2026 | 04/03/2026 | |
| 4   | - Xây dựng entity **MealFood** (bảng `meal_food`) <br>&emsp; + `meal`, `food`, `quantity (gram)` <br>&emsp; + `calories`, `protein`, `carbs`, `fats` tự tính khi tạo: `quantity / 100 * per100gValue` <br>&emsp; + `MealFoodController`: thêm food vào bữa, liệt kê, xóa <br> - Xây dựng entity **DailyNutrition** + `DailyNutritionController`: tính tổng và lưu dinh dưỡng ngày | 05/03/2026 | 05/03/2026 | |
| 5   | - Xây dựng **DietScreen** (Frontend) <br>&emsp; + Hiển thị 4 bữa hôm nay qua `ensureDailyMeals` <br>&emsp; + Mỗi bữa: danh sách food, cột calo, progress bar <br>&emsp; + Modal "Thêm thực phẩm": tìm kiếm, nhập gram, submit → `addFoodToMeal` <br>&emsp; + Progress bar tổng calo ngày <br>&emsp; + Pull-to-refresh | 06/03/2026 | 06/03/2026 | |
| 6   | - Xây dựng **DietHistoryScreen** (Frontend) <br>&emsp; + Lịch tháng — nhấn ngày xem bữa ăn của ngày đó <br>&emsp; + Bày thực phẩm + tổng calo theo từng bữa <br> - Test toàn bộ luồng theo dõi dinh dưỡng | 07/03/2026 | 07/03/2026 | |

### Kết quả đạt được tuần 8:

* **Backend — Module Food & Nutrition**:
  * Entity `Food` được seed dữ liệu thực phẩm từ crawler (hơn 100 món ăn).
  * `MealFood` tự động tính macro khi insert.
  * Phân trang `GET /api/foods` hoạt động với `PageResponse<T>`.
  * Tìm kiếm case-insensitive LIKE query hoạt động.
* **Frontend — Theo dõi dinh dưỡng**:
  * `DietScreen` tạo đủ 4 bữa cho ngày hiện tại.
  * Modal search thực phẩm với kết quả phân trang.
  * Thêm food: backend tính macro → UI refresh số liệu.
  * `DietHistoryScreen` hiển thị lịch sử dinh dưỡng theo ngày chọn.

### Kiến thức AWS đã học và giả sử áp dụng cho project:

* Nắm quy trình tích hợp Amazon Bedrock Runtime và lựa chọn model theo tiêu chí latency/chi phí/chất lượng.
* Hiểu kỹ thuật prompt engineering để định nghĩa persona fitness coach ổn định cho output.
* Biết thiết kế guardrails ở tầng ứng dụng: giới hạn ngữ cảnh, kiểm soát input/output và fallback khi lỗi.
* Hiểu cách quản lý quota và retry/backoff khi gọi dịch vụ AI trên cloud.
### Kế hoạch tuần tiếp theo:

* **Backend**: Xây dựng module User Metric — `BodyMetric` và `HealthCalculation` với logic tính BMI/BMR/TDEE.
* **Frontend**: Xây dựng `HealthDashboardScreen`, `BodyMetricListScreen`, `BodyMetricFormScreen`, và các chart sức khỏe.


### Mục tiêu tuần 8:

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


### Kết quả đạt được tuần 8:

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


