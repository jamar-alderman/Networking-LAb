# DHCP snooping: configuration and observed limitation

`show ip dhcp snooping` reported global enablement, configured VLANs `25,30,45`, **operational VLANs `none`**, and Option 82 enabled. Gi0/1 reported trusted `yes`, allow option `yes`, and rate `unlimited`; client-facing FastEthernet ports reported trusted `no`.

The trust boundary and configured VLAN list are visible in the supplied summary. Operational enforcement on VLANs 25, 30, and 45 is **not verified** because the output reported `none`. Packet Tracer behavior may explain this, but the observation alone does not establish the cause.

**TODO:** Add complete `show ip dhcp snooping` output and screenshot showing both configured and operational VLAN lines. If testing enforcement later, record the test setup and result separately.
