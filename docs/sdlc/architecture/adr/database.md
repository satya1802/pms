<!-- sdlc:auto:start adr -->
# ADR-0003: Use PostgreSQL 16 for Database

Status: Accepted  
Date: 2026-10-30

## Context and Problem Statement

Which Database technology does the project use? Decided in architecture v1.

## Considered Options

- PostgreSQL 16
- MySQL
- SQLite

## Decision Outcome

Chosen option: PostgreSQL 16, because Relational model fits employees, departments and self-referencing manager lines, and its built-in full-text search answers directory search without an extra engine at a few-thousand-record scale.

## Consequences

Full-text ranking is simpler than a dedicated search engine, which is acceptable at this scale (NFR-001).
<!-- sdlc:auto:end adr -->