# PMS — SDLC Documentation

> Maintained by QuorQ AI SDLC. Text between `sdlc:auto` markers is regenerated; anything outside them is yours and is kept.

<!-- sdlc:auto:start overview -->
Simple people management system

**Documentation version:** v1
<!-- sdlc:auto:end overview -->

## Contents

<!-- sdlc:auto:start contents -->
| Document | State |
|---|---|
| [Requirements](requirements/README.md) | v1 approved |
| [Architecture](architecture/README.md) | 1 entry |
| [Development](development/README.md) | 1 entry |
| [Testing](testing/README.md) | 1 entry |
| [Deployment](deployment/README.md) | 1 entry |
| [Maintenance](maintenance/README.md) | 1 entry |
| [Data model](architecture/data-model.md) | not generated yet |
| [API (OpenAPI)](architecture/api/openapi.yaml) | not generated yet |
| [Decisions (ADRs)](architecture/adr/README.md) | 0 decisions |
| [Sprint plan](development/sprint-plan.md) | not generated yet |
| [Developer guide](development/developer-guide.md) | not generated yet |
| [API reference](development/api-reference.md) | 0 routes |
| [Test report](testing/test-report.md) | not run yet |
| [Tests](testing/test-cases.md) | 0 tests |
| [Deployment guide](deployment/deployment-guide.md) | not deployed yet |
| [Runbook](deployment/runbook.md) | not deployed yet |
| [Release notes](deployment/release-notes.md) | 0 releases |
| [Traceability matrix](traceability-matrix.md) | 17 requirements |
| [Changelog](CHANGELOG.md) | 1 version |
<!-- sdlc:auto:end contents -->

## Open gaps

<!-- sdlc:auto:start open-gaps -->
### Requirements

- Employee record field list (name, photo, title, department, work email, phone, manager, location/office, start date) is explicitly flagged in the input as assumed, not yet confirmed by the product owner.
- Performance targets are qualitative ('within a few seconds'); no precise latency SLA or photo size/type limit values are specified for architecture or testing to validate against.
- NFR-011 accepts no audit trail as a risk -- worth reconfirming with the product owner once the system handles real personnel changes.

### Architecture

- Architecture phase has not started: no system design, component diagrams, API design, data model, or deployment topology have been recorded beyond the technology stack and services already approved in the requirements phase.

### Development

- Development phase has not started: no sprint plans, tickets, code, or implementation notes exist yet to document.

### Testing

- Testing phase has not started: no test plans, test cases, or results exist yet to verify any of the requirements' acceptance criteria.

### Deployment

- No deployment recorded yet: AWS hosting, in-region configuration, and environment/secrets setup (AWS_ACCESS_KEY_ID, AWS_SECRET_ACCESS_KEY, AWS_REGION, S3_BUCKET, SMTP_HOST, SMTP_PORT, SMTP_USER, SMTP_PASSWORD) have not been confirmed as provisioned.

### Maintenance

- No maintenance notes exist yet: there is no deployed system in operation to generate incidents, fixes, or follow-up work.
<!-- sdlc:auto:end open-gaps -->
