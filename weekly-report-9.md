# CKBuilders Weekly Report 9: From Spindle Validation to FiberLatch


This week I continued from the Spindle review work in Week 8.

Last week, I focused on validating whether Spindle’s original direction made sense after submitting it to the CKBuilder project tracker. Spindle was technically working as a public MVP surface, with Vercel deployment, Neon Postgres, API docs, scenarios, and a clear Fiber reachability blocker. But the bigger question became product fit.

The main issue was not whether Spindle could be built. The issue was whether the broad “Fiber gateway for agent backends” direction was specific enough for the current CKB/Fiber ecosystem.

After feedback from Neon and more research, I decided not to keep forcing Spindle as the main direction.

## Why I paused Spindle

Spindle helped me learn a lot about Fiber payment flows, API boundaries, policy checks, audit logs, idempotency, and payment-state handling.

But after review, the product need was still not sharp enough.

The question I kept coming back to was:

**Who needs this urgently right now?**

The answer was not clear enough.

Neon also pointed out that there may be more concrete gaps around client-side Fiber use cases, especially POS, bookkeeping, sales tracking, revenue management, and settlement/off-ramp records.

I did not want to blindly follow that suggestion either, because a broad POS or merchant dashboard can quickly become another generic product. So I treated the feedback as a signal to research deeper, not as an automatic pivot.

## What I researched

I looked at the broader Fiber direction and the projects already around it.

The important finding was that Fiber is already moving around payments, micropayments, paid content, tipping, and app-level payment flows.

But many adjacent directions already have projects or clear lanes:

- checkout UI and “Pay with Fiber” type flows
- creator memberships and paid content
- tipping and community micropayments
- paywall-style demos
- POS and merchant payment experiments

Because of that, I did not want to build another checkout button, creator platform, POS tool, merchant accounting dashboard, or generic payment gateway.

The sharper gap I found was smaller:

**After a Fiber payment is verified, how does an app issue access safely and prove that access later?**

That became the starting point for FiberLatch.

## New direction: FiberLatch

This week I started a new project called **FiberLatch**.

FiberLatch is a backend-only service that turns a verified payment signal into a signed access receipt.

The simple idea is:

**verified payment signal → signed access receipt → unlock content, files, or API access**

FiberLatch is not trying to be Spindle.

It is also not trying to be:

- a checkout UI
- a creator platform
- a POS system
- a merchant dashboard
- an accounting tool
- a subscription platform
- an off-ramp product
- a generic payment gateway
- a raw Fiber RPC wrapper

The scope is intentionally narrow.

## What FiberLatch is now

FiberLatch is currently a backend-only service.

It is:

- single-tenant
- testnet-first
- scoped to access control
- focused on signed receipts
- built to prove the access lifecycle before adding real Fiber testnet verification

The project is designed for apps that need to unlock something after payment, such as:

- gated content
- a downloadable file
- a protected API route
- a small paid resource

## What I built this week

I built the backend skeleton with:

- Fastify
- TypeScript
- Prisma
- SQLite
- Zod
- tests

I added the first public API contract under `/v1`:

- `POST /v1/access-intents`
- `GET /v1/access-intents/:id`
- `POST /v1/receipts/verify`
- `POST /v1/receipts/redeem`
- `GET /.well-known/jwks.json`
- `GET /health`

I added persisted models for:

- `ResourcePolicy`
- `AccessIntent`
- `AccessReceipt`
- `EventLog`

I also added:

- signed JWT/JWS receipts
- JWKS support
- atomic redemption
- replay protection
- exhaustion handling
- idempotent access intent creation
- reconciliation worker
- fake Fiber adapter for local development
- real Fiber adapter shape for future testnet work
- safe live-test script for future Fiber proof
- local end-to-end demo script
- quickstart docs
- reviewer notes
- API contract docs
- state machine docs
- non-goals docs

## What is proven now

The local receipt lifecycle works end to end.

The current implementation proves:

- an access intent can be created
- receipt issuance works locally
- signed receipts can be verified
- JWKS works
- receipts can be redeemed
- replay is blocked
- exhausted receipts are handled
- lifecycle events are recorded
- the reviewer can run a local demo and understand the flow

This is the main thing FiberLatch proves right now:

**A verified payment signal can be converted into a signed access receipt, and that receipt can be verified or redeemed safely.**

## What is not proven yet

The important missing piece is real Fiber testnet verification.

FiberLatch does **not** yet prove:

- real Fiber testnet payment verification
- real Fiber RPC envelope and auth behavior
- any live Fiber payment reference
- production readiness
- mainnet usage

The current local demo uses the fake Fiber adapter to prove the receipt lifecycle.

That is intentional for now, but it is still a real boundary.

## What became clearer

The most important lesson this week was that I should not keep building around a vague thesis.

Spindle was technically useful, but the direction was still too broad.

FiberLatch is narrower because it focuses on one exact layer:

**payment verified → receipt issued → access unlocked**

That makes the project easier to reason about and easier to review.

It also avoids competing directly with existing Fiber-related work around checkout, creator platforms, tipping, or POS.

## Current status

FiberLatch is at a clean reviewable stopping point.

The local access-receipt system works.

The docs explain the scope and non-goals.

The proof boundary is clear.

The project is not claiming real Fiber testnet proof yet.

Current honest summary:

**FiberLatch has a complete local access-receipt system. It is ready for real Fiber testnet proof, but that proof has not happened yet.**

Repository:

https://github.com/Ticoworld/fiber-latch

## Blockers

The main blocker is real Fiber testnet verification.

The next step is to connect the real Fiber adapter and prove one Fiber-backed verification flow.

The target is:

- create or reference a real Fiber payment
- verify payment status through Fiber
- issue a signed access receipt from that signal
- redeem the receipt successfully
- document the command output clearly

## Next step

Next I want to focus on Phase 2:

**Real Fiber testnet proof.**

The goal is not to add a frontend or broaden the product.

The goal is to prove one real Fiber-backed payment verification path through the FiberLatch receipt lifecycle.

After that, FiberLatch can move from a local backend prototype to a stronger Fiber-backed proof of concept.
