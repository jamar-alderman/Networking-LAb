# Topology screenshot observations — September 28, 2026

[View the Packet Tracer screenshot](../screenshots/campus-topology-2026-09-28.png).

The image visibly shows:
- Two 3560 core switches and two 3560 floor distribution switches, with a link from each distribution to each core.
- One Server-PT device cabled to each distribution switch.
- Three-link access bundles to room switches, though the screenshot only partly covers the Floor 1 access layer.
- Unconnected/staged endpoint and wireless devices near the canvas edges.
- A red link/status triangle on the far-left access bundle. This needs CLI verification; the screenshot alone does not prove whether a member is suspended, administratively down, or affected by some other state.

The image does **not** display the exact server-facing interface names, server IP/gateway settings, SVI addresses, DHCP pools, or passing core pings. It therefore corroborates the physical topology but does not promote those planned services to verified status. Device labels on the canvas use names such as CORE-FLOOR 1/2 and may not match IOS hostnames CORE-1/CORE-2; use the CLI hostname and CDP to identify ports.
