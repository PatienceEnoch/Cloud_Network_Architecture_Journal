Why IS-IS Is Preferred at Scale

Before anything else, we define our core term:

Truth = the real, current state of the network: all routers, all links, and all costs.

Large-scale networks depend on distributing this truth efficiently, consistently, and with minimal overhead.

This is where IS-IS excels.

1. IS-IS Was Built for Massive Networks

IS-IS originated as part of CLNP (ISO/OSI networking), not IP.
Because of this, it was engineered from day one to:

handle huge topologies

carry flexible addressing

scale cleanly

support variable-length fields

operate independently of IP itself

This gave IS-IS a structural advantage over OSPF before OSPF even existed.

2. TLVs Make IS-IS Future-Proof

IS-IS uses Type-Length-Value (TLV) encoding for all LSAs/LSPs.

This makes it extremely easy to extend.

Want to add:

Segment Routing?

New metrics?

New flooding behavior?

New node attributes?

New link attributes?

Just add a new TLV — no redesign needed.

Key insight:

IS-IS evolves without breaking.

OSPF requires new LSA types, new procedures, and often complex compatibility logic.

3. IS-IS Lives at Layer 2 (Link Layer)

IS-IS does NOT depend on IP to run.

It uses its own Layer 2 protocol:

No IP address is needed on interfaces

No IP forwarding issues affect the protocol

No dependency on IPv4 vs IPv6

Cleaner adjacencies and failure detection

This makes IS-IS much more stable in:

dual-stack networks

IPv6 migrations

high-churn environments

4. IS-IS Flooding Is More Scalable

Because IS-IS uses:

areas modeled as Levels (L1/L2)

a simpler flooding domain

fewer LSA types

fewer state machines

simpler reflooding behavior

…it handles large amounts of truth better.

In huge networks, OSPF’s flooding can become:

heavier

more repetitive

prone to LSA storms

difficult for routers to pace correctly

IS-IS remains calm when OSPF becomes chaotic.

5. Cleaner LSDB Structure

OSPF has:

many LSA types

separate databases per area

complex inter-area rules

rigid encoding formats

IS-IS has:

one LSP type per level

simpler database logic

minimal special-case behavior

This matters a LOT at hyperscale.

6. IS-IS Handles IPv6 Gracefully

OSPF had to be redesigned into OSPFv3 to support IPv6.

IS-IS:

already supported TLVs

just added IPv6 reachability TLVs

required no redesign

remains unified for IPv4 + IPv6

This consistency is why SR-MPLS and SRv6 use IS-IS so cleanly.

7. IS-IS Works Better with Segment Routing (SR)

SR requires:

segment IDs

adjacency SIDs

node SIDs

intricate topology attributes

IS-IS distributes SR attributes through TLVs effortlessly.

OSPF supports SR too — but less cleanly and with more overhead.

This is why hyperscalers say:

“Our SR network runs over IS-IS.”

8. IS-IS Is Less Common = Less Misconfigured

Enterprise networks often use OSPF.

So they:

misconfigure areas

break DR/BDR logic

misuse virtual links

create LSA storms

ISPs and hyperscalers use IS-IS.

Engineers who use it are generally:

more specialized

more disciplined

better trained

The result?
Far fewer broken networks.

9. Architect Mindset

When deciding between link-state protocols, ask:

How big is the network?

How dynamic is the topology?

Will we run Segment Routing?

Do we need dual-stack stability?

Are we building a backbone or enterprise LAN?

Do we want clean extensibility?

If you're building a massive or future-oriented network, IS-IS wins.

10. Key Insight

IS-IS scales where OSPF strains.
IS-IS evolves cleanly where OSPF requires redesign.
IS-IS supports future architectures better than OSPF.

This is why cloud providers and ISPs rely on it.

Attribution

Developed with architectural support from Padlinksky.
