# CKBuilders Weekly Report 3 and 4

## Context
I missed the Week 3 update while I was deep in development, so I am combining Week 3 and Week 4 here.

After the hackathon push in the previous update, I wanted to spend more time working through direct CKB exercises in code so the core flow would make more sense to me beyond the project context.

## What I worked on
These two weeks were more focused on hands-on CKB work inside a React app.

I worked on:
- setting up a React frontend around the CCC flow using `useCcc()`
- querying the balance of Account 0 from local OffCKB devnet and converting Shannon to CKB
- building and signing a transfer transaction to send 100 CKB to Account 1
- storing the text `Hello Ghost Mode` on chain by writing it into Cell data
- scanning Cells with `client.findCells(...)` to locate the stored message and decode it back into readable text
- working through xUDT structure more directly
- formatting token amounts into the required 16-byte little-endian form with `ccc.numToBytes(5000, 16)`
- building the mint flow by generating the xUDT args from the lock script hash, fetching the known xUDT script, adding the required cell deps, and constructing the token output

## What became clearer to me
These two weeks helped me understand the basic flow better because I was no longer only thinking about it in theory.

A few things made more sense while doing the exercises:
- checking balance through code made the live Cell idea feel more practical
- sending CKB made the input, output, and change flow easier to picture
- storing text on chain made capacity feel less abstract because I had to think about the box needing enough room for both the structure and the data
- reading the stored message back by scanning Cells made the data model click better
- xUDT started to make more sense once I broke it into three parts: lock script for ownership, type script for the token rule, and data for the token amount

## Week 3 progress
Week 3 was mostly about the basic read and write flow.

I got a React app running against local OffCKB devnet and used CCC through `useCcc()`.

From there I:
- checked the balance of Account 0
- built the send flow for 100 CKB to Account 1
- stored `Hello Ghost Mode` as Cell data
- added a read flow that scans Cells and decodes the stored message back into text

That part was useful because it forced me to see CKB less as a concept and more as something I could interact with directly from code.

## Week 4 progress
Week 4 was more about tokens and structure.

I spent time working through the xUDT side and trying to understand how the token box is actually shaped.

I worked on:
- formatting a human token amount into the required on-chain form
- generating the xUDT args from the lock script hash
- fetching the known xUDT script through CCC
- attaching the xUDT dependency
- building the token output with lock, type, capacity, and token data

That helped me see more clearly that the token amount is not some abstract balance field. It is strict data sitting in the Cell in the required 16-byte format.

## Proof of work
- React app using CCC through `useCcc()`
- balance check flow
- transfer flow
- store-data flow
- read-data flow
- token data formatting flow
- xUDT mint flow in code
- local OffCKB devnet usage through these exercises

If the mint transaction is what I end up keeping as the final proof for this stage, the tx hash is:

`0x965e62f059408d7c0f30bf5fd9bc96fc61fdee71438e503b73bde7f2d7bcb5fbc`

## Blockers
The main issue in this stretch was less about setup and more about making sure I was not just copying patterns without understanding what each part was doing.

I also had to be more careful around:
- how data is encoded before writing it on chain
- how Cells are searched when reading data back
- how token data has to be formatted exactly
- how script deps fit into the minting flow

## Next step
Next I want to keep tightening the basics so the flow feels more natural and less like I am following steps mechanically.

The next things I want to improve are:
- getting even more comfortable with transaction structure
- understanding xUDT flow more confidently
- cleaning up the app-side code so the exercises feel more intentional and easier to explain
