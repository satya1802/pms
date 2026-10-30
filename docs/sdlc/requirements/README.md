# Product Requirements

> Maintained by QuorQ AI SDLC. Text between `sdlc:auto` markers is regenerated; anything outside them is yours and is kept.

<!-- sdlc:auto:start narrative -->
## Summary

### REQ-EPIC-001 · draft · source: requirements:EPIC-001

Defines sign-in, role-based access control, HR/admin account provisioning, and logout for PMS. Two roles exist: HR/admin and regular employee.

- US-001 (critical) Email/password login: registered users log in with email+password to reach the directory home page. AC-001: correct credentials authenticate and redirect to directory home. AC-002: a non-matching email/password combination is refused with a single generic error that does not reveal which field was wrong. AC-003: unauthenticated direct access to any directory/profile page redirects to login.
- US-002 (critical) Role-based access control: add/edit/remove restricted to HR/admin. AC-004: regular employees see read-only profiles with no add/edit/delete controls. AC-005: a regular employee attempting add/edit/remove directly is refused with an authorization error. AC-006: HR/admin users see add/edit/remove controls on directory and profiles.
- US-003 (high) Administrator provisioning of HR/admin accounts: AC-007: administrator creates an HR/admin account (email + role) and that user can log in with HR/admin privileges. AC-008: administrator can revoke an HR/admin account, after which the user can no longer log in or perform HR/admin actions.
- US-004 (medium) Log out: AC-009: logging out ends the session and returns the user to the login page. AC-010: using browser back button after logout redirects to login.
Assumptions stated in input: email/password with admin-provisioned HR accounts only (no SSO this version); exactly two roles (HR/admin, regular employee).

**Related:** US-001, US-002, US-003, US-004, NFR-003, NFR-004, NFR-005, NFR-006

### REQ-EPIC-002 · draft · source: requirements:EPIC-002

Defines HR/admin creation, editing, removal, and photo upload for employee records, including validation and reporting-line cleanup on removal.

- US-005 (critical) Create record: AC-011 HR/admin enters name, job title, department, work email, phone, manager, location/office, start date and saves; record becomes findable in directory (photo optional). AC-012: empty required field or malformed work email blocks save with a validation message. AC-013: duplicate work email blocks save with a uniqueness message.
- US-006 (high) Edit record: AC-014 changed fields save and display on profile. AC-015: invalid data (malformed email, cleared required field) is rejected with a validation message.
- US-007 (high) Remove record: AC-016 confirmed removal deletes the record from search/browse. AC-017: removing someone who is another employee's manager clears or prompts reassignment of the affected reporting relationships. AC-018: cancelling the confirmation leaves the record unchanged.
- US-008 (medium) Photo upload: AC-019 supported image uploads store to Amazon S3 and display on profile and in search results. AC-020: unsupported type or oversize file is rejected with an explanatory message, existing photo unchanged. AC-021: no-photo employees show a default placeholder image.
Epic-level assumptions: no bulk import/export and no audit log in this version; onboarding/offboarding, leave management, and document management are explicitly out of scope.

**Related:** US-005, US-006, US-007, US-008, NFR-010, NFR-011

- ⚠ Employee record field list (name, photo, title, department, work email, phone, manager, location/office, start date) is explicitly flagged in the input as assumed, not yet confirmed by the product owner.

### REQ-EPIC-003 · draft · source: requirements:EPIC-003

Defines directory search, browse/filter, profile viewing, and responsive desktop/mobile behavior for all authenticated users.

- US-009 (critical) Search: AC-022 typing part of name/job title/department into the search box returns matches with name, job title, photo. AC-023: no-match search shows a clear 'no results found' message. AC-024: results return within a few seconds at up to a few thousand records.
- US-010 (high) Browse: AC-025 directory shows a paginated or scrollable employee list. AC-026: filtering by department narrows the list accordingly.
- US-011 (critical) View profile: AC-027 selecting an employee shows name, photo, job title, department, work email, phone, manager, location/office, start date. AC-028: regular employees see all details read-only with no edit/delete controls.
- US-012 (medium) Responsive access: AC-029 mobile browser layout adapts and keeps search/browse/view usable. AC-030: desktop browser layout uses the larger screen. Assumption: web-only, responsive; no native app.
Scale assumption: up to a few thousand records, tens of concurrent users.

**Related:** US-009, US-010, US-011, US-012, NFR-001, NFR-002, NFR-009

### REQ-EPIC-004 · draft · source: requirements:EPIC-004

Defines department management and manager-based reporting-line structure, including guardrails against orphaned departments and circular reporting.

