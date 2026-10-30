# Sprint Plan

> Maintained by QuorQ AI SDLC. Text between `sdlc:auto` markers is regenerated; anything outside them is yours and is kept.

<!-- sdlc:auto:start sprints -->
## Sprint 1: Sprint 1

Stand up authentication, role-based access control, logout, and the department structure that employee records will attach to

Capacity: 20 points · Committed: 20

| Key | Type | Title | Points | Role | Depends on |
|---|---|---|---|---|---|
| US-001 | Story | Email/password login | 8 | backend-agent | — |
| ↳ US-001-T1 | Task | Implement login endpoint | — | backend-agent | — |
| ↳ US-001-T2 | Task | Add route-guard and login page | — | frontend-agent | — |
| ↳ US-001-T3 | Task | Add session validation middleware | — | backend-agent | — |
| US-002 | Story | Role-based access control | 5 | backend-agent | US-001 |
| US-004 | Story | Log out | 2 | backend-agent | US-001 |
| US-013 | Story | Manage departments | 5 | backend-agent | US-002 |

## Sprint 2: Sprint 2

Enable administrator-provisioned HR accounts and ship the first full-stack vertical slice: creating an employee record with a manager assignment

Capacity: 20 points · Committed: 18

| Key | Type | Title | Points | Role | Depends on |
|---|---|---|---|---|---|
| US-003 | Story | Administrator provisioning of HR/admin accounts | 5 | backend-agent | US-001, US-002 |
| US-005 | Story | Create an employee record | 8 | backend-agent | US-002, US-013 |
| ↳ US-005-T1 | Task | Add employees table migration | — | backend-agent | — |
| ↳ US-005-T2 | Task | Implement create-employee endpoint | — | backend-agent | — |
| ↳ US-005-T3 | Task | Build create-employee form | — | frontend-agent | — |
| US-014 | Story | Set reporting relationships | 5 | backend-agent | US-005 |

## Sprint 3: Sprint 3

Support editing, removing, and photo upload for employee records, including S3 integration

Capacity: 20 points · Committed: 18

| Key | Type | Title | Points | Role | Depends on |
|---|---|---|---|---|---|
| US-006 | Story | Edit an employee record | 5 | backend-agent | US-005 |
| US-007 | Story | Remove an employee record | 5 | backend-agent | US-005, US-014 |
| US-008 | Story | Upload an employee photo | 8 | integration-agent | US-005 |
| ↳ US-008-T1 | Task | Implement photo upload endpoint | — | integration-agent | — |
| ↳ US-008-T2 | Task | Add placeholder fallback | — | backend-agent | — |
| ↳ US-008-T3 | Task | Build photo upload UI | — | frontend-agent | — |

## Sprint 4: Sprint 4

Deliver directory search, browse, profile viewing, and org/reporting-line navigation

Capacity: 20 points · Committed: 16

| Key | Type | Title | Points | Role | Depends on |
|---|---|---|---|---|---|
| US-009 | Story | Search the directory | 5 | backend-agent | US-005 |
| US-010 | Story | Browse the directory | 5 | backend-agent | US-005 |
| US-011 | Story | View an employee profile | 3 | frontend-agent | US-005 |
| US-015 | Story | View org/department structure | 3 | frontend-agent | US-014, US-011 |

## Sprint 5: Sprint 5

Polish responsive layout and confirm the data-protection and in-country hosting posture

Capacity: 20 points · Committed: 9

| Key | Type | Title | Points | Role | Depends on |
|---|---|---|---|---|---|
| US-012 | Story | Responsive access on desktop and mobile browsers | 3 | frontend-agent | US-009, US-010, US-011 |
| US-016 | Story | Restrict personal data to authenticated, authorized users | 3 | security-agent | US-001, US-002 |
| US-017 | Story | Store data within the operating country | 3 | devops-agent | — |

## Unscheduled

_Nothing unscheduled._
<!-- sdlc:auto:end sprints -->
