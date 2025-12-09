Clean State - How Routers Reset Their View of Truth

Before anything else, we define our foundational term:

Truth = the real, current state of the network: which routers exist, which links are up, what the topology looks like, and how the system is connected.

Link-state protocols like IS-IS and OSPF rely on distributing truth accurately and consistently.

But sometimes, the control plane becomes overwhelmed or corrupted with too many truth changes.

That’s when “clean state” becomes necessary.


1. What Is Clean State?

Clean state is when a router deliberately resets part or all of its control-plane databases so it can rebuild truth safely.

This is like saying:

“I no longer trust the truth I currently have.
I’m going to wipe my understanding and re-learn the real topology.”

A clean state might include:

clearing neighbor adjacencies

resetting SPF timers

wiping the LSDB or LSP database

reinitializing the link-state engine

restarting flooding mechanisms

resetting sequence numbers

This allows the router to start fresh and rebuild a stable, correct view of the network.


2. Why Clean State Happens

Routers may enter clean state because of:

   1. Excessive churn

Too many truth updates in too short a time:

flapping links

unstable adjacencies

rapid topology changes

repeated SPF triggers

   2. LSDB inconsistencies

Router detects:

missing LSAs

corrupted LSPs

mismatched sequence numbers

incomplete flooding

   3. Control-plane overload

When overwhelmed, routers choose:

“Reset and rebuild rather than continue with corrupted truth.”

   4. Graceful restart scenarios

When certain protocols restart, they temporarily rebuild their control-plane truth.


3. Why IS-IS Uses Clean State More Elegantly

IS-IS has historically been preferred by hyperscalers because:

it uses TLVs (Type-Length-Value)

it handles large-scale flooding more cleanly

it supports SR and modern extensions

it manages sequence numbers robustly

it can recover from inconsistent truth more gracefully

When IS-IS enters clean state, it can rebuild truth faster and with less chaos than OSPF in massive networks.


4. Clean State and Truth Propagation

When a router enters clean state:

It discards its outdated or corrupted truth

It requests fresh LSAs/LSPs from neighbors

It rebuilds the LSDB from scratch

It re-runs SPF

It re-installs the RIB/FIB

It rejoins the network with a validated view of reality

This ensures that corrupted truth does not spread.

Clean state = truth recovery.


5. Clean State in Large Networks

Backbone and hyperscaler networks rely on clean state because:

partial truth is dangerous

inconsistent LSDBs cause loops

SPF on bad data = instability

suppressing churn doesn’t always fix the root cause

Engineers sometimes force clean state manually:

clearing adjacency

clearing LSPs

resetting BGP sessions

restarting the IS-IS process

Why?

Because it is often faster and safer than debugging corrupted truth.


6. Architect Mindset

When diagnosing a network issue, ask:

Is this router holding bad truth?

Is its LSDB inconsistent with neighbors?

Is it failing to flood or receive floods?

Has churn overwhelmed it?

Would forcing clean state allow a safe rebuild?

This is real-world reasoning.


7. Key Insight

Clean state is the router’s way of saying:
“I need to start over so I can learn the true topology again.”

It is an essential mechanism for stability in:

IS-IS

OSPF

BGP

Segment Routing

large-scale distributed systems


Understanding this makes you think like a network doctor - someone who can reset systems to health.


Attribution

Developed with architectural support from Padlinksky.
