Churn, Flapping, and Suppression - The Mechanics of Instability

Before we begin, we define our essential term:

Truth = the real, current state of the network.

Routers must agree on truth: which links exist, which routers are alive, which neighbors are reachable, and what the topology looks like.

When truth changes too often, instability begins.

1. What Is Churn?

Churn = constant, rapid changes in the network’s truth.

Examples:

a link goes up, then down, then up again

a router reboots repeatedly

an interface loses packets intermittently

cost metrics fluctuate

BFD or Hello timers flap

Each time truth changes, routers must:

generate new LSAs/LSPs

flood those truths

update their LSDBs

rerun SPF

update their RIB/FIB

Too much churn → routers get overwhelmed.

2. What Is Flapping?

Flapping is a specific cause of churn.

A link or route is “flapping” when it toggles between available and unavailable.

Examples:

an Ethernet port with a bad cable

a radio link with unstable signal

a neighbor adjacency that comes and goes

a prefix that appears then disappears

Flapping creates storms of truth changes.

3. Why Flapping is Devastating

Every flap means:

New LSAs

New floods

New SPF calculations

New RIB/FIB installs

Multiply this by many routers and you get:

CPU spikes

massive SPF delays

flooding storms

LSDB inconsistencies

routers falling behind

global convergence failures

This is where networks “feel haunted.”

4. What Is Route Suppression?

Suppression = protecting the control plane from constant truth changes.

When a route or link is unstable, routers may:

hold down the route

delay accepting new truth

ignore repeated flaps

dampen signals

slow down flooding

wait before advertising the change

This prevents runaway instability.

The big idea:

Not every truth is worth acting on immediately.

5. Why Suppression Exists

Without suppression:

A single bad link could destabilize an entire network

ISPs would suffer massive outages from small failures

SPF would run constantly

Control planes would collapse under load

Suppression protects large-scale networks from chaos.

6. Architect Mindset

When diagnosing instability, don’t just ask:

“What route changed?”

Ask:

Is this link flapping?

Is this prefix unstable?

Are routers being flooded too often?

Is SPF backing off properly?

Are LSAs being suppressed?

Is churn overwhelming the control plane?

Is this a physical problem disguised as a routing problem?

Real-world instability almost always traces back to churn.

7. Key Insight

Truth must be shared — but not too often.
Stability requires selective truth.

Flooding every truth instantly = instability.
Suppressing unstable truths = resilience.

This is the heartbeat of real-world routing.

Attribution

Developed with architectural support from Padlinksky.
