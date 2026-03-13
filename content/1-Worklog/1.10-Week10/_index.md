---
title: "Week 10 Worklog"
date: 2026-03-16
weight: 10
chapter: false
pre: " <b> 1.10. </b> "
---

### Week 10 Objectives:

* **Backend**: Refine API endpoints — improve input validation, pagination, and write unit tests for core service methods.
* **Frontend**: Build the `ChatScreen` with AWS Bedrock AI integration and `ProfileScreen` with user account management.
* Deliver the AI-powered assistant feature as a differentiating value-add for the application.

### Tasks to be carried out this week:
| Day | Task | Start Date | Completion Date | Reference Material |
| --- | ---- | ---------- | --------------- | ------------------ |
| 2   | - Backend endpoint refinements <br>&emsp; + Add `@Valid` annotations and custom constraint validators to all request DTOs <br>&emsp; + Standardize paginated responses: `PageResponse<T>` with `page`, `size`, `totalPages`, `totalElements` <br>&emsp; + Add `GET /api/sessions/user/{userId}?startDate=&endDate=` date-range filter for session history | 03/17/2026 | 03/17/2026 | |
| 3   | - Write **unit tests** (Spring Boot Test + JUnit 5 + Mockito) <br>&emsp; + `UserWorkoutPlanServiceTest`: clone method, activate logic, IDOR prevention <br>&emsp; + `HealthCalculationServiceTest`: BMI/BMR/TDEE formulas for various inputs <br>&emsp; + `UserWorkoutSessionServiceTest`: active session query, deactivate behavior | 03/18/2026 | 03/18/2026 | |
| 4   | - Build **chatService** (Frontend) <br>&emsp; + Direct AWS Bedrock Runtime API call (no Lambda proxy) <br>&emsp; + Model: `anthropic.claude-3-5-haiku-20241022-v1:0` <br>&emsp; + Vietnamese system prompt: fitness coach persona <br>&emsp; + Send last 12 conversation turns as context (sliding window memory) | 03/19/2026 | 03/19/2026 | <https://docs.aws.amazon.com/bedrock/> |
| 5   | - Build **ChatScreen** (Frontend) <br>&emsp; + Full-screen chat UI with message bubble list (user / bot) <br>&emsp; + Animated "typing" indicator (3 bouncing dots) while waiting for response <br>&emsp; + 4 quick-option chips: "Suggest exercises", "Today’s menu", "Calorie goal", "Weight loss advice" <br>&emsp; + Vietnamese initial greeting from the fitness bot <br>&emsp; + Animated keyboard avoidance <br>&emsp; + `notifyAlert` error handling via global alert proxy | 03/20/2026 | 03/20/2026 | |
| 6   | - Build **ProfileScreen** (Frontend) <br>&emsp; + Display avatar (initial-letter fallback), name, email, username, birthdate, gender <br>&emsp; + Edit modal: update birthdate (YYYY-MM-DD) and gender via `updateUserProfile` API + `dispatch(updateUserProfile)` <br>&emsp; + Logout: `signOut` (Cognito revoke) + `dispatch(logout)` + clear secure storage <br>&emsp; + Delete account: `deleteUserProfile` + `signOut` — both gated by `ConfirmModal` | 03/21/2026 | 03/21/2026 | |

### Week 10 Achievements:

* **Backend — Refinements & Testing**:
  * All request DTOs now have `@Valid` constraints — invalid inputs return structured `ApiResponse` field errors.
  * `PageResponse<T>` standardizes all paginated endpoints consistently.
  * Date-range session filter (`?startDate=&endDate=`) working with `@DateTimeFormat` parsing.
  * Unit tests pass for `UserWorkoutPlanService` clone, activate, and IDOR prevention scenarios.
  * BMI/BMR/TDEE formulas verified with edge case inputs (min/max allowed ranges).
* **Frontend — AI Chat**:
  * `chatService.sendChatToBedrock` calls AWS Bedrock Runtime directly using credentials from `.env`.
  * Sliding window of 12 turns maintains conversation context economically.
  * Quick-option chips provide instant first interaction without typing.
  * Typing indicator creates natural chat feel; keyboard avoidance works on both iOS and Android.
* **Frontend — Profile**:
  * Profile data loaded from Redux `authSlice` — no extra API call needed on screen mount.
  * Edit modal updates local state optimistically and confirms via API.
  * Logout and delete account flows both require confirmation — no accidental data loss.

### AWS Knowledge Learned (Assumed Application):

* Learned backend container packaging workflow and publishing images to Amazon ECR.
* Understood ECS Fargate as a serverless container runtime for reduced infrastructure overhead.
* Learned task definition/service rollout concepts for safer production releases.
* Connected CI/CD thinking with GitHub Actions build-test-deploy pipelines to AWS.
### Next Week Plan:

* **Backend**: Final API review, Docker Compose refinement with health checks, environment variable documentation.
* **Frontend**: Build `HomeScreen` dashboard with parallel data fetching, resolve remaining bugs, and polish overall UX.


### Week 10 Objectives:

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


### Week 10 Achievements:

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
