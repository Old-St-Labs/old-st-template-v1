# User Story Creation Guide for GitHub Issues

> **Purpose:** This guide helps Business Analysts create well-structured GitHub issues optimized for AI-assisted development. It can be fed directly to GitHub Copilot to generate issue content.

---

## Quick Start: Copilot Prompts by Story Type

### 🎨 Frontend Story Prompt

```
Create a FRONTEND GitHub issue following our user story guidelines:

**Project:** [Project name and brief description]
**Feature:** [What UI feature to build]
**User:** [Who is the primary user]
**Design Reference:** [Figma link]
**Tech Stack:** [e.g., React, TypeScript, Tailwind]

Generate the issue with:
1. User Story (As a... I want... so that...)
2. Expected Results (UI behaviors, states, interactions)
3. Frontend Acceptance Criteria in Gherkin format covering:
   - Component display and layout
   - User interactions (click, hover, focus)
   - Form validation (inline errors)
   - Loading, empty, error, success states
   - Responsive behavior
   - Keyboard navigation and accessibility
4. Technical Context — Frontend (components, routes, state management)
5. Non-Functional Requirements (performance, accessibility, browser support)
6. Out of Scope
```

### ⚙️ Backend Story Prompt

```
Create a BACKEND GitHub issue following our user story guidelines:

**Project:** [Project name and brief description]
**Feature:** [What API/service to build]
**Consumer:** [Frontend app, mobile app, external service]
**Tech Stack:** [e.g., Node.js, Express, PostgreSQL]

Generate the issue with:
1. User Story (As a... I want... so that...)
2. Expected Results (API behavior, data flow, system responses)
3. Backend Acceptance Criteria in Gherkin format covering:
   - API endpoint behavior (success responses)
   - Request validation (required fields, formats)
   - Error responses (400, 401, 403, 404, 500)
   - Database operations (CRUD)
   - Business logic rules
   - Edge cases (duplicate data, concurrent requests)
4. Technical Context — Backend with full API contract:
   - Endpoint: METHOD /path
   - Request headers, body schema
   - Response schemas for each status code
   - Database schema changes
5. Non-Functional Requirements (response time, rate limiting, security)
6. Out of Scope
```

### 🔗 Integration Story Prompt

```
Create an INTEGRATION GitHub issue following our user story guidelines:

**Project:** [Project name and brief description]
**Integration:** [What systems/components are being connected]
**Frontend Ticket:** [Related FE ticket number]
**Backend Ticket:** [Related BE ticket number]

Generate the issue with:
1. User Story (As a... I want... so that...)
2. Expected Results (end-to-end flow, system interactions)
3. Integration Acceptance Criteria in Gherkin format covering:
   - Happy path end-to-end flow
   - Error propagation from BE to FE
   - Loading state handling
   - Timeout and retry behavior
   - Data consistency across systems
4. Technical Context — Integration:
   - Frontend → Backend API mapping
   - Request/Response contract with examples
   - Error code mapping
   - Authentication flow
5. Testing Requirements (contract tests, E2E scenarios)
6. Out of Scope
```

---

## Complete Guidelines

### 1. User Story Principles

#### Make It User-Focused
Describe what the user wants to accomplish — not what the system should do.

#### Keep It Clear and Specific
Avoid vague language. Be explicit about:
- **Who** the user is
- **What** action they want
- **Why** they need it
- **What** "done" looks like

#### Ensure It's Valuable and Independent
Each user story should:
- Deliver measurable value
- Stand alone without depending on other stories
- Be small enough to finish within a sprint

### 2. Story Type Definitions

| Type | Scope | Primary Focus |
|------|-------|---------------|
| **Full Stack** | End-to-end feature | Complete user-facing feature with UI and API |
| **Frontend Only** | UI layer | Components, pages, state, styling, interactions |
| **Backend Only** | API/Service layer | Endpoints, business logic, database, integrations |
| **Integration** | Connection layer | Contract verification, E2E flow, error handling |

### 3. When to Split Stories

**Create separate tickets when:**
- Frontend and Backend can be developed in parallel
- Different developers/teams will work on each layer
- One layer is significantly more complex
- API contract needs to be agreed upon first

**Keep as single ticket when:**
- Small feature with simple FE and BE changes
- Same developer handles both layers
- Tightly coupled changes that must ship together

**Linking Convention:**
- Use the "Related Tickets" field to link FE ↔ BE ↔ Integration tickets
- Format: `Frontend: SMP-02, Backend: SMP-03`

