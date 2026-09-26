# Voice VLAN SVI changed state

## Problem

Vlan30 initially reported `192.168.30.1 up/down`.

## Investigation / evidence

Phone power and link state were investigated. Power adapter changes produced `%ILPOWER-5-IEEE_DISCONNECT` and line-protocol changes. See [phone power notes](phone-power-and-link-state.md).

## Resolution

The connectivity/power issue was resolved and links returned green. The supplied summary does not specify every physical troubleshooting step.

## Verification / current state

Vlan30 later reported `192.168.30.1 up/up`, and the routing table showed `C 192.168.30.0/24 is directly connected, Vlan30`. MAC entries in VLAN 30 appeared on Fa0/7 and Fa0/8. This does not by itself identify the phones' leased IPs.

**TODO:** Add before/after screenshots or full switch output.
