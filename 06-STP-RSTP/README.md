# 06 - STP / RSTP

## 1. Overview

This project demonstrates Spanning Tree Protocol using Rapid PVST+ (RSTP) on two Cisco switches.

Two parallel Layer 2 links are intentionally configured between the switches. RSTP prevents a switching loop by placing one redundant path into an alternate/blocking state.

## 2. Objectives

* Understand the purpose of STP/RSTP.
* Configure Rapid PVST+.
* Identify the root bridge.
* Identify root, designated, and alternate ports.
* Verify STP port states.
* Understand how RSTP prevents Layer 2 loops.
* Verify network connectivity after STP convergence.

## 3. Network Scenario

The network contains two switches connected by two parallel trunk links.

PC1 is connected to SW1 and PC2 is connected to SW2.

Both PCs belong to VLAN 10.

The two parallel links create a redundant Layer 2 path. RSTP is used to prevent a switching loop.

SW1 is configured as the root bridge for VLAN 10.

## 4. Skills Demonstrated

* VLAN configuration
* Access port configuration
* Trunk configuration
* Rapid PVST+ configuration
* Root bridge selection
* STP role identification
* STP state verification
* Layer 2 loop prevention
* Connectivity testing

## 5. Prerequisites

* Basic Cisco IOS CLI knowledge
* Basic VLAN knowledge
* Basic trunking knowledge
* Cisco Packet Tracer
* Two Cisco 2960 switches
* Two PCs

## 6. Lab Environment

| Device | Role             |
| ------ | ---------------- |
| SW1    | Root Bridge      |
| SW2    | Secondary Switch |
| PC1    | End Device       |
| PC2    | End Device       |

Protocol:

```text
Rapid PVST+
```

VLAN:

```text
VLAN 10 - SALES
```

## 7. Network Design

### Connections

```text
PC1 ── SW1
       ║ ║
       ║ ║
       SW2 ── PC2
```

### Switch Links

```text
SW1 Fa0/23 ↔ SW2 Fa0/23
SW1 Fa0/24 ↔ SW2 Fa0/24
```

### PC Addressing

| Device | VLAN | IP Address    | Subnet Mask   |
| ------ | ---: | ------------- | ------------- |
| PC1    |   10 | 192.168.10.10 | 255.255.255.0 |
| PC2    |   10 | 192.168.10.20 | 255.255.255.0 |

No default gateway is required because both PCs are in the same VLAN and subnet.

## 8. Configuration Approach

VLAN 10 was created on both switches.

Fa0/1 was configured as an access port for the connected PC.

Fa0/23 and Fa0/24 were configured as trunk ports between the switches.

Rapid PVST+ was enabled using:

```text
spanning-tree mode rapid-pvst
```

SW1 was configured as the primary root bridge:

```text
spanning-tree vlan 10 root primary
```

SW2 was configured as the secondary root:

```text
spanning-tree vlan 10 root secondary
```

## 9. Verification Approach

The following commands were used:

```text
show vlan brief
show interfaces trunk
show spanning-tree vlan 10
show spanning-tree summary
```

Connectivity was tested from PC1 using:

```text
ping 192.168.10.20
```

## 10. Testing & Expected Behavior

SW1 was verified as the root bridge for VLAN 10.

SW2 selected Fa0/23 as its Root Port and placed Fa0/24 into the Alternate/Blocking state.

This demonstrates that RSTP prevents a Layer 2 loop while maintaining a redundant physical path.

PC1 successfully reached PC2.

The final ping result was:

```text
Packets: Sent = 4, Received = 4, Lost = 0 (0% loss)
```

## 11. Troubleshooting Approach

The following areas were checked during verification:

1. VLAN 10 exists on both switches.
2. PC-facing Fa0/1 ports are assigned to VLAN 10.
3. SW1-SW2 links are operating as trunks.
4. Rapid PVST+ is enabled.
5. SW1 is the root bridge.
6. SW2 has one Root Port and one Alternate/Blocking port.
7. End-to-end connectivity is successful.

## 12. Key Concepts Learned

### Root Bridge

The root bridge is the central reference point used by STP/RSTP to calculate the Layer 2 topology.

### Root Port

A non-root switch uses its Root Port as the best path toward the root bridge.

### Designated Port

A designated port provides the forwarding path for a network segment.

### Alternate Port

An alternate port provides a backup path and can remain in a discarding/blocking state to prevent a Layer 2 loop.

### RSTP

Rapid PVST+ provides faster spanning-tree convergence than traditional 802.1D STP.

## 13. Outcome

The STP/RSTP lab was successfully completed.

The lab demonstrated:

* Rapid PVST+ operation
* Root bridge selection
* STP port roles
* Alternate/blocking path
* Layer 2 loop prevention
* Successful network connectivity

The actual verification output confirmed that SW1 is the root bridge and SW2 Fa0/24 is the alternate/blocking path.

## 14. Related Files

```text
topology/
configuration/
    SW1-config.txt
    SW2-config.txt
verification/
    verification.md
screenshots/
    topology.png
    sw1-spanning-tree.png
    sw2-spanning-tree.png
    trunk-verification.png
    ping-test.png
```