### 4. Ticket Number Format

Format: `ABC-01`
- Three-letter project prefix
- Hyphen
- Sequential number

**Example:** `SMP-01` = First ticket for Project Sample

### 5. User Story Format

```
As a [type of user],
I want to [action/goal],
so that [desired outcome/value].
```

### 6. Acceptance Criteria by Story Type

#### Frontend Acceptance Criteria Focus

```
**Component Display**
- **Scenario: Component renders correctly**
  - Given the user navigates to /page
  - When the page loads
  - Then
    - Header displays with title "[Title]"
    - Form renders with fields:
      - Email input — (Required)
      - Password input — (Required)
      - Submit button — (Disabled until form valid)

**User Interactions**
- **Scenario: User interacts with form**
  - Given the form is displayed
  - When the user types in the email field
  - Then
    - Input value updates in real-time
    - Character count displays (if applicable)

**States**
- **Scenario: Loading state**
  - Given the user submits the form
  - When the API request is in progress
  - Then
    - Submit button shows spinner
    - Form fields are disabled
    - User cannot submit again

- **Scenario: Error state**
  - Given the API returns an error
  - When the error response is received
  - Then
    - Error banner displays with message
    - Form fields are re-enabled
    - User can retry

**Responsive Behavior**
- **Scenario: Mobile viewport**
  - Given the viewport is < 768px
  - When the user views the page
  - Then
    - Navigation collapses to hamburger menu
    - Form stacks vertically
    - Touch targets are minimum 44x44px
```

#### Backend Acceptance Criteria Focus

```
**API Endpoint — Success**
- **Scenario: Valid request returns data**
  - Given a valid JWT token in Authorization header
  - And request body: { "email": "user@example.com", "name": "John" }
  - When POST /api/v1/users is called
  - Then
    - Response status: 201 Created
    - Response body: { "id": "uuid", "email": "...", "name": "...", "createdAt": "..." }
    - User record is created in database
    - Audit log entry is created

**Request Validation**
- **Scenario: Missing required field**
  - Given request body is missing "email" field
  - When POST /api/v1/users is called
  - Then
    - Response status: 400 Bad Request
    - Response body: { "error": "VALIDATION_ERROR", "details": [{ "field": "email", "message": "Email is required" }] }
    - No database record is created

- **Scenario: Invalid email format**
  - Given request body has email: "not-an-email"
  - When POST /api/v1/users is called
  - Then
    - Response status: 400 Bad Request
    - Response body: { "error": "VALIDATION_ERROR", "details": [{ "field": "email", "message": "Invalid email format" }] }

**Authentication/Authorization**
- **Scenario: Missing auth token**
  - Given no Authorization header is provided
  - When POST /api/v1/users is called
  - Then
    - Response status: 401 Unauthorized
    - Response body: { "error": "UNAUTHORIZED", "message": "Authentication required" }

- **Scenario: Insufficient permissions**
  - Given user has role "viewer" (not "admin")
  - When POST /api/v1/users is called
  - Then
    - Response status: 403 Forbidden
    - Response body: { "error": "FORBIDDEN", "message": "Admin role required" }

**Edge Cases**
- **Scenario: Duplicate email**
  - Given a user with email "existing@example.com" already exists
  - When POST /api/v1/users is called with same email
  - Then
    - Response status: 409 Conflict
    - Response body: { "error": "DUPLICATE_ENTRY", "message": "Email already registered" }
```

#### Integration Acceptance Criteria Focus

```
**End-to-End Flow**
- **Scenario: Complete user registration flow**
  - Given the user is on the registration page
  - When the user fills the form and clicks Submit
  - Then
    - Frontend sends POST /api/v1/users with form data
    - Backend validates and creates user
    - Backend returns 201 with user data
    - Frontend receives response
    - Frontend redirects to /dashboard
    - Frontend displays success toast

**Error Propagation**
- **Scenario: Backend validation error shown in UI**
  - Given the user submits an invalid email
  - When Backend returns 400 with field errors
  - Then
    - Frontend parses error response
    - Frontend displays inline error on email field
    - Frontend does not redirect

- **Scenario: Server error handling**
  - Given the backend is unavailable
  - When the API request times out after 10 seconds
  - Then
    - Frontend displays generic error message
    - Frontend logs error to monitoring service
    - User can retry the action

**Contract Verification**
- **Scenario: Request format matches contract**
  - Given the API contract specifies { email: string, name: string }
  - When Frontend sends a request
  - Then
    - Request body matches expected schema
    - Content-Type header is application/json
    - Authorization header is present

- **Scenario: Response handling matches contract**
  - Given the API returns 201 with user object
  - When Frontend receives the response
  - Then
    - Frontend correctly parses all fields
    - Frontend stores user in state
    - Frontend handles optional fields gracefully
```

