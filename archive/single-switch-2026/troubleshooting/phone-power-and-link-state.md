# Phone power and link state

## Problem

The Cisco 7960-type Packet Tracer phone/link state affected voice-side connectivity during the lab.

## Investigation / evidence

Plugging and unplugging a phone power adapter generated `%ILPOWER-5-IEEE_DISCONNECT` and line-protocol changes. The phone Config tab did not expose an obvious IP configuration view in this workflow.

## Resolution

After the phone/link issue was resolved, links returned green. The exact adapter sequence and phone-side lease are not supplied.

## Verification / current state

Vlan30 reached up/up and its connected route appeared. Switch MAC-table observations are in [voice verification](../verification/voice-vlan-verification.md).

**TODO:** Add event-log and final topology screenshots, if available.
