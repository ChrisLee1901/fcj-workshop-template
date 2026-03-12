---
title: "Week 11 Worklog"
date: 2026-03-23
weight: 11
chapter: false
pre: " <b> 1.11. </b> "
---

### Week 11 Objectives:

* **Backend**: Final API review, Docker Compose production-readiness, and complete environment variable documentation.
* **Frontend**: Build `HomeScreen` as the central dashboard, resolve all outstanding bugs, and polish the overall UX across the app.
* Achieve a fully functional, integrated application ready for final testing.

### Tasks to be carried out this week:
| Day | Task | Start Date | Completion Date | Reference Material |
| --- | ---- | ---------- | --------------- | ------------------ |
| 2   | - Build **HomeScreen** (Frontend) — 5 parallel data fetches on mount <br>&emsp; + Today’s meals: sum MealFood calories → daily calorie progress bar vs. 2500 kcal target <br>&emsp; + Latest `HealthCalculation` → show BMI <br>&emsp; + Latest `BodyMetric` → show current height/weight <br>&emsp; + Active workout plan name → quick link to PlanDetail <br>&emsp; + This-week session count → weekly progress vs. 4 sessions target | 03/24/2026 | 03/24/2026 | |
| 3   | - Backend **Docker Compose** final refinements <br>&emsp; + Add `healthcheck` to `postgres` service: `pg_isready` with `interval`, `timeout`, `retries` <br>&emsp; + Add `depends_on.db.condition: service_healthy` to API service <br>&emsp; + Verify `Spring Actuator` `/actuator/health` liveness + readiness probes <br>&emsp; + Complete `.env.example` with all required variables documented | 03/25/2026 | 03/25/2026 | |
| 4   | - Comprehensive **bug fix** session across all Frontend screens <br>&emsp; + Fix `WorkoutSessionScreen`: edge case when all exercises completed before timer finishes <br>&emsp; + Fix `DietScreen`: ensure `ensureDailyMeals` not called on every render — move to `useEffect` with empty deps <br>&emsp; + Fix `HealthDashboardScreen`: loading state shown during `calculateMetrics` call <br>&emsp; + Fix `BMITrendChart`: empty state when user has fewer than 2 health calculations | 03/26/2026 | 03/26/2026 | |
| 5   | - **Response interceptor** improvements (Axios `client.ts`) <br>&emsp; + Implement token refresh with request queue: concurrent `401` responses queued, one refresh attempted, all retried <br>&emsp; + On refresh failure: `forceLogout` clears tokens + dispatches Redux `logout` + navigates to Login <br>&emsp; + Handle `code === 4040` "user not found for cognitoId" → auto `forceLogout` | 03/27/2026 | 03/27/2026 | |
| 6   | - **UX polish** pass across all screens <br>&emsp; + Add `NotificationBox` global alert component (replaces native `Alert.alert` via `installAlertProxy`) <br>&emsp; + Add pull-to-refresh on `HomeScreen` <br>&emsp; + Ensure consistent loading spinners and error states across all screens <br>&emsp; + Add `ActivityLevelLabels` Vietnamese display names for all enum values <br>&emsp; + Vietnamese label consistency check across navigation tabs and headings | 03/28/2026 | 03/28/2026 | |

### Week 11 Achievements:

* **Backend — Docker Compose**:
  * Health check on PostgreSQL service ensures the API container waits for DB to be fully ready.
  * `GET /actuator/health` returns `{status: UP}` with liveness/readiness sub-probes.
  * `.env.example` fully documents all 10+ required environment variables with descriptions.
* **Frontend — HomeScreen**:
  * 5 parallel `Promise.all` API calls complete in under 1.5s on localhost.
  * Daily calorie + weekly session progress indicators give users clear at-a-glance goals.
  * BMI and body metric snapshot visible on home without navigating away.
* **Frontend — Bug Fixes**:
  * Workout session completion edge case resolved — app no longer freezes on final set.
  * `ensureDailyMeals` called only once on first mount — eliminated 4 redundant API calls per render.
  * Token refresh queue prevents logged-out flash when multiple concurrent requests get 401.
* **Frontend — UX Polish**:
  * `NotificationBox` replaces native alerts — consistent in-app notification style.
  * All loading states and error messages standardized across the application.
  * Vietnamese labels complete and consistent throughout the UI.

### Next Week Plan:

* Run full end-to-end integration test of the complete application (all features, all screens).
* Write project documentation (README, API reference, architecture diagram).
* Prepare final demo and code cleanup for project handoff.


### Week 11 Objectives:

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


### Week 11 Achievements:

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
