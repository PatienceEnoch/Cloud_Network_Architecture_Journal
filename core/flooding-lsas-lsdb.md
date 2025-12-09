Flooding, LSAs, and the LSDB - How Routers Share Truth

Before anything else, we define the core concept used throughout link-state routing:

What is “truth” in a link-state network?

Truth = the real, accurate description of the network’s current state.

It includes:

which routers exist

which interfaces and links are up

which neighbors are reachable

the cost of each link

which prefixes are advertised

which areas or levels routers belong to

Truth is the actual topology and condition of the network right now.
Link-state protocols exist to distribute that truth to every router.

1. LSAs/LSPs: Packets of Truth

OSPF and IS-IS routers describe their understanding of the network using small structured messages:

OSPF: LSAs

IS-IS: LSPs

Each message contains truths such as:

“These are my active interfaces.”

“These are my neighbors.”

“This is the cost of each link.”

“This prefix exists behind me.”

Each LSA/LSP is signed with the router’s identity (the loopback).

LSAs don’t contain routes - they contain truth about the topology.

2. Flooding: How Truth Spreads

Flooding is the mechanism that ensures every router learns every truth.

When a router receives a new truth (an LSA/LSP), it:

Stores it in the LSDB

Forwards it to all neighbors EXCEPT the one it learned it from

This hop-by-hop process continues until:

Every router has seen every truth.

Flooding is “controlled” - routers use sequence numbers and checks to avoid loops and duplicates.

Flooding exists for one reason:

Without shared truth, the network cannot agree on paths.
3. The LSDB: The Shared Book of Truth

Every router stores every truth it has learned in its LSDB.

Think of the LSDB as a shared encyclopedia:

Every router has a copy

Every router must have the SAME copy

If one router has different truth, routing breaks

The LSDB is the foundation for SPF.

4. SPF: Turning Truth Into the Map

Once all routers have the same set of truths in their LSDBs, each router independently runs:

SPF (Shortest Path First)

SPF uses the shared truth to build:

the routing table (RIB)

the forwarding table (FIB)

SPF assumes the LSDB is complete and correct.
If the truth is wrong → the map is wrong → forwarding is wrong.

5. Why Flooding and LSDB Sync Matter

If the LSDB is inconsistent…

routers believe different truths

SPF produces different outputs

routing loops form

some routers blackhole traffic

convergence falls apart

For link-state to work:

All routers must know the same truth, at the same time.

This is why flooding is so aggressive and sensitive.

6. Architect Mindset

When debugging link-state problems, always ask:

Did every router receive the truth?

Do all LSDBs match?

Is someone failing to flood?

Is someone flooding too much?

Is churn (constant truth changes) overwhelming the control plane?

High-level engineers debug truth flow, not “routes.”

Key Insight

Link-state protocols do not trade routes.
They trade truth.

Routes are calculated from truth.
Truth is distributed through flooding.

Without truth, nothing else works.

Attribution

Developed with architectural support from Padlinksky.
