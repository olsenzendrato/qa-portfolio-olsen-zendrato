# Test Cases — CMS Digipac (Web Back-End Platform)

**Project:** CMS Digipac  
**Platform:** Web Back-End (Chrome, Safari, Firefox)  
**Testing Type:** Functional, Regression, UI/UX, Role-Based Access Control (RBAC)  
**Techniques:** Equivalence Partitioning, Use Case Testing, Exploratory  

---

## Module 1: User Authentication & Login

| Test ID | Scenario | Preconditions | Test Steps | Test Data | Expected Result | Technique | Priority |
|---|---|---|---|---|---|---|---|
| TC-DIG-001 | Login with valid credentials | User has active account | 1. Open CMS URL<br>2. Enter valid email & password<br>3. Click Login | Email: admin@digipac.id<br>Pass: ValidPass123! | User redirected to dashboard. Session token generated. | EP (Valid) | High |
| TC-DIG-002 | Login with invalid password | User has active account | 1. Open CMS URL<br>2. Enter valid email, wrong password<br>3. Click Login | Email: admin@digipac.id<br>Pass: WrongPass | Error message shown: "Invalid email or password". No session created. | EP (Invalid) | High |
| TC-DIG-003 | Login with unregistered email | — | 1. Open CMS URL<br>2. Enter unregistered email<br>3. Click Login | Email: unknown@test.com | Error message: "Account not found." | EP (Invalid) | High |
| TC-DIG-004 | Login with empty fields | — | 1. Open CMS URL<br>2. Leave email & password blank<br>3. Click Login | Empty | Form validation triggers. Both fields show required error. Login button disabled or no API call made. | EP (Invalid) | Medium |
| TC-DIG-005 | Session timeout after inactivity | User is logged in | 1. Login successfully<br>2. Leave session idle for 30 minutes<br>3. Attempt any action | — | User is automatically logged out. Redirected to login page with session expired message. | Use Case | High |
| TC-DIG-006 | Logout clears session | User is logged in | 1. Click Logout button<br>2. Press browser back button | — | User cannot access dashboard via back navigation. Redirected to login. | Use Case | High |

---

## Module 2: Content Publishing Workflow

| Test ID | Scenario | Preconditions | Test Steps | Test Data | Expected Result | Technique | Priority |
|---|---|---|---|---|---|---|---|
| TC-DIG-010 | Publish new article with all required fields | Logged in as Editor | 1. Navigate to Create Article<br>2. Fill title, body, category, thumbnail<br>3. Click Publish | Title: "Test Article"<br>Body: 200+ chars<br>Category: Technology | Article published successfully. Visible on front-end within 60 seconds. Status shows "Published". | Use Case | High |
| TC-DIG-011 | Publish article with empty title | Logged in as Editor | 1. Navigate to Create Article<br>2. Leave title blank, fill other fields<br>3. Click Publish | Title: (empty) | Form validation triggers. Article not submitted. Error: "Title is required." | EP (Invalid) | High |
| TC-DIG-012 | Publish article with title exceeding max character limit | Logged in as Editor | 1. Navigate to Create Article<br>2. Enter title with 256 characters | Title: 256-char string | System rejects input at 255 chars OR shows validation error on submit. | BVA | Medium |
| TC-DIG-013 | Save article as Draft | Logged in as Editor | 1. Fill article form partially<br>2. Click Save as Draft | Title: "Draft Test" | Article saved with status "Draft". Not visible on front-end. Accessible in Drafts tab. | Use Case | Medium |
| TC-DIG-014 | Edit published article | Logged in as Editor | 1. Open existing published article<br>2. Modify body content<br>3. Click Update | Modified body text | Changes saved and reflected on front-end. Updated timestamp recorded. | Use Case | High |
| TC-DIG-015 | Delete article | Logged in as Admin | 1. Select published article<br>2. Click Delete<br>3. Confirm deletion | — | Article removed from CMS and front-end. Cannot be accessed by direct URL. | Use Case | High |

---

## Module 3: Role-Based Access Control (RBAC)

| Test ID | Scenario | Preconditions | Test Steps | Test Data | Expected Result | Technique | Priority |
|---|---|---|---|---|---|---|---|
| TC-DIG-020 | Editor cannot access User Management | Logged in as Editor | 1. Navigate directly to /admin/users | — | Access denied. Redirected to dashboard or 403 page. | Use Case | High |
| TC-DIG-021 | Admin can create new user | Logged in as Admin | 1. Navigate to User Management<br>2. Create new user with role Editor<br>3. Save | Name: "New Editor"<br>Role: Editor | New user created. Appears in user list. Email invitation sent. | Use Case | High |
| TC-DIG-022 | Viewer cannot publish content | Logged in as Viewer | 1. Open any draft article<br>2. Attempt to click Publish | — | Publish button is hidden or disabled. No publish action possible. | Use Case | High |

---

## Module 4: Cross-Browser Compatibility

| Test ID | Scenario | Browser | Expected Result | Status |
|---|---|---|---|---|
| TC-DIG-030 | Dashboard renders correctly | Chrome (latest) | All elements visible, no layout breaks | — |
| TC-DIG-031 | Dashboard renders correctly | Safari (latest) | All elements visible, no layout breaks | — |
| TC-DIG-032 | Dashboard renders correctly | Firefox (latest) | All elements visible, no layout breaks | — |
| TC-DIG-033 | Rich text editor functions in all browsers | Chrome, Safari, Firefox | Bold, italic, image upload, link insertion all work | — |
| TC-DIG-034 | File upload works across browsers | Chrome, Safari, Firefox | Image/document upload completes, preview shown | — |

---

> **Note:** Test data and product names are based on real project experience. Sensitive business data has been anonymized.