- US-013 (high) Manage departments: AC-031 employees assigned to a department appear under it when browsing/filtering. AC-032: deleting a department with employees still assigned is prevented or prompts reassignment first.
- US-014 (high) Set reporting relationships: AC-033 assigning a manager on an employee record stores and displays the relationship. AC-034: a direct circular reporting loop (A->B, B->A) is prevented with a warning.
- US-015 (medium) View org/department structure: AC-035 a profile shows the employee's manager with navigation to the manager's profile. AC-036: a manager's profile lists their direct reports.
Assumption: reporting structure is represented solely via the per-employee manager field (no separate org-chart model).

**Related:** US-013, US-014, US-015

### REQ-EPIC-005 · draft · source: requirements:EPIC-005

Requires all employee personal data to be restricted to authenticated, role-appropriate users and stored entirely within the organization's single operating country/region.

- US-016 (critical) Restrict personal data: AC-037 unauthenticated visitors are denied and receive no personal data. AC-038: authenticated regular employees can view but not create/edit/remove records.
- US-017 (high) In-country storage: AC-039 the application, relational database, and Amazon S3 photo storage are all deployed/configured so employee data resides in the organization's country/region.
Assumptions: single-country jurisdiction only (no cross-border transfer handling, no multi-region GDPR+CCPA overlap); no payment/billing functionality since this is an internal tool.

**Related:** US-016, US-017, NFR-007, NFR-008

### REQ-NFR · draft · source: requirements:non-functional-requirements

Eleven non-functional requirements cover performance, scale, security, privacy, compliance, compatibility, and one accepted maintainability risk.

- NFR-001 (performance): directory search returns within a few seconds up to a few thousand records. Applies to US-009.
- NFR-002 (scalability): supports one small-to-medium org, up to a few thousand records, tens of concurrent users. Applies to whole system.
- NFR-003 (security): all directory/profile pages and data require login; unauthenticated visitors redirected, no data returned. Applies to US-001, US-016.
- NFR-004 (security): add/edit/remove restricted to HR/admin and enforced server-side. Applies to US-002, US-016.
- NFR-005 (security): login errors never reveal which field (email or password) was wrong. Applies to US-001.
- NFR-006 (security): logout ends session; browser back button after logout returns to login. Applies to US-004.
- NFR-007 (privacy): employee records are personal data, viewable only when authenticated, changeable only by HR/admin. Applies to US-016.
- NFR-008 (compliance): all employee data and photos (DB + S3) stored within the organization's single country/region; no cross-border/multi-region handling. Applies to US-017.
- NFR-009 (compatibility): responsive layout works on desktop and mobile browsers; no native app. Applies to US-012.
- NFR-010 (performance): photo uploads limited to supported types and a size limit; invalid uploads rejected with existing photo unchanged. Applies to US-008.
- NFR-011 (maintainability, accepted risk): no audit log of who created/edited/removed records in this version; explicitly accepted as out of scope for the lightweight build. Applies to whole system.

**Related:** NFR-001, NFR-002, NFR-003, NFR-004, NFR-005, NFR-006, NFR-007, NFR-008, NFR-009, NFR-010, NFR-011, US-001, US-002, US-004, US-008, US-009, US-012, US-016, US-017

- ⚠ Performance targets are qualitative ('within a few seconds'); no precise latency SLA or photo size/type limit values are specified for architecture or testing to validate against.
- ⚠ NFR-011 accepts no audit trail as a risk -- worth reconfirming with the product owner once the system handles real personnel changes.

### REQ-TECH · approved · source: requirements:technology-stack-and-services

Product owner approved an exact technology stack and two external services for PMS; no substitutions permitted.

Technology stack (approved, design against exactly these):
- Backend: FastAPI 0.115 -- lean Python framework for CRUD, search, and role enforcement; built-in request validation for clean personal data input.
- Cloud: AWS -- single-region hosting to satisfy no-cross-border requirement; provides managed PostgreSQL and file storage under one provider.
- Database: PostgreSQL 16 -- relational model fits employee/department/manager relationships; built-in text search covers name/title lookup at this scale.
- Frontend: React 19 -- responsive web app for browse/search/profile screens on desktop and mobile; widely available talent pool.
Runtime services (approved, include exactly these):
- File storage: Amazon S3 (saas) -- stores optional employee photos in-region; env vars AWS_ACCESS_KEY_ID, AWS_SECRET_ACCESS_KEY, AWS_REGION, S3_BUCKET.
- Email: SMTP server (saas) -- sends account-setup and password-reset emails via an in-country mail server; env vars SMTP_HOST, SMTP_PORT, SMTP_USER, SMTP_PASSWORD.
Full required API key/env list: AWS_ACCESS_KEY_ID, AWS_REGION, AWS_SECRET_ACCESS_KEY, S3_BUCKET, SMTP_HOST, SMTP_PASSWORD, SMTP_PORT, SMTP_USER.

