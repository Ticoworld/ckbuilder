# CKBuilders Weekly Report 2

## Context
This week was more build-focused because I took part in the Claw & Order CKB AI Agent Hackathon.

Most of my time went into trying to build and get something working, so a lot of my learning this week came from that process.

## What I worked on
This week I worked on Remit for the hackathon.

Main things I worked on:
- building the prototype flow with rules, task input, agent proposal, decision states, approval queue, and runtime log
- testing with local OffCKB
- testing with hosted testnet flow
- showing transaction hashes and explorer links
- adding approve-and-execute and reject flows for queued actions
- debugging address validation, CCC issues, and stale UI state
- cleaning up the repo, README, screenshots, demo video, and submission

## What I learned this week
This week was more hands-on than reading-focused.

A few things became clearer while building:
- local OffCKB devnet and CKB testnet behave differently, so I had to be more careful with setup
- simple prefix checks are not enough for CKB addresses, proper parsing matters
- some CCC issues were not just app logic problems, they were tied to script and dep-group assumptions
- using a server-side executor made the MVP easier to finish, but that is different from a real wallet flow
- the allow, approval-needed, and blocked flow made more sense once I saw it working through the UI

## CKB-related areas I touched
- OffCKB
- CCC
- local devnet
- CKB testnet
- RPC setup
- address parsing and validation
- transaction building and sending
- transaction hash handling
- faucet usage
- explorer links
- script and dep-group debugging
- minimum transfer and cell-capacity-related handling

## Proof of work
- hackathon repo
- hosted app
- screenshots of the UI states
- demo video
- testnet transaction hashes and explorer links
- local OffCKB testing
- updated README and setup notes

## Blockers
The main pressure this week was the hackathon deadline.

Other issues I ran into:
- address validation that looked fine in the UI but failed at execution
- differences between local devnet and testnet setup
- CCC script and dep-group issues
- stale UI state during testing
- time going into submission cleanup, screenshots, video, and hosting

## Next step
Now that the hackathon is done, my next step is to go back over the CKB parts I used during the build and tighten my understanding of them while continuing the handbook path in a more structured way.