---

## Example Issues by Type

### Example 1: Frontend Only — User Profile Card

**Ticket Number:** SMP-15

**Story Type:** Frontend Only

**Related Tickets:** Backend: SMP-14 (User Profile API)

**User Story:**
```
As a logged-in user,
I want to see my profile information in a card on the dashboard,
so that I can quickly view and verify my account details.
```

**Expected Results:**
- Profile card displays user avatar, name, email, and member since date
- Card has hover state with subtle elevation
- Edit button navigates to profile settings
- Graceful handling when profile image fails to load
- Skeleton loader while data is fetching

**Design:** https://figma.com/file/abc123/profile-card

**Acceptance Criteria:**

**Profile Card Display**
- **Scenario: Profile card renders with user data**
  - Given the user is logged in
  - And the profile API has returned successfully
  - When the dashboard loads
  - Then
    - Profile card displays with:
      - User avatar (64x64px, circular) — Falls back to initials if no image
      - Full name — (Required)
      - Email address — (Required)
      - "Member since [date]" — (Required, formatted as "Jan 2024")
      - Edit Profile button

**Loading State**
- **Scenario: Profile card loading**
  - Given the dashboard is loading
  - When the profile API request is in progress
  - Then
    - Skeleton loader displays for avatar, name, email
    - Edit button is disabled

**Error State**
- **Scenario: Profile image fails to load**
  - Given the user's avatar URL returns 404
  - When the image fails to load
  - Then
    - Fallback displays user's initials in colored circle
    - No broken image icon shown

**Interactions**
- **Scenario: User clicks Edit Profile**
  - Given the profile card is displayed
  - When the user clicks "Edit Profile"
  - Then
    - User is navigated to /settings/profile
    
- **Scenario: Hover state**
  - Given the profile card is displayed
  - When the user hovers over the card
  - Then
    - Card elevation increases (shadow)
    - Cursor changes to pointer

**Technical Context — Frontend:**
```
Relevant Files:
- src/components/dashboard/ProfileCard.tsx (create new)
- src/components/common/Avatar.tsx (reuse)
- src/components/common/Skeleton.tsx (reuse)
- src/hooks/useProfile.ts (existing)

Routes:
- Dashboard: /dashboard (where card displays)
- Edit Profile: /settings/profile (navigation target)

State Management:
- useProfile hook provides: { data, isLoading, error }
- Profile data cached in React Query

UI Components:
- Use existing Avatar component with fallback prop
- Use existing Skeleton component for loading state
- Card styling from design system tokens
```

**Non-Functional Requirements:**
- Performance: Card renders within 100ms of data availability
- Accessibility: Card is not focusable (not interactive as whole), Edit button is focusable
- Browser Support: Chrome, Firefox, Safari, Edge

**Out of Scope:**
- Profile editing functionality (separate ticket)
- Profile card on mobile app
- Social links display

---

### Example 2: Backend Only — User Profile API

**Ticket Number:** SMP-14

**Story Type:** Backend Only

**Related Tickets:** Frontend: SMP-15 (Profile Card UI)

**User Story:**
```
As a frontend application,
I want to fetch the current user's profile via API,
so that I can display their information in the UI.
```

**Expected Results:**
- GET endpoint returns authenticated user's profile
- Response includes id, name, email, avatar URL, and created date
- Returns 401 for unauthenticated requests
- Returns 404 if user profile doesn't exist (edge case for deleted users)
- Response time under 200ms

**Acceptance Criteria:**

**GET /api/v1/users/me — Success**
- **Scenario: Authenticated user fetches own profile**
  - Given a valid JWT token for user "user-123"
  - When GET /api/v1/users/me is called
  - Then
    - Response status: 200 OK
    - Response body:
      ```json
      {
        "id": "user-123",
        "email": "john@example.com",
        "firstName": "John",
        "lastName": "Doe",
        "fullName": "John Doe",
        "avatarUrl": "https://cdn.example.com/avatars/user-123.jpg",
        "createdAt": "2024-01-15T10:30:00Z"
      }
      ```

**Authentication Errors**
- **Scenario: Missing authentication token**
  - Given no Authorization header is provided
  - When GET /api/v1/users/me is called
  - Then
    - Response status: 401 Unauthorized
    - Response body: { "error": "UNAUTHORIZED", "message": "Authentication required" }

