Anycast, State, and Why Failover Is Unpredictable

Before we begin, we define our anchor:

Truth = the actual, current state of the network that all routers must agree on.

Truth includes which routers exist, which paths are available, and how traffic should flow right now.

Anycast works beautifully when truth is stable.
It becomes unpredictable when truth changes.

1. What Anycast Really Is

Anycast = one IP address announced from many locations.

Example:

8.8.8.8 (Google DNS)
1.1.1.1 (Cloudflare DNS)


Multiple servers around the world advertise the SAME prefix.

BGP chooses the “closest” one based on AS-path and policy.

The user sees one IP.
The network sees many possible destinations.
2. Why Anycast Is Powerful

Anycast gives:

automatic load distribution

lower latency for users

local failover

simple IP addressing

global redundancy

It’s used everywhere:

CDNs

DNS resolvers

edge compute (Cloudflare Workers / Akamai)

DDoS absorption

global proxies

But there’s a catch.

3. Anycast Hides Independent Failure Domains

Anycast looks like one IP,
but behind the scenes it is many independent systems.

Each site:

has its own health

has its own servers

has its own upstreams

has its own routers

has its own truth about the network

can fail independently

This is where things get weird.

4. Why Failover Is Not Predictable

If one Anycast site goes down:

some users reroute instantly

some reroute slowly

some don’t reroute at all

some flap between sites

some hit a blackhole until reconvergence completes

Why?

Because failover depends on:

how fast BGP withdraws the prefix

how fast neighboring ASes accept the withdrawal

how many AS hops propagate truth

suppression timers

minimum route advertisement intervals

churn levels in the global Internet

Anycast relies on eventually consistent truth across the Internet.

That means:

Different parts of the Internet believe different truths at the same time.

5. Why Stateful Applications Break on Anycast

TCP connections depend on:

one continuous path

one endpoint

one stateful session

But Anycast endpoints are not the same servers.

Traffic may start to:

Site A

Then failover to Site B

But Site B doesn’t have the session state

Result?

Broken TCP

Reset connections

Partial uploads

Timeout errors

“My app is haunted” behavior

Anycast + State = Fragile

This is why CDNs and cloud providers push:

QUIC

Stateless protocols

Stateless microservices

Replicated key-value stores (eventual consistency)

6. Architect Mindset

When designing Anycast systems, ask:

What happens when truth fails to propagate?

How long will BGP take to converge?

What timers influence suppression and withdrawal?

How much state does the application depend on?

How does loss of a single site affect users in different regions?

Is session stickiness required?

Anycast is simple in theory but deeply complex in reality.

7. Key Insight

Anycast is eventually consistent, not strongly consistent.

There is no global “instant truth.”

Different parts of the network will temporarily disagree about:

which sites exist

which paths are valid

which endpoint is closest

This disagreement → unpredictable failover.

Attribution

Clarified through architecture sessions with Padlinksky.
