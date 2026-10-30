<!-- sdlc:auto:start adr -->
# ADR-0004: Use AWS for Cloud

Status: Accepted  
Date: 2026-10-30

## Context and Problem Statement

Which Cloud technology does the project use? Decided in architecture v1.

## Considered Options

- AWS
- Azure
- GCP

## Decision Outcome

Chosen option: AWS, because Single-region RDS PostgreSQL and S3 pin all employee data and photos inside the operating country, satisfying in-country residency with one provider.

## Consequences

Single-region/single-AZ dev footprint keeps cost low but offers no multi-region resilience, which is out of scope.
<!-- sdlc:auto:end adr -->