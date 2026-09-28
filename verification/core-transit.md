# Core transit verification

CORE-2 `show ip route` reported connected routes:
```
C 10.255.0.4/30 is directly connected, GigabitEthernet0/2
C 10.255.0.12/30 is directly connected, GigabitEthernet0/1
```

DISTRIBUTION-FLOOR-2 `show ip route` reported:
```
C 10.255.0.8/30 is directly connected, GigabitEthernet0/1
C 10.255.0.12/30 is directly connected, GigabitEthernet0/2
```

Floor 2's `show ip interface brief` showed Gi0/1 10.255.0.10 and Gi0/2 10.255.0.14, both `up/up`. CDP at one point reported Gi0/1 -> CORE-1 Gi0/2 and Gi0/2 -> CORE-2 Gi0/1. CORE-1's `show ip interface brief` showed Gi0/1 10.255.0.1 and Gi0/2 10.255.0.9, both `up/up`.

**Failure observed before cabling correction:** Floor 2 ping to 10.255.0.9 and to 10.255.0.13 each returned 0/5. The opposite CORE-2 -> 10.255.0.14 ping also returned 0/5. Floor 2's ARP table held only its own .10 and .14 entries; CORE-2's held its own .5 and .13 plus Floor 1's .6, with no .14. The /30 subnet math and running configurations were correct; no static or dynamic routing was yet configured.

The user later reported that the core links speak to distribution. **Passing ping output after the physical correction has not been supplied**, so this document does not claim a measured failover or inter-floor route. See [the ARP drop trace](../troubleshooting/floor-2-arp-drop.md).
