# Supplied campus configuration captures

These three text files are copies of the uploaded configuration exports. They capture the **earlier LACP/trunk build stage**, not the complete September 29 configuration. Their default endpoint ports and absent routed/SVI/OSPF settings should not be interpreted as the final running configuration.

| Capture | Observed content |
| --- | --- |
| [Floor 2 Room 1](floor-2-room-1.txt) | Hostname FLOOR-2-ROOM-1; Po1; Fa0/19–21 LACP passive; native 99; allowed 10,20,30,45,99 |
| [Floor 2 Room 2](floor-2-room-2.txt) | Export hostname Switch; source filename identifies Room 2; Po2; Fa0/22–24 passive; matching trunk VLANs |
| [Distribution switching-stage export](distribution-switching-stage.txt) | Export hostname Switch; floor not identified; Po1/Po2; Fa0/19–24 LACP active; explicit dot1q encapsulation |

The exports are retained as supplied, with line endings normalized to LF. For the later service/routing state, see [the September 29 record](../../verification/campus-services-2026-09-29.md), [current addressing](../../address-plan.md), and the existing observed core/distribution captures elsewhere in configs/.
