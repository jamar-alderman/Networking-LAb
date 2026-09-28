# Voice and data VLAN verification

Vlan30 was first observed as `192.168.30.1 up/down`, and later as `192.168.30.1 up/up`. Its `192.168.30.0/24` connected route then appeared. Selected `show mac address-table` entries:

```text
25 0001.43c5.4e05 STATIC  Fa0/7
25 0001.640b.d3bd STATIC  Fa0/8
25 0002.1669.4b15 DYNAMIC Gig0/1
25 0007.eca6.8a88 STATIC  Fa0/7
25 00d0.584b.1bc8 STATIC  Fa0/8
30 0001.43c5.4e05 STATIC  Fa0/7
30 00d0.584b.1bc8 STATIC  Fa0/8
45 0002.177a.6774 DYNAMIC Fa0/23
```

`0001.640B.D3BD` was identified as the PC on Fa0/8. VLAN 30 entries on Fa0/7 and Fa0/8 support voice VLAN learning. In this Packet Tracer workflow `show mac address-table vlan 30` was not accepted, so the full table was inspected. The phone Config tab did not expose an obvious IP view; a specific phone lease is not established by these switch entries.

**TODO:** Add the full MAC table, SVI output, screenshot, and phone-side lease/call evidence if available.
