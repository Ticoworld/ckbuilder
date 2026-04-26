# CKBuilders Weekly Report 6

## Context
This week I spent my time working on Spindle.

Spindle is the more focused version of my earlier Remit idea. The direction here is an API-first payment gateway for agent backends on CKB through Fiber, with policy checks and audit logging around payment execution.

## What I worked on
This week I focused on the main backend flow.

I worked on:
- API key auth using the `X-API-KEY` header
- hashing API keys instead of storing them in plain text
- route-level scope checks for things like invoice read and payment write access
- policy checks before payment execution
- rules for approved destination addresses
- max-per-action spend limits
- rolling 24-hour spend caps
- Fiber JSON-RPC integration for invoice creation, payment execution, and payment status lookup
- audit logging for auth failure, policy rejection, RPC failure, and successful actions
- duplicate in-flight payment blocking
- retry handling for already-settled invoices
- stale payment recovery and reconciliation for payments stuck in `PROCESSING`
- a `/scenarios` dashboard to show gateway outcomes with seeded data

## What became clearer
This week made the real MVP boundary clearer for me.

A few things stood out:
- the hard part is not just sending a payment, it is controlling when an agent is allowed to send one
- policy checks need to happen before Fiber is touched
- handling in-flight and half-failed payments is one of the most important parts of the gateway
- testnet integration is useful, but it also exposes edge cases quickly when node behaviour is unstable
- audit logs are not just nice to have here, they are part of making the system usable and explainable

## Blockers
The main issue this week was around edge cases, especially when payment execution gets interrupted or the node behaves inconsistently.

That forced me to spend more time on:
- duplicate execution protection
- stale payment recovery
- clearer failure handling
- making the API return honest errors instead of vague ones

## Current status
The main V1 flow is there now.

The gateway can:
- authenticate requests
- enforce route scopes
- apply policy rules
- create invoices
- execute Fiber testnet payments
- check payment status
- record audit outcomes

It is still testnet-focused, and the policy enforcement is server-side, not on-chain.

## Next step
Next I want to keep tightening the edge cases and make the payment flow more reliable under failure conditions.

I also want to improve the audit/query side and keep narrowing the product boundary so it stays honest and focused.
