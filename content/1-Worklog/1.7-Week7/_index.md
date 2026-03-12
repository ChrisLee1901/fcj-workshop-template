---
title: "Week 7 Worklog"
date: 2026-02-23
weight: 7
chapter: false
pre: " <b> 1.7. </b> "
---

### Week 7 Objectives:

* **Backend**: Build the Media module — `Image` entity with polymorphic association (food / exercise / workout plan), AWS S3 integration.
* **Frontend**: Build `SessionDetailScreen` (past workout recap) and `SessionCalendarScreen` (monthly calendar view), plus the `mediaService` with image caching.
* Enable images to be displayed for exercises and workout plans throughout the app.

### Tasks to be carried out this week:
| Day | Task | Start Date | Completion Date | Reference Material |
| --- | ---- | ---------- | --------------- | ------------------ |
| 2   | - Build **Image** entity (`module/media`) <br>&emsp; + Fields: `url (≤500)`, `isThumbnail`, `food (@ManyToOne nullable)`, `workoutPlan (@ManyToOne nullable)`, `exercise (@ManyToOne nullable)` <br>&emsp; + DB check constraint `chk_image_exclusive`: exactly ONE of `food_id`, `workout_plan_id`, `exercise_id` is non-null (exclusive polymorphic FK) <br>&emsp; + Write Flyway **V3** migration: `image` table with exclusive FK constraint | 09/22/2025 | 09/22/2025 | |
| 3   | - Build **ImageController** (`/api/images`) <br>&emsp; + `POST /` — register image record (URL stored; file lives in S3) <br>&emsp; + `GET /{id}`, `GET /food/{foodId}`, `GET /workout-plan/{workoutPlanId}`, `GET /exercise/{exerciseId}` <br>&emsp; + `PUT /{id}`, `DELETE /{id}` | 09/23/2025 | 09/23/2025 | |
| 3   | - Configure **AWS S3** integration (`config/AwsS3Config.java`) <br>&emsp; + AWS SDK v1: `AmazonS3` bean configured with region `ap-southeast-1` <br>&emsp; + Bucket name from env `S3_BUCKET_NAME` (default `crawl.fitness`) <br>&emsp; + Upload utility method for media files | 09/23/2025 | 09/23/2025 | <https://docs.aws.amazon.com/sdk-for-java/> |
| 4   | - Build **mediaService** (Frontend) <br>&emsp; + `getImageUrl(owner, id)` — fetch image URL from `GET /api/images/{owner}/{id}` <br>&emsp; + In-memory URL cache + in-flight deduplication (prevents duplicate API calls for the same image) <br>&emsp; + Bulk helpers: `getFoodImageUrlMap(ids[])`, `getWorkoutPlanImageUrlMap(ids[])`, `getExerciseImageUrlMap(ids[])` | 09/24/2025 | 09/24/2025 | |
| 5   | - Build **SessionDetailScreen** (Frontend) <br>&emsp; + Past workout recap: exercises grouped by `exerciseId` <br>&emsp; + Shows sets × reps × weight per exercise <br>&emsp; + Formatted date/time display with `utils/date.ts` | 09/25/2025 | 09/25/2025 | |
| 6   | - Build **SessionCalendarScreen** (Frontend) <br>&emsp; + Monthly calendar view with dot indicators on days that have sessions <br>&emsp; + Month navigation (prev/next chevrons) <br>&emsp; + Click a date to show session logs below the calendar <br>&emsp; + Vietnamese day/month labels (Thứ 2–CN, Tháng 1–12) | 09/26/2025 | 09/26/2025 | |

### Week 7 Achievements:

* **Backend — Media module**:
  * Flyway V3 migration applied with exclusive FK constraint on `image` table — DB-level data integrity for polymorphic images.
  * `POST /api/images` registers image URL records linked to food/exercise/plan.
  * `GET /api/images/exercise/{id}` and similar endpoints return all images for a given entity.
  * AWS S3 `AmazonS3` bean configured locally (uses environment variables; real uploads tested with `generate_s3_json.py` tooling).
* **Frontend — Session History**:
  * `SessionDetailScreen` correctly groups workout logs by exercise and renders sets/reps/weight clearly.
  * `SessionCalendarScreen` marks training days with dots; tap to reveal session details inline.
  * Month navigation works; Vietnamese labels render correctly.
* **Frontend — Media Service**:
  * `mediaService` caches fetched image URLs in memory — no duplicate API calls for images already loaded.
  * In-flight deduplication ensures concurrent requests for the same image share a single promise.
  * Workout plan tiles and exercise list items now display associated images from S3.

### Next Week Plan:

* **Backend**: Build the Food & Nutrition module — `Food`, `Meal`, `MealFood`, `DailyNutrition` entities with full CRUD and nutrition calculation.
* **Frontend**: Build `DietScreen` with meal management, food search, and add-food-to-meal flow.


### Week 7 Objectives:

* Connect and get acquainted with members of First Cloud Journey.
* Understand basic AWS services, how to use the console & CLI.

### Tasks to be carried out this week:
| Day | Task                                                                                                                                                                                                   | Start Date | Completion Date | Reference Material                        |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------- | --------------- | ----------------------------------------- |
| 2   | - Get acquainted with FCJ members <br> - Read and take note of internship unit rules and regulations                                                                                                   | 08/11/2025 | 08/11/2025      |
| 3   | - Learn about AWS and its types of services <br>&emsp; + Compute <br>&emsp; + Storage <br>&emsp; + Networking <br>&emsp; + Database <br>&emsp; + ... <br>                                              | 08/12/2025 | 08/12/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 4   | - Create AWS Free Tier account <br> - Learn about AWS Console & AWS CLI <br> - **Practice:** <br>&emsp; + Create AWS account <br>&emsp; + Install & configure AWS CLI <br> &emsp; + How to use AWS CLI | 08/13/2025 | 08/13/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 5   | - Learn basic EC2: <br>&emsp; + Instance types <br>&emsp; + AMI <br>&emsp; + EBS <br>&emsp; + ... <br> - SSH connection methods to EC2 <br> - Learn about Elastic IP   <br>                            | 08/14/2025 | 08/15/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 6   | - **Practice:** <br>&emsp; + Launch an EC2 instance <br>&emsp; + Connect via SSH <br>&emsp; + Attach an EBS volume                                                                                     | 08/15/2025 | 08/15/2025      | <https://cloudjourney.awsstudygroup.com/> |


### Week 7 Achievements:

* Understood what AWS is and mastered the basic service groups: 
  * Compute
  * Storage
  * Networking 
  * Database
  * ...

* Successfully created and configured an AWS Free Tier account.

* Became familiar with the AWS Management Console and learned how to find, access, and use services via the web interface.

* Installed and configured AWS CLI on the computer, including:
  * Access Key
  * Secret Key
  * Default Region
  * ...

* Used AWS CLI to perform basic operations such as:

  * Check account & configuration information
  * Retrieve the list of regions
  * View EC2 service
  * Create and manage key pairs
  * Check information about running services
  * ...

* Acquired the ability to connect between the web interface and CLI to manage AWS resources in parallel.
* ...
