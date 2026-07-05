# CKBuilders Weekly Report 16: FiberLatch Access Voting Approval and Fiber Hackathon Preparation

## Context

This week continued from Week 15.

Last week, FiberLatch Access moved from private proposal drafting into public `[DIS]` discussion.

Week 15 also included early Fiber payment-readiness research connected to the Fiber infrastructure hackathon direction.

Week 16 moved both tracks forward.

For FiberLatch Access, the proposal moved from public discussion into voting and was marked approved.

For the Fiber infrastructure hackathon direction, I continued working from the payment-readiness research, but I am keeping the implementation details limited until the final submission is ready.

The two tracks are still separate:

- FiberLatch Access is the DAO proposal around access control after Fiber payment.
- The hackathon work is a separate Fiber infrastructure direction around payment readiness.

## What changed this week

The biggest update this week is that FiberLatch Access moved from discussion into the DAO voting stage.

The proposal passed the voting threshold and was marked approved.

This is an important step, but it does not mean the work is already delivered.

The approved scope is still small and focused:

`paid Fiber payment -> signed access receipt -> one-time redemption`

I also continued keeping the project positioned as an access-control layer after payment, not a payment collection tool, checkout product, POS system, merchant dashboard, or hosted service.

## FiberLatch Access voting update

The FiberLatch Access proposal moved from `[DIS]` to `[VOT]`.

The vote passed and the proposal was marked approved.

The proposal received support through the DAO process, with review and support from the CKBuilder, Nervos, and DAO community.

This helps confirm that the access-control direction is worth building.

At the same time, I still want to keep the implementation disciplined.

The goal is not to expand the scope just because the proposal passed.

The goal is to deliver the small access-control package and reference example properly.

## Scope discipline

I am keeping the FiberLatch Access scope narrow.

FiberLatch Access should focus on what happens after a Fiber payment is verified.

The simple framing remains:

`Fiber proves payment happened.`

`FiberLatch Access helps the app decide what that payment unlocks.`

The approved work should not turn into:

- a checkout app
- a POS system
- a merchant dashboard
- a hosted payment service
- a generic Fiber payment gateway
- a replacement for existing Fiber payment tools

The backend remains the reference implementation.

The smaller package should focus on the reusable access-control layer.

## FiberLatch Access build preparation

Now that the proposal has passed voting, I started preparing the first build phase.

The next implementation work needs to begin with the core boundaries, not extra features.

The important areas to prepare are:

- access receipt format
- signing and verification rules
- expiration rules
- replay-protection rules
- package boundary
- paid-resource example plan
- documentation structure

This keeps the first build phase focused and easier to review.

## Fiber infrastructure hackathon progress

Alongside the FiberLatch Access voting update, I also worked on a separate Fiber Network infrastructure hackathon direction.

This continued from the Week 15 payment-readiness research.

The work focused on understanding and improving how developers reason about Fiber payment readiness, especially around channel state, liquidity, reserve requirements, and funding capacity.

I made progress turning the earlier manual research into a more structured local tool, but I am keeping the details limited until the hackathon submission is finalized.

The main goal is still simple:

`detect payment readiness -> identify channel/liquidity issues -> help make the payment path easier to reason about`

## Validation

I ran local checks against the current hackathon work and continued testing the payment-readiness flow.

The current work is still being prepared for final submission, so I am not treating it as production infrastructure or a finished public tool yet.

I also continued reviewing the FiberLatch Access scope so the approved DAO work can start from a clean and narrow implementation plan.

## Why this matters

This week matters because FiberLatch Access moved from proposal discussion into an approved DAO direction.

That means the next phase is no longer just explaining the idea.

The next phase is delivering the approved scope carefully.

The hackathon work also matters because the Fiber payment-readiness research from Week 15 is now becoming more practical.

It is helping me understand what kind of infrastructure support developers may need when a payment path is not ready yet.

## What is not being claimed

This week does not claim that:

- FiberLatch Access delivery is already complete
- grant funds have already been received
- the FiberLatch Access package is already published
- FiberLatch Access is production-ready
- FiberLatch Access is mainnet-ready
- the hackathon project has already been submitted
- the hackathon project has won anything
- the hackathon work is production infrastructure
- the local hackathon work proves all real network cases

The FiberLatch Access proposal has passed voting, but delivery still needs to begin properly.

The hackathon work is still being prepared for final submission.

## Current state

Current state:

- FiberLatch Access moved from discussion to voting
- the vote passed and the proposal was marked approved
- FiberLatch Access implementation planning has started
- the scope remains narrow around access control after payment
- separate Fiber infrastructure hackathon work is in progress
- the hackathon direction is based on payment-readiness research from Week 15
- final demo, writeup, and submission polish are still pending

## Links

FiberLatch Access public discussion:

https://talk.nervos.org/t/dis-fiberlatch-access-open-source-access-control-for-fiber-payments/10414?u=ticoworld

FiberLatch repo:

https://github.com/Ticoworld/fiber-latch

CKBuilder tracker:

https://github.com/Nervos-Community-Catalyst/CKBuilder-projects/issues/17

## Current open points

The main open points are:

- confirming the next administrative step after the FiberLatch Access vote approval
- preparing the first FiberLatch Access implementation milestone
- keeping the FiberLatch Access scope small and deliverable
- continuing the Fiber infrastructure hackathon work without exposing too much before submission
- preparing the final hackathon demo and writeup

## Next step

The next steps are:

1. confirm the next step after FiberLatch Access voting approval
2. prepare the first FiberLatch Access build milestone
3. keep the implementation focused on the approved access-control scope
4. continue preparing the Fiber infrastructure hackathon build for final submission
5. record the short hackathon demo video
6. finalize the hackathon submission writeup and links
7. do one final cold review before submission

For now, the FiberLatch Access boundary remains:

`paid Fiber payment -> signed access receipt -> one-time redemption`

And the Fiber hackathon direction remains:

`detect payment readiness -> identify channel/liquidity issues -> make the payment path easier to reason about`
