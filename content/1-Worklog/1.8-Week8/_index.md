---
title: "Week 8 Worklog"
date: 2026-03-02
weight: 8
chapter: false
pre: " <b> 1.8. </b> "
---

### Week 8 Objectives:

* **Backend**: Build the complete Food & Nutrition module — `Food`, `Meal`, `MealFood`, `DailyNutrition` with auto-calculated macro nutrients.
* **Frontend**: Build the `DietScreen` with today’s 4-meal layout, food search modal, and add-food-to-meal flow; plus `DietHistoryScreen`.
* Enable users to track daily calorie and macro intake across all meal types.

### Tasks to be carried out this week:
| Day | Task | Start Date | Completion Date | Reference Material |
| --- | ---- | ---------- | --------------- | ------------------ |
| 2   | - Build **Food** entity (table `food`) <br>&emsp; + Fields: `name`, `caloriesPer100g`, `proteinPer100g`, `carbsPer100g`, `fatsPer100g`, `unit` <br>&emsp; + `FoodController` (`/api/foods`): `POST /`, `GET /{id}`, `GET /` (paginated), `GET /search?keyword=`, `PUT /{id}` | 03/03/2026 | 03/03/2026 | |
| 3   | - Build **Meal** entity (table `meal`) <br>&emsp; + Fields: `userProfile (@ManyToOne)`, `date (LocalDateTime)`, `mealType (enum: BREAKFAST/LUNCH/SNACK/DINNER)`, `note` <br>&emsp; + `MealController` (`/api/meals`): create, get by ID, list (paginated), filter by date, filter by type | 03/04/2026 | 03/04/2026 | |
| 4   | - Build **MealFood** entity (table `meal_food`) — join table with computed macros <br>&emsp; + Fields: `meal (@ManyToOne)`, `food (@ManyToOne)`, `quantity (float grams)` <br>&emsp; + `calories`, `protein`, `carbs`, `fats` auto-calculated at insertion from Food’s per-100g values × (quantity/100) <br>&emsp; + `MealFoodController` (`/api/meal-foods`): add food to meal, list foods in meal, remove | 03/05/2026 | 03/05/2026 | |
| 4   | - Build **DailyNutrition** entity (table `daily_nutrition`) <br>&emsp; + Fields: `nutritionDate (LocalDate)`, `totalCalories`, `totalProtein`, `totalCarbs`, `totalFats` <br>&emsp; + `DailyNutritionController` (`/api/daily-nutrition`): `POST /calculate?date=` recomputes & saves daily totals; `GET /?date=` retrieves | 03/05/2026 | 03/05/2026 | |
| 5   | - Build **DietScreen** (Frontend) <br>&emsp; + Display today’s 4 meals (Breakfast/Lunch/Snack/Dinner) via `ensureDailyMeals` <br>&emsp; + Each meal: food items list, calorie count, progress bar vs. target <br>&emsp; + "Add food" modal: search by name (`searchFoods`), input quantity in grams, submit → `addFoodToMeal` <br>&emsp; + Total daily calorie progress bar at top <br>&emsp; + Pull-to-refresh | 03/06/2026 | 03/06/2026 | |
| 6   | - Build **DietHistoryScreen** (Frontend) <br>&emsp; + Monthly calendar view — tap a date to see that day’s meal breakdown <br>&emsp; + Per-meal food items with calorie totals <br> - Integrate `foodService`: `getMealsByUser`, `getMealFoodsByMealId`, `addFoodToMeal`, `deleteMealFood` into DietScreen <br> - Test full nutrition tracking loop: add food → view nutrient breakdown → track daily total | 03/07/2026 | 03/07/2026 | |

### Week 8 Achievements:

* **Backend — Food & Nutrition module**:
  * `Food` entity seeded with real food data from the `fitness_crawler` tool (over 100 food items in local DB).
  * `MealFood` correctly auto-calculates `calories`, `protein`, `carbs`, `fats` on insertion based on `quantity / 100 * per100gValue`.
  * `POST /api/daily-nutrition/calculate?date=` aggregates all `MealFood` entries for a date into a single `DailyNutrition` record.
  * Pagination on `GET /api/foods` works — `PageResponse<T>` wrapper handles `page`, `size`, `totalPages`, `totalElements`.
  * Keyword search on `GET /api/foods/search?keyword=` performs case-insensitive LIKE query.
* **Frontend — Diet tracking**:
  * `DietScreen` correctly calls `ensureDailyMeals` to guarantee 4 meal slots exist for today.
  * Food search modal shows paginated results with lazy loading.
  * Adding food: quantity input → backend calculates and stores macros → UI refreshes with updated totals.
  * `DietHistoryScreen` calendar correctly loads meal data for selected dates.
  * Daily calorie progress bar reflects `totalCalories / 2500` target accurately.

### AWS Knowledge Learned (Assumed Application):

* Learned Bedrock Runtime integration and model selection trade-offs across latency/cost/quality.
* Improved prompt engineering skills to keep fitness-coach persona outputs consistent.
* Applied application-level guardrails: context limits, input/output controls, and fallback behavior.
* Learned quota-aware retry/backoff strategy for resilient AI service calls.
### Next Week Plan:

* **Backend**: Build the User Metric module — `BodyMetric` entity and `HealthCalculation` with BMI / BMR / TDEE computation logic.
* **Frontend**: Build `HealthDashboardScreen` with wheel pickers, `BodyMetricListScreen`, `BodyMetricFormScreen`, and all health chart components.


### Week 8 Objectives:

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


### Week 8 Achievements:

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
