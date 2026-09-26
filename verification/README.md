# Verification index

These notes summarize only reported switch observations from the supplied lab specification. They are not substitutes for the complete original IOS output. Add dated, sanitized captures and cross-check them against the summaries.

| Command | Status |
| --- | --- |
| `show vlan brief` | VLAN names/assignments summarized; full output TODO |
| `show ip interface brief` | Relevant SVI states summarized; full output TODO |
| `show ip route` | Five connected routes summarized; full output TODO |
| `show mac address-table` | Selected entries supplied; full output TODO |
| `show port-security` | Detailed Fa0/7 values supplied; aggregate output TODO |
| `show port-security interface fa0/7` | Selected values supplied; full output TODO |
| `show port-security interface fa0/8` | TODO |
| `show ip dhcp snooping` | Key fields supplied, including operational VLANs none; full output TODO |
| `show ntp status` | Synchronization line supplied; full output TODO |
| `show clock` | Updated to Aug 2, 2026; exact output TODO |
| `show running-config` | Selected snippets supplied; sanitized full output TODO |

Configuration alone does not prove a feature worked; reported device state also has limits. Add client-side tests where a claim depends on actual client connectivity.
