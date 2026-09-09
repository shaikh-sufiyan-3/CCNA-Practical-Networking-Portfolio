# 15 - ACL

## 1. Overview

This project demonstrates the configuration and verification of an Extended Access Control List (ACL) on a Cisco router.

The ACL is used to control communication between two VLANs. In this lab, traffic from PC1 in VLAN 10 to PC2 in VLAN 20 is intentionally blocked, while reverse communication from PC2 to PC1 remains allowed.

## 2. Objectives

* Configure VLAN 10 and VLAN 20.
* Configure router-on-a-stick inter-VLAN routing.
* Configure an Extended ACL.
* Apply the ACL in the correct direction.
* Verify ACL matching using Cisco IOS commands.
* Test permitted and denied traffic.

## 3. Network Scenario

The network contains:

* One Cisco 2960 switch.
* One Cisco router.
* Two PCs.
* VLAN 10 named SALES.
* VLAN 20 named HR.
* An 802.1Q trunk between SW1 and R1.

The ACL requirement is:

```text
PC1 (192.168.10.10) → PC2 (192.168.20.10) = BLOCK
PC2 (192.168.20.10) → PC1 (192.168.10.10) = ALLOW
```

## 4. Skills Demonstrated

* VLAN configuration
* Access port configuration
* Trunk configuration
* Router-on-a-stick
* Extended ACL configuration
* ACL direction and placement
* ACL verification
* Connectivity testing
* Interpretation of ACL match counters

## 5. Prerequisites

* Cisco Packet Tracer
* Basic Cisco IOS knowledge
* Basic IPv4 addressing
* Basic VLAN and trunk knowledge
* Basic understanding of router-on-a-stick

## 6. Lab Environment

| Device       | Role                       |
| ------------ | -------------------------- |
| Cisco 2960   | Layer 2 switch             |
| Cisco Router | Inter-VLAN routing and ACL |
| PC1          | VLAN 10 host               |
| PC2          | VLAN 20 host               |

## 7. Network Design

| Device | Interface | VLAN | IP Address       |
| ------ | --------- | ---: | ---------------- |
| PC1    | SW1 Fa0/1 |   10 | 192.168.10.10/24 |
| PC2    | SW1 Fa0/2 |   20 | 192.168.20.10/24 |
| R1     | G0/0.10   |   10 | 192.168.10.1/24  |
| R1     | G0/0.20   |   20 | 192.168.20.1/24  |

Default gateways:

* PC1 → `192.168.10.1`
* PC2 → `192.168.20.1`

SW1 Fa0/24 is the trunk toward R1.

## 8. Configuration Approach

VLAN 10 and VLAN 20 were created on SW1.

PC1 was assigned to VLAN 10 and PC2 was assigned to VLAN 20.

The SW1-to-R1 connection was configured as an 802.1Q trunk.

R1 uses two subinterfaces:

* G0/0.10 for VLAN 10
* G0/0.20 for VLAN 20

Extended ACL 100 was configured as:

```text
access-list 100 deny ip host 192.168.10.10 host 192.168.20.10
access-list 100 permit ip any any
```

The ACL was applied inbound on G0/0.10.

This placement allows the router to filter traffic originating from PC1's VLAN before it is routed toward VLAN 20.

## 9. Verification Approach

The following commands were used:

```text
show ip interface brief
show access-lists
show ip interface GigabitEthernet0/0.10
show vlan brief
show interfaces trunk
```

Connectivity was tested from both PCs.

## 10. Testing & Expected Behavior

### PC1 → Gateway

Expected: successful.

Actual: 4/4 replies, 0% loss.

### PC1 → PC2

Expected: blocked by ACL 100.

Actual: 4/4 packets lost, 100% loss.

The ACL deny statement recorded 4 matches.

### PC2 → PC1

Expected: successful because the ACL is applied inbound only on VLAN 10.

Actual: 4/4 replies, 0% loss.

## 11. Troubleshooting Approach

The following areas were checked:

1. Router subinterfaces were checked for `up/up` status.
2. VLAN membership was verified on SW1.
3. The trunk status was verified.
4. ACL entries and match counters were checked.
5. ACL direction on G0/0.10 was verified.
6. Connectivity was tested from both directions.

## 12. Key Concepts Learned

* ACLs control traffic according to configured rules.
* Extended ACLs can match both source and destination IP addresses.
* ACL placement and direction are important.
* ACLs are processed in order.
* The `permit ip any any` statement allows traffic that is not matched by the deny rule.
* ACL match counters provide useful verification evidence.
* A failed ping can be an intentional result of an ACL and does not automatically indicate a network fault.

## 13. Outcome

The Extended ACL was successfully configured and verified.

PC1 was blocked from reaching PC2 as intended, while PC2 successfully reached PC1.

The ACL match counters confirmed that the deny rule was actively matching traffic.

**Project Status: COMPLETE / VERIFIED**

## 14. Related Files

```text
15-ACL/
├── topology/
│   └── 15-ACL-Lab.pkt
├── configuration/
│   ├── R1-config.txt
│   └── SW1-config.txt
├── verification/
│   └── verification.md
├── screenshots/
│   ├── topology.png
│   ├── acl-verification.png
│   └── ping-test.png
└── README.md
```
