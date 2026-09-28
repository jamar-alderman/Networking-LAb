# Proposed gateway and DHCP server-port configuration

**Status: proposed commands from the September 27–28 session.** The supplied Floor 2 running config predates these changes and has no VLAN SVIs or DHCP server Fa0/1 config. Do not describe this page as implemented until current device output verifies it. VLANs 10,20,30,45,99 must exist locally and trunks must be active.

## Floor 1 distribution SVIs

```ios
configure terminal
interface vlan 10
 ip address 10.1.10.1 255.255.255.0
 no shutdown
exit
interface vlan 20
 ip address 10.1.20.1 255.255.255.0
 no shutdown
exit
interface vlan 30
 ip address 10.1.30.1 255.255.255.0
 no shutdown
exit
interface vlan 45
 ip address 10.1.45.1 255.255.255.0
 no shutdown
exit
interface vlan 99
 ip address 10.1.99.1 255.255.255.0
 no shutdown
end
```

## Floor 2 distribution SVIs

```ios
configure terminal
interface vlan 10
 ip address 10.2.10.1 255.255.255.0
 no shutdown
exit
interface vlan 20
 ip address 10.2.20.1 255.255.255.0
 no shutdown
exit
interface vlan 30
 ip address 10.2.30.1 255.255.255.0
 no shutdown
exit
interface vlan 45
 ip address 10.2.45.1 255.255.255.0
 no shutdown
exit
interface vlan 99
 ip address 10.2.99.1 255.255.255.0
 no shutdown
end
```

## Proposed local server ports and static server IPs

If Fa0/1 is unused on each distribution, connect DHCP-1 to FLOOR-1 Fa0/1 and DHCP-2 to FLOOR-2 Fa0/1. Apply on **each** distribution:

```ios
configure terminal
interface FastEthernet0/1
 description DHCP-SERVER
 switchport mode access
 switchport access vlan 30
 spanning-tree portfast
 no shutdown
end
```

| Server | Static IP / mask | Default gateway |
| --- | --- | --- |
| DHCP-1 | 10.1.30.10/24 | 10.1.30.1 |
| DHCP-2 | 10.2.30.10/24 | 10.2.30.1 |

Confirm local gateway-to-server ping first. Remote client VLANs need `ip helper-address` on their **distribution SVI** after routing to the server works. Each pool needs the corresponding floor/VLAN network and gateway. Two DHCP servers are not redundant merely because both exist: if both serve the same client subnet, use nonoverlapping ranges and relay to both. DHCP snooping and DAI should follow a proven DHCP lease and binding, not precede it.

Verification: `show vlan brief`, `show ip interface brief`, `show ip route connected`, local server pings, then client leases. Static routes, OSPF, DHCP helpers, security features, guest ACLs, and failover tests have not been demonstrated in the recreated topology.
