SPF and Convergence — How Routers Turn Truth Into Action

Before anything else, we define the core idea used across link-state protocols:

What “Truth” Means in Networking

Truth = the real, current state of the network.
This includes:

which routers exist

which links are up or down

who each router’s neighbors are

the cost of every link

which networks are reachable and where

All routers must agree on this truth to build correct routing tables.

Link-state protocols share this truth through LSAs (OSPF) or LSPs (IS-IS), and they store it in the LSDB (Link-State Database).

Once truth is synchronized, routers can run SPF.

1. What SPF (Shortest Path First) Actually Does

SPF does not find paths the way beginners think.

SPF reads the LSDB, the complete set of truths about the topology, and uses those relationships to build the best possible map.

SPF does this:

Reads every fact (truth) in the LSDB

Builds a graph of all router relationships

Calculates the least-cost paths

Produces the RIB (routing table)

Updates next hops and forwarding decisions

If all routers share the same truth →
they all compute the same map.

2. What Convergence Means

Convergence is the point where:

Every router has the same truth and has finished recalculating SPF.

A converged network is:

stable

predictable

consistent

A non-converged network behaves:

inconsistently

unpredictably

dangerously

This is where flaps, loops, and outages occur.

3. What Breaks Convergence

Convergence is fragile in real networks.

It can break due to:

unstable links

repeated link flapping

overloaded routers

excessive LSA flooding

slow SPF computation

mismatched timers

misconfigurations

topology changes happening too fast

These conditions cause routers to disagree about truth — producing chaos.

4. SPF Triggering, Backoff, and Throttling

SPF is CPU-intensive.

If routers run SPF too often, they melt.

So protocols implement:

SPF hold timers

SPF backoff algorithms

LSA pacing

Flooding dampening

This keeps the network from recalculating truth too frequently during churn.

5. Architect Mindset

When diagnosing any link-state network:

Ask:

Do all routers share the same truth in their LSDB?

Are LSAs flooding correctly?

Is a specific router failing to update its truth?

Is SPF running too often?

How long does convergence take after a failure?

Is the control plane overwhelmed?

These are the questions asked by:

SREs

ISPs

Cloud network engineers

Hyperscaler routing teams

6. Key Insight

Truth then SPF and then  Convergence

Truth describes the network

SPF builds the best map from that truth

Convergence is the moment every router agrees

When truth is correct and convergence is fast the network is healthy.

When truth is inconsistent or convergence is slow the network becomes unstable.

Attribution

Developed with architectural support from Padlinksky.
