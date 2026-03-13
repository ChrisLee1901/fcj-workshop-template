---
title: "Week 3 Worklog"
date: 2026-01-19
weight: 3
chapter: false
pre: " <b> 1.3. </b> "
---

### Week 3 Objectives:

* **Backend**: Build the application-wide common layer — exception handling, CORS, and the `GoalType` module.
* **Frontend**: Scaffold the complete navigation hierarchy and implement the multi-step Onboarding flow.
* Ensure end-to-end flow from login → onboarding → main app works before adding deeper features.

### Tasks to be carried out this week:
| Day | Task | Start Date | Completion Date | Reference Material |
| --- | ---- | ---------- | --------------- | ------------------ |
| 2   | - Implement **GlobalExceptionHandler** (`@RestControllerAdvice`) <br>&emsp; + Handle `MethodArgumentNotValidException` → field-level validation errors <br>&emsp; + Handle `EntityNotFoundException`, custom business exceptions <br>&emsp; + All errors returned in `ApiResponse` envelope with appropriate HTTP status | 01/20/2026 | 01/20/2026 | |
| 2   | - Configure **CorsConfig** globally <br>&emsp; + Allow origins for local dev and production frontend URLs <br>&emsp; + Allow headers: `Authorization`, `Content-Type` <br>&emsp; + Allow all HTTP methods | 01/20/2026 | 01/20/2026 | |
| 3   | - Build **GoalType** module <br>&emsp; + Entity: `name (UNIQUE)`, `description` <br>&emsp; + Repository, Service, Controller <br>&emsp; + Endpoints (all **public**): `POST /api/goal-types`, `GET /api/goal-types`, `GET /api/goal-types/{id}`, `GET /api/goal-types/by-name/{name}` | 01/21/2026 | 01/21/2026 | |
| 4   | - Build **Frontend** `RootNavigator` <br>&emsp; + Reads Redux `isAuthenticated` + `hasCompletedOnboarding` from `authSlice` <br>&emsp; + Routes to `AuthStack` (unauthenticated) / `OnboardingStack` (pending) / `MainTabs` (ready) <br> - Build **AuthStack**: `WelcomeScreen` + `LoginScreen` <br> - Build **MainTabs** with `CustomTabBar` <br>&emsp; + 4 bottom tabs: Home, Workout, Diet, Health <br>&emsp; + Center floating Chat button splitting left/right tabs | 01/22/2026 | 01/22/2026 | <https://reactnavigation.org/> |
| 5   | - Build **OnboardingStack** (5-step wizard) <br>&emsp; + Step 1: Gender + Date-of-birth (day/month/year sliders) + Height + Weight <br>&emsp; + Step 2: Activity level + Job type <br>&emsp; + Step 3: Main fitness goal + Target weight + Target body areas <br>&emsp; + Step 4: Diet preferences + Food allergies + Meals per day + Water intake <br>&emsp; + Step 5: Experience level + Workout location + Frequency + Session duration | 01/23/2026 | 01/23/2026 | |
| 6   | - Add **CaloriesScreen** and **TrainingScreen** to Onboarding preview <br>&emsp; + CaloriesScreen: animated calorie management demo UI <br>&emsp; + TrainingScreen: weekly workout plan by day preview <br> - Wire onboarding completion: `dispatch(completeOnboarding())` → sync user profile to backend via `POST /user/sync` | 01/24/2026 | 01/24/2026 | |

### Week 3 Achievements:

* **Backend — Common Layer**:
  * `GlobalExceptionHandler` catches all standard and custom exceptions; returns consistent `ApiResponse` to clients.
  * CORS configured globally — frontend running on `localhost:8081` can communicate with the API on `localhost:8080`.
* **Backend — GoalType module**:
  * `GoalType` entity persisted to PostgreSQL; supports types like **Weight Loss**, **Muscle Gain**, **Maintenance**.
  * All 4 public endpoints operational: create, list all, get by ID, get by name.
  * GoalTypes serve as the backbone for linking workout plans to user fitness goals.
* **Frontend — Navigation**:
  * `RootNavigator` correctly redirects based on auth + onboarding state — no logic in individual screens.
  * `MainTabs` renders with `CustomTabBar`; tab bar splits left (Home, Workout) and right (Diet, Health) around a center Chat button.
  * All stacks registered: `AuthStack`, `OnboardingStack`, `WorkoutStack`, `DietStack`, `HealthStack`.
* **Frontend — Onboarding**:
  * Full 5-step wizard implemented with slide animations between steps.
  * User data collected (gender, DOB, height, weight, goals, diet prefs, workout prefs) ready to be stored in profile.
  * Onboarding completion dispatches `completeOnboarding()` and calls the backend sync endpoint.

### AWS Knowledge Learned (Assumed Application):

* Understood CORS implications for split-domain frontend/backend deployments in AWS environments.
* Learned how public/private endpoint boundaries can align with future API Gateway integration.
* Recognized the value of centralized exception handling for better CloudWatch troubleshooting.
* Standardized API responses with future observability and tracing in mind.
### Next Week Plan:

* **Backend**: Build the System Workout module — `MuscleGroup`, `Exercise`, `WorkoutPlan`, `WorkoutPlanExercise` entities with admin CRUD and public read endpoints.
* **Frontend**: Implement the `SuggestedPlanScreen` (3-step plan selection wizard) and `PlanExercisePicker`.


### Week 3 Objectives:

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


### Week 3 Achievements:

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
