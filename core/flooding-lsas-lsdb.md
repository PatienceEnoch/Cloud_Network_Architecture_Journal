Flooding, LSAs, and the LSDB - How Link-State Protocols Spread Truth

(Truth = the actual, real state of the network at this moment.)

Link-state protocols (OSPF, IS-IS) depend on a simple idea:

Every router must know the same truth about the network.

To accomplish that, they use:

LSAs (OSPF) or LSPs (IS-IS)

Flooding

The LSDB (Link-State Database)

This is how link-state protocols synchronize reality.

1. LSAs: Packets of Truth

An LSA is a small packet that describes something true about the router that created it:

“Here are my interfaces.”

“Here are my neighbors.”

“Here is the cost of my links.”

“Here is a new prefix I learned.”

“Here is a link that just went down.”

LSAs contain facts, not opinions.

Every LSA is signed with the router’s identity (the loopback you documented earlier).

2. Flooding: Hop-by-Hop Truth Sharing

When a router receives an LSA, it must:

Install it in the LSDB

Forward (flood) it to every neighbor except where it came from

This creates a domino effect:

R1 → R2 → R3 → R4 → R5


Until EVERY router in the area has the same information.

Flooding ensures:

Truth propagates fast

No one is left out

Everyone builds the same map

Flooding is controlled. It uses mechanisms to prevent loops, duplicates, and infinite propagation.

3. The LSDB: The Map of All Truth

The LSDB is a collection of all LSAs from all routers.

Think of it like a shared book that every router must have a copy of:

If one LSA changes every router must update

If one route fails every router must learn it

If one cost increases recalculation happens everywhere

All routers MUST agree on the LSDB.

If they don’t, the network becomes inconsistent.

4. SPF: Turning Truth Into a Map

Once the LSDB is fully synchronized, each router runs:

SPF (Shortest Path First)
also known as Dijkstra’s algorithm.

SPF takes the LSDB and produces:

A routing table (RIB)

A forwarding table (FIB)

SPF doesn't discover paths —
it discovers the relationships described in the LSDB.

5. Why Flooding Exists

Flooding exists because:

Truth must propagate quickly

All routers must agree on the same facts

The network must converge consistently

Without flooding:

Networks would form loops

Different routers would see different realities

SPF would operate on bad information

Flooding = synchronized reality.

6. Architect Mindset: What This Really Means

You don’t troubleshoot OSPF or IS-IS by guessing.

You ask:

Did the truth flood correctly?

Did every router install the LSA?

Does everyone’s LSDB match?

Is someone suppressing or corrupting truth?

Did churn overwhelm the control plane?

Did SPF run too often?

This is high-level thinking.

Key Insight

Link-state protocols do not trade routes.
They trade truth.

Each router:

shares what it knows

forwards what it learns

participates in a network-wide agreement about reality

The LSDB is the foundation for all routing decisions.

Attribution

Conceptual clarity developed through discussions with Padlinksky.
