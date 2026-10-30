<!-- sdlc:auto:start adr -->
# ADR-0002: Use FastAPI 0.115 for Backend

Status: Accepted  
Date: 2026-10-30

## Context and Problem Statement

Which Backend technology does the project use? Decided in architecture v1.

## Considered Options

- FastAPI 0.115
- Django REST Framework
- Flask

## Decision Outcome

Chosen option: FastAPI 0.115, because Handles the CRUD, auth and search endpoints with built-in Pydantic validation keeping personal data clean on input, comfortably within headroom at tens of concurrent users.

## Consequences

Auth, password hashing and multipart upload need small supporting libraries rather than being bundled.
<!-- sdlc:auto:end adr -->