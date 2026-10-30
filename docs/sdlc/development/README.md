# Development

> Maintained by QuorQ AI SDLC. Text between `sdlc:auto` markers is regenerated; anything outside them is yours and is kept.

<!-- sdlc:auto:start narrative -->
### PLAN-OVERVIEW · approved · source: plan

PMS development plan version 1 is approved and organizes work into 5 sprints of capacity 20 each, covering 5 epics and 17 user stories (US-001 through US-017) plus their task breakdowns.

Plan status: approved, version 1. Five sprints planned, each with capacity 20: Sprint 1 (auth, RBAC, logout, department structure foundation), Sprint 2 (admin-provisioned HR accounts + first full-stack employee-creation slice), Sprint 3 (edit/remove employee records, photo upload with S3), Sprint 4 (directory search/browse/profile view, org/reporting-line navigation), Sprint 5 (responsive layout polish, data-protection and in-country hosting confirmation). Backlog is grouped under 5 epics: EPIC-001 Authentication and Role-Based Access, EPIC-002 Employee Record Management, EPIC-003 Directory Search/Browse/Profile View, EPIC-004 Department and Reporting-Line Structure, EPIC-005 Data Protection and Hosting.

**Related:** US-001, US-002, US-003, US-004, US-005, US-006, US-007, US-008, US-009, US-010, US-011, US-012, US-013, US-014, US-015, US-016, US-017

- ⚠ No record of actual development execution, code artifacts, commits, or ticket completion status for any sprint -- only the plan itself was supplied.
- ⚠ No dates given for sprint start/end.

### SPRINT-1 · approved · source: plan:Sprint 1

Sprint 1 targets standing up authentication, role-based access control, logout, and the department structure that employee records will later attach to.

Goal: 'Stand up authentication, role-based access control, logout, and the department structure that employee records will attach to.' Capacity: 20 points. Likely covers stories US-001 (Email/password login), US-002 (RBAC), US-004 (Log out), and department-structure groundwork (US-013 Manage departments) based on goal wording.

**Related:** US-001, US-002, US-004, US-013

- ⚠ Input does not explicitly assign stories to this sprint -- story association above is inferred from the sprint goal text only, not stated directly.
- ⚠ No execution status (completed/in-progress/blocked) reported for this sprint.

### SPRINT-2 · approved · source: plan:Sprint 2

Sprint 2 targets administrator-provisioned HR accounts and the first full-stack vertical slice for creating an employee record with a manager assignment.

Goal: 'Enable administrator-provisioned HR accounts and ship the first full-stack vertical slice: creating an employee record with a manager assignment.' Capacity: 20 points. Likely covers US-003 (Administrator provisioning of HR/admin accounts) and US-005 (Create an employee record), which implies a manager-assignment relationship tied to US-014 (Set reporting relationships).

**Related:** US-003, US-005

- ⚠ Input does not explicitly assign stories to this sprint -- inferred from goal text only.
- ⚠ Relationship between 'manager assignment' in this sprint and story US-014 is not explicitly confirmed by the input.
- ⚠ No execution status reported for this sprint.

### SPRINT-3 · approved · source: plan:Sprint 3

Sprint 3 targets editing, removing, and photo upload for employee records, including S3 integration.

Goal: 'Support editing, removing, and photo upload for employee records, including S3 integration.' Capacity: 20 points. Likely covers US-006 (Edit an employee record), US-007 (Remove an employee record), and US-008 (Upload an employee photo).

**Related:** US-006, US-007, US-008

- ⚠ Input does not explicitly assign stories to this sprint -- inferred from goal text only.
- ⚠ No execution status reported for this sprint.

### SPRINT-4 · approved · source: plan:Sprint 4

Sprint 4 targets directory search, browse, profile viewing, and org/reporting-line navigation.

Goal: 'Deliver directory search, browse, profile viewing, and org/reporting-line navigation.' Capacity: 20 points. Likely covers US-009 (Search the directory), US-010 (Browse the directory), US-011 (View an employee profile), and US-015 (View org/department structure).

**Related:** US-009, US-010, US-011, US-015

