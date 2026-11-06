# Product Requirements

> Maintained by QuorQ AI SDLC. Text between `sdlc:auto` markers is regenerated; anything outside them is yours and is kept.

<!-- sdlc:auto:start narrative -->
## Summary

### REQ-SCOPE · approved · source: requirements:v1

Delivery scope is 'lightweight', requirements version 1. Approved technology stack: FastAPI 0.115 (serves static files only), AWS (static hosting), PostgreSQL 16 (named as platform default, unused — no data persists), React 19 (all functionality, client-side).

Product owner approved stack to design against exactly, no substitutions:
- Backend: FastAPI 0.115 — serves the single-page app and its files only; no server-side arithmetic.
- Cloud: AWS — standard deployment target, delivers a static page at any expected traffic level.
- Database: PostgreSQL 16 — named as the platform's default for future stored features; holds no calculator data as built.
- Frontend: React 19 — implements keypad, click/touch and keyboard input, the four operations, divide-by-zero handling, and decimal handling.
Out of scope: scientific functions (powers, roots, trig, logs), percentage, and memory functions (M+, M-, MR, MC).

### EPIC-001 · approved · source: requirements:EPIC-001

Number Entry epic: lets any user enter operands using digit keys 0-9 and a decimal point on a single-page keypad, no login required.

Assumption: input is via a standard calculator keypad on a single page with no login or account required. Covers US-001 (whole numbers) and US-002 (decimal numbers).

**Related:** US-001, US-002

### US-001 · approved · source: requirements:US-001

Critical story: users enter whole numbers using digit keys 0-9, which appear in sequence on the display, replacing the initial leading zero on first digit press.

AC-001: Pressing digits 4, 2 in sequence on an empty display shows "42".
AC-002: With display showing "0", pressing 7 replaces the leading zero so display shows "7".

**Related:** EPIC-001

### US-002 · approved · source: requirements:US-002

High-priority story: users can enter a decimal point to type non-integer numbers like 3.5; a second decimal point is ignored; starting with a decimal point shows "0.".

AC-003: Display "3", pressing decimal point then 5 shows "3.5".
AC-004: If current number already has a decimal point, pressing it again adds no second decimal point; number stays validly formatted.
AC-005: If display is empty or "0" and decimal point is pressed first, display shows "0." so entry stays valid.

**Related:** EPIC-001

### EPIC-002 · approved · source: requirements:EPIC-002

Arithmetic Operations and Results epic: performs addition, subtraction, multiplication and division, computes result on equals, with reasonable decimal precision, all client-side.

Covers US-003 (four basic operations), US-004 (equals computes result), US-005 (decimal precision). All calculation happens in the browser.

**Related:** US-003, US-004, US-005

### US-003 · approved · source: requirements:US-003

Critical story: calculator performs the four basic arithmetic operations — addition, subtraction, multiplication, division.

AC-006: 8 + 5 = then display shows "13".
AC-007: 9 - 4 = then display shows "5".
AC-008: 6 × 7 = then display shows "42".
AC-009: 20 ÷ 4 = then display shows "5".

**Related:** EPIC-002

### US-004 · approved · source: requirements:US-004

Critical story: pressing equals computes the result of the entered operation; pressing a digit after a result starts a new entry instead of appending.

AC-010: Entering 10 + 5 then equals shows computed result "15".
AC-011: After a result is shown from equals, pressing a digit key begins a new number entry instead of appending to the previous result.

**Related:** EPIC-002

### US-005 · approved · source: requirements:US-005

High-priority story: decimal results are shown with reasonable precision, avoiding floating-point artefacts and fitting the display.

AC-012: 0.1 + 0.2 = shows "0.3", not a long floating-point artefact.
AC-013: A division producing a repeating or very long decimal (e.g. 10 ÷ 3) is rounded to a reasonable number of decimal places and fits within the display.

**Related:** EPIC-002, NFR-003

### EPIC-003 · approved · source: requirements:EPIC-003

Clearing and Error Handling epic: a clear key resets the calculation; division by zero and invalid entries are handled with a friendly message rather than a crash.

Assumption: a single clear action resets the current calculation. Covers US-006 (clear), US-007 (divide-by-zero message), US-008 (invalid entry message).

**Related:** US-006, US-007, US-008

### US-006 · approved · source: requirements:US-006

High-priority story: pressing clear resets the calculator to a fresh state, discarding any pending operation or error.

AC-014: With a number or in-progress operation shown, pressing clear resets display to "0" and discards any pending operation.
AC-015: With an error message displayed, pressing clear dismisses it and returns the calculator to its initial ready state.

**Related:** EPIC-003

### US-007 · approved · source: requirements:US-007

High-priority story: dividing by zero shows a friendly, human-readable message instead of crashing; clear dismisses it.

