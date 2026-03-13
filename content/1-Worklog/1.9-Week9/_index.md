---
title: "Week 9 Worklog"
date: 2026-03-09
weight: 9
chapter: false
pre: " <b> 1.9. </b> "
---

### Week 9 Objectives:

* **Backend**: Build the User Metric module — `BodyMetric` for recording physical measurements and `HealthCalculation` for computing BMI, BMR, and TDEE.
* **Frontend**: Build `HealthDashboardScreen` with goal input + calculation, `BodyMetricListScreen`, `BodyMetricFormScreen`, and all health visualization chart components.
* Give users clear, actionable insight into their physical health and calorie targets.

### Tasks to be carried out this week:
| Day | Task | Start Date | Completion Date | Reference Material |
| --- | ---- | ---------- | --------------- | ------------------ |
| 2   | - Build **BodyMetric** entity (table `body_metric`) <br>&emsp; + Fields: `user (@ManyToOne)`, `heightCm (Float, min=50)`, `weightKg (Float, min=20)`, `age (Integer, min=10)`, `gender (Gender enum)`, `activityLevel (ActivityLevel enum)` <br>&emsp; + `BodyMetricController` (`/api/body-metrics`): create, get by user (newest first), get latest, get/update/delete by ID | 03/10/2026 | 03/10/2026 | |
| 3   | - Build **HealthCalculation** entity (table `health_calculation`) <br>&emsp; + Fields: `user`, `bodyMetric (optional snapshot FK)`, `bmi`, `bmr`, `tdee`, `goalType (GoalTypes enum)` <br>&emsp; + Calculation formulas: <br>&emsp;&emsp; BMI = weight / (height in m)² <br>&emsp;&emsp; BMR (Mifflin-St Jeor): Men = 10×w + 6.25×h - 5×age + 5; Women = −5 <br>&emsp;&emsp; TDEE = BMR × activity multiplier | 03/11/2026 | 03/11/2026 | |
| 3   | - Build **HealthMetricsController** (`/api/metrics`) <br>&emsp; + `POST /calculate` — compute & persist BMI/BMR/TDEE from `CalculateMetricsRequest` <br>&emsp; + `GET /user/{userId}` (full history), `GET /user/{userId}/latest`, `GET /{id}` | 03/11/2026 | 03/11/2026 | |
| 4   | - Build **HealthDashboardScreen** (Frontend) <br>&emsp; + `WheelPicker` for height (cm) and weight (kg) selection <br>&emsp; + `ActivityLevel` dropdown picker <br>&emsp; + Goal type selector: Cutting / Bulking / Maintain / UP_Power <br>&emsp; + On submit: `createBodyMetric` + `calculateMetrics` → display `HealthResultCard` (BMI, BMR, TDEE, Macros) <br>&emsp; + Redirect to Profile if gender/birthdate missing | 03/12/2026 | 03/12/2026 | |
| 5   | - Build health **chart components** (`src/components/health/`) <br>&emsp; + `BMITrendChart`: line chart with time range filter (7d/30d/90d/all) + color-coded BMI zones <br>&emsp; + `WeightChart`: line chart + optional 7-day moving average + distance to goal weight <br>&emsp; + `CalorieEnergyCharts`: dual-line BMR + TDEE with mode toggle <br>&emsp; + `MacrosDisplay`: 3 progress bars (protein/carbs/fat) with grams + % labels <br>&emsp; + `HealthResultCard`: summary card aggregating all computed values | 03/13/2026 | 03/13/2026 | |
| 6   | - Build **BodyMetricListScreen** (Frontend) <br>&emsp; + Lists all body metric history with formatted dates <br>&emsp; + `WeightChart` displayed at top of list <br>&emsp; + Edit (navigate to `BodyMetricFormScreen`) and delete with `ConfirmModal` <br> - Build **BodyMetricFormScreen** <br>&emsp; + Create or edit: height, weight, activity level, goal type <br>&emsp; + Derives gender + age from `authSlice` user state | 03/14/2026 | 03/14/2026 | |

### Week 9 Achievements:

* **Backend — User Metric module**:
  * `BodyMetric` records persisted with proper validation (height ≥ 50 cm, weight ≥ 20 kg, age ≥ 10).
  * BMR computed correctly using Mifflin-St Jeor equation; TDEE applies activity multipliers (1.2 – 1.9).
  * `POST /api/metrics/calculate` returns `HealthCalculationResponse` with BMI, BMR, TDEE, and derived macros (protein/carbs/fat grams for goal type).
  * History endpoints return records sorted by `createdAt DESC`.
* **Frontend — Health Dashboard**:
  * `HealthDashboardScreen` wheel pickers provide smooth UX for entering height/weight.
  * Results display immediately in `HealthResultCard` after API response.
  * `BMITrendChart` color-codes data points: underweight (blue), normal (green), overweight (yellow), obese (red).
  * `WeightChart` shows moving average trend line when user has ≥ 7 data points.
  * `CalorieEnergyCharts` allows toggling between BMR-only, TDEE-only, and combined view.
  * `BodyMetricListScreen` shows full measurement history with inline edit/delete.

### AWS Knowledge Learned (Assumed Application):

* Learned secret management using AWS Secrets Manager/SSM Parameter Store instead of hardcoding.
* Understood AWS KMS role in encrypting sensitive values at rest.
* Applied secret rotation mindset to reduce long-term credential exposure risk.
* Improved environment-specific config separation to prevent deployment mistakes.
### Next Week Plan:

* **Backend**: Add pagination refinements, endpoint validation improvements, and write unit/integration tests for key service methods.
* **Frontend**: Build `ChatScreen` with AWS Bedrock AI chat integration and `ProfileScreen` with user profile edit and account management.


### Week 9 Objectives:

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


### Week 9 Achievements:

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
