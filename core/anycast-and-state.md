Anycast, State, and Why Failover Is Unpredictable

Before we begin, we define the core term:

Truth = the real, current state of the network that all routers must agree on.

Truth includes which routers exist, which links are up, which costs apply, and how the topology is shaped.

Anycast depends entirely on each router’s view of this truth and that creates inherent unpredictability.

1. What Anycast Actually Is

Anycast is one IP address announced from multiple locations.

Example:

192.0.2.10  
↳ announced in New York  
↳ announced in Chicago  
↳ announced in Dallas


Traffic is routed to whichever location appears closest according to routing truth.

Key point:

Different users see different “closest” nodes.

This is why Anycast is powerful and why it’s unpredictable.

2. Why Anycast Works Only If Truth Is Consistent

Routers forward packets based on:

their local LSDB

their local RIB

their understanding of path cost

If truth changes, or is inconsistent, different routers may make different decisions.

This means:

User A might reach the New York node

User B might reach Chicago

User C might suddenly switch to Dallas

This is normal behavior.

Anycast is not load balancing; it is decentralized path selection.

3. Why Failover Is Unpredictable

Anycast failover depends on:

convergence time

propagation of truth

how each router interprets topology

which prefixes change

how quickly churn settles

Your users may reach:

Node 1 before a failure

Node 3 during convergence

Node 2 afterward

Different parts of the Internet converge at different speeds, so the shift is never perfectly smooth.

Anycast is eventually correct, not immediately correct.

4. Anycast + Stateful Traffic = Fragile

Stateful protocols require:

a session

a specific server

continuity

consistent return paths

But Anycast can break all of this.

Example:

A TCP session established with New York suddenly shifts to Chicago mid-session due to a topology change.

Results:

Session breaks

Connection resets

User sees instability

This is why CDNs and SREs treat Anycast for TCP as dangerous unless engineered carefully.

5. Anycast + Stateless Traffic = Strong

Stateless workloads (like DNS over UDP) work flawlessly with Anycast because:

no session needs to persist

packets can be independently routed

failures self-heal instantly

Anycast nodes can scale horizontally

This is why DNS is one of the largest Anycast use cases on Earth.

6. Why SREs Say “Anycast is eventually consistent”

Because routing truth takes time to propagate.

During transitions:

some routers know the truth

some do not

some think the old path exists

some think the new one is best

For a brief time, the network is in mixed truth state.

Eventually all routers converge, but:

users hit different backends

stateful sessions break

performance varies

This is by design — not a bug.

7. Architect Mindset

When evaluating Anycast, ask:

Is this workload stateful or stateless?

How sensitive is it to path changes?

What is the impact of partial convergence?

What happens if different regions learn truth at different speeds?

Are we prepared for unpredictable failover?

Should we design for idempotency and retryability?

This is why modern cloud design prefers:

stateless APIs

QUIC

connectionless workloads

Anycast + stateless = beautiful
Anycast + stateful = fragile

Key Insight

Anycast does not guarantee stable routing. It guarantees dynamic routing.

Routing follows truth, and truth changes.
Failover is therefore inherently unpredictable but incredibly powerful when used correctly.

Attribution

Developed with architectural support from Padlinksky.