AC-016: Entering a number, ÷, 0, then equals shows a friendly error message; the application does not crash or freeze.
AC-017: With a division-by-zero error displayed, pressing clear clears the message and allows a new calculation to begin.

**Related:** EPIC-003, NFR-002

### US-008 · approved · source: requirements:US-008

Medium-priority story: invalid or incomplete entries (e.g. "5 +" with no second operand, or two operators in a row) are handled gracefully without crashing.

AC-018: Pressing equals on an incomplete operation such as "5 +" causes the calculator to either wait for more input or show a friendly message, without crashing.
AC-019: Entering a malformed sequence such as two operators in a row is handled gracefully on the second operator press (e.g. by replacing the pending operator), without error or crash.

**Related:** EPIC-003, NFR-002

### EPIC-004 · approved · source: requirements:EPIC-004

Input Methods and Interface epic: a standard calculator keypad on a single page, operable by click/touch and physical keyboard.

Assumption: conventional calculator layout with digits 0-9, decimal point, four operators, equals and clear. Covers US-009 (click/touch) and US-010 (physical keyboard).

**Related:** US-009, US-010

### US-009 · approved · source: requirements:US-009

Critical story: all keypad buttons are operable by mouse click or touchscreen tap, with visible press feedback, usable on a single page without login.

AC-020: Clicking or tapping on-screen digit, operator, equals or clear buttons performs the action exactly as if typed, with visible feedback that it was pressed.
AC-021: On a touchscreen device, all keys (0-9, decimal, +, -, ×, ÷, =, clear) are visible and usable on a single page without needing to log in.

**Related:** EPIC-004, NFR-004, NFR-005

### US-010 · approved · source: requirements:US-010

High-priority story: the calculator can be operated entirely by physical keyboard — digits, decimal, operators, Enter/= to compute, Escape/Delete to clear.

AC-022: With the page focused, pressing number keys, the decimal key, +, -, * and / enters the corresponding digits, decimal point and operations.
AC-023: With the page focused, pressing Enter or = computes the result; pressing Escape or Delete clears the calculator.

**Related:** EPIC-004, NFR-005

### EPIC-005 · approved · source: requirements:EPIC-005

Open Access and Client-Side Operation epic: free, single-page app open to the public, no login, no payments, no server-side storage; scientific/percentage/memory functions out of scope.

Covers US-011 (instant open access) and US-012 (client-side calculation, nothing persisted).

**Related:** US-011, US-012

### US-011 · approved · source: requirements:US-011

High-priority story: the calculator is usable immediately on page load, with no login, sign-up, payment, or personal-detail requirement.

AC-024: On first page load, the calculator is fully usable with no login, sign-up, or account prompt.
AC-025: Performing any operation never prompts for payment, registration, or personal details — the product is free with no billing.

**Related:** EPIC-005, NFR-001

### US-012 · approved · source: requirements:US-012

Medium-priority story: all calculation happens client-side in the browser; nothing is stored or sent to a server, and nothing persists across sessions.

AC-026: Closing/reopening or refreshing the page retains no history, previous results, or account data — the calculator starts fresh.
AC-027: Computation is carried out in the browser with no data persisted to a server or database.

**Related:** EPIC-005, NFR-001

### NFR-001 · approved · source: requirements:NFR-001

Privacy: all arithmetic stays in the visitor's browser; nothing is stored or sent to a server, nothing persists between sessions, and no registration, personal details, or payment is ever requested.

Applies to US-011 and US-012. Quality requirement, not implemented as its own story.

**Related:** US-011, US-012

### NFR-002 · approved · source: requirements:NFR-002

Availability: the calculator never crashes or freezes on bad input — division by zero and incomplete/malformed entries are handled with a friendly message or by waiting for more input.

Applies to US-007 and US-008. Quality requirement, not implemented as its own story.

**Related:** US-007, US-008

### NFR-003 · approved · source: requirements:NFR-003

Usability: decimal results are shown with reasonable precision, rounded to fit the display (e.g. 0.1 + 0.2 reads as "0.3").

Applies to US-005. Quality requirement, not implemented as its own story.

**Related:** US-005

### NFR-004 · approved · source: requirements:NFR-004

Usability: on-screen keys give visible feedback when clicked/tapped and perform their action exactly as if typed.

Applies to US-009. Quality requirement, not implemented as its own story.

**Related:** US-009

### NFR-005 · approved · source: requirements:NFR-005

Compatibility: every key is usable on a single page via mouse click, touchscreen tap, and physical keyboard, across desktop and touchscreen devices, without login.

Applies to US-009 and US-010. Quality requirement, not implemented as its own story.

**Related:** US-009, US-010
<!-- sdlc:auto:end narrative -->

