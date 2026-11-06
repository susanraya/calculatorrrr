<!-- sdlc:auto:start adr -->
# ADR-0001: Use React 19 for Frontend

Status: Proposed  
Date: 2026-11-06

## Context and Problem Statement

Which Frontend technology does the project use? Decided in architecture v1.

## Considered Options

- React 19
- Vue
- Svelte
- Vanilla JS

## Decision Outcome

Chosen option: React 19, because All product behaviour lives here: the keypad, click/touch and physical-keyboard input, the four operations, decimal handling, and the friendly error messages. React's component model and keyboard-event handling fit a fixed calculator interface that redraws instantly as the user types.

## Consequences

React is heavier than vanilla JS for such a small UI, but gives maintainable state management for the entry/compute/error flow and matches the approved stack.
<!-- sdlc:auto:end adr -->