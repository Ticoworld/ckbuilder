# CKBuilders Weekly Report 10: FiberLatch Real Fiber Testnet Attempts

## Context

This week I continued from the FiberLatch work in Week 9.

Last week, I moved from Spindle validation into FiberLatch. The goal was to narrow the problem instead of forcing Spindle forward as a broad Fiber gateway.

FiberLatch is focused on one smaller flow:

**verified Fiber payment signal -> signed access receipt -> unlock content, files, or API access**

At the end of Week 9, the local receipt flow was working. FiberLatch could create access intents, issue signed receipts, expose JWKS, verify receipts, redeem receipts once, block replay, and record lifecycle events.

The missing part was real Fiber testnet verification.

So this week I focused on trying to move FiberLatch from local proof into real Fiber testnet behavior.

## What I worked on

This week I focused on the real Fiber testnet path.

The target was to:

- align the real Fiber adapter with the current Fiber RPC shape
- connect to public Fiber testnet nodes
- create or reference a real Fiber invoice
- get a real `payment_hash`
- try to pay the invoice from a local Fiber node
- verify the paid status through FiberLatch
- issue a signed access receipt only after real payment verification

I did not add a frontend, checkout UI, dashboard, POS feature, creator tool, or merchant feature this week.

The work was mostly about proof and integration.

## Adapter alignment

The first thing I had to fix was the real Fiber adapter.

The local receipt flow worked, but the real adapter still had assumptions that were too generic.

So I checked it against the Fiber `v0.8.1` RPC shape and updated the adapter around the actual RPC style.

I worked around:

- `new_invoice`
- `get_invoice`
- `get_payment`
- JSON-RPC params as an array with one object
- `payment_hash` instead of a generic payment reference
- invoice statuses like `Open`, `Received`, `Paid`, `Expired`, and `Cancelled`
- payment statuses like `Created`, `Inflight`, `Success`, and `Failed`

I also updated the tests to use official-shaped mocked responses, so the adapter is no longer only shaped around the fake local flow.

This did not prove live paid verification yet, but it removed one real blocker.

## Public Fiber node testing

After the adapter alignment, I tested public Fiber testnet nodes.

I was able to reach public nodes and confirm they were running Fiber `0.8.1`.

I tested:

- public node1
- public node2
- `node_info`
- `new_invoice`
- `get_invoice`

The public node path worked.

On public node2, I was able to create a real invoice and get a real `payment_hash`.

When I queried the invoice by `payment_hash`, Fiber returned the invoice status as:

`Open`

That was expected because the invoice had not been paid yet.

This was still useful because FiberLatch was no longer only working with fake local data. It could now reach real public Fiber testnet RPC, create an invoice, and correctly see that the invoice was unpaid.

FiberLatch also correctly refused to issue a receipt because the invoice was not `Paid`.

That is the right behavior.

## Local Fiber payer setup

The next step was trying to pay the invoice.

For that, I needed a local Fiber node.

This turned into a proper environment setup task.

At first, the machine did not have the required local Fiber tooling ready.

I installed and verified:

- `fnn Fiber v0.8.1`
- `fnn-cli 0.8.1`
- `fnn-migrate 0.8.1`
- `ckb-cli 2.0.0`

I kept the tool binaries and local runtime folder outside the FiberLatch repo so that no local node data, key files, or runtime files would be committed by mistake.

## Account and funding

I created a local CKB testnet account using `ckb-cli`.

I was careful not to expose private material.

Only public information like the testnet address, `lock_arg`, and `lock_hash` was kept as evidence. No private key, seed phrase, password, keystore JSON, or local node data was committed.

The testnet address was funded through the Nervos faucet.

After funding, I exported the key into the external Fiber node directory, still outside the repo.

At that point, I had a funded local account and could start the local Fiber node.

## Local Fiber node and channel

I started the local Fiber node successfully.

The node returned `node_info`, showed Fiber `0.8.1`, and used the funded key.

Then I connected the local node to public node1.

The first CLI attempt had a multiaddr issue, but the raw JSON-RPC call worked.

After that, I opened a channel from the local node to public node1.

The channel first entered funding negotiation, then reached:

`ChannelReady`

This was an important step because it proved the local node was not just running locally. It was connected to the public Fiber network and had a ready channel to public node1.

## Payment attempt

After the channel reached `ChannelReady`, I created a fresh invoice on public node2.

The invoice returned a real `invoice_address` and a real `payment_hash`.

Then I tried to pay that invoice from the local node.

The first real payment attempt failed with:

```text
PathFind error: no path found
