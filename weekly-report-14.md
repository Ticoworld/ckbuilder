# CKBuilders Weekly Report 14: FiberLatch Access Scoping and DAO Proposal Draft

## Context

This week continued from Week 13.

Last week, FiberLatch moved from proof cleanup into access-control hardening and reusable core preparation.

After the Week 13 report, Neon suggested that the SDK direction could be useful if scoped carefully, especially as a smaller grant direction. That feedback helped clarify that FiberLatch should not grow into a broad checkout app, merchant dashboard, POS system, or generic Fiber payment gateway.

The better direction is narrower:

`paid Fiber payment -> signed access receipt -> one-time redemption`

This week focused on turning that direction into a clearer, smaller, and easier-to-review plan.

## What Became Clearer

The main thing that became clearer is that FiberLatch should be framed around access after payment, not payment collection itself.

Tools like fiber-pay focus on helping developers accept Fiber payments.

FiberLatch Access focuses on what happens after payment.

A simple way to describe the direction is:

`fiber-pay helps apps accept Fiber payments`

`FiberLatch Access helps apps decide what a paid user can access after payment`

That framing makes the project easier to understand and avoids overlapping with broader Fiber payment tooling.

## What I Focused On

This week was mainly scoping and proposal preparation.

I focused on:

- narrowing the SDK direction
- separating payment handling from access control
- deciding what should remain in the backend reference implementation
- deciding what could become a small developer-facing access package
- reducing the scope so it can fit a small Community DAO proposal
- preparing a draft proposal for private review before any public post

The goal was to avoid rushing into code or overclaiming before the direction was clear.

## Current Direction

The current direction is now **FiberLatch Access**.

FiberLatch Access would be a lightweight access-control addon for Fiber payment flows.

It would help developers with:

- creating access receipts
- verifying access receipts
- checking whether access should be allowed or denied
- showing a simple paid-resource example
- documenting how Fiber payments can connect to app-level access

The backend will remain the reference implementation.

The smaller developer tool should focus only on the reusable access-control layer.

## DAO Proposal Preparation

I also prepared a smaller proposal draft based on Neon’s feedback.

The current draft is scoped around:

- **Name:** FiberLatch Access
- **Amount:** $3,000
- **ETA:** 6 weeks
- **Scope:** one small package, one paid-resource example, documentation, and a final report
- **Hosting cost:** $0

The draft has been sent to Neon privately for feedback before any public `[DIS]` post.

This is not a formal DAO submission yet. It is still private review.

## What Is Not Being Claimed

FiberLatch is still not:

- production-ready
- mainnet-ready
- a published SDK package
- an npm package
- a full merchant product
- a checkout product
- a POS system
- a hosted payment service
- a replacement for fiber-pay

The current work is still direction, scoping, and proposal preparation.

## Current Open Point

The main open point is Neon’s feedback on the updated proposal draft.

Once the draft is reviewed, the next decision is whether to prepare it for a public `[DIS]` post or adjust the scope again.

The technical direction is now clearer, but I still want to avoid making public claims before the proposal wording and scope are reviewed properly.

## Next Step

The next step is to wait for Neon’s feedback on the draft.

After that, the likely next work is:

1. finalize the public proposal wording
2. prepare the `[DIS]` post if the scope looks right
3. keep the implementation narrow
4. begin with the smallest useful access-control package boundary
5. keep the backend as the reference implementation
6. avoid claiming a finished SDK until the package actually exists

For now, FiberLatch remains focused on the same core pattern:

`paid Fiber payment -> signed access receipt -> one-time redemption`

The next phase is making that pattern easier for other Fiber developers to reuse without copying the full backend.
