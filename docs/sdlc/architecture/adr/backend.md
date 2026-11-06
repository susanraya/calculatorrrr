<!-- sdlc:auto:start adr -->
# ADR-0002: Use FastAPI 0.115 for Backend

Status: Accepted  
Date: 2026-11-06

## Context and Problem Statement

Which Backend technology does the project use? Decided in architecture v1.

## Considered Options

- FastAPI 0.115
- nginx static hosting
- Node/Express static server

## Decision Outcome

Chosen option: FastAPI 0.115, because Serves the single-page app and its static files. It is lightweight, starts fast, and adds almost nothing to run since there is no server-side arithmetic or storage.

## Consequences

Using an app framework purely as a static file server is more than strictly needed, but it keeps the project on the platform-standard backend with room to add endpoints later.
<!-- sdlc:auto:end adr -->