**Related:** EPIC-001, EPIC-002, EPIC-003, EPIC-004, EPIC-005

### REQ-SCOPE · draft · source: requirements:scope-summary

PMS is a lightweight employee directory: record CRUD, search/browse, profile view, department/reporting structure, and photo storage -- explicitly excluding onboarding/offboarding, leave management, and document management.

In scope: employee record creation, profile view, directory search and browse, record editing, record removal, department and reporting-line structure, employee photo upload, email/password login, standard record fields (name, photo, title, department, contact), Amazon S3 for photo storage.
Out of scope (explicitly excluded, not to be designed or built): onboarding/offboarding workflows, time-off/leave management, employee document management.
Delivery scope marked 'lightweight'; requirements version 1.

**Related:** EPIC-001, EPIC-002, EPIC-003, EPIC-004, EPIC-005
<!-- sdlc:auto:end narrative -->

<!-- sdlc:auto:start summary -->
**Requirements version:** v1  
**Delivery scope:** lightweight  
**Approved:** 2026-10-30

**Capabilities in scope:** Employee record creation, Employee profile view, Directory search and browse, Employee record editing, Employee record removal, Department and reporting-line structure, Employee photo upload, Email/password login, Standard employee record fields (name, photo, title, department, contact), Amazon S3 for employee photo storage

**Approved technology stack:**

| Layer | Choice | Rationale |
|---|---|---|
| backend | FastAPI | The product is a straightforward set of operations — create/edit/remove employee records, search, and enforce who may edit versus only view. FastAPI is a lean Python framework that covers this with little ceremony, and its built-in request validation helps keep personal data clean on the way in. At tens of concurrent users it has ample headroom. |
| cloud | AWS | You need cloud hosting with the data kept inside your single operating country. AWS has data centres in most countries and lets you pin everything to one region, which satisfies your no-cross-border requirement directly. It also provides managed PostgreSQL and file storage for photos, so the whole system lives with one provider. |
| database | PostgreSQL | Employee records, departments and manager relationships are naturally tabular and related to each other, which is exactly what a relational database is for. PostgreSQL also has strong built-in text search, so looking people up by name or title needs no extra search engine at your scale of a few thousand records. It keeps all personal data in one place you can host inside your country. |
| frontend | React | Your directory is a responsive web app that staff use to browse, search and view profiles on both desktop and mobile browsers. React handles exactly this kind of interactive, list-and-detail screen well, and because it is the most widely used option it is the easiest for you to hire for or hand over later. No native app is in scope, so a web-only framework is the right fit. |
<!-- sdlc:auto:end summary -->

<!-- sdlc:auto:start epics -->
## EPIC-001: Authentication and Role-Based Access

Users sign in with email/password credentials, and access to features is governed by two roles: HR/admin and regular employee. HR/admin accounts are provisioned by an administrator. Assumption: email/password login with admin-provisioned HR accounts is assumed; SSO is not required for this version. Assumption: two roles only (HR/admin and regular employee).

### US-001: Email/password login

**Priority:** critical

> As a registered user (HR/admin or employee), I want to log in with my email address and password, so that I can access the employee directory securely.

| ID | Given | When | Then |
|---|---|---|---|
| AC-001 | I am a registered user on the login page | I enter my correct email and password and submit | I am authenticated and taken to the directory home page |
| AC-002 | I am on the login page | I enter an email/password combination that does not match any account | I am denied access and shown an error message without revealing which field was wrong |
| AC-003 | I am not authenticated | I attempt to open any directory or profile page directly | I am redirected to the login page |

### US-002: Role-based access control

**Priority:** critical

> As a the organization, I want edit, add, and remove capabilities restricted to HR/admin users only, so that regular employees can view but not change employee records.

| ID | Given | When | Then |
|---|---|---|---|
| AC-004 | I am logged in as a regular employee | I view an employee profile | I see read-only details with no add, edit, or delete controls |
| AC-005 | I am logged in as a regular employee | I attempt to access an add/edit/remove action directly | the action is refused with an authorization error |
| AC-006 | I am logged in as an HR/admin user | I view the directory and profiles | I see add, edit, and remove controls available |