- ⚠ Input does not explicitly assign stories to this sprint -- inferred from goal text only.
- ⚠ No execution status reported for this sprint.

### SPRINT-5 · approved · source: plan:Sprint 5

Sprint 5 targets responsive layout polish and confirming the data-protection and in-country hosting posture.

Goal: 'Polish responsive layout and confirm the data-protection and in-country hosting posture.' Capacity: 20 points. Likely covers US-012 (Responsive access on desktop and mobile browsers), US-016 (Restrict personal data to authenticated, authorized users), and US-017 (Store data within the operating country).

**Related:** US-012, US-016, US-017

- ⚠ Input does not explicitly assign stories to this sprint -- inferred from goal text only.
- ⚠ No execution status reported for this sprint.

### EPIC-001 · approved · source: plan:EPIC-001

Epic covering authentication and role-based access control for PMS, including login, RBAC, admin-provisioned accounts, and logout.

Backlog breakdown: US-001 Email/password login (8 pts, backend-agent) with tasks US-001-T1 Implement login endpoint (backend-agent), US-001-T2 Add route-guard and login page (frontend-agent), US-001-T3 Add session validation middleware (backend-agent). US-002 Role-based access control (5 pts, backend-agent). US-003 Administrator provisioning of HR/admin accounts (5 pts, backend-agent). US-004 Log out (2 pts, backend-agent).

**Related:** US-001, US-002, US-003, US-004

- ⚠ No completion/status data for any item in this epic -- only backlog definitions were provided.

### EPIC-002 · approved · source: plan:EPIC-002

Epic covering employee record management: creating, editing, removing records, and uploading employee photos.

Backlog breakdown: US-005 Create an employee record (8 pts, backend-agent) with tasks US-005-T1 Add employees table migration (backend-agent), US-005-T2 Implement create-employee endpoint (backend-agent), US-005-T3 Build create-employee form (frontend-agent). US-006 Edit an employee record (5 pts, backend-agent). US-007 Remove an employee record (5 pts, backend-agent). US-008 Upload an employee photo (8 pts, integration-agent) with tasks US-008-T1 Implement photo upload endpoint (integration-agent), US-008-T2 Add placeholder fallback (backend-agent), US-008-T3 Build photo upload UI (frontend-agent).

**Related:** US-005, US-006, US-007, US-008

- ⚠ No completion/status data for any item in this epic -- only backlog definitions were provided.
- ⚠ S3 integration mentioned in Sprint 3's goal is not explicitly tied to a specific task here (e.g. US-008-T1) beyond implication.

### EPIC-003 · approved · source: plan:EPIC-003

Epic covering directory search, browse, profile viewing, and responsive access across devices.

Backlog breakdown: US-009 Search the directory (5 pts, backend-agent). US-010 Browse the directory (5 pts, backend-agent). US-011 View an employee profile (3 pts, frontend-agent). US-012 Responsive access on desktop and mobile browsers (3 pts, frontend-agent).

**Related:** US-009, US-010, US-011, US-012

- ⚠ No completion/status data for any item in this epic -- only backlog definitions were provided.

### EPIC-004 · approved · source: plan:EPIC-004

Epic covering department management and reporting-line/org structure.

Backlog breakdown: US-013 Manage departments (5 pts, backend-agent). US-014 Set reporting relationships (5 pts, backend-agent). US-015 View org/department structure (3 pts, frontend-agent).

**Related:** US-013, US-014, US-015

- ⚠ No completion/status data for any item in this epic -- only backlog definitions were provided.

### EPIC-005 · approved · source: plan:EPIC-005

Epic covering data protection and in-country hosting requirements for PMS.

Backlog breakdown: US-016 Restrict personal data to authenticated, authorized users (3 pts, security-agent). US-017 Store data within the operating country (3 pts, devops-agent).

**Related:** US-016, US-017

- ⚠ No completion/status data for any item in this epic -- only backlog definitions were provided.
- ⚠ No industry/regulatory skill was specified in the input, so compliance-specific regulations (if any apply to this data-protection epic) could not be traced.
<!-- sdlc:auto:end narrative -->