- **Scenario: Invalid/expired token**
  - Given an expired JWT token
  - When GET /api/v1/users/me is called
  - Then
    - Response status: 401 Unauthorized
    - Response body: { "error": "TOKEN_EXPIRED", "message": "Please log in again" }

**Edge Cases**
- **Scenario: User exists but profile incomplete**
  - Given user has no avatar set
  - When GET /api/v1/users/me is called
  - Then
    - Response status: 200 OK
    - avatarUrl field is null

- **Scenario: User deleted but token still valid**
  - Given user was deleted but token hasn't expired
  - When GET /api/v1/users/me is called
  - Then
    - Response status: 404 Not Found
    - Response body: { "error": "USER_NOT_FOUND" }

**Technical Context — Backend:**
```
Relevant Files:
- src/controllers/userController.ts
- src/services/userService.ts
- src/models/User.ts
- src/middleware/auth.ts

API Contract:
GET /api/v1/users/me
Headers:
  Authorization: Bearer <jwt_token>

Response (200):
{
  "id": "string (UUID)",
  "email": "string",
  "firstName": "string",
  "lastName": "string",
  "fullName": "string (computed)",
  "avatarUrl": "string | null",
  "createdAt": "string (ISO 8601)"
}

Response (401):
{ "error": "UNAUTHORIZED" | "TOKEN_EXPIRED", "message": "string" }

Response (404):
{ "error": "USER_NOT_FOUND", "message": "string" }

Database:
- Table: users
- Columns: id, email, first_name, last_name, avatar_url, created_at
- No schema changes required
```

**Non-Functional Requirements:**
- Performance: Response time < 200ms (p95)
- Security: Only return own user data, no access to other profiles via this endpoint
- Rate Limiting: 100 requests/minute per user

**Assumptions & Dependencies:**
- JWT authentication middleware exists and is applied
- User table and model already exist

**Out of Scope:**
- PATCH /api/v1/users/me (update profile) — separate ticket
- GET /api/v1/users/:id (view other users) — separate ticket
- Avatar upload endpoint

---

### Example 3: Integration — User Registration Flow

**Ticket Number:** SMP-20

**Story Type:** Integration / API Contract

**Related Tickets:** Frontend: SMP-18, Backend: SMP-19

**User Story:**
```
As a development team,
I want to verify the integration between the registration UI and API,
so that new users can successfully create accounts end-to-end.
```

**Expected Results:**
- Frontend form submission triggers correct API call
- Backend validation errors display correctly in UI
- Successful registration redirects and shows confirmation
- Error states are handled gracefully with user-friendly messages
- E2E tests cover the complete flow

**Acceptance Criteria:**

**Happy Path E2E**
- **Scenario: Successful user registration**
  - Given the user is on /register
  - And fills in:
    - Email: "newuser@example.com"
    - Password: "SecurePass123!"
    - Confirm Password: "SecurePass123!"
  - And checks "Accept Terms"
  - When the user clicks "Create Account"
  - Then
    - Frontend shows loading state on button
    - Frontend sends POST /api/v1/auth/register with:
      ```json
      { "email": "newuser@example.com", "password": "SecurePass123!", "acceptedTerms": true }
      ```
    - Backend validates, creates user, returns 201 with token
    - Frontend stores token in localStorage
    - Frontend redirects to /dashboard
    - Toast displays: "Account created successfully!"

**Validation Error Flow**
- **Scenario: Backend rejects invalid email**
  - Given the user submits email "not-valid"
  - When Backend returns 400 with:
    ```json
    { "error": "VALIDATION_ERROR", "details": [{ "field": "email", "message": "Invalid email format" }] }
    ```
  - Then
    - Frontend parses the error response
    - Email field shows inline error: "Invalid email format"
    - Form remains on page (no redirect)
    - User can correct and resubmit

- **Scenario: Email already registered**
  - Given the user submits an existing email
  - When Backend returns 409 Conflict
  - Then
    - Frontend displays error: "An account with this email already exists"
    - Link to /login is shown
    - Form data is preserved

**Error Handling**
- **Scenario: Network failure**
  - Given the network is unavailable
  - When the registration request fails
  - Then
    - Frontend displays: "Unable to connect. Please check your internet and try again."
    - Retry button is available
    - Form data is preserved

- **Scenario: Server error (500)**
  - Given the backend returns 500
  - When Frontend receives the error
  - Then
    - Frontend displays: "Something went wrong. Please try again later."
    - Error is logged to monitoring (Sentry/DataDog)
    - User can retry

