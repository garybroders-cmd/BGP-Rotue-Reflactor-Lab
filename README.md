# BGP-Rotue-Reflactor-Lab

Verification on vIOS1 & VIOS2

show ip ospf neighbor
show ip bgp summary
show ip bgp neighbors 10.255.0.3 | include Reflector


On the client routers, show ip bgp 192.168.3.1 shows an Originator ID and Cluster List.  These are added by the reflectors for loop prevention.

# Lab Design Notes.

Same cluster ID on both RRs (1.1.1.1) means a client route reflected by R1 and then received by R2 is rejected as a loop. That avoids duplicate routes, but it also means clients must peer with both RRs, as they do here. If you give the RRs different cluster IDs, you get more redundancy in the paths but more route duplication.
RR-to-RR peering is a normal (non-client) iBGP session. Clients never peer with each other.
Next-hop-self is not needed here because every router’s loopback is in OSPF. It would be needed if clients learned eBGP routes from outside the AS, since the next hop would otherwise be unreachable.
Reflectors only reflect best paths. They do not change the next hop or attributes of reflected routes.
In a real network, the RRs are usually dedicated control-plane devices (or virtual RRs) placed in separate sites, not necessarily in the forwarding path.
