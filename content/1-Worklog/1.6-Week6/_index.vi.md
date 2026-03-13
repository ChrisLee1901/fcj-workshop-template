---
title: "Worklog Tuần 6"
date: 2026-02-09
weight: 6
chapter: false
pre: " <b> 1.6. </b> "
---

### Mục tiêu tuần 6:

* **Backend**: Xây dựng module `UserWorkoutSession` và `WorkoutLog` để ghi lại hoạt động tập luyện thực tế.
* **Frontend**: Xây dựng `PlanDetailScreen` và `WorkoutSessionScreen` — trải nghiệm tập luyện trực tiếp.
* Hoàn thiện vòng lặp chính: kế hoạch → buổi tập → log set → kết thúc.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --------- | ------------ | --------------- | -------------- |
| 2   | - Xây dựng **UserWorkoutSession** entity <br>&emsp; + `user`, `userWorkoutPlan (@ManyToOne)`, `workoutDate (LocalDate)`, `isActive`, `weekIndex`, `dayIndex` <br>&emsp; + Cascade to `WorkoutLog` qua `@OneToMany(cascade = ALL)` | 10/02/2026 | 10/02/2026 | |
| 3   | - Xây dựng **WorkoutLog** entity <br>&emsp; + `userWorkoutSession`, `exercise`, `setNumber`, `reps`, `weight (Float)`, `durationSeconds` <br> - Xây dựng **UserWorkoutSessionController** (`/api/sessions`) <br>&emsp; + Create, Get by ID/user/date, Get active, Deactivate, Add log | 11/02/2026 | 11/02/2026 | |
| 4   | - Xây dựng **PlanDetailScreen** (Frontend) <br>&emsp; + Hiển thị kế hoạch active, bộ chọn ngày Thứ 2–CN <br>&emsp; + Nút "Bắt đầu tập": tạo session → chuyển đến `WorkoutSessionScreen` <br>&emsp; + Banner session đang tiến hành nếu có <br>&emsp; + Link đến `SessionCalendar` để xem lịch sử | 12/02/2026 | 12/02/2026 | |
| 5   | - Xây dựng **workoutSessionSlice** (Redux) <br>&emsp; + State: `sessionId`, `exercises[]`, `currentExIndex`, `currentSet`, `completedSets[]`, `phase`, `restSeconds` <br>&emsp; + Actions: `initializeSession`, `logSetStart/Success/Failure`, `finishRest`, `skipExercise`, `resetSession` <br>&emsp; + Lưu session vào `AsyncStorage` — khôi phục khi app reload | 13/02/2026 | 13/02/2026 | |
| 6   | - Xây dựng **WorkoutSessionScreen** (Frontend) <br>&emsp; + `ActiveExerciseCard`: hiển thị tên bài tập, tiến độ set, mục tiêu rep <br>&emsp; + `LogSetSheet`: nhập rep + cân nặng → gọi `addWorkoutLog` API <br>&emsp; + `RestTimer`: đếm ngược, tự chuyển bài tập sau khi nghỉ <br> - Xây dựng **WorkoutSuccessScreen** <br>&emsp; + Trophy screen với tóm tắt buổi tập <br>&emsp; + Chặn nút back phần cứng | 14/02/2026 | 14/02/2026 | |

### Kết quả đạt được tuần 6:

* **Backend — Module Session**:
  * Entity `UserWorkoutSession` + `WorkoutLog` lưu thành công với cascade DELETE.
  * API tạo session, deactivate và log set hoạt động đúng.
  * Query theo ngày và lấy active session hoạt động chính xác.
* **Frontend — Tập Thực Tế**:
  * `PlanDetailScreen` load kế hoạch active; bộ chọn ngày lọc bài tập theo `dayOfWeek`.
  * Redux `workoutSessionSlice` quản lý toàn bộ trạng thái buổi tập, lưu AsyncStorage.
  * `WorkoutSessionScreen` hướng dẫn user qua tất cả bài tập/set với timer nghỉ.
  * Vòng lặp tập luyện hoàn chỉnh được test end-to-end.

### Kiến thức AWS đã học và giả sử áp dụng cho project:

* Nắm cách tổ chức logging theo structured format để dễ truy vấn trong CloudWatch Logs.
* Hiểu các metric ứng dụng quan trọng (request latency, error rate, active sessions) để tạo alarm.
* Biết cách thiết kế dashboard giám sát cho luồng workout realtime để phát hiện sự cố sớm.
* Hiểu quy trình cảnh báo theo ngưỡng và phản ứng sự cố cơ bản (triage, rollback, verify).
### Kế hoạch tuần tiếp theo:

* **Backend**: Xây dựng module Media — entity `Image`, tích hợp AWS S3, `ImageController` liên kết hình ảnh với bài tập/thực phẩm/kế hoạch.
* **Frontend**: Xây dựng `SessionDetailScreen` và `SessionCalendarScreen` (lịch tháng có chấm buổi tập).


### Mục tiêu tuần 6:

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


### Kết quả đạt được tuần 6:
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


