# CKBuilders Weekly Report 12: FiberLatch Review Cleanup and Proof Hardening

## Context

This week continued from the FiberLatch live paid testnet proof in Week 11.

Last week, FiberLatch crossed its first main technical proof line. The project proved the narrow flow I had been working toward:

paid Fiber payment -> signed access receipt -> one-time redemption

A live paid Fiber testnet `payment_hash` was verified through Fiber v0.8.1 RPC, converted into a signed access receipt, verified, redeemed once, and rejected on second redemption.

That changed the project state.

FiberLatch is no longer just a local prototype. It now has a real testnet proof. But it is still not production-ready, not mainnet-ready, and not a checkout, POS, merchant dashboard, creator platform, or generic Fiber gateway.

So this week I did not try to force a new feature.

The goal was simpler:

make the public repo more accurate, safer to review, and less likely to mislead someone reading it after the proof milestone.

## What I worked on

This week I focused on review cleanup and proof hardening.

After the live paid proof landed, I audited the repo again to check whether the public docs and scripts still matched the real project state.

The main question was:

Does the repo now accurately reflect the live paid proof, or are there stale claims left from before the proof succeeded?

The audit found three concrete issues.

First, `CHANGELOG.md` still had a stale line saying no live paid Fiber verification had been proven yet. That was no longer true. The same file later described the successful proof, so the first lines contradicted the rest of the repo.

Second, `docs/overlap-guard.md` was an empty tracked file. It had no content and no references anywhere in the repo. Keeping it would only make the repo look less clean to a reviewer.

Third, `scripts/demo-live-paid-issuance.ts` had a proof-script safety issue. The script proved the live paid issuance path, but it did not throw loudly if receipt verification or the first redemption returned a non-200 response. That meant a failed verify or redeem call could print an error-like value but still exit successfully.

That was not acceptable for a proof script.

A proof script should fail loudly when the proof breaks.

## What changed

I made one focused commit for Week 12:

`9e9e1ec`

Commit message:

`fix: harden live proof script and clean stale docs`

The commit did three things:

1. Corrected the stale `CHANGELOG.md` header so it now reflects that live paid Fiber testnet verification is proven at Phase 3.

2. Removed `docs/overlap-guard.md`, which was an empty tracked file with no content and no references.

3. Hardened `scripts/demo-live-paid-issuance.ts` by adding explicit status-code checks after receipt verification and first redemption.

Now, if the live proof script hits a failed receipt verification or failed first redemption response, it throws instead of silently passing.

That matters because this script is part of the proof trail.

This was not a new product feature. It was a cleanup and correctness pass after the live proof milestone.

## Validation

After the cleanup, I ran the normal checks again:

- `npm test`
- `npm run build`
- `npm run demo:local-access`

The test suite still passes:

- 32 tests
- 3 test files
- 0 failures

The build is clean.

The local demo still proves the local receipt lifecycle:

- first redemption is granted
- second redemption is denied

So this was not just a documentation cleanup. It also made the proof script safer without changing the product scope.

## Current FiberLatch state

FiberLatch now has a cleaner public state.

The current proven claims are:

- local access receipt lifecycle works
- Fiber v0.8.1 adapter is aligned
- public Fiber testnet RPC contact is proven
- live paid Fiber testnet payment verification is proven
- a paid Fiber `payment_hash` can be converted into a signed access receipt
- the receipt can be verified
- the receipt can be redeemed once
- duplicate redemption is rejected

The current safe claim is:

FiberLatch proves a full testnet flow where a live paid Fiber `payment_hash` is verified through Fiber v0.8.1 RPC, converted into a signed access receipt, verified, redeemed once, and rejected on second redemption.

The current boundaries are still important:

- not production-ready
- not mainnet-ready
- not merchant checkout-ready
- not a POS system
- not a dashboard
- not a subscription system
- not a generic Fiber gateway
- not a replacement for Fiber node-level permissions

## Public links

FiberLatch repo:

https://github.com/Ticoworld/fiber-latch

Live paid proof release:

https://github.com/Ticoworld/fiber-latch/releases/tag/fiberlatch-live-paid-proof

Nervos Talk post:

https://talk.nervos.org/t/fiberlatch-live-paid-fiber-testnet-payment-to-signed-access-receipt/10324

CKBuilder tracker:

https://github.com/Nervos-Community-Catalyst/CKBuilder-projects/issues/17

Previous Spindle tracker:

https://github.com/Nervos-Community-Catalyst/CKBuilder-projects/issues/13

## What became clearer

The main thing that became clearer this week is that FiberLatch does not need another pivot right now.

The technical proof exists.

The next risk is overbuilding.

It would be easy to start adding UI, dashboards, checkout pages, merchant features, or a broader payment product. That would weaken the narrow proof that currently makes FiberLatch understandable.

The better direction is to keep FiberLatch focused around the access receipt layer until feedback says otherwise.

## Current blocker

The main blocker is no longer payment verification.

The main blocker is review and direction feedback.

I need to know whether the FiberLatch access-receipt model makes sense to the Fiber and CKBuilder side.

The questions are:

- Is the signed receipt model useful for Fiber-based access control?
- Is this narrow enough as a CKBuilder project?
- Should the next step stay backend-only?
- Would a small demo client help reviewers understand the proof?
- Should the next work focus on repeatability, examples, or a clearer integration path?

Until that feedback comes in, I do not want to broaden the product.

## Next step

The next useful technical step is not another large feature.

The next step should be one of these:

1. Add missing access-safety tests, such as resource or subject mismatch rejection, revoked receipt behavior, and multi-redemption behavior.

2. Make the live proof more repeatable from a fresh invoice in one clean command.

3. Add a small reviewer walkthrough only if it clearly helps reviewers understand the proof faster.

4. Wait for CKBuilder feedback before deciding whether a demo client is needed.

For now, FiberLatch will stay narrow:

paid Fiber payment -> signed access receipt -> one-time redemption

That is still the cleanest boundary.
