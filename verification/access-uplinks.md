# Access-to-distribution verification

**Observed on DISTRIBUTION-FLOOR-1:** `show etherchannel summary` reported both Po1(SU) and Po2(SU). Fa0/19–21 were marked (P) in Po1; Fa0/22–24 were marked (P) in Po2. `S` denotes a Layer 2 bundle, `U` in use, and `P` a participating member.

The later `show interfaces trunk` output showed Po1 and Po2 trunking with native VLAN 99. VLANs 10,20,30,45,99 were allowed, active, and in spanning-tree forwarding state on **both** bundles. Earlier, VLANs had not been carried into the copied configuration's VLAN database; creating VLANs on the relevant switches moved the allowed-and-active field from `none` to all five VLANs. A transient VLAN 99 STP blocking state was subsequently followed by output showing VLAN 99 forwarding on both port-channels.

**Observed on DISTRIBUTION-FLOOR-2:** its supplied running config has Po1 and Po2 with Fa0/19–21 and Fa0/22–24, respectively, in active LACP mode, dot1q trunks, native 99, and allowed 10,20,30,45,99. `show ip interface brief` later showed both port-channels and all six member links `up/up`. No post-change per-VLAN forwarding output for Floor 2 is included here.

The Room 1 access peer uses one passive LACP port-channel on Fa0/19–21; Room 2 uses one passive LACP port-channel on Fa0/22–24. For the far-left Room 2 access switch, the newly supplied `show etherchannel summary` read `Po2(SU) LACP Fa0/22(P) Fa0/23(P) Fa0/24(P)`. This verifies the access-side bundle even though the topology screenshot displayed a red indicator on one drawn link. An access-switch port-channel group number need not match its peer numerically, but the physical link membership and trunk parameters must agree.

**Evidence still needed:** sanitized `show etherchannel summary`, `show interfaces trunk`, and `show spanning-tree vlan 99` captures from all four access switches and both distribution switches in the final topology.
