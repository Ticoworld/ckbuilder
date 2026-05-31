# CKBuilders Weekly Report 11: FiberLatch Live Paid Testnet Proof

## Context

This week continued from the FiberLatch work in Week 10.

In Week 10, I moved FiberLatch beyond the local-only receipt proof and started testing against real Fiber testnet infrastructure.

That week proved a lot of the surrounding setup:

- public Fiber testnet nodes were reachable
- public node invoices could be created
- real `payment_hash` values could be returned
- local Fiber tooling was installed and working
- a local testnet account was created and funded
- a local Fiber node could start
- the local node could connect to public node1
- a channel could reach `ChannelReady`

But the main missing proof was still live paid verification.

The payment attempts were blocked around route discovery and outbound liquidity. So FiberLatch could see real public Fiber data, but it could not yet prove the full paid path.

This week, that changed.

## What I worked on

This week I focused on getting FiberLatch from real Fiber testnet attempts into a clean live paid proof.

The target was still narrow:

**paid Fiber payment -> signed access receipt -> one-time redemption**

I did not add a checkout app, POS feature, merchant dashboard, creator platform, subscription layer, off-ramp system, or generic payment gateway behavior.

The work was focused on proving the small FiberLatch boundary properly.

## Main progress this week

The main progress is that FiberLatch now has its first live paid Fiber testnet proof.

A real paid Fiber `payment_hash` was verified through Fiber `v0.8.1` RPC.

That paid signal was then converted into a signed access receipt.

The receipt was:

- issued after payment verification
- verified successfully
- redeemed once
- rejected on second redemption

That means the basic FiberLatch idea is now proven on testnet:

**a paid Fiber payment can unlock a signed access receipt, and that receipt can be used once without allowing replay.**

## Why this matters

Before this week, FiberLatch had a working local access receipt system, but the Fiber side was not proven yet.

The local proof already showed that the backend could:

- create access intents
- issue signed receipts
- expose JWKS
- verify receipts
- redeem receipts
- block replay
- record lifecycle events

But without live paid Fiber verification, the project was still missing the most important part.

This week proved that the receipt lifecycle can start from a real paid Fiber testnet signal, not just a fake local adapter.

That makes the project much stronger than it was in Week 9 and Week 10.

## Public proof

I also packaged the proof more clearly for public review.

The FiberLatch repository is public:

https://github.com/Ticoworld/fiber-latch

I created a GitHub release for the live paid proof:

https://github.com/Ticoworld/fiber-latch/releases/tag/fiberlatch-live-paid-proof

I also submitted a Nervos Talk post for the proof, and it has now been approved:

https://talk.nervos.org/t/fiberlatch-live-paid-fiber-testnet-payment-to-signed-access-receipt/10324

I opened a fresh CKBuilder tracker issue for FiberLatch:

https://github.com/Nervos-Community-Catalyst/CKBuilder-projects/issues/17

The old Spindle tracker issue was closed because Spindle has been superseded by the narrower FiberLatch direction:

https://github.com/Nervos-Community-Catalyst/CKBuilder-projects/issues/13

## Spindle status

Spindle is no longer the active project direction.

It was useful because it helped me explore Fiber payment flows, API boundaries, policy checks, audit logs, idempotency, and payment-state handling.

But the feedback made it clear that the original gateway framing was too broad.

Fiber already has its own node-level permission concepts, and the need for a broad gateway in front of Fiber was not clearly validated.

So I closed the old Spindle direction and moved the work into something narrower.

FiberLatch is the active direction now.

## What FiberLatch is

FiberLatch is a backend-only service for apps that need to unlock something after a Fiber payment is paid.

The important point is that a protected resource should not unlock just because an invoice exists.

It should unlock only after the Fiber payment is actually verified as paid.

The current boundary is:

**paid Fiber payment -> signed access receipt -> one-time redemption**

That is the whole scope for now.

FiberLatch is not trying to be:

- a checkout app
- a POS system
- a merchant dashboard
- a creator platform
- an off-ramp tool
- a subscription platform
- a generic payment gateway
- a production payment product
- a mainnet-ready service

It is still a testnet proof.

## Repo cleanup and review readiness

This week I also cleaned the public repo so the review path is clearer.

I removed scratch and planning notes that did not need to be in the public repo.

I restored a broken public docs reference with a cleaner status document.

I aligned the README and reviewer notes with the current proof state.

The repo now presents FiberLatch as the active project direction with the correct boundary:

- testnet-only proof
- live paid Fiber verification proven
- signed access receipt proven
- one-time redemption proven
- duplicate redemption rejection proven
- no production or mainnet claim

I also ran the validation checks after cleanup.

## What is proven now

The strongest proven claim is:

**FiberLatch proves a tiny live Fiber testnet flow: paid Fiber payment -> signed access receipt -> one-time redemption.**

More specifically, the current proof shows:

- a real paid Fiber `payment_hash` can be verified through Fiber `v0.8.1` RPC
- a signed access receipt can be issued from that paid signal
- the receipt can be verified
- the receipt can be redeemed once
- a second redemption attempt is rejected
- the flow can be documented and reviewed from the public repo and release

## What is not being claimed

I am keeping the boundary clear.

FiberLatch does not claim:

- production readiness
- mainnet readiness
- merchant checkout readiness
- generalized payment gateway behavior
- POS support
- off-ramp support
- creator platform support
- frontend product readiness
- broad ecosystem adoption

The current proof is real, but it is still narrow.

That is intentional.

## What became clearer

The main thing that became clearer this week is that FiberLatch is strongest when it stays small.

The project should not become another broad payment product.

The useful part is the receipt layer after payment.

That layer can be useful for apps that need to unlock:

- gated content
- downloadable files
- protected API routes
- small paid resources
- one-time access flows

The important idea is not checkout.

The important idea is what happens after payment is confirmed.

## Current status

FiberLatch is now the active CKB/Fiber project.

The old Spindle direction is closed.

FiberLatch has moved past local-only proof.

The live paid Fiber testnet proof is complete.

The public review trail now includes:

- GitHub repo
- GitHub release
- Nervos Talk post
- CKBuilder tracker issue
- closed Spindle tracker showing the old direction was replaced

Current honest summary:

**FiberLatch has proven a live paid Fiber testnet payment can be converted into a signed access receipt, verified, redeemed once, and rejected on second redemption.**

## Blockers

The main blocker is no longer live paid Fiber verification.

That part is now proven.

The next blocker is presentation and review clarity.

The flow works, but it still needs to become easier for reviewers to follow without digging through too much backend detail.

Right now, the proof is real, but it is still mostly backend-oriented.

## Next step

The next step is not another pivot.

The next step is to make the proof easier to review.

The next technical milestone is a simple reviewer-friendly walkthrough:

- create access intent
- pay through Fiber testnet
- verify paid `payment_hash`
- issue signed receipt
- verify receipt
- redeem once
- reject duplicate redemption

This could be packaged as a small demo client or a clearer proof walkthrough.

For now, I want to keep FiberLatch backend-only until feedback says a UI or demo client is actually useful.
