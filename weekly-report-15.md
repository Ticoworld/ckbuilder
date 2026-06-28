# CKBuilders Weekly Report 15: FiberLatch Access Public DAO Discussion and Fiber Payment Readiness Research

## Context

This week continued from Week 14.

Last week, the main focus was FiberLatch Access scoping and preparing a smaller DAO proposal draft for private review.

That work clarified the direction:

`paid Fiber payment -> signed access receipt -> one-time redemption`

Week 15 moved that work forward in two ways.

First, the FiberLatch Access proposal moved from private draft preparation into public DAO discussion.

Second, I also did a separate Fiber Network research spike around payment readiness, channel setup, reserve requirements, and usable liquidity.

This was not a heavy implementation week for FiberLatch itself.

The main work was public proposal discussion, scope clarification, and manual Fiber payment-readiness research.

## What changed this week

The biggest change this week is that FiberLatch Access is no longer only a private draft.

The proposal has now moved into the public discussion stage as a `[DIS]` proposal on Nervos Talk.

That means the project direction is now being reviewed publicly instead of only being discussed privately.

The goal is still narrow:

FiberLatch Access should focus on access after payment, not payment collection itself.

Fiber proves that payment happened.

FiberLatch Access helps an application decide what that payment unlocks, for how long, and how to prevent reuse.

## FiberLatch Access public discussion

The public proposal keeps the scope small.

It does not try to turn FiberLatch into a checkout app, POS system, merchant dashboard, hosted payment service, or generic Fiber gateway.

The proposal focuses on a small access-control layer for Fiber payment flows.

The useful boundary remains:

`paid Fiber payment -> signed access receipt -> one-time redemption`

The public discussion also helped make the deliverables clearer.

The proposal is now framed around:

- a small Node.js package
- access receipt format
- signing and verification rules
- expiration rules
- replay-protection rules
- a paid-resource example
- documentation
- final report

This makes the project easier to review because it is not just saying “SDK” in a vague way.

It explains what the small package should actually help developers do.

## Community discussion and support quality

The proposal has started receiving public attention and support from the Nervos and CKBuilder community.

At the same time, I also realized that support quality matters.

Some support can come from newer accounts, so I started focusing more on getting review and feedback from active CKBuilder and Nervos community members.

The goal is not only to collect likes.

The goal is to make sure the discussion is useful, the scope is clear, and the project is reviewed by people who understand the Fiber ecosystem.

## What became clearer

This week made the FiberLatch Access pitch clearer.

The simpler explanation is:

`Fiber proves payment happened.`

`FiberLatch Access helps the app decide what that payment unlocks.`

That means FiberLatch Access sits at the application layer.

It does not replace Fiber payment tools.

It complements them by handling the access-control side after payment has been verified.

This framing is important because it avoids overlap with broader Fiber payment tooling and keeps the proposal focused.

## Fiber Network payment-readiness research

I also did a separate Fiber Network research spike connected to the new Fiber infrastructure hackathon direction.

This was not final product implementation.

The goal was to better understand practical Fiber payment-readiness issues around channel setup, usable liquidity, reserve requirements, and funding capacity.

The main thing I observed is that a payment can fail even when the wallet appears funded, because payment readiness also depends on channel state and usable capacity.

This helped me narrow the problem space for a possible infrastructure-focused hackathon build.

## Manual research spike

The manual spike helped me confirm a few practical constraints:

- channel readiness matters
- usable liquidity matters
- reserve requirements matter
- wallet balance and spendable funding capacity are not always the same thing
- better tooling could help developers understand why a Fiber payment path is or is not ready

This is still research and validation.

Product implementation for the hackathon project has not started yet.

## Why this matters

This research connects directly to Fiber infrastructure.

If developers or users do not understand channel readiness, reserve requirements, usable liquidity, and spendable funding capacity, payments can fail even when the wallet looks funded.

A useful Fiber infrastructure tool should help make those constraints easier to see and reason about.

The hackathon direction is still early, but this spike helped expose the real problem:

Fiber payment readiness is not only about having a wallet balance.

It also depends on channel state, outbound capacity, reserve requirements, and spendable funding availability.

## What is not being claimed

This week does not claim that:

- FiberLatch Access is already funded
- the DAO proposal has passed
- voting has started
- the SDK package is already published
- the Fiber hackathon product is already built
- the payment-readiness research is a finished product
- FiberLatch is production-ready
- FiberLatch is mainnet-ready

The FiberLatch Access work is currently in public DAO discussion.

The Fiber payment-readiness work is currently research and manual spike work.

Product implementation for the hackathon project has not started yet.

## Current state

Current state:

- FiberLatch Access public `[DIS]` proposal is live
- the proposal has entered community discussion
- the scope is clearer than it was in Week 14
- the proposal is still not approved or funded
- FiberLatch remains focused on access after payment
- Fiber payment-readiness research has started for the infrastructure hackathon direction
- a manual payment-readiness spike has been completed
- product implementation for the hackathon project has not started yet

## Links

FiberLatch Access public discussion:

https://talk.nervos.org/t/dis-fiberlatch-access-open-source-access-control-for-fiber-payments/10414?u=ticoworld

FiberLatch repo:

https://github.com/Ticoworld/fiber-latch

CKBuilder tracker:

https://github.com/Nervos-Community-Catalyst/CKBuilder-projects/issues/17

## Current open points

The main open points are:

- whether the FiberLatch Access proposal gets enough clean community review and support
- whether the proposal should move from discussion to voting
- how to keep the package scope small enough to deliver well
- how to continue narrowing the Fiber payment-readiness research into a small hackathon direction

## Next step

The next steps are:

1. continue answering questions on the FiberLatch Access proposal
2. get more review from active CKBuilder and Nervos community members
3. prepare for the voting stage if the discussion support is accepted
4. add the required funding address before voting if needed
5. keep FiberLatch Access narrow and avoid adding unrelated payment features
6. continue narrowing the Fiber payment-readiness research into a small hackathon direction

For now, the FiberLatch Access boundary remains:

`paid Fiber payment -> signed access receipt -> one-time redemption`

And the Fiber hackathon research direction remains:

`understand payment readiness -> identify channel/liquidity constraints -> keep the final build small and useful`
