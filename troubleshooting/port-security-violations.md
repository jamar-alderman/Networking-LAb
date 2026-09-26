# Port-security violations on phone/PC ports

## Problem

The original maximum of two secure MAC addresses caused violations during Packet Tracer phone+PC MAC learning.

## Investigation / evidence

The later `Fa0/7` status reported Restrict mode and a historical violation count of six. The lab also tested/observed Protect, Restrict, and Shutdown behavior, but exact per-mode command output has not been supplied.

## Resolution

The maximum was increased from two to three while sticky learning and Restrict mode were retained on the representative Fa0/7 configuration. Fa0/8 uses a similar design; its full output is pending.

## Verification / current state

Fa0/7 later reported Secure-up, maximum three, two total secure MACs, and two sticky MACs. The historical violation count remained six. See [status values](../verification/port-security-verification.md).

**TODO:** Add before/after CLI captures and per-mode test output if retained.
