# 12 - Default Route

## 1. Overview

This project demonstrates the configuration and verification of a static default route in a small routed network.

R1 uses a default route to forward traffic for unknown destination networks toward R2. R2 uses a specific static route to provide the return path to the 192.168.10.0/24 network.

The lab demonstrates how default routing can simplify routing-table configuration when one router has a single preferred upstream path.

---

## 2. Objectives

* Configure IPv4 addressing on routers and PCs.
* Configure a static default route on R1.
* Configure a return static route on R2.
* Verify routing-table entries.
* Verify gateway and inter-router connectivity.
* Verify end-to-end connectivity between both LANs.
* Understand the purpose of a default route.

---

## 3. Network Scenario

The network contains two LANs connected through two routers.

```text
PC1 ── SW1 ── R1 ───── R2 ── SW2 ── PC2
```

R1 is connected to the 192.168.10.0/24 LAN and R2 is connected to the 192.168.20.0/24 LAN.

The router-to-router connection uses the 10.0.0.0/30 network.

R1 does not have a specific route for 192.168.20.0/24. Instead, it uses a default route toward R2.

---

## 4. Skills Demonstrated

* IPv4 addressing
* Static routing
* Default route configuration
* Routing-table verification
* Gateway verification
* End-to-end connectivity testing
* Basic Cisco IOS troubleshooting

---

## 5. Prerequisites

* Basic Cisco IOS CLI knowledge
* Understanding of IPv4 addressing
* Basic understanding of routing
* Cisco Packet Tracer

---

## 6. Lab Environment

| Device | Role                               |
| ------ | ---------------------------------- |
| R1     | Edge router / default-route router |
| R2     | Remote router                      |
| SW1    | LAN switch                         |
| SW2    | LAN switch                         |
| PC1    | LAN 1 host                         |
| PC2    | LAN 2 host                         |

---

## 7. Network Design

### LAN 1

* Network: `192.168.10.0/24`
* R1 G0/0: `192.168.10.1`
* PC1: `192.168.10.10`
* Default gateway: `192.168.10.1`

### R1-R2 Link

* Network: `10.0.0.0/30`
* R1 G0/1: `10.0.0.1`
* R2 G0/1: `10.0.0.2`

### LAN 2

* Network: `192.168.20.0/24`
* R2 G0/0: `192.168.20.1`
* PC2: `192.168.20.10`
* Default gateway: `192.168.20.1`

### Routing

R1:

```text
0.0.0.0/0 → 10.0.0.2
```

R2:

```text
192.168.10.0/24 → 10.0.0.1
```

---

## 8. Configuration Approach

R1 was configured with a static default route:

```text
ip route 0.0.0.0 0.0.0.0 10.0.0.2
```

R2 was configured with a specific static route back to the LAN behind R1:

```text
ip route 192.168.10.0 255.255.255.0 10.0.0.1
```

This provides two-way routing between the two LANs.

---

## 9. Verification Approach

The following commands were used:

```text
show ip interface brief
show ip route
```

PC verification used:

```text
ipconfig
ping 192.168.10.1
ping 192.168.20.1
ping 10.0.0.1
ping 10.0.0.2
ping 192.168.20.10
ping 192.168.10.10
```

---

## 10. Testing & Expected Behavior

R1 successfully showed:

```text
S* 0.0.0.0/0 [1/0] via 10.0.0.2
```

This confirms that R1 has a valid static default route.

R2 successfully showed:

```text
S 192.168.10.0/24 [1/0] via 10.0.0.1
```

This confirms the return route.

All documented connectivity tests completed successfully with **0% packet loss**, including:

* PC1 → R1
* PC1 → R2
* PC1 → PC2
* PC2 → R2
* PC2 → R1
* PC2 → PC1

---

## 11. Troubleshooting Approach

If connectivity fails, verify in this order:

1. Check interface status using `show ip interface brief`.
2. Verify the connected networks using `show ip route`.
3. Confirm R1 has the default route.
4. Confirm R2 has the return route.
5. Verify PC IP addresses and default gateways.
6. Test the local gateway first.
7. Test the inter-router link.
8. Test end-to-end connectivity.

The key point is that a default route on R1 alone does not automatically provide a return path from R2.

---

## 12. Key Concepts Learned

* A default route matches destinations that are not already present in the routing table.
* `0.0.0.0 0.0.0.0` represents the default route.
* `S*` indicates a static candidate default route.
* A default route provides a forwarding path, but return traffic still requires a valid route.
* Connected routes are automatically installed when interfaces are configured and operational.
* End-to-end testing is required to confirm actual network connectivity.

---

## 13. Outcome

The default-route lab was successfully configured and verified.

R1 correctly forwards unknown destinations toward R2 using the static default route, while R2 uses a static return route toward the 192.168.10.0/24 network.

All end-to-end connectivity tests completed with **0% packet loss**.

**Project Status: COMPLETE / VERIFIED**

---

## 14. Related Files

```text
12-Default-Route/
├── topology/
│   └── 12-Default-Route-Lab.pkt
├── configuration/
│   ├── R1-config.txt
│   ├── R2-config.txt
│   ├── SW1-config.txt
│   └── SW2-config.txt
├── verification/
│   └── verification.md
├── screenshots/
│   ├── topology.png
│   ├── default-route-verification.png
│   └── ping-test.png
└── README.md
```
