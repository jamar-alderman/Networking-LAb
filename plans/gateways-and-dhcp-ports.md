# Gateway and DHCP implementation reference

The earlier proposed 10.1.x/10.2.x addressing was superseded by the [September 29 address map](../address-plan.md). The builder confirmed working DHCP for PCs and phones on both floors.

Servers use static addresses in VLAN 30: Floor 1 192.168.30.10/24 with gateway 192.168.30.1, and Floor 2 192.168.130.10/24 with gateway 192.168.130.1. Each server's distribution connection is an access port in VLAN 30; the exact physical port is not identified in the supplied exports.

The following are documented configuration excerpts, not complete running-config exports:

```ios
! Floor 1 distribution
interface vlan 10
 ip helper-address 192.168.30.10
interface vlan 20
 ip helper-address 192.168.30.10
```

```ios
! Floor 2 distribution
interface vlan 10
 ip helper-address 192.168.130.10
interface vlan 20
 ip helper-address 192.168.130.10
```

Each client DHCP pool supplies its client VLAN's gateway. A server's NIC gateway belongs to the server subnet. Gateway addresses and client networks are listed in the current address map.
