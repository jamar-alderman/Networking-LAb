# Address plan

## Core transit /30 address plan

These assignments reflect the supplied CORE-2 and Floor 2 running configurations; CORE-1 addresses also appeared in `show ip interface brief`. The builder later clarified that the physical cables, not these IP assignments, were wrong. They moved the cables to match this map and report that direct pings worked. Post-fix CDP and passing ping output have not yet been captured here. Floor 1's complete current running configuration has not been captured here.

| Link | Network | Core interface / IP | Distribution interface / IP | Broadcast |
| --- | --- | --- | --- | --- |
| Core 1 to Floor 1 | 10.255.0.0/30 | CORE-1 Gi0/1 10.255.0.1 | FLOOR-1 Gi0/1 10.255.0.2 | 10.255.0.3 |
| Core 2 to Floor 1 | 10.255.0.4/30 | CORE-2 Gi0/2 10.255.0.5 | FLOOR-1 Gi0/2 10.255.0.6 | 10.255.0.7 |
| Core 1 to Floor 2 | 10.255.0.8/30 | CORE-1 Gi0/2 10.255.0.9 | FLOOR-2 Gi0/1 10.255.0.10 | 10.255.0.11 |
| Core 2 to Floor 2 | 10.255.0.12/30 | CORE-2 Gi0/1 10.255.0.13 | FLOOR-2 Gi0/2 10.255.0.14 | 10.255.0.15 |

All transit networks use mask 255.255.255.252. The /30 network allocations and endpoint IP pairs remain valid; the corrected physical cable endpoints should be verified with post-fix CDP output. The next unused /30 is 10.255.0.16/30; no inter-core link has been established.

## Proposed floor VLAN subnets

The following SVI commands were supplied during the session, but **no post-change SVI output was provided**. Treat this as the planned gateway map until verified.

| VLAN | Purpose | Floor 1 subnet / gateway | Floor 2 subnet / gateway |
| --- | --- | --- | --- |
| 10 | USERS | 10.1.10.0/24 / 10.1.10.1 | 10.2.10.0/24 / 10.2.10.1 |
| 20 | VOICE | 10.1.20.0/24 / 10.1.20.1 | 10.2.20.0/24 / 10.2.20.1 |
| 30 | SERVERS | 10.1.30.0/24 / 10.1.30.1 | 10.2.30.0/24 / 10.2.30.1 |
| 45 | GUEST | 10.1.45.0/24 / 10.1.45.1 | 10.2.45.0/24 / 10.2.45.1 |
| 99 | MGMT | 10.1.99.0/24 / 10.1.99.1 | 10.2.99.0/24 / 10.2.99.1 |

The VLAN IDs repeat on the two floors, but the two routed distribution-to-core boundaries keep the IP networks distinct. These /24 client subnets are a simple initial allocation, not a host-count-optimized VLSM design. DHCP-1 at 10.1.30.10 and DHCP-2 at 10.2.30.10 were proposed, not observed configured.
