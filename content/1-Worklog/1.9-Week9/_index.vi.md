---
title: "Worklog Tuần 9"
date: 2026-03-09
weight: 9
chapter: false
pre: " <b> 1.9. </b> "
---

### Mục tiêu tuần 9:

* **Backend**: Xây dựng module User Metric — `BodyMetric` và `HealthCalculation` với BMI/BMR/TDEE.
* **Frontend**: Xây dựng `HealthDashboardScreen`, `BodyMetricListScreen`, `BodyMetricFormScreen`, và các chart component sức khỏe.
* Cung cấp cho user thông tin rõ ràng về sức khỏe và mục tiêu calo.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --------- | ------------ | --------------- | -------------- |
| 2   | - Xây dựng entity **BodyMetric** (bảng `body_metric`) <br>&emsp; + `user`, `heightCm (min=50)`, `weightKg (min=20)`, `age (min=10)`, `gender (enum)`, `activityLevel (enum)` <br>&emsp; + `BodyMetricController`: tạo, lấy theo user, lấy mới nhất, get/update/delete | 10/03/2026 | 10/03/2026 | |
| 3   | - Xây dựng entity **HealthCalculation** + lôgic tính toán <br>&emsp; + BMI = w / (h/100)² <br>&emsp; + BMR (Mifflin-St Jeor): Nam = 10×w + 6.25×h - 5×age + 5; Nữ = Nam - 161 <br>&emsp; + TDEE = BMR × hệ số hoạt động (1.2 – 1.9) <br> - `HealthMetricsController` (`/api/metrics`): tính toán & lưu, lấy lịch sử, lấy mới nhất | 11/03/2026 | 11/03/2026 | |
| 4   | - Xây dựng **HealthDashboardScreen** (Frontend) <br>&emsp; + `WheelPicker` nhập chiều cao (cm) và cân nặng (kg) <br>&emsp; + Dropdown ActivityLevel và GoalType <br>&emsp; + Submit: `createBodyMetric` + `calculateMetrics` → hiển `HealthResultCard` <br>&emsp; + Redirect Profile nếu thiếu giới tính/ngày sinh | 12/03/2026 | 12/03/2026 | |
| 5   | - Xây dựng các **health chart components** (`src/components/health/`) <br>&emsp; + `BMITrendChart`: biểu đồ BMI theo thời gian, lọc 7d/30d/90d/all + màu theo vùng BMI <br>&emsp; + `WeightChart`: cân nặng + moving average tùy chọn + khoảng cách đến cân nặng mục tiêu <br>&emsp; + `CalorieEnergyCharts`: BMR + TDEE dual-line <br>&emsp; + `MacrosDisplay`: 3 progress bar protein/carbs/fat | 13/03/2026 | 13/03/2026 | |
| 6   | - Xây dựng **BodyMetricListScreen** và **BodyMetricFormScreen** (Frontend) <br>&emsp; + List: hiển thị lịch sử chỉ số, `WeightChart` ở trên cùng, sửa/xóa <br>&emsp; + Form: tạo hoặc chỉnh sửa body metric, lấy gender + age từ `authSlice` | 14/03/2026 | 14/03/2026 | |

### Kết quả đạt được tuần 9:

* **Backend — Module User Metric**:
  * `BodyMetric` lưu thành công với validation đầy đủ.
  * BMR tính đúng theo Mifflin-St Jeor; TDEE áp dụng đúng hệ số hoạt động.
  * `POST /api/metrics/calculate` trả về BMI, BMR, TDEE và macro gợi ý theo goal.
* **Frontend — Sức khỏe**:
  * `HealthDashboardScreen` wheel picker UX mượt mà; kết quả hiển ngay sau API.
  * `BMITrendChart` màu sắc phân vùng BMI rõ ràng.
  * `WeightChart` hiển moving average khi có ≥7 điểm dữ liệu.
  * `BodyMetricListScreen` lưu lịch sử đo lường đầy đủ.

### Kế hoạch tuần tiếp theo:

* **Backend**: Hoàn thiện pagination, cải thiện validation endpoint, viết unit test.
* **Frontend**: Xây dựng `ChatScreen` với AWS Bedrock AI và `ProfileScreen` quản lý hồ sơ.


### Mục tiêu tuần 9:

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


### Kết quả đạt được tuần 9:

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


