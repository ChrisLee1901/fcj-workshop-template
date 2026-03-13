---
title: "Week 6 Worklog"
date: 2026-02-09
weight: 6
chapter: false
pre: " <b> 1.6. </b> "
---

### Week 6 Objectives:

* **Backend**: Build the `UserWorkoutSession` and `WorkoutLog` modules to record actual workout activity in real time.
* **Frontend**: Build `PlanDetailScreen` (active plan with day selector and session start) and `WorkoutSessionScreen` (fully interactive live workout experience).
* Complete the core workout tracking loop: plan → session → log sets → finish.

### Tasks to be carried out this week:
| Day | Task | Start Date | Completion Date | Reference Material |
| --- | ---- | ---------- | --------------- | ------------------ |
| 2   | - Build **UserWorkoutSession** entity <br>&emsp; + Fields: `user (@ManyToOne)`, `userWorkoutPlan (@ManyToOne)`, `workoutDate (LocalDate)`, `isActive (default true)`, `weekIndex`, `dayIndex` <br>&emsp; + Cascade to `WorkoutLog` via `@OneToMany(cascade = ALL)` | 02/10/2026 | 02/10/2026 | |
| 3   | - Build **WorkoutLog** entity <br>&emsp; + Fields: `userWorkoutSession (@ManyToOne)`, `exercise (@ManyToOne)`, `setNumber`, `reps`, `weight (Float)`, `durationSeconds` | 02/11/2026 | 02/11/2026 | |
| 3   | - Build **UserWorkoutSessionController** (`/api/sessions`) <br>&emsp; + `POST /` — create session <br>&emsp; + `GET /{id}`, `GET /user/{userId}`, `GET /user/{userId}/by-date?date=` <br>&emsp; + `GET /user/{userId}/active` — fetch currently active session <br>&emsp; + `PATCH /{sessionId}/deactivate` — mark session completed <br>&emsp; + `POST /{sessionId}/logs` — log an exercise set | 02/11/2026 | 02/11/2026 | |
| 4   | - Build **PlanDetailScreen** (Frontend) <br>&emsp; + Display active plan name and description <br>&emsp; + Day-of-week selector (Mon–Sun) — shows exercises for selected day <br>&emsp; + "Start Workout" button: create session via `POST /api/sessions`, navigate to `WorkoutSessionScreen` <br>&emsp; + Show active session banner if session already in progress <br>&emsp; + Navigate to `SessionCalendar` for history | 02/12/2026 | 02/12/2026 | |
| 5   | - Build **workoutSessionSlice** (Redux) <br>&emsp; + State: `sessionId`, `planId`, `exercises[]`, `currentExIndex`, `currentSet`, `completedSets[]`, `phase (workout/rest/done)`, `restSeconds`, `isSavingLog` <br>&emsp; + Actions: `initializeSession`, `restoreSessionState`, `logSetStart/Success/Failure`, `finishRest`, `skipExercise`, `skipSet`, `resetSession` <br>&emsp; + Persist session to `AsyncStorage` on every set — restore on app reload | 02/13/2026 | 02/13/2026 | |
| 6   | - Build **WorkoutSessionScreen** (Frontend) <br>&emsp; + `ActiveExerciseCard`: shows exercise name, set progress, reps target <br>&emsp; + `LogSetSheet`: input actual reps + weight → `addWorkoutLog` API call <br>&emsp; + `RestTimer`: countdown timer with auto-advance to next exercise/set after rest <br>&emsp; + Finish: `deactivateSession` → `resetSession` → navigate to `WorkoutSuccessScreen` <br> - Build **WorkoutSuccessScreen** <br>&emsp; + Trophy screen with exercise summary (exercises done, sets, total reps) <br>&emsp; + Blocks hardware back button → force navigate to Home | 02/14/2026 | 02/14/2026 | |

### Week 6 Achievements:

* **Backend — Session module**:
  * `UserWorkoutSession` + `WorkoutLog` entities persisted correctly with cascade DELETE.
  * `POST /api/sessions` creates a session linked to a plan and user; `PATCH /{id}/deactivate` marks it done.
  * `POST /api/sessions/{id}/logs` records individual set logs (exercise, set number, reps, weight).
  * `GET /user/{userId}/active` correctly returns the in-progress session or null.
  * Date-filtered query `GET /by-date?date=` working for session history retrieval.
* **Frontend — Live Workout**:
  * `PlanDetailScreen` loads active plan; day selector filters exercises by `dayOfWeek`.
  * Session state fully managed in Redux `workoutSessionSlice` — persisted to AsyncStorage for crash recovery.
  * `WorkoutSessionScreen` guides user through all exercises/sets with automatic rest timer.
  * Each set logged to backend via `addWorkoutLog` API call before advancing.
  * `WorkoutSuccessScreen` shows achieved stats and prevents accidental back navigation.
  * Complete workout loop tested end-to-end: plan → start session → log sets → rest timer → finish → success.

### AWS Knowledge Learned (Assumed Application):

* Learned structured logging practices to improve searchability in CloudWatch Logs.
* Identified key app metrics (latency, error rate, active sessions) for alert configuration.
* Built monitoring mindset for real-time workout flows with actionable dashboards.
* Learned threshold-based alarm handling and basic incident response workflow.
### Next Week Plan:

* **Backend**: Build the Media module — `Image` entity, S3 integration, and `ImageController` for associating images with exercises, foods, and workout plans.
* **Frontend**: Build `SessionDetailScreen` (past workout recap) and `SessionCalendarScreen` (monthly calendar with session dots).


### Week 6 Objectives:

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


### Week 6 Achievements:

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
