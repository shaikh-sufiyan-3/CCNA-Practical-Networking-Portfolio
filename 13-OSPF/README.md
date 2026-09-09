# 13 - OSPF

## 1. Overview

This project demonstrates dynamic routing using Open Shortest Path First (OSPF).

Two routers are connected through a point-to-point network, with each router connected to a separate LAN. OSPF Area 0 is configured so that each router dynamically learns the remote LAN network.

---

## 2. Objectives

* Configure IPv4 addressing on routers and PCs.
* Configure OSPF on R1 and R2.
* Use OSPF Area 0.
* Establish an OSPF neighbor adjacency.
* Verify dynamically learned routes.
* Test end-to-end connectivity between both LANs.

---

## 3. Network Scenario

```text
PC1 ── SW1 ── R1 ───── R2 ── SW2 ── PC2
```

R1 connects the `192.168.10.0/24` LAN and R2 connects the `192.168.20.0/24` LAN.

The routers are connected through the `10.0.0.0/30` network.

OSPF is used instead of manually configured routes.

---

## 4. Skills Demonstrated

* OSPF configuration
* OSPF Area 0
* OSPF router IDs
* OSPF neighbor adjacency
* Dynamic route learning
* IPv4 routing
* Routing-table verification
* End-to-end connectivity testing

---

## 5. Prerequisites

* Basic Cisco IOS CLI knowledge
* Understanding of IPv4 addressing
* Basic routing concepts
* Basic understanding of OSPF
* Cisco Packet Tracer

---

## 6. Lab Environment

| Device | Role                        |
| ------ | --------------------------- |
| R1     | OSPF router / LAN 1 gateway |
| R2     | OSPF router / LAN 2 gateway |
| SW1    | LAN 1 switch                |
| SW2    | LAN 2 switch                |
| PC1    | LAN 1 host                  |
| PC2    | LAN 2 host                  |

---

## 7. Network Design

### LAN 1

* Network: `192.168.10.0/24`
* R1 G0/0: `192.168.10.1`
* PC1: `192.168.10.10`
* Gateway: `192.168.10.1`

### R1-R2 Link

* Network: `10.0.0.0/30`
* R1 G0/1: `10.0.0.1`
* R2 G0/1: `10.0.0.2`

### LAN 2

* Network: `192.168.20.0/24`
* R2 G0/0: `192.168.20.1`
* PC2: `192.168.20.10`
* Gateway: `192.168.20.1`

### OSPF

* Process ID: `1`
* Area: `0`
* R1 Router ID: `1.1.1.1`
* R2 Router ID: `2.2.2.2`

---

## 8. Configuration Approach

R1 advertises:

```text
192.168.10.0/24
10.0.0.0/30
```

R2 advertises:

```text
192.168.20.0/24
10.0.0.0/30
```

Both routers participate in OSPF Area 0.

No static route is required for the remote LANs.

---

## 9. Verification Approach

The following commands were used:

```text
show ip interface brief
show ip ospf neighbor
show ip route
```

PC connectivity was verified using:

```text
ipconfig
ping
```

The most important OSPF verification was the neighbor state and the `O` routes in the routing tables.

---

## 10. Testing & Expected Behavior

R1 successfully formed an OSPF adjacency with R2:

```text
2.2.2.2    FULL/BDR    10.0.0.2
```

R2 successfully formed an OSPF adjacency with R1:

```text
1.1.1.1    FULL/DR     10.0.0.1
```

R1 learned:

```text
O 192.168.20.0/24 via 10.0.0.2
```

R2 learned:

```text
O 192.168.10.0/24 via 10.0.0.1
```

All tested connectivity paths completed with **0% packet loss**.

---

## 11. Troubleshooting Approach

If the OSPF route is missing:

1. Check interface status with `show ip interface brief`.
2. Verify the router-to-router IP addresses.
3. Check `show ip ospf neighbor`.
4. Confirm the neighbor state reaches `FULL`.
5. Check `show ip route` for `O` routes.
6. Verify PC IP addresses and default gateways.
7. Test connectivity progressively from the local gateway to the remote PC.

The OSPF neighbor relationship should be verified before troubleshooting the learned routes.

---

## 12. Key Concepts Learned

* OSPF is a dynamic routing protocol.
* Routers form neighbor relationships before exchanging routing information.
* Area 0 is the OSPF backbone area.
* `FULL` indicates a fully established OSPF adjacency.
* `O` in the routing table identifies an OSPF-learned route.
* OSPF uses administrative distance `110` for internal OSPF routes.
* Dynamic routing removes the need to manually configure every remote network.

---

## 13. Outcome

OSPF was successfully configured between R1 and R2 using Area 0.

Both routers established FULL OSPF adjacencies and dynamically learned the remote LAN routes.

End-to-end connectivity between PC1 and PC2 was successfully verified in both directions with **0% packet loss**.

**Project Status: COMPLETE / VERIFIED**

---

## 14. Related Files

```text
13-OSPF/
├── topology/
│   └── 13-OSPF-Lab.pkt
├── configuration/
│   ├── R1-config.txt
│   ├── R2-config.txt
│   ├── SW1-config.txt
│   └── SW2-config.txt
├── verification/
│   └── verification.md
├── screenshots/
│   ├── topology.png
│   ├── ospf-verification.png
│   └── ping-test.png
└── README.md
```
