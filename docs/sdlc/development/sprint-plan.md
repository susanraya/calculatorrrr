# Sprint Plan

> Maintained by QuorQ AI SDLC. Text between `sdlc:auto` markers is regenerated; anything outside them is yours and is kept.

<!-- sdlc:auto:start sprints -->
## Sprint 1: Sprint 1

Core arithmetic engine (entry, operations, equals, clear) and public static hosting are in place

Capacity: 20 points · Committed: 20

| Key | Type | Title | Points | Role | Depends on |
|---|---|---|---|---|---|
| US-001 | Story | Enter whole numbers with digit keys | 3 | frontend-agent | — |
| US-002 | Story | Enter decimal numbers | 2 | frontend-agent | US-001 |
| US-003 | Story | Perform the four basic operations | 5 | frontend-agent | US-001 |
| US-004 | Story | Compute the result with equals | 3 | frontend-agent | US-003 |
| US-006 | Story | Clear the calculation | 2 | frontend-agent | US-001 |
| US-011 | Story | Immediate open access with no account | 5 | devops-agent | — |

## Sprint 2: Sprint 2

Polish: decimal precision, friendly error handling, full click/touch/keyboard input, and no-persistence confirmation

Capacity: 20 points · Committed: 17

| Key | Type | Title | Points | Role | Depends on |
|---|---|---|---|---|---|
| US-005 | Story | Decimal results with reasonable precision | 2 | frontend-agent | US-004 |
| US-007 | Story | Friendly message for division by zero | 2 | frontend-agent | US-003, US-004 |
| US-008 | Story | Friendly message for invalid entries | 3 | frontend-agent | US-003, US-004 |
| US-009 | Story | Operate the calculator by click or touch | 5 | frontend-agent | US-001, US-003, US-004, US-006 |
| US-010 | Story | Operate the calculator by physical keyboard | 3 | frontend-agent | US-009 |
| US-012 | Story | Client-side calculation with nothing persisted | 2 | frontend-agent | US-004 |

## Unscheduled

_Nothing unscheduled._
<!-- sdlc:auto:end sprints -->
