IGP vs BGP — The Two Layers of Internet Routing

Before anything else, we define our core term:

Truth = the real, current state of connectivity inside a routing domain or across the Internet.

Different protocols carry different kinds of truth.

This leads to the biggest distinction in routing:

IGPs learn truth INSIDE a network.
BGP learns truth BETWEEN networks.

1. What Is an IGP? (OSPF, IS-IS)

An Interior Gateway Protocol (IGP) operates within a single network — a single organization, ISP, or cloud provider.

Its job is to learn internal truth:

which routers exist

which links are up

link costs

topological structure

shortest paths within the domain

Examples:

IS-IS

OSPF

EIGRP (Cisco-specific)

Key behaviors:

Flooding of detailed truth (LSAs / LSPs)

SPF to compute best internal paths

Requires full trust between all nodes

Must converge quickly

IGPs are like the nervous system inside a single creature.

2. What Is BGP? (The Internet’s Routing Protocol)

Border Gateway Protocol (BGP) operates between networks — between companies, ISPs, clouds, carriers, and nations.

Its job is to learn external truth:

which networks (prefixes) exist

which AS (Autonomous System) owns each

which paths lead to those ASes

policy-based reachability

Key behaviors:

Does NOT flood truth

Does NOT use SPF

Propagates paths, not link-state truth

Makes decisions based on policy, not cost

Converges slowly compared to IGPs

BGP is like the communication network between entire creatures.

3. The Roles Are Completely Different
Feature	IGP (OSPF/IS-IS)	BGP
Purpose	Internal truth & shortest paths	External truth & policy
What is shared?	Link-state truth	Reachability (prefix + AS-path)
Convergence	Fast	Slow
Trust model	Full trust	Zero trust
Behavior	Flooding + SPF	Path vector + policies
Scope	Inside an AS	Between ASes

They solve different problems.

4. Why You MUST Use Both
IGP handles internal connectivity.

If a router can’t reach another router inside your network, BGP cannot function.

BGP handles external reachability.

IGPs are not designed for global scale — they would melt down instantly.

This leads to the golden rule:

IGP builds the underlay; BGP builds the overlay.

5. Why Cloud Architects Care

Cloud networks like AWS, Google, and Azure rely on both layers:

IGPs (often IS-IS) maintain internal topologies

BGP handles customer routing, Anycast, global traffic engineering, cross-region connectivity, and edge distribution

If you understand this distinction, you understand cloud routing.

6. Key Insight

IGP gives you fast, detailed truth inside your network.
BGP gives you slow, policy-based truth about the outside world.

You cannot design large-scale networks without understanding how these two layers interact.

Attribution

Developed with architectural support from Padlinksky.
