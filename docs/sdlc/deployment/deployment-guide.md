# Deployment Guide

> Maintained by QuorQ AI SDLC. Text between `sdlc:auto` markers is regenerated; anything outside them is yours and is kept.

<!-- sdlc:auto:start how-it-deploys -->
Pushes to `main` run `.github/workflows/deploy.yml`, which builds the API image (if there is a backend) and deploys the SPA to AWS Amplify. Commits touching only `docs/sdlc/**` don't deploy. Deployments can also be started from the platform's Deployment tab.
<!-- sdlc:auto:end how-it-deploys -->

<!-- sdlc:auto:start environments -->
| Name | Service | Runtime | Scaling | Environment |
|---|---|---|---|---|
| calculator-web | FastAPI static app server serving the React build | Python 3.12 + Uvicorn (FastAPI 0.115) | single small instance for dev; stateless and horizontally scalable | dev |
| postgres | PostgreSQL 16 (platform default, unused by current scope) | PostgreSQL 16 | single instance | dev |
<!-- sdlc:auto:end environments -->

<!-- sdlc:auto:start live -->
_Not deployed yet._
<!-- sdlc:auto:end live -->

<!-- sdlc:auto:start topology -->
```mermaid
graph LR
  n_calculator_web["calculator-web<br/>FastAPI static app server serving the React build"]
  n_postgres["postgres<br/>PostgreSQL 16 (platform default, unused by current scope)"]
  n_calculator_web -->|"TCP (provisioned per approved stack; no queries issued as built)"| n_postgres
```
<!-- sdlc:auto:end topology -->
