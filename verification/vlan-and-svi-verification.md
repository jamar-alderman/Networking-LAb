# VLAN and SVI verification

The supplied summary reports VLANs 25 ENDusrs, 30 VOICE, 35 MNGMNT, 45 MNGMNTUSRS, 101 ACL, and 200 OTHERS. SVIs 25, 30, 45, 101, and 200 eventually showed `up/up`. Vlan30 previously showed `up/down`; see [voice troubleshooting](../troubleshooting/voice-vlan-svi.md). VLAN 35's subnet/SVI is not established.

**TODO:** Add unabridged `show vlan brief` and `show ip interface brief` output and the corresponding screenshot. Check VLAN names, access-port assignments, and SVI status against the [addressing table](../README.md#topology-and-architecture).
