# Product Requirements

> Maintained by QuorQ AI SDLC. Text between `sdlc:auto` markers is regenerated; anything outside them is yours and is kept.

<!-- sdlc:auto:start narrative -->
## Summary

### REQ-SCOPE · approved · source: requirements:v1

Requirements v1 defines a lightweight-delivery, single-page arithmetic calculator with no accounts, payments, or persistence.

Delivery scope: lightweight. Requirements version: 1. In scope: digit entry (0-9) and decimal point, +, -, ×, ÷, equals, clear, click/touch and physical keyboard input, friendly division-by-zero and invalid-entry messages, decimal results with reasonable precision, standard single-page keypad, open access with no login, no payments, all calculation client-side with nothing stored. Out of scope: scientific functions (powers, roots, trig, logs), percentage, and memory functions (M+, M-, MR, MC).

**Related:** EPIC-001, EPIC-002, EPIC-003, EPIC-004, EPIC-005

### REQ-TECH-STACK · approved · source: requirements:tech-stack

Product owner approved a fixed technology stack to design and build against exactly as specified.

Backend: FastAPI 0.115 -- serves the static single-page app only; no server-side arithmetic logic. Cloud: AWS -- standard deployment target, static page delivery. Database: PostgreSQL 16 -- named as platform default but holds no calculator data since nothing persists. Frontend: React 19 -- implements the keypad, click/touch and physical-keyboard input, the four operations, divide-by-zero messaging, and decimal handling. Team is instructed to design against exactly these choices, not substitute.

### US-001 · approved · source: requirements:US-001

Critical story: users enter whole numbers using digit keys 0-9, which appear in sequence on the display.

Acceptance criteria: AC-001 - pressing 4 then 2 on an empty display shows "42". AC-002 - with display showing "0", pressing 7 replaces the leading zero so the display shows "7".

**Related:** EPIC-001, AC-001, AC-002

### US-002 · approved · source: requirements:US-002

High-priority story: users can enter a decimal point to type non-integer numbers such as 3.5.

Acceptance criteria: AC-003 - display "3", then decimal point then 5 shows "3.5". AC-004 - a second decimal point in the same number is ignored; number stays validly formatted. AC-005 - pressing decimal point first on empty/"0" display shows "0." so entry stays valid.

**Related:** EPIC-001, AC-003, AC-004, AC-005

### US-003 · approved · source: requirements:US-003

Critical story: the calculator performs the four basic arithmetic operations -- add, subtract, multiply, divide.

Acceptance criteria: AC-006 - 8 + 5 = "13". AC-007 - 9 - 4 = "5". AC-008 - 6 × 7 = "42". AC-009 - 20 ÷ 4 = "5".

**Related:** EPIC-002, AC-006, AC-007, AC-008, AC-009

### US-004 · approved · source: requirements:US-004

Critical story: pressing equals computes and displays the result of the entered operation.

Acceptance criteria: AC-010 - entering 10 + 5 then equals shows result "15". AC-011 - after a result is shown, pressing a digit key starts a new number entry instead of appending to the previous result.

**Related:** EPIC-002, AC-010, AC-011

### US-005 · approved · source: requirements:US-005

High-priority story: decimal results are shown with reasonable precision rather than raw floating-point artefacts.

Acceptance criteria: AC-012 - 0.1 + 0.2 displays as "0.3", not a long floating-point artefact. AC-013 - a long/repeating decimal such as 10 ÷ 3 is rounded to a reasonable number of decimal places and fits within the display.

**Related:** EPIC-002, NFR-003, AC-012, AC-013

### US-006 · approved · source: requirements:US-006

High-priority story: a clear key resets the calculator to start a new calculation.

Acceptance criteria: AC-014 - pressing clear while a number/operation is shown resets display to "0" and discards any pending operation. AC-015 - pressing clear while an error message is shown dismisses the error and returns to the initial ready state.

**Related:** EPIC-003, AC-014, AC-015

