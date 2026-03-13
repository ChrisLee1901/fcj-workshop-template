---
title: "Week 2 Worklog"
date: 2026-01-12
weight: 2
chapter: false
pre: " <b> 1.2. </b> "
---

### Week 2 Objectives:

* **Backend**: Integrate AWS Cognito authentication into Spring Security. Build the `UserProfile` module.
* **Frontend**: Implement the complete authentication flow — from the Login screen through token storage and state management.
* Establish secure token handling patterns that will be reused across the entire application.

### Tasks to be carried out this week:
| Day | Task | Start Date | Completion Date | Reference Material |
| --- | ---- | ---------- | --------------- | ------------------ |
| 2   | - Study AWS Cognito User Pools concepts <br>&emsp; + User Pool configuration: password policies, app clients, PKCE <br>&emsp; + ID Token vs Access Token — difference and proper usage <br>&emsp; + Cognito JWT claims: `sub`, `cognito:groups`, `token_use` | 01/13/2026 | 01/13/2026 | <https://docs.aws.amazon.com/cognito/> |
| 3   | - Implement **Spring Security** JWT configuration <br>&emsp; + Add `spring-security-oauth2-resource-server` dependency <br>&emsp; + Configure `SecurityConfig`: stateless sessions, CSRF disabled, CORS enabled <br>&emsp; + Set Cognito issuer-uri in `application.properties` <br>&emsp; + Write custom `OAuth2TokenValidator` — reject tokens where `token_use != "access"` | 01/14/2026 | 01/14/2026 | <https://docs.spring.io/spring-security/> |
| 3   | - Implement role extraction from JWT <br>&emsp; + Read `cognito:groups` claim → convert to Spring `ROLE_<GROUP>` authorities <br>&emsp; + Configure `@PreAuthorize("hasRole('ADMIN')")` for admin endpoints <br>&emsp; + Define authorization rules: public endpoints, authenticated, admin-only | 01/14/2026 | 01/14/2026 | |
| 4   | - Build **UserProfile** entity & repository <br>&emsp; + Fields: `cognitoId (UNIQUE)`, `email (UNIQUE)`, `username`, `name`, `gender`, `birthdate`, `phoneNumber`, `picture`, `emailVerified` <br>&emsp; + `UserProfileRepository` extends `JpaRepository` | 01/15/2026 | 01/15/2026 | |
| 4   | - Build **UserProfileService** & **UserProfileController** <br>&emsp; + `POST /user/sync` — upsert profile from Cognito claims (IDOR-safe: `cognitoSub` from JWT `sub`) <br>&emsp; + `GET /user/{id}`, `PUT /user/{id}`, `DELETE /user/{id}` | 01/15/2026 | 01/15/2026 | |
| 5   | - Build **Frontend** `LoginScreen` <br>&emsp; + Single "Sign in with AWS Cognito" button <br>&emsp; + Initiate PKCE flow via `expo-auth-session` + `expo-web-browser` <br>&emsp; + Handle redirect callback: exchange code → tokens <br>&emsp; + Decode ID Token with `jwt-decode` to extract user claims | 01/16/2026 | 01/16/2026 | <https://docs.expo.dev/guides/authentication/> |
| 6   | - Build **authSlice** (Redux) and token storage <br>&emsp; + State: `isAuthenticated`, `user`, `token`, `refreshToken`, `hasCompletedOnboarding` <br>&emsp; + Actions: `login`, `logout`, `completeOnboarding`, `updateUserProfile` <br>&emsp; + Persist tokens to `expo-secure-store` (mobile) / `localStorage` (web) via `utils/storage.ts` <br> - Wire Axios **request interceptor**: auto-attach `Authorization: Bearer <token>` | 01/17/2026 | 01/17/2026 | |

### Week 2 Achievements:

* **Backend — Security**:
  * Spring Security fully configured with AWS Cognito as JWT issuer.
  * Custom `OAuth2TokenValidator` blocks ID tokens — only Access Tokens accepted at the API layer.
  * Role-based access control works: `ROLE_ADMIN` group from Cognito grants admin privileges.
  * All security rules defined: public health check, authenticated user routes, admin-only `/admin/**` routes.
* **Backend — UserProfile module**:
  * `POST /user/sync` correctly upserts user from Cognito JWT claims without IDOR vulnerability.
  * Full CRUD (`GET`, `PUT`, `DELETE`) on `/user/{id}` with proper authorization checks.
  * `UserProfile` entity persisted to PostgreSQL via JPA.
* **Frontend — Authentication**:
  * `LoginScreen` renders correctly; tapping the button opens Cognito Hosted UI in browser.
  * PKCE code exchange works end-to-end — tokens returned and stored securely.
  * `authSlice` correctly toggles `isAuthenticated`; `RootNavigator` redirects to the right stack.
  * Axios interceptor auto-attaches Bearer token — subsequent API calls authenticated.

### AWS Knowledge Learned (Assumed Application):

* Learned Cognito User Pool architecture and OAuth2/OIDC PKCE flow for mobile authentication.
* Understood the difference between ID tokens and access tokens, and why APIs should validate access tokens.
* Learned how to map cognito:groups claims into app roles for secure RBAC.
* Practiced issuer/audience/expiration validation patterns to reduce token abuse risks.
### Next Week Plan:

* **Backend**: Build the common infrastructure layer — `GlobalExceptionHandler`, `CorsConfig`. Implement the `GoalType` module (first business module).
* **Frontend**: Build navigation foundation — `RootNavigator`, `AuthStack`, `MainTabs` with custom tab bar, `OnboardingStack`.


### Week 2 Objectives:

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


### Week 2 Achievements:

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