### US-003: Administrator provisioning of HR/admin accounts

**Priority:** high

> As a an administrator, I want to provision HR/admin accounts, so that only authorized staff can manage employee records.

| ID | Given | When | Then |
|---|---|---|---|
| AC-007 | I am an administrator | I create a new HR/admin account with an email and role | the account is created and that user can log in with HR/admin privileges |
| AC-008 | an HR/admin account exists | the administrator revokes it | that user can no longer log in or perform HR/admin actions. Assumption: HR/admin accounts are admin-provisioned rather than self-registered |

### US-004: Log out

**Priority:** medium

> As a an authenticated user, I want to log out of the application, so that my session cannot be used by someone else on a shared device.

| ID | Given | When | Then |
|---|---|---|---|
| AC-009 | I am logged in | I select log out | my session is ended and I am returned to the login page |
| AC-010 | I have logged out | I use the browser back button to reach a directory page | I am redirected to the login page |

## EPIC-002: Employee Record Management

HR/admin users create, update, and remove employee records. Each record holds identity and contact details. Assumption: the record fields (name, photo, job title, department, work email, phone, manager, location/office, start date) are assumed and not yet confirmed; photo is optional. Out of scope: onboarding/offboarding workflows, leave management, and document management. Assumption: no bulk import/export and no audit log in this version.

### US-005: Create an employee record

**Priority:** critical

> As a an HR/admin user, I want to add a new employee record with their identity and contact details, so that the new employee appears in the directory.

| ID | Given | When | Then |
|---|---|---|---|
| AC-011 | I am an HR/admin user on the create-employee form | I enter name, job title, department, work email, phone, manager, location/office and start date and save | the record is created and becomes findable in the directory. Assumption: these fields are assumed, not confirmed, and photo is optional |
| AC-012 | I am creating an employee record | I leave a required field such as name or work email empty, or enter a malformed work email | the record is not saved and I see a validation message identifying the problem |
| AC-013 | I am creating an employee record | I enter a work email that already belongs to another employee | the record is not saved and I am told the work email must be unique |

### US-006: Edit an employee record

**Priority:** high

> As a an HR/admin user, I want to update an existing employee's details, so that the directory stays accurate when roles or contact information change.

| ID | Given | When | Then |
|---|---|---|---|
| AC-014 | I am an HR/admin user viewing an existing employee record | I change one or more fields and save | the updated details are stored and shown on the employee's profile |
| AC-015 | I am editing an employee record | I enter invalid data such as a malformed email or clear a required field | the change is rejected and I see a validation message |

### US-007: Remove an employee record

**Priority:** high

> As a an HR/admin user, I want to remove an employee record, so that people who have left the organization no longer appear in the directory.

| ID | Given | When | Then |
|---|---|---|---|
| AC-016 | I am an HR/admin user viewing an employee record | I choose to remove it and confirm | the record is deleted and no longer appears in directory search or browse results |
| AC-017 | I remove an employee who is set as another employee's manager | the removal completes | the system prevents dangling reporting lines by clearing or prompting me to reassign the affected reporting relationships |
| AC-018 | I select remove on a record | I am asked to confirm and I cancel | the record is retained unchanged |

### US-008: Upload an employee photo

**Priority:** medium

> As a an HR/admin user, I want to upload or replace an employee's photo, so that profiles are easier to recognize.

| ID | Given | When | Then |
|---|---|---|---|
| AC-019 | I am an HR/admin user editing an employee record | I upload a supported image file | the image is stored in Amazon S3 and displayed on the employee's profile and in search results |
| AC-020 | I upload a file that is not a supported image type or exceeds the size limit | I attempt to save it | the upload is rejected with an explanatory message and the existing photo is unchanged |
| AC-021 | an employee has no photo | their profile or directory entry is displayed | a default placeholder image is shown. Assumption: photo is optional and stored in Amazon S3 |

## EPIC-003: Directory Search, Browse and Profile View

All authenticated users can browse and search the directory and view employee profiles. The experience is a responsive web app usable on desktop and mobile browsers. Assumption: scale is small-to-medium (up to a few thousand records, tens of concurrent users).

### US-009: Search the directory

**Priority:** critical

> As a an authenticated user, I want to search for employees by name and other key fields, so that I can quickly find the person I am looking for.

| ID | Given | When | Then |
|---|---|---|---|
| AC-022 | I am an authenticated user on the directory | I type part of an employee's name, job title or department into the search box | matching employees are listed with their name, job title and photo |
| AC-023 | I search for a term that matches no employees | the search completes | I see a clear 'no results found' message |
| AC-024 | a directory of up to a few thousand records | I run a search | results are returned within a few seconds. Assumption: expected scale is up to a few thousand records and tens of concurrent users |

