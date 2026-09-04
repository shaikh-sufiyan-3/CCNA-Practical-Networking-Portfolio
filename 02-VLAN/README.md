# 02 - VLAN Configuration & Segmentation

## 1. Overview

This lab demonstrates VLAN configuration and network segmentation on a Cisco switch.

VLANs are used to logically separate devices into different broadcast domains. In this lab, two VLANs are created and assigned to different switch ports to demonstrate basic network segmentation.

## 2. Objectives

* Create and configure VLANs on a Cisco switch.
* Assign switch access ports to specific VLANs.
* Verify VLAN configuration and port assignments.
* Demonstrate communication behavior between different VLANs.

## 3. Network Scenario

A small office network needs to separate two departments using VLANs.

* **SALES** devices are placed in VLAN 10.
* **HR** devices are placed in VLAN 20.

The departments are logically separated even though they are connected to the same physical switch.

## 4. Skills Demonstrated

* VLAN creation
* VLAN naming
* Access port configuration
* VLAN port assignment
* VLAN verification
* Basic connectivity testing

## 5. Prerequisites

* Cisco Packet Tracer
* Basic Cisco IOS knowledge
* Basic networking knowledge
* Basic understanding of IPv4 addressing

## 6. Lab Environment

| Component    | Details             |
| ------------ | ------------------- |
| Simulator    | Cisco Packet Tracer |
| Switch       | Cisco 2960          |
| End Devices  | PC1, PC2            |
| Network Type | LAN                 |
| Technology   | VLAN                |

## 7. Network Design

The lab uses one Cisco switch with two connected PCs.

| Device | Switch Port | VLAN            | IP Address       |
| ------ | ----------- | --------------- | ---------------- |
| PC1    | Fa0/1       | VLAN 10 - SALES | 192.168.10.10/24 |
| PC2    | Fa0/2       | VLAN 20 - HR    | 192.168.20.10/24 |

PC1 and PC2 are placed in different VLANs. Since no Inter-VLAN Routing is configured, traffic between the two VLANs is not routed.

## 8. Configuration Approach

The switch was configured with two VLANs:

* VLAN 10 — SALES
* VLAN 20 — HR

The connected switch ports were configured as access ports and assigned to their respective VLANs.

The actual configuration is available in the `configuration/` folder.

## 9. Verification Approach

The VLAN configuration was verified using:

```text
show vlan brief
```

This command was used to confirm that VLAN 10 and VLAN 20 were active and that the correct switch ports were assigned to each VLAN.

Connectivity was tested from PC1 to PC2 using `ping`.

The complete verification evidence is available in the `verification/` folder.

## 10. Testing & Expected Behavior

The following tests were performed:

* Verified VLAN 10 and VLAN 20.
* Verified Fa0/1 assignment to VLAN 10.
* Verified Fa0/2 assignment to VLAN 20.
* Tested connectivity between PC1 and PC2.

### Expected Behavior

* PC1 belongs to VLAN 10.
* PC2 belongs to VLAN 20.
* PC1 and PC2 should not communicate because they are in different VLANs and no Inter-VLAN Routing is configured.
* The ping test should therefore fail.

## 11. Troubleshooting Approach

The following logical troubleshooting steps were used:

1. Check physical connections.
2. Verify the correct switch ports.
3. Check VLAN creation using `show vlan brief`.
4. Verify port-to-VLAN assignments.
5. Check the IP configuration of the PCs.
6. Test connectivity using `ping`.

## 12. Key Concepts Learned

* VLANs provide logical network segmentation.
* Each VLAN represents a separate broadcast domain.
* Access ports can be assigned to specific VLANs.
* Devices in different VLANs require routing to communicate.
* `show vlan brief` is useful for verifying VLAN membership.

## 13. Outcome

Successfully created VLAN 10 (SALES) and VLAN 20 (HR), assigned the appropriate switch ports, verified the configuration, and demonstrated that communication between different VLANs is blocked without Inter-VLAN Routing.

## 14. Related Files

* `topology/` → Network topology and Packet Tracer lab file
* `configuration/` → SW1 VLAN configuration
* `verification/` → VLAN verification and connectivity test
* `screenshots/` → Visual evidence of the lab

