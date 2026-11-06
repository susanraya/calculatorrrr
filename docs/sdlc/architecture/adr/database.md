<!-- sdlc:auto:start adr -->
# ADR-0003: Use PostgreSQL 16 for Database

Status: Proposed  
Date: 2026-11-06

## Context and Problem Statement

Which Database technology does the project use? Decided in architecture v1.

## Considered Options

- PostgreSQL 16
- SQLite
- no database

## Decision Outcome

Chosen option: PostgreSQL 16, because Named per the approved stack as the platform default should a stored feature ever be added. As built there is no history, no accounts, and nothing persists, so it holds no calculator data.

## Consequences

Provisioning a database the current scope does not use adds idle cost, accepted to keep the standard platform shape ready for future persistence.
<!-- sdlc:auto:end adr -->