# 03 - Access & Trunk Ports

## 1. Overview

This lab demonstrates the use of **Access Ports** and **Trunk Ports** on Cisco switches.

Two Cisco 2960 switches are connected through a trunk link. Both end devices are placed in **VLAN 10 (SALES)**. The trunk allows VLAN 10 traffic to pass between the switches.

The lab verifies VLAN assignment, trunk operation, and end-to-end connectivity.

---

## 2. Objectives

* Configure VLAN 10 on both switches.
* Configure end-device ports as access ports.
* Configure the switch-to-switch link as a trunk port.
* Verify VLAN and trunk configuration.
* Test connectivity between devices connected to different switches.

---

## 3. Network Scenario

The network contains:

* 2 Cisco 2960 switches
* 2 PCs
* VLAN 10 - SALES
* One trunk link between SW1 and SW2

Topology:

```text
PC1 ── SW1 ═════════ SW2 ── PC2
       Fa0/1  Trunk  Fa0/24
                      Fa0/24
                         Fa0/1
```

Connections:

* PC1 → SW1 Fa0/1
* SW1 Fa0/24 → SW2 Fa0/24
* PC2 → SW2 Fa0/1

---

## 4. Skills Demonstrated

* VLAN creation
* Access port configuration
* Trunk port configuration
* 802.1Q trunk verification
* VLAN membership verification
* Basic Layer 2 connectivity testing
* Cisco IOS CLI configuration

---

## 5. Prerequisites

Basic knowledge of:

* Cisco IOS CLI
* VLANs
* Access ports
* Trunk ports
* IPv4 addressing
* Ping testing

---

## 6. Lab Environment

| Device | Model      | Role           |
| ------ | ---------- | -------------- |
| SW1    | Cisco 2960 | Access + Trunk |
| SW2    | Cisco 2960 | Access + Trunk |
| PC1    | PC         | End Device     |
| PC2    | PC         | End Device     |

Software:

* Cisco Packet Tracer

---

## 7. Network Design

### VLAN Configuration

| VLAN | Name  | Device Port |
| ---- | ----- | ----------- |
| 10   | SALES | SW1 Fa0/1   |
| 10   | SALES | SW2 Fa0/1   |

### IP Addressing

| Device | IP Address    | Subnet Mask   |
| ------ | ------------- | ------------- |
| PC1    | 192.168.10.10 | 255.255.255.0 |
| PC2    | 192.168.10.20 | 255.255.255.0 |

Both PCs belong to the same IP subnet and VLAN, so a default gateway is not required for this lab.

### Port Roles

| Switch | Port   | Mode   | Purpose   |
| ------ | ------ | ------ | --------- |
| SW1    | Fa0/1  | Access | PC1       |
| SW1    | Fa0/24 | Trunk  | SW1 ↔ SW2 |
| SW2    | Fa0/1  | Access | PC2       |
| SW2    | Fa0/24 | Trunk  | SW2 ↔ SW1 |

---

## 8. Configuration Approach

The configuration was performed using Cisco IOS CLI.

### SW1

* Created VLAN 10 named SALES.
* Configured Fa0/1 as an access port in VLAN 10.
* Configured Fa0/24 as a trunk port.

### SW2

* Created VLAN 10 named SALES.
* Configured Fa0/1 as an access port in VLAN 10.
* Configured Fa0/24 as a trunk port.

The switch-to-switch connection uses **802.1Q trunking**.

---

## 9. Verification Approach

The following commands were used to verify the configuration:

```text
show vlan brief
show interfaces trunk
```

Connectivity was tested from PC1 using:

```text
ping 192.168.10.20
```

Verification confirmed:

* VLAN 10 is active on both switches.
* Fa0/1 is assigned to VLAN 10.
* Fa0/24 is operating as a trunk.
* VLAN 10 is active and forwarding across the trunk.
* PC1 can successfully reach PC2.

---

## 10. Testing & Expected Behavior

### VLAN Verification

VLAN 10 should appear as:

```text
VLAN  Name      Status    Ports
10    SALES     active    Fa0/1
```

### Trunk Verification

Fa0/24 should show:

```text
Status: trunking
Encapsulation: 802.1q
```

VLAN 10 should be listed as active and forwarding on the trunk.

### Connectivity Test

PC1:

```text
C:\>ping 192.168.10.20
```

Expected result:

```text
4 replies received
0% packet loss
```

The actual lab test successfully achieved **0% packet loss**.

---

## 11. Troubleshooting Approach

If connectivity fails, check the following:

1. Confirm VLAN 10 exists on both switches.
2. Confirm PC-facing Fa0/1 is assigned to VLAN 10.
3. Confirm Fa0/24 is operating as a trunk.
4. Check that VLAN 10 is active on the trunk.
5. Verify PC1 and PC2 have correct IP addresses and subnet masks.
6. Test connectivity again using `ping`.

Useful commands:

```text
show vlan brief
show interfaces trunk
```

---

## 12. Key Concepts Learned

### Access Port

An access port connects an end device to a specific VLAN.

Example:

```text
Fa0/1 → VLAN 10
```

### Trunk Port

A trunk port is used to carry VLAN traffic between network devices.

Example:

```text
SW1 Fa0/24 ↔ SW2 Fa0/24
```

### 802.1Q

802.1Q is the VLAN tagging method used on the trunk link.

### VLAN Continuity

The trunk allows VLAN 10 to exist across both switches, allowing PC1 and PC2 to communicate as members of the same VLAN.

---

## 13. Outcome

The lab was successfully completed and verified.

The following were successfully demonstrated:

* VLAN 10 configuration
* Access port configuration
* Trunk port configuration
* 802.1Q trunking
* VLAN 10 forwarding across the trunk
* Successful PC-to-PC connectivity

**Lab Status: Successfully Verified**

---

## 14. Related Files

```text
03-Access-and-Trunk-Ports/
├── topology/
│   └── access-trunk-topology.pkt
│
├── configuration/
│   ├── SW1-config.txt
│   └── SW2-config.txt
│
├── verification/
│   └── verification.md
│
├── screenshots/
│   ├── topology.png
│   ├── sw1-verification.png
│   ├── sw2-verification.png
│   └── ping-test.png
│
└── README.md
```

