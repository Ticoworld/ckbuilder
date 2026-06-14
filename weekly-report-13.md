# CKBuilders Weekly Report 13: FiberLatch Access Hardening and Reusable Core Preparation

## Context

This week continued from Weekly Report 12.

At the end of Week 12, FiberLatch already had the live paid Fiber testnet proof, and the repo had been cleaned up for review.

The open question was no longer whether FiberLatch could verify a paid Fiber payment. That part was already proven.

The open question was what should come next.

This week, I got useful feedback from Yukang on the CKBuilder issue. He confirmed that the signed receipt model makes sense for Fiber-based access control, and that:

`paid Fiber payment -> signed access receipt -> one-time redemption`

is a useful application-layer boundary.

He also pointed out that the reusable core may be more useful as an SDK or library later, while the current backend can remain a reference implementation.

So this week I focused on turning that feedback into concrete progress without pretending that FiberLatch is already a finished SDK.

## What changed this week

This week focused on three areas:

1. hardening the access-control behavior
2. adding a small protected resource demo
3. preparing a cleaner reusable core boundary

I did not add checkout, POS, dashboard, subscription, merchant tooling, or generic gateway features.

The scope stayed narrow around resource access control.

## Access-control hardening

I added more safety around receipt redemption and denial behavior.

The important boundary is:

- invalid or clearly denied receipt states should fail before atomic redemption
- `GRANTED` and `EXHAUSTED` should still be owned by the atomic redemption path

This makes the access-control flow easier to reason about.

It also avoids mixing early validation failures with the backend path that controls real one-time redemption.

## Protected resource demo

I added a small protected resource demo to make the use case clearer.

The demo shows the actual application behavior:

- no receipt -> access denied
- valid receipt -> access granted
- reused receipt -> access denied

This helps explain FiberLatch as more than a proof script.

It shows how an app could use the receipt flow to protect content, files, or an API route after a Fiber payment is verified.

## Reusable core preparation

I started cleaning the reusable core boundary.

The main change was adding an internal core entry point for reusable helpers and separating receipt claim generation from the JWT signing layer.

That matters because receipt claim generation is reusable logic, while JWT signing belongs to the backend reference implementation.

The current reusable core surface now includes:

- Fiber status mapping
- receipt claim generation
- pre-atomic redemption denial checks
- related clean domain types

This gives FiberLatch a clearer path toward a future SDK or library shape, but it does not claim that an SDK exists today.

## Validation

Latest validation is clean:

- `npm run build` passes
- full test suite passed: 57/57
- protected resource demo passes
- core barrel smoke test passes
- post-push working tree is clean

The test suite grew from Week 12:

- Week 12: 32 tests across 3 files
- Week 13: 57 tests across 8 files

This reflects the shift from proof cleanup into access-control hardening and reusable core preparation.

## Current state

FiberLatch now has:

- live paid Fiber testnet proof
- signed access receipt issuance
- receipt verification
- one-time redemption
- duplicate redemption rejection
- protected resource demo
- clearer denial behavior
- internal reusable core direction
- isolated receipt claim generation
- core entry-point smoke coverage

The current safe claim is still narrow:

FiberLatch proves a full testnet flow where a live paid Fiber `payment_hash` is verified through Fiber v0.8.1 RPC, converted into a signed access receipt, verified, redeemed once, and rejected on second redemption.

This week made that flow safer, clearer, and easier to reuse later.

## What is not being claimed

FiberLatch is still not:

- production-ready
- mainnet-ready
- a published SDK package
- an npm package
- a checkout app
- a POS system
- a merchant dashboard
- a generic Fiber gateway

The SDK or library direction has started only as reusable core preparation.

## Links

FiberLatch repo:

https://github.com/Ticoworld/fiber-latch

CKBuilder tracker:

https://github.com/Nervos-Community-Catalyst/CKBuilder-projects/issues/17

## What became clearer

The main thing that became clearer this week is that FiberLatch should stay narrow, but the reusable parts should become cleaner.

The backend can still be useful as the reference implementation, but another app should not necessarily need to call a separate backend just to reuse simple access-control logic.

The next work should keep separating dependency-light core logic from backend-only implementation details.

## Current open questions

The main open question is the best integration boundary.

In particular:

- should `custom_records` carry a resource ID or access intent reference?
- should the mapping stay outside Fiber and use `payment_hash` as the lookup key?
- what is the smallest SDK or library shape that would actually help other Fiber developers?
- how much should remain only in the backend reference implementation?

This is no longer blocked on live payment verification.

The question now is how best to make the access-control pattern reusable.

## Next step

The next useful technical steps are:

1. investigate how `custom_records` should be used for resource or access binding
2. add clearer receipt claim examples
3. continue separating reusable core logic from backend-only implementation details
4. decide later whether a small SDK or library package is justified
5. keep the protected resource demo as the main reviewer-facing example

For now, the FiberLatch boundary remains:

`paid Fiber payment -> signed access receipt -> one-time redemption`
