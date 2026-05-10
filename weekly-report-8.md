# CKBuilders Weekly Report 8: Spindle Feedback Review and Fiber Capability Validation

## Context

This week I continued from the Spindle MVP submission work in Week 7.

Last week, I focused on making Spindle reviewable: deploying the MVP, connecting Neon Postgres, cleaning up the product surface, improving the docs, and submitting the project to the CKBuilder project tracker.

This week was more about validation than building new features.

After submitting Spindle for review, I received feedback questioning whether the project is actually needed in front of Fiber, especially because Fiber already has its own RPC model and permission layer.

## What I worked on

This week I focused on understanding whether Spindle adds a real layer above Fiber, or whether it duplicates things Fiber already handles.

I worked on:

- reviewing feedback from the CKBuilder project tracker
- fixing the Spindle repository visibility issue after it was accidentally private
- clarifying the intended Spindle workflow in the tracker discussion
- reviewing Fiber RPC capabilities around invoices, payments, and node access
- reviewing Fiber’s Biscuit-based RPC permission model
- comparing Fiber’s built-in permissions with Spindle’s original gateway idea
- identifying that Spindle should not be positioned as a generic permission layer in front of Fiber
- pausing new feature work until the product gap is clearer

## What became clearer

The biggest learning this week is that Spindle’s original positioning was too broad.

Fiber already has its own RPC methods for invoice and payment operations, and it also has Biscuit-based permission checks for RPC access. So Spindle should not pretend that Fiber lacks basic permissions or payment primitives.

That means the old framing of Spindle as a general Fiber payment gateway is weak.

The stronger possible direction is narrower:

Spindle may only make sense as an application-layer gateway for teams operating private Fiber nodes, where multiple apps or agent backends need scoped access, tenant or project separation, audit logs, idempotency handling, and higher-level policy before requests reach the node.

This is different from saying Fiber itself needs a gateway.

## Current status

Spindle is still a useful CKBuilder prototype, but I am treating it as under validation now.

The public MVP is still deployed here:

https://spindle-nine.vercel.app

The project tracker issue is here:

https://github.com/Nervos-Community-Catalyst/CKBuilder-projects/issues/13

The repository is public here:

https://github.com/Ticoworld/spindle

At this point, I do not want to keep adding features blindly. The next important question is whether there is a real application-layer gap above Fiber’s Biscuit/RPC model.

## Blockers

The main blocker this week is product fit, not implementation.

The key question is:

Does Fiber need an application-layer access and audit gateway above Biscuit for private node operators, or is that not useful at the current stage of the ecosystem?

If the gap is real, Spindle can be repositioned around private Fiber node operators.

If the gap is not real, then Spindle should be paused and I should move toward a more immediate Fiber developer tool or demo project.

## What I learned

This week helped me understand that building on CKB/Fiber is not only about making something technically possible.

A project can have a working MVP and still need sharper ecosystem fit.

The feedback helped me see that Spindle should not compete with Fiber’s existing permission model. If it continues, it needs to sit above Fiber as an application/operator layer, not duplicate Fiber itself.

## Next step

Next I want to:

- wait for more feedback from the Fiber / CKBuilder side
- define exactly what Spindle adds above Biscuit, if anything
- decide whether Spindle should be repositioned as a private Fiber node operator gateway
- pause Spindle if the gap is not strong enough
- avoid adding more features until the direction is validated