### US-007 · approved · source: requirements:US-007

High-priority story: dividing by zero shows a friendly message instead of crashing the app.

Acceptance criteria: AC-016 - entering a number, ÷, 0, then equals shows a friendly human-readable error message; app does not crash or freeze. AC-017 - pressing clear while the division-by-zero message is shown clears it and allows a new calculation.

**Related:** EPIC-003, NFR-002, AC-016, AC-017

### US-008 · approved · source: requirements:US-008

Medium-priority story: invalid or incomplete entries (e.g. "5 +" or two operators in a row) are handled gracefully rather than crashing.

Acceptance criteria: AC-018 - pressing equals on an incomplete operation such as "5 +" either waits for more input or shows a friendly message, without crashing. AC-019 - entering two operators in a row is handled gracefully (e.g. replacing the pending operator) without error or crash.

**Related:** EPIC-003, NFR-002, AC-018, AC-019

### US-009 · approved · source: requirements:US-009

Critical story: every keypad button is operable by mouse click or touchscreen tap with visible press feedback.

Acceptance criteria: AC-020 - clicking/tapping digit, operator, equals or clear buttons performs the action exactly as if typed, with visible feedback that the button was pressed. AC-021 - on a touchscreen, all keys (0-9, decimal, +, -, ×, ÷, =, clear) are visible and usable on a single page with no login required.

**Related:** EPIC-004, NFR-004, NFR-005, AC-020, AC-021

### US-010 · approved · source: requirements:US-010

High-priority story: the calculator is fully operable via physical keyboard.

Acceptance criteria: AC-022 - with the page focused, number keys, decimal key, +, -, *, / enter the corresponding digits, decimal point and operations. AC-023 - Enter or = computes the result; Escape or Delete clears the calculator.

**Related:** EPIC-004, NFR-005, AC-022, AC-023

### US-011 · approved · source: requirements:US-011

High-priority story: the calculator is immediately usable by the public with no login, account, or payment.

Acceptance criteria: AC-024 - on first page load, the calculator is fully usable with no login, sign-up, or account prompt. AC-025 - during use, the user is never asked to pay, register, or provide personal details; the product is free with no billing.

**Related:** EPIC-005, NFR-001, AC-024, AC-025

### US-012 · approved · source: requirements:US-012

Medium-priority story: all calculation happens client-side in the browser with nothing persisted between sessions.

Acceptance criteria: AC-026 - closing/reopening or refreshing the page retains no history, previous results, or account data; the calculator starts fresh. AC-027 - computation is carried out in the browser with no data persisted to a server or database.

**Related:** EPIC-005, NFR-001, AC-026, AC-027

### NFR-001 · approved · source: requirements:NFR-001

Privacy NFR: all arithmetic stays in the visitor's browser; nothing is stored, sent to a server, or persisted between sessions, and no registration/personal details/payment are ever requested.

Applies to US-011 and US-012. Quality attribute category: privacy.

**Related:** US-011, US-012

### NFR-002 · approved · source: requirements:NFR-002

Availability NFR: the calculator must never crash on bad input -- division by zero or incomplete/malformed entries are handled gracefully with a friendly message or by waiting for more input.

Applies to US-007 and US-008. Quality attribute category: availability.

**Related:** US-007, US-008

### NFR-003 · approved · source: requirements:NFR-003

Usability NFR: decimal results are shown with reasonable precision and rounded to fit the display, avoiding floating-point artefacts.

Applies to US-005. Quality attribute category: usability.

**Related:** US-005

### NFR-004 · approved · source: requirements:NFR-004

Usability NFR: on-screen keys must give visible feedback when pressed and perform exactly as if typed.

Applies to US-009. Quality attribute category: usability.

**Related:** US-009

### NFR-005 · approved · source: requirements:NFR-005

Compatibility NFR: every key must be usable by mouse click, touchscreen tap, and physical keyboard across desktop and touchscreen devices.

Applies to US-009 and US-010. Quality attribute category: compatibility.

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
