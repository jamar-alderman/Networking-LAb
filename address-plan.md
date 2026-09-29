# Campus address map

Current design documented during the September 29 lab session. Each floor uses the same VLAN IDs with distinct IP subnets; the routed core links separate the floor Layer 2 domains. Gateways are SVIs on the respective floor distribution switch.

## VLANs and gateways

| VLAN | Purpose | Floor 1 subnet | Floor 1 gateway | Floor 2 subnet | Floor 2 gateway |
| --- | --- | --- | --- | --- | --- |
| 10 | USERS | 192.168.10.0/24 | 192.168.10.1 | 192.168.110.0/24 | 192.168.110.1 |
| 20 | VOICE | 192.168.20.0/24 | 192.168.20.1 | 192.168.120.0/24 | 192.168.120.1 |
| 30 | SERVERS | 192.168.30.0/24 | 192.168.30.1 | 192.168.130.0/24 | 192.168.130.1 |
| 45 | GUEST | 192.168.45.0/24 | 192.168.45.1 | 192.168.145.0/24 | 192.168.145.1 |
| 99 | MGMT / native | 192.168.99.0/24 | 192.168.99.1 | 192.168.199.0/24 | 192.168.199.1 |

All client/server VLAN subnets use mask 255.255.255.0. The earlier proposed 10.1.x/10.2.x VLAN allocation was replaced by the 192.168.x allocation above; it should not be used as the current client address plan.

## DHCP servers

| Server | VLAN | Static address | Default gateway |
| --- | --- | --- | --- |
| Floor 1 Server0 | 30 | 192.168.30.10/24 | 192.168.30.1 |
| Floor 2 Server1 | 30 | 192.168.130.10/24 | 192.168.130.1 |

The server NIC gateway is the server VLAN gateway. Each DHCP pool supplies its client VLAN gateway. Client SVIs relay DHCP to their floor's server. Exact final pool start/end ranges are not recorded in the supplied exports.

## Routed core-to-distribution links

| Link | Subnet | Core interface / IP | Distribution interface / IP |
| --- | --- | --- | --- |
| Core 1 ↔ Floor 1 | 10.255.0.0/30 | CORE-1 Gi0/1 — 10.255.0.1 | FLOOR-1 Gi0/1 — 10.255.0.2 |
| Core 2 ↔ Floor 1 | 10.255.0.4/30 | CORE-2 Gi0/2 — 10.255.0.5 | FLOOR-1 Gi0/2 — 10.255.0.6 |
| Core 1 ↔ Floor 2 | 10.255.0.8/30 | CORE-1 Gi0/2 — 10.255.0.9 | FLOOR-2 Gi0/1 — 10.255.0.10 |
| Core 2 ↔ Floor 2 | 10.255.0.12/30 | CORE-2 Gi0/1 — 10.255.0.13 | FLOOR-2 Gi0/2 — 10.255.0.14 |

All transit links use mask 255.255.255.252. These are separate routed links, not one EtherChannel spanning independent core devices.
