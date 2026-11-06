<!-- sdlc:auto:start adr -->
# ADR-0004: Use AWS for Cloud

Status: Accepted  
Date: 2026-11-06

## Context and Problem Statement

Which Cloud technology does the project use? Decided in architecture v1.

## Considered Options

- AWS
- Vercel
- Netlify
- Cloudflare Pages

## Decision Outcome

Chosen option: AWS, because Because the whole calculator runs in the visitor's browser, hosting only needs to deliver a static page quickly and reliably to the general public, which AWS does comfortably at any expected traffic level, and it is the platform's standard deployment target.

## Consequences

AWS is more configuration than a pure static host for a page this simple, accepted as the standard target.
<!-- sdlc:auto:end adr -->