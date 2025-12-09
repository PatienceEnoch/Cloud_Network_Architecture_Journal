Adjacency - What It REALLY Means When Routers Become Neighbors


Before everything else, we define our foundational concept:

⭐ Truth = the real, current state of the network, including which routers exist, which links are up, and who can reach whom.

Adjacency is how routers discover and share this truth.


Becoming neighbors is not “hey, I see you.”
It is a formal agreement to exchange truth.


1. Adjacency Is a Control-Plane Relationship

Adjacency is NOT:

a cable being plugged in

a link being up

a ping working

Adjacency is when two routers say:

“I trust you enough to share truth with you.”

This is a control-plane partnership.

2. What Must Match for Adjacency to Form (OSPF/IS-IS)

Routers must agree on:

the network type

timers

authentication

area/level

MTU (in some protocols)

capabilities and settings

If these differ, routers refuse adjacency because exchanging truth would be unsafe or inconsistent.

3. The Purpose of Adjacency: Exchange of Truth

Once adjacency forms, routers:

exchange identity

exchange capabilities

synchronize LSDBs / LSP databases

flood new truth as it arrives

Adjacency is how link-state networks ensure:

consistent truth

complete LSDBs

stable topology understanding

If adjacency is broken → truth stops flowing.

4. Adjacency States (OSPF Example)

OSPF uses states to safely bring neighbors into full truth-sharing:

Down — no Hellos seen

Init — I see you, but we’re not talking

2-Way — mutual recognition

ExStart — negotiating database exchange

Exchange — trading LSDB summaries

Loading — requesting missing LSAs

Full — synchronized truth

IS-IS is simpler but follows the same conceptual idea.

Adjacency is not trivial — it’s a carefully staged process.

5. When Adjacency Breaks

If adjacency breaks:

truth exchange stops

the LSDB becomes incomplete

SPF recalculates

flooding changes

convergence may stall

routing loops can appear

Anycast shifts unpredictably

BGP may lose reachability

Adjacency is one of the most fragile yet critical components of the control plane.

6. Adjacency and Link Flapping (Churn)

Unstable links cause adjacency to flap:

UP → DOWN → UP → DOWN

Every flap forces:

new LSAs

floods

SPF runs

partial convergence

instability across the network

This is why suppression, hold timers, and stable physical links matter so much.

7. Architect Mindset: The Most Important Question

When something breaks, ask:

**“Are the routers actually adjacent?”

or
“Are they adjacent but not fully synchronized?”**

These two states are very different:

Adjacent but not synchronized = inconsistent truth (dangerous)

Not adjacent = no truth exchange (also dangerous)

Knowing which is happening instantly narrows the problem.

8. Key Insight

Adjacency is the foundation of truth exchange.
Without adjacency, there is no LSDB, no SPF, no stability, and no routing.

A link being up means nothing.
A ping working means nothing.

Adjacency means everything.

Attribution

Developed with architectural support from Padlinksky.
