# CORE-1 and Floor 1 distribution evidence

No full post-change `show running-config` was supplied for these two devices. The blocks below combine the commands provided for this lab with interface/status observations; they are **not verbatim running-config exports**.

## CORE-1 routed uplinks

`show ip interface brief` showed Gi0/1 `10.255.0.1 up/up` and Gi0/2 `10.255.0.9 up/up`. The intended interface commands were:

```ios
ip routing
interface GigabitEthernet0/1
 description TO-DISTRIBUTION-FLOOR-1
 no switchport
 ip address 10.255.0.1 255.255.255.252
 no shutdown
!
interface GigabitEthernet0/2
 description TO-DISTRIBUTION-FLOOR-2
 no switchport
 ip address 10.255.0.9 255.255.255.252
 no shutdown
```

## DISTRIBUTION-FLOOR-1 access and routed uplinks

The distribution's `show etherchannel summary` reported Po1(SU) Fa0/19–21(P) and Po2(SU) Fa0/22–24(P). Its `show interfaces trunk` reported both port-channels trunking with native VLAN 99 and all five VLANs allowed, active, and forwarding. Earlier `show vlan brief` showed VLAN 10 USERS, 20 VOICE, 30 SERVERS, 45 GUEST, and 99 MGMT. The routed interface plan supplied for this device was:

```ios
ip routing
interface GigabitEthernet0/1
 description TO-CORE-1
 no switchport
 ip address 10.255.0.2 255.255.255.252
 no shutdown
!
interface GigabitEthernet0/2
 description TO-CORE-2
 no switchport
 ip address 10.255.0.6 255.255.255.252
 no shutdown
```

CORE-2's ARP table learned 10.255.0.6 on Gi0/2, supporting connectivity on that link at the time of the capture. Final `show running-config` and bidirectional pings remain to be added.
