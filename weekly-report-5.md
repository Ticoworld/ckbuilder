# CKBuilders Weekly Report 5

## Context
This week I moved past the basic transfer flow and spent more time practicing some of the deeper CKB concepts through code examples.

I did not build a full advanced product around them yet, but I worked through the ideas in a more hands-on way so they would make more practical sense.

## What I worked on
This week I focused on:
- practicing how xUDT-related flow works and why native CKB is still needed when moving custom tokens
- working through the Spore idea and how digital objects relate to Cell capacity and storage
- spending time on Omnilock and what it means for wallet compatibility and onboarding
- understanding the RISC-V side of CKB and why execution works differently from the usual contract model
- looking into the off-chain and on-chain split in CKB
- learning how open transactions and aggregators help reduce contention

## What became clearer to me

### xUDT and token movement
What became clearer to me is that custom tokens on CKB still depend on the Cell model.

It is not enough to only hold the token itself. Since the token lives inside a Cell, moving it can require native CKB to support the capacity of the new Cells being created.

That made the flow feel more practical, because a wallet can hold tokens and still be unable to move them if there is not enough native CKB available.

### Spore and digital objects
I also spent time understanding Spore more clearly.

What stood out to me is that the storage side is much more tied to CKB itself than the usual NFT pattern where the asset often depends on an external link.

That made the floor value idea easier to understand because the object is tied to actual CKB capacity.

### Omnilock
Omnilock also made more sense to me this week.

The main thing that clicked is the onboarding angle. Instead of forcing users into one wallet flow, CKB can support different signature styles, which makes it easier to imagine users coming from Bitcoin, Ethereum, or passkey-style authentication.

### Execution model
I also looked more closely at the execution side.

What became clearer is that CKB is more focused on verifying the final machine-level instructions than forcing developers into one special contract language.

That makes the model feel closer to real computing than the usual smart contract setup.

### Off-chain work and on-chain verification
Another thing that became clearer is why the network can stay efficient.

The heavier work can happen off-chain, while the chain mainly verifies the result. That made the fee model and execution design easier to understand.

### Open transactions and aggregators
I also spent time looking at how CKB handles shared-state pressure.

The aggregator model made more sense once I thought of it less like a normal middleman and more like a system that helps combine signed intents into valid settlement flow.

## Proof of work
This week was not only reading. I also worked through examples around these concepts so they would not stay abstract.

The main thing I gained from that was a more practical understanding of how these ideas connect back to the Cell model.

## Blockers
The main challenge this week was making sure I was not just memorizing terms.

I had to slow down and keep checking whether the concepts actually made sense to me in practical terms.

## Next step
Next I want to keep tying these deeper concepts back to more direct code and transaction flow so they feel even more natural from practice.