<!-- sdlc:auto:start summary -->
**Requirements version:** v1  
**Delivery scope:** lightweight  
**Approved:** 2026-11-06

**Capabilities in scope:** Numeric key entry for digits 0–9 and a decimal point, Addition, subtraction, multiplication and division, Equals key to compute the result, Clear key to reset the calculation, Click/touch and physical keyboard input, Friendly message for division by zero and invalid entries, Decimal results with reasonable precision, Standard calculator keypad on a single page, Open access with no login or account, All calculation in the browser with nothing stored or persisted, Free to use with no payments or billing

**Approved technology stack:**

| Layer | Choice | Rationale |
|---|---|---|
| backend | FastAPI | Your calculator does all its arithmetic in the browser and stores nothing, so there is genuinely no server-side work to do. FastAPI is included here only as the standard way to serve the single-page app and its files. It is lightweight and starts fast, so it adds almost nothing to run. |
| cloud | AWS | Because the whole calculator runs in the visitor's browser, hosting only needs to deliver a static page to the general public quickly and reliably. AWS does this comfortably at any traffic level you're likely to see, and is the platform's standard deployment target. |
| database | PostgreSQL | You confirmed there is no history, no accounts, and nothing persists between sessions — so this product does not actually need a database. PostgreSQL is named here as the platform's default should you ever add a stored feature; as built today it holds no calculator data. |
| frontend | React | Everything your product does happens here: the keypad layout, click/touch and physical-keyboard input, the four operations, the friendly divide-by-zero message, and decimal handling. React builds a single-page calculator that redraws instantly as the user types, and its keyboard-event handling covers the physical-keyboard requirement cleanly. For a fixed, well-understood interface like a calculator keypad it is a comfortable, reliable fit. |
<!-- sdlc:auto:end summary -->

<!-- sdlc:auto:start epics -->
## EPIC-001: Number Entry

Lets any user enter the numbers they want to calculate with using the numeric keys (0-9) and a decimal point, forming the operands for an arithmetic operation. Assumption: input is via a standard calculator keypad on a single page with no login or account required.

### US-001: Enter whole numbers with digit keys

**Priority:** critical

> As a calculator user, I want to enter numbers using the digit keys 0 through 9, so that I can provide the values I want to calculate with.

| ID | Given | When | Then |
|---|---|---|---|
| AC-001 | the calculator is open with an empty display | I press the digit keys 4, 2 in sequence | the display shows "42" |
| AC-002 | the display shows "0" as the initial value | I press the digit 7 | the leading zero is replaced and the display shows "7" |

### US-002: Enter decimal numbers

**Priority:** high

> As a calculator user, I want to enter a decimal point so I can type non-integer numbers, so that I can calculate with values such as 3.5.

| ID | Given | When | Then |
|---|---|---|---|
| AC-003 | the display shows "3" | I press the decimal point and then 5 | the display shows "3.5" |
| AC-004 | the current number already contains a decimal point | I press the decimal point again | no second decimal point is added and the number remains validly formatted |
| AC-005 | the display is empty or shows "0" | I press the decimal point first | the display shows "0." so the entry stays valid |

## EPIC-002: Arithmetic Operations and Results

Performs the four basic arithmetic operations — addition, subtraction, multiplication and division — on the numbers entered, and computes the result when the user presses equals. Results are shown with reasonable decimal precision. All calculation happens client-side in the browser.

### US-003: Perform the four basic operations

**Priority:** critical

> As a calculator user, I want to add, subtract, multiply and divide the numbers I enter, so that I can get the result of a basic arithmetic calculation.

| ID | Given | When | Then |
|---|---|---|---|
| AC-006 | I have entered 8 | I press +, then 5, then equals | the display shows "13" |
| AC-007 | I have entered 9 | I press -, then 4, then equals | the display shows "5" |
| AC-008 | I have entered 6 | I press ×, then 7, then equals | the display shows "42" |
| AC-009 | I have entered 20 | I press ÷, then 4, then equals | the display shows "5" |

### US-004: Compute the result with equals

**Priority:** critical

> As a calculator user, I want to press equals to compute the result of the operation I have entered, so that I can see the answer to my calculation.

| ID | Given | When | Then |
|---|---|---|---|
| AC-010 | I have entered a complete operation such as 10 + 5 | I press equals | the computed result "15" is shown on the display |
| AC-011 | a result is already shown after pressing equals | I press a digit key | a new number entry begins instead of appending to the previous result |

### US-005: Decimal results with reasonable precision

**Priority:** high

> As a calculator user, I want results involving decimals to be shown with reasonable precision, so that I can trust the answers without being overwhelmed by floating-point noise.

