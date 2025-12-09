Segment Routing (SR) - The Modern Control of Network Paths


Before anything else, we define our core term:

Truth = the real, current state of the network that all routers must agree on.

SR relies on this truth to build flexible paths without requiring per-flow state in the network core.


1. What Segment Routing Actually Is
   

Segment Routing (SR) is a way to control packet paths without requiring the routers in the middle to store per-flow state (labels, LSPs, tunnels, etc.).

Instead of the network carrying the state, the packet itself carries instructions.

These instructions are called segments.

A segment is an instruction like:

“Go through Router A”

“Use this link only”

“Take the low-latency path”

“Avoid congested nodes”

“Exit the network here”

Packets get a list of these segments, forming a Segment List.

The packet literally carries its own roadmap.


2. Two Major Flavors of SR
SR-MPLS

Segments are MPLS labels.
Huge in ISPs and backbone networks.

SRv6

Segments are IPv6 addresses with encoded behavior.
This is what hyperscalers (Meta, Google, Cloudflare) love because it's:

programmable

flexible

stateless in the core


3. Why SR Relies on IS-IS
   

SR needs a routing protocol to distribute the segments (identities and instructions).

IS-IS is the protocol of choice because:

it scales better than OSPF at massive size

it handles TLVs (Type-Length-Value) cleanly

it supports SR extensions seamlessly

it’s widely used in provider networks

This is why hyperscalers say:

“We will run SR over IS-IS.”

It means:

IS-IS distributes SR segments

SR defines how packets flow

The control plane stays simple and scalable


4. Why SR Is Replacing Traditional MPLS
   

Traditional MPLS requires:

per-LSP state in every router

signaling protocols (LDP, RSVP-TE)

heavy control-plane load

brittle, complex architectures

SR eliminates nearly ALL of this.

SR gives you:

stateless core (no per-flow state)

programmatic paths

simple steering

fast reroute

service chaining

SR simplifies the backbone while giving more control.


5. How SR Supports Cloud-Native Thinking


SR is built for:

Anycast

microservices

distributed workloads

per-application traffic engineering

programmable networks

zero-trust routing

edge networks

Cloud-native traffic isn’t about tunnels and circuits — it’s about:

“Send traffic using this intent.”

SR lets you encode INTENT in the packet itself.


6. SR and Truth
   

SR depends on IS-IS to distribute truth:

which routers exist

their SID (Segment ID) values

available paths

link metrics

topology structure

When truth changes (link failure, churn):

IS-IS floods new state

routers update their segment databases

SR paths automatically adjust

SR inherits the strengths — and limitations — of link-state truth propagation.


7. Architect Mindset
   

When evaluating SR, ask:

Do we need fine control over paths?

Is the network large enough to need a stateless core?

What segments do applications need?

Are we running IS-IS to support SR?

Do we prefer SR-MPLS or SRv6?

How much churn can our SR fabric handle?

SR is about intent-based networking at backbone scale.


8. Key Insight
   

Segment Routing moves complexity from the network core into the packet itself.
This creates:

simpler routers

better programmability

faster convergence

more resilient architectures

cloud-friendly traffic engineering

This is why SR is the future of provider and hyperscaler networks.


Attribution

Developed with architectural support from Padlinksky.
