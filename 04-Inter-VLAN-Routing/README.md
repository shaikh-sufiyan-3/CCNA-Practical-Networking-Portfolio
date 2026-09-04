# 04 - Inter-VLAN Routing

## 1. Overview

This lab demonstrates **Inter-VLAN Routing** using a Cisco router and switch.

Two separate VLANs are configured on SW1:

* VLAN 10 - SALES
* VLAN 20 - HR

A router is used to provide communication between the two VLANs using the **Router-on-a-Stick** method.

---

## 2. Objectives

* Create VLAN 10 and VLAN 20.
* Assign end-device ports to the correct VLANs.
* Configure a trunk between SW1 and R1.
* Configure router subinterfaces for each VLAN.
* Configure default gateways for both PCs.
* Verify routing between VLANs.
* Test inter-VLAN connectivity.

---

## 3. Network Scenario

The lab contains:

* 1 Cisco 2960 switch
* 1 Cisco router
* 2 PCs

Topology:

```text
PC1 ── SW1 ───── R1
        │  Trunk
PC2 ────┘
```

Connections:

* PC1 → SW1 Fa0/1
* PC2 → SW1 Fa0/2
* SW1 Fa0/24 → R1 G0/0

---

## 4. Skills Demonstrated

* VLAN configuration
* Access port configuration
* Trunk configuration
* Router-on-a-Stick
* 802.1Q VLAN tagging
* Router subinterface configuration
* IPv4 default gateway configuration
* Inter-VLAN routing
* Routing table verification
* Connectivity testing

---

## 5. Prerequisites

Basic knowledge of:

* Cisco IOS CLI
* VLANs
* Access ports
* Trunk ports
* IPv4 addressing
* Default gateways
* Basic routing concepts

---

## 6. Lab Environment

| Device | Model        | Role               |
| ------ | ------------ | ------------------ |
| SW1    | Cisco 2960   | VLAN and Trunk     |
| R1     | Cisco Router | Inter-VLAN Routing |
| PC1    | PC           | VLAN 10            |
| PC2    | PC           | VLAN 20            |

Software:

* Cisco Packet Tracer

---

## 7. Network Design

### VLAN Plan

| VLAN | Name  | Port  |
| ---- | ----- | ----- |
| 10   | SALES | Fa0/1 |
| 20   | HR    | Fa0/2 |

### IP Addressing

| Device | IP Address    | Subnet Mask   | Default Gateway |
| ------ | ------------- | ------------- | --------------- |
| PC1    | 192.168.10.10 | 255.255.255.0 | 192.168.10.1    |
| PC2    | 192.168.20.10 | 255.255.255.0 | 192.168.20.1    |

### Router Subinterfaces

| Interface | VLAN | IP Address   |
| --------- | ---: | ------------ |
| G0/0.10   |   10 | 192.168.10.1 |
| G0/0.20   |   20 | 192.168.20.1 |

---

## 8. Configuration Approach

### SW1

SW1 was configured with:

* VLAN 10 named SALES
* VLAN 20 named HR
* Fa0/1 as an access port in VLAN 10
* Fa0/2 as an access port in VLAN 20
* Fa0/24 as a trunk port toward R1

### R1

R1 was configured using Router-on-a-Stick:

* G0/0.10 for VLAN 10
* G0/0.20 for VLAN 20
* 802.1Q encapsulation
* `192.168.10.1` as the VLAN 10 gateway
* `192.168.20.1` as the VLAN 20 gateway

---

## 9. Verification Approach

The following commands were used:

### SW1

```text
show vlan brief
show interface trunk
```

### R1

```text
show ip interface brief
show ip route
```

### PC1

```text
ping 192.168.20.10
```

Verification confirmed that both VLANs were active, the trunk was operational, both router subinterfaces were up, and both networks were present in the routing table.

---

## 10. Testing & Expected Behavior

PC1 belongs to VLAN 10:

```text
192.168.10.10
```

PC2 belongs to VLAN 20:

```text
192.168.20.10
```

Because the PCs are in different VLANs, their traffic must pass through R1 for communication.

The initial ping test produced:

```text
Sent = 4
Received = 3
Lost = 1
25% loss
```

The first request timed out and the following three requests were successful.

This can occur during initial ARP resolution. A repeated ping should ideally show 4 successful replies and 0% packet loss.

---

## 11. Troubleshooting Approach

If inter-VLAN communication fails, check:

1. VLAN 10 and VLAN 20 exist on SW1.
2. Fa0/1 is assigned to VLAN 10.
3. Fa0/2 is assigned to VLAN 20.
4. Fa0/24 is operating as a trunk.
5. VLAN 10 and VLAN 20 are active on the trunk.
6. R1 subinterfaces are up/up.
7. PC default gateways are correct.
8. R1 routing table contains both networks.

Useful commands:

```text
show vlan brief
show interfaces trunk
show ip interface brief
show ip route
```

---

## 12. Key Concepts Learned

### Inter-VLAN Routing

Different VLANs are separate Layer 2 broadcast domains. A Layer 3 device such as a router is required for communication between them.

### Router-on-a-Stick

A single physical router interface can use multiple subinterfaces to route traffic for multiple VLANs.

### Default Gateway

Each PC uses the router subinterface in its own VLAN as its default gateway.

### 802.1Q

802.1Q provides VLAN tagging on the trunk link between the switch and router.

---

## 13. Outcome

The lab successfully demonstrated:

* VLAN 10 and VLAN 20 configuration
* Access port configuration
* Trunk configuration
* 802.1Q encapsulation
* Router-on-a-Stick configuration
* Layer 3 routing between VLANs
* Successful replies between the two VLAN networks

The initial connectivity test showed one lost packet during the first ping, followed by successful replies.

**Lab Status: Configuration Successfully Verified**

---

## 14. Related Files

```text
04-Inter-VLAN-Routing/
├── topology/
│   └── inter-vlan-routing.pkt
│
├── configuration/
│   ├── SW1-config.txt
│   └── R1-config.txt
│
├── verification/
│   └── verification.md
│
├── screenshots/
│   ├── topology.png
│   ├── sw1-verification.png
│   ├── r1-verification.png
│   └── inter-vlan-ping.png
│
└── README.md
```