| ID | Given | When | Then |
|---|---|---|---|
| AC-012 | I calculate 0.1 + 0.2 | I press equals | the display shows "0.3" rather than a long floating-point artefact |
| AC-013 | I calculate a division that produces a repeating or very long decimal such as 10 ÷ 3 | I press equals | the result is rounded to a reasonable number of decimal places and fits within the display |

## EPIC-003: Clearing and Error Handling

Lets the user reset the calculation with a clear key, and handles error conditions such as division by zero and invalid entries with a friendly message rather than crashing. Assumption: a single clear action resets the current calculation.

### US-006: Clear the calculation

**Priority:** high

> As a calculator user, I want to press a clear key to reset the calculator, so that I can start a new calculation from scratch.

| ID | Given | When | Then |
|---|---|---|---|
| AC-014 | the display shows a number or an in-progress operation | I press clear | the display resets to "0" and any pending operation is discarded |
| AC-015 | the display is showing an error message | I press clear | the error is dismissed and the calculator returns to its initial ready state |

### US-007: Friendly message for division by zero

**Priority:** high

> As a calculator user, I want a friendly message instead of a crash when I divide by zero, so that I understand what went wrong and can continue.

| ID | Given | When | Then |
|---|---|---|---|
| AC-016 | I have entered a number followed by ÷ and 0 | I press equals | a friendly, human-readable error message is shown and the application does not crash or freeze |
| AC-017 | a division-by-zero error message is displayed | I press clear | the message clears and I can begin a new calculation |

### US-008: Friendly message for invalid entries

**Priority:** medium

> As a calculator user, I want a friendly message when I attempt an invalid or incomplete entry, so that I am guided rather than left with a broken interface.

| ID | Given | When | Then |
|---|---|---|---|
| AC-018 | I press equals with an incomplete operation such as "5 +" and no second operand | I attempt to compute the incomplete entry | the calculator either waits for more input or shows a friendly message, and does not crash |
| AC-019 | I attempt to enter a malformed sequence such as two operators in a row | I press the second operator | the calculator handles it gracefully (for example, replacing the pending operator) without error or crash |

## EPIC-004: Input Methods and Interface

Presents a standard calculator keypad on a single web page and lets users operate every function by both mouse/touch click and physical keyboard. Assumption: the layout is a conventional calculator with digits 0-9, decimal point, the four operators, equals and clear.

### US-009: Operate the calculator by click or touch

**Priority:** critical

> As a calculator user on any device, I want to tap or click the on-screen keypad buttons, so that I can use the calculator with a mouse or on a touchscreen.

| ID | Given | When | Then |
|---|---|---|---|
| AC-020 | the calculator page is displayed | I click or tap the on-screen digit, operator, equals or clear buttons | each button performs its action exactly as if typed, and provides visible feedback that it was pressed |
| AC-021 | the page is viewed on a touchscreen device | the keypad is shown | all keys (0-9, decimal, +, -, ×, ÷, =, clear) are visible and usable on a single page without needing to log in |

### US-010: Operate the calculator by physical keyboard

**Priority:** high

> As a calculator user with a keyboard, I want to use my physical keyboard to enter numbers and operators, so that I can calculate quickly without using the mouse.

| ID | Given | When | Then |
|---|---|---|---|
| AC-022 | the calculator page has focus | I press number keys, the decimal key, +, -, * and / keys | the corresponding digits, decimal point and operations are entered |
| AC-023 | the calculator page has focus | I press Enter or = to compute and Escape or Delete to clear | the result is computed or the calculator is cleared accordingly |

## EPIC-005: Open Access and Client-Side Operation

The calculator is a free, single-page web application open to the general public with no login or account, no payments, and no server-side storage. All calculation happens in the browser and nothing is persisted between sessions. Scientific, percentage and memory functions are explicitly out of scope.

### US-011: Immediate open access with no account

**Priority:** high

> As a member of the general public, I want to use the calculator immediately without logging in or creating an account, so that I can calculate without any barrier.

| ID | Given | When | Then |
|---|---|---|---|
| AC-024 | I open the calculator's web page as a first-time visitor | the page loads | the calculator is fully usable with no login, sign-up, or account prompt |
| AC-025 | I am using the calculator | I perform any operation | I am never asked to pay, register, or provide personal details (the product is free to use with no billing) |

### US-012: Client-side calculation with nothing persisted

**Priority:** medium

> As a privacy-conscious user, I want all calculation to happen in my browser with nothing stored, so that none of my inputs or results are saved or sent to a server.

| ID | Given | When | Then |
|---|---|---|---|
| AC-026 | I perform calculations during a session | I close and reopen the page or refresh it | no history, previous results, or account data is retained — the calculator starts fresh at its initial state |
| AC-027 | I am performing a calculation | the result is computed | the computation is carried out in the browser with no data persisted to a server or database |
<!-- sdlc:auto:end epics -->
