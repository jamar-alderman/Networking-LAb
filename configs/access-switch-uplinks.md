# Room switch uplink templates and observed state

Floor distribution switches use Fa0/19–21 in Po1 to Room 1 and Fa0/22–24 in Po2 to Room 2. Each room switch has **one** bundle to its distribution: Room 1 Fa0/19–21 in Po1, Room 2 Fa0/22–24 in Po2. The access side was configured in LACP passive mode; the distribution side was active. The channel group number only needs to match between local physical members and their local Port-channel interface.

The following represents the access-side configuration described in the device outputs. On a 2960, `switchport trunk encapsulation dot1q` may not be available and is not required. Distribution 3560 trunks did require selecting dot1q before forcing trunk mode.

```ios
! Room 1 access switch
interface Port-channel1
 switchport mode trunk
 switchport trunk native vlan 99
 switchport trunk allowed vlan 10,20,30,45,99
!
interface range FastEthernet0/19 - 21
 switchport mode trunk
 switchport trunk native vlan 99
 switchport trunk allowed vlan 10,20,30,45,99
 channel-group 1 mode passive
```

```ios
! Room 2 access switch
interface Port-channel2
 switchport mode trunk
 switchport trunk native vlan 99
 switchport trunk allowed vlan 10,20,30,45,99
!
interface range FastEthernet0/22 - 24
 switchport mode trunk
 switchport trunk native vlan 99
 switchport trunk allowed vlan 10,20,30,45,99
 channel-group 2 mode passive
```

Create VLANs 10/20/30/45/99 locally on every access switch. Copying running configuration from another switch did not transfer the VLAN database in this lab. Host-facing Fa0/1–18 were not yet assigned to user, voice, guest, or server VLANs in the supplied running configs.

Observed Floor 1 distribution: Po1(SU) and Po2(SU) with all six member ports (P); both trunks forwarding all five VLANs. Floor 2 distribution: both Po interfaces and six member ports `up/up` in the supplied `show ip interface brief`. See [verification](../verification/access-uplinks.md).
