---
title: "Week 5 Worklog"
date: 2026-02-02
weight: 5
chapter: false
pre: " <b> 1.5. </b> "
---

### Week 5 Objectives:

* **Backend**: Build the `UserWorkoutPlan` module — personal plans with cloning from system templates, soft-delete, and one-active-plan enforcement.
* **Frontend**: Build the plan management screens — `MyPlansScreen`, `CreatePlanScreen`, and `PlanEditScreen` with day-tabbed exercise editing.
* Allow users to fully own their personal workout schedule with flexibility to create, clone, and customize plans.

### Tasks to be carried out this week:
| Day | Task | Start Date | Completion Date | Reference Material |
| --- | ---- | ---------- | --------------- | ------------------ |
| 2   | - Build **UserWorkoutPlan** entity <br>&emsp; + Fields: `user (@ManyToOne)`, `name (≤150)`, `description`, `goalTypeId (UUID)`, `isActive (default true)`, `isDeleted (default false)` <br>&emsp; + Soft-delete via `@SQLRestriction("is_deleted = false")` — deleted plans invisible to all Hibernate queries <br>&emsp; + Write Flyway **V1** migration: `user_workout_plan`, `user_workout_plan_exercises` tables | 02/03/2026 | 02/03/2026 | |
| 2   | - Write Flyway **V2** migration: add `is_deleted BOOLEAN DEFAULT FALSE` to `user_workout_plans` | 02/03/2026 | 02/03/2026 | |
| 3   | - Build **UserWorkoutPlanExercise** entity <br>&emsp; + Same scheduling fields as system: `dayOfWeek`, `sets`, `reps`, `restSeconds`, `dayIndex`, `weekIndex`, `orderIndex` <br>&emsp; + References `Exercise` (system entity), `UserWorkoutPlan` | 02/04/2026 | 02/04/2026 | |
| 3   | - Implement **UserWorkoutPlanService** key business logic <br>&emsp; + `userId` always extracted from `Jwt.getSubject()` → never from request body (IDOR prevention) <br>&emsp; + **Clone**: deep-copy all `WorkoutPlanExercise` entries into `UserWorkoutPlanExercise` — no FK to source plan retained <br>&emsp; + **Activate**: set `isActive=true` on target plan, set `isActive=false` on all other user plans (one-active rule) | 02/04/2026 | 02/04/2026 | |
| 4   | - Build **UserWorkoutPlanController** (`/api/user-workout-plans`) <br>&emsp; + `POST /me` — create new plan <br>&emsp; + `POST /me/clone/{systemPlanId}` — clone system template <br>&emsp; + `GET /me` (summary list), `GET /me/active`, `GET /{id}` <br>&emsp; + `PUT /{id}` (update metadata), `PUT /{id}/activate`, `DELETE /{id}` (soft) <br>&emsp; + `POST /{planId}/exercises`, `GET /{planId}/exercises`, `PUT /{planId}/exercises/{id}`, `DELETE /{planId}/exercises/{id}` | 02/05/2026 | 02/05/2026 | |
| 5   | - Build **MyPlansScreen** (Frontend) <br>&emsp; + Lists all user plans with active indicator badge <br>&emsp; + Activate/deactivate toggle; soft-delete with `ConfirmModal` <br>&emsp; + Navigate to `CreatePlanScreen` or `PlanEditScreen` | 02/06/2026 | 02/06/2026 | |
| 5   | - Build **CreatePlanScreen** (Frontend) <br>&emsp; + Form: plan name, description, goal type dropdown (fetched from `GET /api/goal-types`) <br>&emsp; + On submit: `createMyPlan` then navigate to `PlanEditScreen` | 02/06/2026 | 02/06/2026 | |
| 6   | - Build **PlanEditScreen** (Frontend) <br>&emsp; + Day-of-week tab bar (Mon-Sun) to switch exercise view per day <br>&emsp; + List exercises for selected day with reorder (up/down arrows), delete button <br>&emsp; + Navigate to `PlanExercisePicker` to add exercises for a given day <br>&emsp; + All changes call `addExerciseToPlan`, `updatePlanExercise`, `removePlanExercise` APIs | 02/07/2026 | 02/07/2026 | |

### Week 5 Achievements:

* **Backend — UserWorkoutPlan module**:
  * Flyway V1 + V2 migrations applied cleanly alongside Hibernate `ddl-auto=create-drop`.
  * Soft-delete pattern with `@SQLRestriction` works — deleted plans never appear in queries.
  * Clone endpoint creates a fully independent copy — verified by checking no FK pointer to source exists.
  * One-active-plan rule enforced at service layer — activating plan X correctly deactivates all others for that user.
  * `userId` always taken from the validated JWT `sub` claim — zero risk of IDOR attacks.
* **Frontend — Plan Management**:
  * `MyPlansScreen` correctly shows active/inactive state; delete prompts confirmation modal.
  * `CreatePlanScreen` form validates name/description before submitting.
  * `PlanEditScreen` day-tab architecture allows intuitive per-day exercise management.
  * Reorder and remove operations reflect immediately in UI after API calls.
  * `uiSlice` (`planEditorDay`, `plansReloadKey`) keeps plan editor state in sync across navigator.

### Next Week Plan:

* **Backend**: Build the `UserWorkoutSession` and `WorkoutLog` modules for tracking live workout activity.
* **Frontend**: Build `PlanDetailScreen` (active plan dashboard with day selector) and `WorkoutSessionScreen` (live workout screen with Redux session state).


### Week 5 Objectives:

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


### Week 5 Achievements:

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
