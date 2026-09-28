# Three-tier topology and physical port map

- **Core:** two independent Catalyst 3560 multilayer switches, CORE-1 and CORE-2.
- **Distribution:** one Catalyst 3560 per floor, DISTRIBUTION-FLOOR-1 and DISTRIBUTION-FLOOR-2.
- **Access:** two Catalyst 2960 room switches per floor, with three FastEthernet member links per room.
- **Servers and endpoints:** DHCP servers were proposed on distribution Fa0/1 in VLAN 30; no completed server or endpoint test output was supplied.

| Distribution port | Peer core port | Addresses |
| --- | --- | --- |
| FLOOR-1 Gi0/1 | CORE-1 Gi0/1 | 10.255.0.2 ↔ 10.255.0.1/30 |
| FLOOR-1 Gi0/2 | CORE-2 Gi0/2 | 10.255.0.6 ↔ 10.255.0.5/30 |
| FLOOR-2 Gi0/1 | CORE-1 Gi0/2 | 10.255.0.10 ↔ 10.255.0.9/30 |
| FLOOR-2 Gi0/2 | CORE-2 Gi0/1 | 10.255.0.14 ↔ 10.255.0.13/30 |

| Floor distribution ports | Access peer | Port-channel | Trunk |
| --- | --- | --- | --- |
| Fa0/19–21 | Room 1 Fa0/19–21 | Po1, LACP active on distribution and passive on access | dot1q, native 99, allowed 10,20,30,45,99 |
| Fa0/22–24 | Room 2 Fa0/22–24 | Po2, LACP active on distribution and passive on access | dot1q, native 99, allowed 10,20,30,45,99 |

Port-channel numbers are local to each device. Do not bundle links from an access switch to two independent distribution switches into one port-channel. The prior canvas labels used floor-like names for core devices; verify the **CLI hostname and interface IP**, not a canvas label, before changing a cable. A Packet Tracer file and current full-topology screenshot remain to be added.
