---
title: "Week 4 Worklog"
date: 2026-01-26
weight: 4
chapter: false
pre: " <b> 1.4. </b> "
---

### Week 4 Objectives:

* **Backend**: Build the System Workout module — the master exercise and workout plan data managed by admins.
* **Frontend**: Build core workout browsing screens — suggested plan wizard and exercise picker.
* Establish the relationship between `GoalType` ↔ `WorkoutPlan` ↔ `Exercise` for plan recommendations.

### Tasks to be carried out this week:
| Day | Task | Start Date | Completion Date | Reference Material |
| --- | ---- | ---------- | --------------- | ------------------ |
| 2   | - Build **MuscleGroup** entity & admin CRUD <br>&emsp; + Entity fields: `name (UNIQUE, ≤100 chars)`, `description (≤500 chars)` <br>&emsp; + `AdminMuscleGroupController` (`/api/admin/muscle-groups`) with `@PreAuthorize("hasRole('ADMIN')")` <br>&emsp; + CRUD: `POST`, `GET /`, `GET /{id}`, `PUT /{id}`, `DELETE /{id}` | 09/01/2025 | 09/01/2025 | |
| 3   | - Build **Exercise** entity & admin CRUD <br>&emsp; + Entity: `name (≤150)`, `description (≤500)`, `equipment`, `muscleGroup (@ManyToOne)` <br>&emsp; + `AdminExerciseController` (`/api/admin/exercises`): full CRUD + filter by muscle group <br>&emsp; + Public: `GET /api/workouts/exercises`, `GET /api/workouts/exercises/{id}`, `GET /api/workouts/exercises/by-muscle-group/{id}`, `POST /api/workouts/exercises/custom` | 09/02/2025 | 09/02/2025 | |
| 4   | - Build **WorkoutPlan** & **WorkoutPlanExercise** entities <br>&emsp; + `WorkoutPlan`: `name`, `description`, `goalType (@ManyToOne)`, `difficultyLevel`, `estimatedDurationMinutes`, `isSystemPlan` <br>&emsp; + `WorkoutPlanExercise`: `dayOfWeek (1-7)`, `sets`, `reps`, `restSeconds`, `dayIndex`, `weekIndex`, `orderIndex` <br>&emsp; + `AdminWorkoutPlanController` with full CRUD + filter by goal type | 09/03/2025 | 09/03/2025 | |
| 4   | - Expose **public workout endpoints** via `WorkoutController` (`/api/workouts`) <br>&emsp; + `GET /muscle-groups`, `GET /muscle-groups/{id}` <br>&emsp; + `GET /exercises`, `GET /exercises/{id}`, `GET /exercises/by-muscle-group/{id}` <br>&emsp; + `GET /plans`, `GET /plans/{id}`, `GET /plans/by-goal-type/{id}` | 09/03/2025 | 09/03/2025 | |
| 5   | - Build **SuggestedPlanScreen** (Frontend) — 3-step wizard <br>&emsp; + Step 1: Select fitness goal type (fetches from `GET /api/goal-types`) <br>&emsp; + Step 2: Browse system workout plan tiles with images and difficulty level <br>&emsp; + Step 3: View full plan detail with exercises grouped by day → clone via `cloneFromSystemPlan` | 09/04/2025 | 09/04/2025 | |
| 6   | - Build **PlanExercisePicker** screen (Frontend) <br>&emsp; + List all system exercises with images and muscle group labels <br>&emsp; + Search/filter by name <br>&emsp; + On select: call `addExerciseToPlan(planId, dayOfWeek, exerciseId)` <br> - Seed initial exercise and muscle group data into the local database via `DatabaseSeeder` | 09/05/2025 | 09/05/2025 | |

### Week 4 Achievements:

* **Backend — System Workout**:
  * `MuscleGroup` entity + admin CRUD fully operational; seeded with common muscle groups (Chest, Back, Legs, Shoulders, Arms, Core).
  * `Exercise` entity + admin CRUD + public read endpoints working.
  * `WorkoutPlan` with `WorkoutPlanExercise` (day-of-week scheduling, multi-week support via `weekIndex`) implemented.
  * All admin endpoints protected by `ROLE_ADMIN`; public read endpoints accessible without auth.
  * `GET /api/workouts/plans/by-goal-type/{id}` correctly filters system plans by goal type.
* **Frontend — Workout Browsing**:
  * `SuggestedPlanScreen` guides users through goal → plan selection in 3 clear steps.
  * Plan tiles display name, difficulty level, estimated duration, and goal type.
  * `PlanExercisePicker` lists all exercises with muscle group context; exercise selection adds to user plan.
* `DatabaseSeeder` populates initial muscle group + exercise data on app start for local dev.

### Next Week Plan:

* **Backend**: Build the `UserWorkoutPlan` module with plan cloning from system templates, soft-delete, and activate/deactivate logic.
* **Frontend**: Build `MyPlansScreen`, `CreatePlanScreen`, and `PlanEditScreen` (day-tabbed exercise editor).


### Week 4 Objectives:

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


### Week 4 Achievements:

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
