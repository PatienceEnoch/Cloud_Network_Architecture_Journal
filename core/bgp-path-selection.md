BGP Path Selection — How the Internet Actually Chooses Paths


Before anything else, we restate our foundational concept:

Truth = the real, current state of reachability that BGP learns from other networks.

It includes which prefixes exist, who is announcing them, and what AS-paths or policies apply.


BGP does not learn topology.
It learns reachability truth and then applies policy to choose the best path.

1. BGP Is a Policy Engine, Not a Shortest-Path Algorithm

Unlike IGPs:

BGP does not run SPF

BGP does not flood truth

BGP does not try to find the shortest or fastest route

BGP selects paths based on policies and business relationships, not performance.

This is the heart of BGP.

2. The BGP Path Selection Order (Architect-Level Summary)

When multiple paths exist to the same prefix, BGP applies this sequence:

1. Highest LOCAL_PREF wins

Internal preference inside your AS.
Often used to:

pick primary vs backup circuits

influence outbound traffic

LOCAL_PREF always comes first.

2. Shortest AS-PATH wins

Fewer autonomous systems = preferred path.
Not “shortest distance,” but “fewest political/economic hops.”

3. Lowest ORIGIN type wins

i > e > ?
(Inherited complexity from old standards.)

4. Lowest MED wins

Neighbor’s suggestion about which link to use.

5. Prefer eBGP over iBGP

External routes trump internal reflections.

6. Lowest IGP metric to next-hop

How close the next-hop router is inside your own network.

7. Oldest route wins

Stability is preferred.

8. Lowest router ID, cluster ID

Tie-breakers.

Key insight:

BGP selects the best policy path, not the best performance path.

3. Why BGP Doesn’t Care About Speed

BGP has no visibility into:

latency

jitter

bandwidth

congestion

physical distance

It only sees:

AS relationships

policies

preferences

This is why users sometimes get routed:

across continents

through slow links

through distant POPs

This isn’t a bug — it’s policy truth, not performance truth.

4. How Business Relationships Shape the Internet

BGP prefers routes based on economic priorities:

Customer > Peer > Provider

Why?

Because:

Sending traffic to a customer = you get paid

Sending traffic to a peer = free

Sending traffic to a provider = you pay

This explains:

asymmetric routing

weird Anycast behavior

unpredictable failover

why Tier 1 vs Tier 2 matters

why the Internet “feels political”

The business truth overrides topology truth.

5. BGP Convergence Is Slow — And That’s On Purpose

BGP intentionally avoids rapid changes because:

flapping prefixes would melt the Internet

instability would propagate globally

routers need time to settle

policy must win over speed

When BGP changes truth, it happens:

slowly

intentionally

with damping

with careful propagation

This prevents global instability.

6. Architect Mindset

When analyzing BGP behavior, ask:

What policy caused this decision?

Which AS-paths exist?

Who is the customer? Peer? Provider?

What does LOCAL_PREF say?

Is the next-hop reachable via IGP?

Is MED influencing selection?

Are we seeing path hunting?

Great engineers troubleshoot BGP by understanding policy truth, not just AS-paths.

7. Key Insight

IGPs choose paths based on topology truth.
BGP chooses paths based on policy truth.

This is why:

the Internet is asymmetric

Anycast is unpredictable

global failover is messy

routing patterns sometimes seem irrational

They are not irrational.
They are governed by policy, economics, and reachability truth.

Attribution

Developed with architectural support from Padlinksky.
