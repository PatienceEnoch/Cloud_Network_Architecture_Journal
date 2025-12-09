CAP Theorem for Networks — Why Routing Cannot Be Perfect

Before exploring CAP, we must define the foundation:

Truth = the real, current state of the network that routers must agree on.

Truth includes which routers are alive, which links exist, what the costs are, and which prefixes are reachable.

Routing protocols try to synchronize this truth across the network — but they face the same limitations that distributed databases face.

1. What the CAP Theorem Says

In any distributed system, you can only guarantee two of these three:

Consistency

Availability

Partition Tolerance

You cannot have all three at the same time.

Example meanings:

Consistency: Everyone sees the same truth at the same time

Availability: The system keeps responding even during failures

Partition Tolerance: The system keeps operating even when parts are disconnected

In real networks, partition tolerance is required (links fail constantly), so the tradeoff becomes:

Consistency vs Availability
2. How CAP Applies to Routing

Routing is a distributed system where routers must:

share truth

update truth

converge on the same truth

forward packets correctly during changes

But networks have:

link failures

churn

slow propagation

partial convergence

So routing protocols must choose:

- Strive for Consistency → risk being unavailable
- Strive for Availability → risk inconsistency during transitions

Routing chooses availability.

3. Why Routing Prioritizes Availability

If routers waited until the entire network agreed on the same truth before forwarding:

outages would expand

failover would be slow

traffic would stop during convergence

the internet would feel broken constantly

Instead, routers prefer:

Forward with the truth you have right now.

Even if that truth is incomplete or outdated.

This preserves availability — but breaks consistency.

4. What Inconsistency Looks Like in Real Networks

During a topology change:

Router A thinks New York is closest

Router B thinks Chicago is closest

Router C still thinks Dallas is best

Router D hasn’t received updated truth yet

This causes:

Anycast shifting

asymmetry

intermittent packet loss

strange user experiences

routes temporarily looping

This is normal CAP behavior.

Routing is eventually consistent, not instantly consistent.

5. Why SREs Talk About “Eventual Consistency at the Edge”

Truth takes time to propagate.

Some routers learn new truth immediately.
Others lag behind.
Some paths flap.
Some suppress instability.

Thus, edge networks become:

partially converged

temporarily inconsistent

eventually synchronized

This is the only possible design in a physical world with latency, failures, and distance.

6. Key Architectural Insight

Routing protocols behave like distributed databases.

The LSDB is the database

LSAs/LSPs are truth updates

SPF is a query engine

Convergence is replication

Churn is write amplification

Suppression is rate-limiting

Anycast is multi-leader routing

This is why deep network engineers and distributed systems engineers think in similar ways.

7. The Real CAP Tradeoff in Networks

Because partition tolerance is mandatory:

You can choose consistency or availability,
but not both.


Routing chooses:

Availability

Packets must keep moving.

Routers cannot all agree at once. Immediate consistancy is a nope.

So routing is:

Available + Partition-Tolerant
Eventually consistent

This explains:

unpredictable Anycast failover

asymmetrical paths

transient loops

momentary blackholes

instability during churn

Not bugs only fundamental laws.

Attribution

Developed with architectural support from Padlinksky.
