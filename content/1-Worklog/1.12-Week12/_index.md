---
title: "Week 12 Worklog"
date: 2026-03-30
weight: 12
chapter: false
pre: " <b> 1.12. </b> "
---

### Week 12 Objectives:

* Conduct full end-to-end integration testing of the entire myFit application (all features, all screens).
* Write comprehensive project documentation — README, API reference, architecture overview.
* Clean up code, remove debug artifacts, and prepare the project for handoff.
* Reflect on the 12-week internship: lessons learned, what went well, and future improvement paths.

### Tasks to be carried out this week:
| Day | Task | Start Date | Completion Date | Reference Material |
| --- | ---- | ---------- | --------------- | ------------------ |
| 2   | - **End-to-end integration testing** — Backend <br>&emsp; + Verify all API endpoints with valid + invalid inputs <br>&emsp; + Confirm Flyway V1/V2/V3 migrations run on fresh DB <br>&emsp; + Docker Compose cold start: `db` + `api` healthy under 30s <br>&emsp; + Review `application.properties` — confirm no dev-only values leak to production | 10/27/2025 | 10/27/2025 | |
| 3   | - **End-to-end integration testing** — Frontend (6 user journeys) <br>&emsp; + Journey 1: Register → Onboard → Home Dashboard <br>&emsp; + Journey 2: Create plan → Clone system plan → Set active plan <br>&emsp; + Journey 3: Start workout session → Log sets → Rest timer → Finish → Success screen <br>&emsp; + Journey 4: Add foods to 4 meals → Verify daily calorie total <br>&emsp; + Journey 5: Enter body metrics → BMI/BMR/TDEE calculated → Charts render <br>&emsp; + Journey 6: Chat with AI assistant → Bedrock responds in Vietnamese | 10/28/2025 | 10/28/2025 | |
| 4   | - Write **Backend README** (`myFit-api/README.md`) <br>&emsp; + Project overview & architecture diagram (API ↔ PostgreSQL ↔ Cognito ↔ S3) <br>&emsp; + Module documentation: Auth, Food, SystemWorkout, UserWorkoutPlan, Session, UserMetric, Media, GoalType <br>&emsp; + Setup guide: prerequisites, `.env` variables, Docker Compose commands <br>&emsp; + API endpoint reference table (all routes, methods, descriptions, auth requirements) | 10/29/2025 | 10/29/2025 | |
| 4   | - Update **Frontend** `guide.md` <br>&emsp; + Tech stack summary table <br>&emsp; + Navigation structure diagram (AuthStack / OnboardingStack / MainTabs) <br>&emsp; + Setup guide: `npm install`, `.env` variables, `npx expo start` <br>&emsp; + Screen inventory with feature descriptions <br>&emsp; + AWS Cognito PKCE + Bedrock setup notes | 10/29/2025 | 10/29/2025 | |
| 5   | - **Code cleanup** — Backend <br>&emsp; + Remove all `TODO`, `FIXME`, debug `System.out.println` statements <br>&emsp; + Ensure public non-trivial methods have Javadoc comments <br>&emsp; + Review security config for inadvertent public route exposure <br>&emsp; + Final build: `mvn clean package -DskipTests` → confirm JAR builds cleanly | 10/30/2025 | 10/30/2025 | |
| 6   | - **Code cleanup** — Frontend <br>&emsp; + Remove all `console.log` debug statements <br>&emsp; + Run `eslint` and fix remaining lint warnings <br>&emsp; + Remove unused imports <br>&emsp; + Final export: `npx expo export` → confirm zero TypeScript errors <br> - **Project retrospective**: document lessons learned, tech decisions in hindsight, potential future improvements | 10/31/2025 | 10/31/2025 | |

### Week 12 Achievements:

* **Integration Testing**:
  * All backend API endpoints pass manual testing with valid and invalid inputs.
  * Docker Compose cold start reliable — API healthy within 25 seconds of `docker-compose up`.
  * Flyway V1, V2, V3 migrations run cleanly on a fresh PostgreSQL database.
  * All 6 user journeys tested end-to-end without critical failures.
* **Documentation**:
  * `myFit-api/README.md` covers full setup guide, environment variable reference, and all endpoint descriptions.
  * Frontend `guide.md` updated with navigation diagram, screen inventory, and AWS service configuration.
  * Architecture overview documented: Spring Boot API ↔ PostgreSQL ↔ AWS Cognito ↔ AWS S3 ↔ React Native App ↔ AWS Bedrock.
* **Code Quality**:
  * Zero `console.log` or `System.out.println` remaining in production paths.
  * TypeScript build (`npx expo export`) passes with zero errors.
  * Maven `mvn clean package` builds final JAR cleanly.
* **Project Retrospective — Key Lessons Learned**:
  * **IDOR prevention** via JWT `sub` extraction is a critical security pattern that must be applied consistently throughout a user-scoped REST API.
  * **Soft delete** with `@SQLRestriction` is more user-friendly than hard delete for user-owned data — allows potential recovery.
  * **Stateless JWT** architecture eliminates server-side session complexity at the cost of token revocation complexity (addressed via forced logout + refresh queue).
  * **React Native + NativeWind** is a powerful combination — TailwindCSS-familiar syntax dramatically speeds up mobile UI development.
  * **Redux + React Query** separation of concerns works well: Redux manages auth/session state; React Query manages server cache and background refetching.
  * **Future improvement path**: Deploy Backend to AWS ECS (Fargate) behind an ALB with HTTPS, Frontend bundled to AWS CloudFront + S3, CI/CD via GitHub Actions (already scaffolded in `.github/workflows/`).


### Week 12 Objectives:

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


### Week 12 Achievements:

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