### US-010: Browse the directory

**Priority:** high

> As a an authenticated user, I want to browse the list of employees, so that I can explore the directory without a specific search term.

| ID | Given | When | Then |
|---|---|---|---|
| AC-025 | I am an authenticated user | I open the directory | I see a paginated or scrollable list of employees that I can navigate |
| AC-026 | I am browsing the directory | I filter by department | only employees in that department are shown |

### US-011: View an employee profile

**Priority:** critical

> As a an authenticated user, I want to open an employee's profile, so that I can see their full contact and role details.

| ID | Given | When | Then |
|---|---|---|---|
| AC-027 | I am an authenticated user viewing search or browse results | I select an employee | their profile shows name, photo, job title, department, work email, phone, manager, location/office and start date |
| AC-028 | I am a regular employee viewing a profile | the profile loads | all details are read-only with no edit or delete controls |

### US-012: Responsive access on desktop and mobile browsers

**Priority:** medium

> As a an authenticated user, I want the application to work well on both desktop and mobile browsers, so that I can use the directory from any device.

| ID | Given | When | Then |
|---|---|---|---|
| AC-029 | I open the application on a mobile browser | I search, browse and view a profile | the layout adapts to the small screen and all core actions remain usable |
| AC-030 | I open the application on a desktop browser | I use the directory | the layout makes full use of the larger screen. Assumption: responsive web app only; no native mobile or desktop app |

## EPIC-004: Department and Reporting-Line Structure

HR/admin users organize employees into departments and set reporting relationships (manager) so the org structure can be represented and viewed. Assumption: reporting structure is represented via the manager field on each employee record.

### US-013: Manage departments

**Priority:** high

> As a an HR/admin user, I want to create and manage departments and assign employees to them, so that the directory reflects the organization's department structure.

| ID | Given | When | Then |
|---|---|---|---|
| AC-031 | I am an HR/admin user | I create a department and assign employees to it | those employees appear under that department when browsing or filtering by department |
| AC-032 | a department has employees assigned | I attempt to delete that department | I am prevented or prompted to reassign its employees before deletion |

### US-014: Set reporting relationships

**Priority:** high

> As a an HR/admin user, I want to assign each employee a manager, so that the reporting lines of the organization are captured.

| ID | Given | When | Then |
|---|---|---|---|
| AC-033 | I am an HR/admin user editing an employee record | I select another employee as their manager and save | the reporting relationship is stored and shown on the employee's profile |
| AC-034 | I am setting a manager | the selection would create a direct circular reporting loop (A reports to B and B reports to A) | the system prevents the invalid relationship and warns me |

### US-015: View org/department structure

**Priority:** medium

> As a an authenticated user, I want to see the reporting and department structure, so that I can understand who reports to whom and how teams are organized.

| ID | Given | When | Then |
|---|---|---|---|
| AC-035 | I am an authenticated user viewing an employee's profile | the profile loads | I can see their manager and navigate to the manager's profile |
| AC-036 | I am viewing a manager's profile | the profile loads | I can see the list of their direct reports |

## EPIC-005: Data Protection and Hosting

Employee records are personal data for staff in a single country. Access is authenticated and role-restricted, and data is stored within the single operating country on cloud hosting with a relational database. Assumption: single-country jurisdiction only; no cross-border transfer handling, no multi-region/GDPR+CCPA overlap. Assumption: no payment/billing/subscription functionality, as this is an internal tool.

### US-016: Restrict personal data to authenticated, authorized users

**Priority:** critical

> As a the organization, I want employee personal data accessible only to authenticated users with appropriate roles, so that personal data is protected from unauthorized access.

| ID | Given | When | Then |
|---|---|---|---|
| AC-037 | an unauthenticated visitor | they attempt to retrieve any employee data | access is denied and no personal data is returned |
| AC-038 | an authenticated regular employee | they access the directory | they can view profiles but cannot create, edit or remove records |

### US-017: Store data within the operating country

**Priority:** high

> As a the organization, I want all employee data and photos stored within the single operating country/region, so that we comply with the local jurisdiction's data-protection rules.

| ID | Given | When | Then |
|---|---|---|---|
| AC-039 | the application and its relational database and Amazon S3 photo storage are deployed | hosting is configured | all employee data resides in the organization's country/region. Assumption: single-country storage only; no cross-border transfer handling and no multi-region compliance overlap |
<!-- sdlc:auto:end epics -->
