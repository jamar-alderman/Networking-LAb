# Routing verification

The supplied routing-table excerpt lists:

```text
C 192.168.9.0/24 is directly connected, Vlan45
C 192.168.10.0/24 is directly connected, Vlan25
C 192.168.20.0/24 is directly connected, Vlan101
C 192.168.30.0/24 is directly connected, Vlan30
C 192.168.99.0/24 is directly connected, Vlan200
```

There is no gateway of last resort in this contained lab. The connected routes support the SVI/inter-VLAN design; the excerpt does not prove end-to-end host reachability.

**TODO:** Add complete `show ip route` output and representative inter-VLAN client tests, if available. Add a DHCP relay/routing screenshot near the [main walkthrough](../README.md#centralized-dhcp-and-relay).
