<!-- sdlc:auto:start adr -->
# ADR-0001: Use React 19 for Frontend

Status: Accepted  
Date: 2026-10-30

## Context and Problem Statement

Which Frontend technology does the project use? Decided in architecture v1.

## Considered Options

- React 19
- Vue
- Svelte

## Decision Outcome

Chosen option: React 19, because Responsive list-and-detail directory UI for desktop and mobile browsers, consuming the PMS REST API and gating HR/admin controls by role.

## Consequences

Web-only as scoped; no native app. Requires a routing layer and HTTP client as separate libraries.
<!-- sdlc:auto:end adr -->