# CKBuilders Weekly Report 7: Spindle MVP Hardening and Project Tracker Submission

## Context

This week I continued from the Spindle backend work in Week 6.

Last week, the main focus was getting the gateway flow working: API key authentication, route scopes, policy checks, Fiber JSON-RPC integration, invoice/payment routes, status lookup, audit logging, duplicate blocking, retry handling, stale recovery, and seeded gateway scenarios.

This week, I focused on making Spindle easier to review as a public MVP.

Spindle is an API-first Fiber payment gateway for agent backends on CKB. The goal is to put authentication, route scopes, spend policy, invoice/payment handling, and audit/query APIs in front of automated payment requests.

## What I worked on

This week I worked on MVP hardening and public review readiness.

I worked on:

- deploying Spindle to Vercel
- connecting the deployed app to Neon Postgres
- verifying that the public app and database connection work
- refining the homepage so it explains Spindle as a narrow Fiber gateway, not a broad infrastructure platform
- tightening the Docs page into a clearer gateway reference
- improving the Scenarios page into a registry-style review surface
- improving the Trace Detail view into a more technical inspector-style surface
- cleaning up the product language so it stays focused on the real MVP boundary
- submitting Spindle to the CKBuilder project tracker for review

## Links

Live MVP:

https://spindle-nine.vercel.app

CKBuilder project tracker issue:

https://github.com/Nervos-Community-Catalyst/CKBuilder-projects/issues/13

Repository:

https://github.com/Ticoworld/spindle

## What became clearer

This week made the review and deployment boundary clearer.

A few things stood out:

- the public product surface matters because reviewers need to understand the project quickly
- the docs need to explain implemented behavior, not future claims
- seeded scenarios are useful for explaining gateway outcomes, but they must be clearly labeled
- Neon works well for the hosted Postgres side of the MVP
- the current blocker is not the database or UI anymore, it is Fiber reachability from the deployed environment

## Current status

The public MVP is deployed and connected to Neon Postgres.

The live app, docs, scenarios, and trace detail pages are reviewable.

`/api/health` confirms that the app and database are working.

The main remaining blocker is live Fiber invoice creation from the deployed environment. The current Fiber node URL is local/private, so invoice creation from Vercel returns `502`. The next step is to decide the cleanest way to make Fiber execution reachable for a public MVP demo.

## Blockers

The main blocker is public Fiber reachability.

The app can run publicly, and the database is hosted, but live Fiber invoice/payment execution needs either:

- a reachable Fiber RPC endpoint, or
- a backend environment that can run beside or reach the Fiber node

This is the next technical problem I need to solve.

## Next step

Next I want to:

- wait for feedback from Neon / CKBuilders on the tracker issue
- improve the live Fiber execution path
- decide the cleanest backend/Fiber deployment shape for demo readiness
- record a short MVP walkthrough
- keep Spindle focused as a narrow Fiber gateway for agent backend payments
