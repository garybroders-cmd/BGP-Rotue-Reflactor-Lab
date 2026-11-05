# BGP-Rotue-Reflector-Lab

Verification on vIOS1 & VIOS2

show ip ospf neighbor<br>
show ip bgp summary</br>
show ip bgp neighbors 10.255.0.3 | include Reflector</br>


On the client routers, show ip bgp 192.168.3.1 shows an Originator ID and Cluster List.  These are added by the reflectors for loop prevention.</br>

# Lab Design Notes.

Same cluster ID on both RRs (1.1.1.1) means a client route reflected by R1 and then received by R2 is rejected as a loop. That avoids duplicate routes, but it also means clients must peer with both RRs, as they do here. If you give the RRs different cluster IDs, you get more redundancy in the paths but more route duplication.</b>
RR-to-RR peering is a normal (non-client) iBGP session. Clients never peer with each other.</br>
Next-hop-self is not needed here because every router’s loopback is in OSPF. It would be needed if clients learned eBGP routes from outside the AS, since the next hop would otherwise be unreachable.</br>
Reflectors only reflect best paths. They do not change the next hop or attributes of reflected routes.</br>
In a real network, the RRs are usually dedicated control-plane devices (or virtual RRs) placed in separate sites, not necessarily in the forwarding path.</br>
