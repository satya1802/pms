# Traceability Matrix

> Maintained by QuorQ AI SDLC. Text between `sdlc:auto` markers is regenerated; anything outside them is yours and is kept.

<!-- sdlc:auto:start legend -->
Built from recorded links, not written by a model: requirement key → plan item (`source_stable_key`) → development ticket (`stable_key`) → the ticket's test steps → the last live deployment that started after the work finished. **AC tests** counts the story's acceptance criteria that have a test case, and those whose test cases all passed in the latest finished E2E run.
<!-- sdlc:auto:end legend -->

<!-- sdlc:auto:start matrix -->
| Requirement | Epic | Title | Plan items | Sprint | Design | Code | Commits | Ticket | Tests | AC tests | Deployed |
|---|---|---|---|---|---|---|---|---|---|---|---|
| US-001 | EPIC-001 | Email/password login | US-001, US-001-T1, US-001-T2, US-001-T3 | 1 | POST /auth/login, api_backend, users, web_frontend | — | — | not started | not run | 0/3 tested · 0/3 passing | — |
| US-002 | EPIC-001 | Role-based access control | US-002 | 1 | api_backend, employees, users, web_frontend | — | — | not started | not run | 0/3 tested · 0/3 passing | — |
| US-003 | EPIC-001 | Administrator provisioning of HR/admin accounts | US-003 | 2 | PATCH /admin/users/{id}, POST /admin/users, api_backend, database, users | — | — | not started | not run | 0/2 tested · 0/2 passing | — |
| US-004 | EPIC-001 | Log out | US-004 | 1 | POST /auth/logout, api_backend, users, web_frontend | — | — | not started | not run | 0/2 tested · 0/2 passing | — |
| US-005 | EPIC-002 | Create an employee record | US-005, US-005-T1, US-005-T2, US-005-T3 | 2 | POST /employees, api_backend, database, departments, employees, web_frontend | — | — | not started | not run | 0/3 tested · 0/3 passing | — |
| US-006 | EPIC-002 | Edit an employee record | US-006 | 3 | PUT /employees/{id}, api_backend, employees, web_frontend | — | — | not started | not run | 0/2 tested · 0/2 passing | — |
| US-007 | EPIC-002 | Remove an employee record | US-007 | 3 | DELETE /employees/{id}, api_backend, employees, web_frontend | — | — | not started | not run | 0/3 tested · 0/3 passing | — |
| US-008 | EPIC-002 | Upload an employee photo | US-008, US-008-T1, US-008-T2, US-008-T3 | 3 | POST /employees/{id}/photo, api_backend, employees, photo_storage, web_frontend | — | — | not started | not run | 0/3 tested · 0/3 passing | — |
| US-009 | EPIC-003 | Search the directory | US-009 | 4 | GET /employees, api_backend, database, departments, employees, web_frontend | — | — | not started | not run | 0/3 tested · 0/3 passing | — |
| US-010 | EPIC-003 | Browse the directory | US-010 | 4 | GET /employees, api_backend, departments, employees, web_frontend | — | — | not started | not run | 0/2 tested · 0/2 passing | — |
| US-011 | EPIC-003 | View an employee profile | US-011 | 4 | GET /employees/{id}, api_backend, employees, web_frontend | — | — | not started | not run | 0/2 tested · 0/2 passing | — |
| US-012 | EPIC-003 | Responsive access on desktop and mobile browsers | US-012 | 5 | web_frontend | — | — | not started | not run | 0/2 tested · 0/2 passing | — |
| US-013 | EPIC-004 | Manage departments | US-013 | 1 | DELETE /departments/{id}, GET /departments, POST /departments, api_backend, database, departments, employees, web_frontend | — | — | not started | not run | 0/2 tested · 0/2 passing | — |
| US-014 | EPIC-004 | Set reporting relationships | US-014 | 2 | PUT /employees/{id}, api_backend, employees, web_frontend | — | — | not started | not run | 0/2 tested · 0/2 passing | — |
| US-015 | EPIC-004 | View org/department structure | US-015 | 4 | GET /employees, GET /employees/{id}, api_backend, employees, web_frontend | — | — | not started | not run | 0/2 tested · 0/2 passing | — |
| US-016 | EPIC-005 | Restrict personal data to authenticated, authorized users | US-016 | 5 | api_backend, employees, users | — | — | not started | not run | 0/2 tested · 0/2 passing | — |
| US-017 | EPIC-005 | Store data within the operating country | US-017 | 5 | database, photo_storage | — | — | not started | not run | 0/1 tested · 0/1 passing | — |
<!-- sdlc:auto:end matrix -->