**Technical Context — Integration:**
```
Frontend → Backend Mapping:
- Form submit → POST /api/v1/auth/register
- Email field → request.body.email
- Password field → request.body.password (plain, HTTPS encrypted)
- Terms checkbox → request.body.acceptedTerms

Error Code Mapping:
| Backend Error | Frontend Display |
|---------------|------------------|
| VALIDATION_ERROR + field | Inline field error |
| EMAIL_EXISTS (409) | "Email already exists" + login link |
| RATE_LIMITED (429) | "Too many attempts. Try again in X minutes." |
| SERVER_ERROR (500) | "Something went wrong. Please try again." |

Authentication Flow:
1. Backend returns { token, user } on success
2. Frontend stores token in localStorage
3. Frontend sets Authorization header for subsequent requests
4. Frontend redirects to /dashboard

Testing Requirements:
- Contract test: Verify request/response schemas match
- E2E test: Cypress test for full registration flow
- Error test: Mock 400/409/500 responses and verify UI handling
```

**Testing Checklist:**
- [ ] E2E test: Successful registration flow
- [ ] E2E test: Validation error displays inline
- [ ] E2E test: Duplicate email shows correct message
- [ ] Contract test: Request body schema matches API spec
- [ ] Contract test: Response parsing handles all fields
- [ ] Unit test (FE): Error mapping function
- [ ] Unit test (BE): Validation returns correct error format

**Non-Functional Requirements:**
- Performance: Complete flow (submit → redirect) < 3 seconds
- Security: Password never logged, HTTPS required
- Monitoring: Failed registrations logged with error type (not password)

**Assumptions & Dependencies:**
- Frontend (SMP-18) and Backend (SMP-19) are complete
- Shared error code constants between FE and BE
- Test environment has seeded test data

**Out of Scope:**
- Email verification flow
- Social registration (OAuth)
- Password strength meter

---

## Copilot Generation Prompt — Universal Template

```
You are a Business Analyst creating a GitHub issue for a development team using AI-assisted coding.

**Story Type:** [Full Stack / Frontend Only / Backend Only / Integration]
**Project Overview:** [Describe the project]
**Feature/Task:** [What to build]
**Related Tickets:** [Link FE/BE tickets if split]
**Design:** [Figma link for Frontend]
**Tech Stack:** [Languages, frameworks, database]

Generate a complete GitHub issue with this structure:

1. **User Story** — As a [user/system], I want [goal], so that [value]

2. **Expected Results** — Bullet list of behaviors, responses, data changes, edge cases

3. **Acceptance Criteria** — Gherkin format:
   - For FRONTEND: UI display, interactions, states (loading/error/empty), responsive, accessibility
   - For BACKEND: API success, request validation, error responses (400/401/403/404/500), edge cases
   - For INTEGRATION: E2E flow, error propagation, contract verification

4. **Technical Context** — Based on story type:
   - FRONTEND: Components, routes, state management, UI components to reuse
   - BACKEND: Full API contract with request/response schemas, database changes
   - INTEGRATION: FE→BE mapping, error code mapping, auth flow, testing requirements

5. **Non-Functional Requirements** — Performance, security, accessibility, browser support

6. **Assumptions & Dependencies** — External/team dependencies

7. **Out of Scope** — What is explicitly NOT included

Format all acceptance criteria with:
- **Bold group headers**
- **Bold scenario names**
- Given/When/Then on indented lines
- For Backend: Include actual JSON request/response examples
- For Frontend: Mark fields as (Required)/(Optional)
```

---

## Tips for Splitting Stories

| Situation | Recommendation |
|-----------|----------------|
| New API + New UI | Split into Backend (API) + Frontend (UI) + Integration (verification) |
| Simple CRUD | Keep as Full Stack if same developer |
| Complex business logic | Backend ticket with detailed rules; Frontend ticket for UI only |
| Multiple consumers | Backend ticket first; separate Frontend/Mobile tickets reference it |
| Tight deadline | Integration ticket to verify contract; FE/BE can work in parallel |

---

## Tips for BAs

1. **Be specific with Copilot prompts** — The more context you provide, the better the output
2. **Review and refine** — Always review AI-generated content for accuracy
3. **Include examples** — When describing expected behavior, concrete examples help
4. **Think like a developer** — Consider what information they need to implement without asking questions
5. **Use the form** — The GitHub Issue Form enforces structure; fill all sections thoughtfully
