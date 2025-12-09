Tier 1 vs Tier 2 ISPs - How the Internet’s Hierarchy Shapes Routing


Before anything else, we define our core term:

Truth = the real, current state of global connectivity — which networks exist, how they interconnect, and which paths are available.


Tier 1 and Tier 2 classifications describe how networks exchange this truth with each other.


1. What Is a Tier 1 ISP?

A Tier 1 ISP:

has no transit providers

reaches the entire Internet using only settlement-free peering

pays zero money to send traffic anywhere

forms part of the global backbone

Examples (not exhaustive):

Lumen (Level 3)

AT&T

Verizon (UUNet)

NTT

Telia

GTT

Cogent

Tier 1 networks exchange traffic with each other for free, forming a global mesh.

Key Insight:

Tier 1 = self-sufficient global reach with no upstream provider.


2. What Is a Tier 2 ISP?

A Tier 2 ISP:

has some peering agreements

BUT also purchases transit from Tier 1 networks

is regional or national in scope

Examples:

Comcast

Charter/Spectrum

Cox

British Telecom (BT)

Deutsche Telekom

Smaller carriers in countries around the world

Key Insight:

Tier 2 = mixes peering + paid transit to reach the full Internet.


3. How This Affects Routing (BGP Reality Check)

Tier 1 ISPs prefer:

their own customers

their own peers

avoiding paid transit (they have none)

Tier 2 ISPs prefer:

local/regional peers

their customers

minimizing transit costs

This leads to:

different paths for different users

asymmetric routing

unpredictable Anycast behavior

different failover speeds

performance differences across regions

This is WHY:

Two users in different cities hit different Anycast backends.


4. Why Cloud Architects and SREs Must Understand the Tier Hierarchy

Because:

latency

cost

reachability

traffic engineering

and failover behavior

all depend on which networks traffic passes through.

Understanding Tier 1 vs Tier 2 is essential for:

CDN design

Anycast deployment

multi-region architecture

performance troubleshooting

routing policy analysis

peering strategies

global-scale cloud networking


5. How Tier Status Connects to “Truth”

The Internet-wide truth includes:

which networks peer with whom

which networks buy transit

which AS-paths exist

how reachability propagates

which paths BGP considers “best”

Tier status shapes this truth.

The control plane (BGP) distributes it.
Routers interpret it.
Applications feel it.


6. Key Insight

Tier 1 = global backbone
Tier 2 = regional ISP with paid transit

This hierarchy explains:

inconsistent Anycast routing

asymmetric flows

wildly different latency between countries

why failover is NOT uniform

why convergence differs across the world

Understanding tiers = understanding the real Internet.


Attribution

Developed with architectural support from Padlinksky.
