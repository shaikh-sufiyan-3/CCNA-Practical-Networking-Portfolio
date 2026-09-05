# 05 - EtherChannel

## 1. Overview

This lab demonstrates **EtherChannel** configuration between two Cisco switches using **LACP**.

Two physical links between SW1 and SW2 are bundled into a single logical **Port-channel 1**. The Port-channel operates as a trunk and carries VLAN 10 traffic between the switches.

The lab also verifies end-to-end connectivity between two PCs connected to the same VLAN.

---

## 2. Objectives

* Create VLAN 10 on both switches.
* Configure PC-facing ports as access ports.
* Configure two physical links as an EtherChannel.
* Use LACP to negotiate the EtherChannel.
* Configure the Port-channel as a trunk.
* Verify EtherChannel operation.
* Test end-to-end connectivity.

---

## 3. Network Scenario

The lab contains:

* 2 Cisco 2960 switches
* 2 PCs
* VLAN 10
* 2 physical links between SW1 and SW2

Topology:

```text
PC1 ── SW1 ═══════ SW2 ── PC2
           EtherChannel
```

Connections:

* PC1 → SW1 Fa0/1
* PC2 → SW2 Fa0/1
* SW1 Fa0/23 ↔ SW2 Fa0/23
* SW1 Fa0/24 ↔ SW2 Fa0/24

---

## 4. Skills Demonstrated

* VLAN configuration
* Access port configuration
* EtherChannel configuration
* LACP
* Port-channel configuration
* Trunk configuration
* 802.1Q verification
* EtherChannel verification
* Basic Layer 2 connectivity testing

---

## 5. Prerequisites

Basic knowledge of:

* Cisco IOS CLI
* VLANs
* Access ports
* Trunk ports
* Layer 2 switching
* Basic EtherChannel concepts

---

## 6. Lab Environment

| Device | Model      | Role       |
| ------ | ---------- | ---------- |
| SW1    | Cisco 2960 | Switch     |
| SW2    | Cisco 2960 | Switch     |
| PC1    | PC         | End Device |
| PC2    | PC         | End Device |

Software:

* Cisco Packet Tracer

---

## 7. Network Design

### VLAN Plan

| VLAN | Name  | SW1   | SW2   |
| ---- | ----- | ----- | ----- |
| 10   | SALES | Fa0/1 | Fa0/1 |

### IP Addressing

| Device | IP Address    | Subnet Mask   |
| ------ | ------------- | ------------- |
| PC1    | 192.168.10.10 | 255.255.255.0 |
| PC2    | 192.168.10.20 | 255.255.255.0 |

Both PCs are in the same VLAN and IP subnet. A default gateway is not required for this lab.

### EtherChannel

| Switch | Physical Ports | Logical Interface | Protocol |
| ------ | -------------- | ----------------- | -------- |
| SW1    | Fa0/23, Fa0/24 | Po1               | LACP     |
| SW2    | Fa0/23, Fa0/24 | Po1               | LACP     |

---

## 8. Configuration Approach

### SW1

* Created VLAN 10 named SALES.
* Configured Fa0/1 as an access port in VLAN 10.
* Added Fa0/23 and Fa0/24 to EtherChannel group 1.
* Used LACP with `mode active`.
* Configured Port-channel1 as a trunk.

### SW2

The same EtherChannel configuration was applied:

* VLAN 10 named SALES.
* Fa0/1 configured as an access port.
* Fa0/23 and Fa0/24 added to EtherChannel group 1.
* LACP configured using `mode active`.
* Port-channel1 configured as a trunk.

---

## 9. Verification Approach

The following commands were used:

### VLAN Verification

```text
show vlan brief
```

### EtherChannel Verification

```text
show etherchannel summary
```

### Trunk Verification

```text
show interfaces trunk
```

### Connectivity Testing

```text
ping 192.168.10.20
```

Verification confirmed that:

* VLAN 10 is active on both switches.
* Both physical links are successfully bundled.
* LACP is operational.
* Port-channel1 is in use.
* Port-channel1 is operating as a trunk.
* VLAN 10 is forwarding across the Port-channel.
* PC1 can successfully reach PC2.

---

## 10. Testing & Expected Behavior

### EtherChannel

The expected EtherChannel state is:

```text
Po1(SU)
Fa0/23(P)
Fa0/24(P)
```

This confirms that:

* Port-channel 1 is in use.
* The EtherChannel is Layer 2.
* Both physical interfaces are successfully bundled.

### Trunk

Port-channel1 should show:

```text
Status: trunking
Encapsulation: 802.1q
```

VLAN 10 should be active and in the STP forwarding state.

### Connectivity

PC1 was tested against PC2:

```text
ping 192.168.10.20
```

Actual result:

```text
Packets: Sent = 4, Received = 4, Lost = 0 (0% loss)
```

The connectivity test was successful.

---

## 11. Troubleshooting Approach

If EtherChannel does not form, check:

1. Both physical links are connected correctly.
2. The same ports are used on both switches.
3. Both sides use the same EtherChannel group.
4. LACP is configured correctly.
5. Member interfaces have compatible configurations.
6. Port-channel1 is operational.

Useful command:

```text
show etherchannel summary
```

If connectivity fails, also verify:

```text
show vlan brief
show interfaces trunk
```

---

## 12. Key Concepts Learned

### EtherChannel

EtherChannel combines multiple physical links into one logical link.

### LACP

LACP is used to dynamically negotiate and maintain the EtherChannel.

In this lab:

```text
channel-group 1 mode active
```

was used on both switches.

### Port-channel

The physical interfaces become members of a logical interface:

```text
Port-channel1
```

### Trunk over EtherChannel

Instead of configuring the two physical links as separate trunk links, the logical Port-channel is configured as the trunk.

---

## 13. Outcome

The lab was successfully completed and verified.

The following were demonstrated:

* VLAN 10 configuration
* Access port configuration
* LACP EtherChannel
* Two physical links bundled into Port-channel1
* Port-channel trunking
* 802.1Q encapsulation
* VLAN 10 forwarding
* Successful PC-to-PC connectivity
* 0% packet loss

**Lab Status: Successfully Verified**

---

## 14. Related Files

```text
05-EtherChannel/
├── topology/
│   └── etherchannel-topology.pkt
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
│   ├── sw1-etherchannel.png
│   ├── sw2-etherchannel.png
│   └── ping-test.png
│
└── README.md
```
