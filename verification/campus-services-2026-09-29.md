# September 29 campus verification record

This record distinguishes pasted CLI evidence from observations and successful tests reported during the lab session. The topology screenshot shows device placement; it is not used as proof of DHCP, routing, or ACL behavior.

## Switching

Earlier supplied show output reported Po1/Po2 as SU, member ports as P, and trunks carrying VLANs 10,20,30,45,99 with native VLAN 99. The uploaded config exports preserve active/passive LACP settings used during that build stage. See [configuration captures](../configs/campus-captures/README.md) and the existing [uplink verification](access-uplinks.md).

## Routing

The session recorded OSPF adjacency and route verification across the two cores and two distributions. The distribution switches reached the opposite floor's user gateway. A PC ping initially lost one packet, then returned a clean 4/4 result. These are session observations, not a new automated test run or evidence of tested failover.

## DHCP

The builder confirmed that both floor DHCP servers were configured and issuing addresses to PCs and phones. Servers remain in VLAN 30; client VLAN SVIs relay requests to the local server. DHCP was disrupted during the snooping experiment and restored by disabling snooping. See [current IP addressing](../address-plan.md).

## Floor 2 guest ACL

The corrected command sequence supplied during the session was:

```ios
access-list 102 deny icmp 192.168.145.0 0.0.0.255 192.168.110.0 0.0.0.255 echo
access-list 102 permit ip any any
interface vlan 45
 ip access-group 102 in
```

The builder supplied this output after correcting the test:

```text
DISTRIBUTION-FLOOR-2#show access-list 102
Extended IP access list 102
    deny icmp 192.168.145.0 0.0.0.255 192.168.110.0 0.0.0.255 echo (4 match(es))
    permit ip any any
```

The deny counter demonstrates that four matching guest ICMP echo requests hit the rule. The destination PC23 was reported as 192.168.110.17/24, gateway 192.168.110.1. The rule blocks those requests only; other IP traffic is permitted. No completed Floor 1 ACL test is claimed.
