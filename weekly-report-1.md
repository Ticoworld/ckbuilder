# CKBuilders Weekly Report 1

## Context
I was onboarded earlier last week, and this was my first proper study/setup week on the CKBuilders track.

## What I worked on
This week I focused on getting my environment ready and understanding the basic CKB model before moving into app-side development.

- reviewed the handbook path to understand the study order
- set up OffCKB locally
- ran offckb node
- ran offckb accounts to inspect the prefunded devnet accounts
- spent time understanding the Cell Model and how it differs from the account model I was more used to

## What I understand so far
My main focus this week was the CKB mental model.

What makes sense to me now is that a Cell is immutable once created. If a live Cell holds 500 CKB and I want to send part of it out, that original Cell is consumed or in a transaction and new output Cells are created from it, usually one for the receiver and one for change, minus transaction fees for the miners.

I also got a clearer understanding of scripts:
- lock script controls who can spend a Cell
- type script adds validation rules for how a Cell can be used

## Proof of work
- OffCKB local devnet running successfully
- Devnet accounts inspected with offckb accounts
- Setup screenshot captured privately

## Blockers
for now no major blocker so far.
The main adjustment was getting used to the Cell-based way of thinking.

## Next step
Next I plan to move into the CCC path, set up the JS/TS app flow, and start interacting with the local node from code.
