# 11 - Static Routing

## 1. Overview

This project demonstrates static routing between two separate IPv4 LANs using two Cisco routers.

R1 and R2 are connected through a `/30` point-to-point network. Each router has a static route to the LAN behind the other router.

## 2. Objectives

* Understand static routing.
* Configure IPv4 addresses on router interfaces.
* Configure a `/30` point-to-point network.
* Configure static routes.
* Verify routing tables.
* Test end-to-end connectivity between different networks.

## 3. Network Scenario

```text
PC1 ── SW1 ── R1 ───── R2 ── SW2 ── PC2
```

The network contains two LANs connected through two routers.

## 4. Skills Demonstrated

* IPv4 addressing
* `/30` subnetting
* Router interface configuration
* Static route configuration
* Routing table verification
* End-to-end connectivity testing

## 5. Prerequisites

* Basic IPv4 knowledge
* Basic subnetting knowledge
* Basic Cisco IOS knowledge
* Cisco Packet Tracer

## 6. Lab Environment

* 2 × Cisco Routers
* 2 × Cisco 2960 Switches
* 2 × PCs
* Cisco Packet Tracer

## 7. Network Design

### LAN 1

```text
Network: 192.168.10.0/24
R1 G0/0: 192.168.10.1
PC1:     192.168.10.10
Gateway: 192.168.10.1
```

### Router-to-Router Network

```text
Network: 10.0.0.0/30
R1 G0/1: 10.0.0.1
R2 G0/1: 10.0.0.2
```

### LAN 2

```text
Network: 192.168.20.0/24
R2 G0/0: 192.168.20.1
PC2:     192.168.20.10
Gateway: 192.168.20.1
```

## 8. Configuration Approach

R1 was configured with:

```text
ip route 192.168.20.0 255.255.255.0 10.0.0.2
```

R2 was configured with:

```text
ip route 192.168.10.0 255.255.255.0 10.0.0.1
```

These static routes provide paths between the two LANs.

## 9. Verification Approach

Router interfaces were verified using:

```text
show ip interface brief
```

Routing tables were verified using:

```text
show ip route
```

PC addressing was checked using:

```text
ipconfig
```

Connectivity was tested using ping between local gateways, the inter-router link, and the remote LAN.

## 10. Testing & Expected Behavior

PC1 successfully reached its local gateway:

```text
192.168.10.1
```

with:

```text
0% packet loss
```

PC1 successfully reached R2:

```text
10.0.0.2
```

with:

```text
0% packet loss
```

The recorded PC1-to-PC2 test was:

```text
192.168.10.10 → 192.168.20.10
Sent = 4
Received = 3
Lost = 1
25% loss
```

The first request timed out and the following three requests succeeded.

The reverse test from PC2 to PC1 completed successfully:

```text
192.168.20.10 → 192.168.10.10
Sent = 4
Received = 4
Lost = 0
0% loss
```

## 11. Troubleshooting Approach

If remote-network connectivity fails:

1. Check both router interfaces with `show ip interface brief`.
2. Verify the router-to-router link.
3. Check R1's route to `192.168.20.0/24`.
4. Check R2's route to `192.168.10.0/24`.
5. Verify PC default gateways.
6. Test connectivity step-by-step from local gateway to remote router and then to the remote PC.

## 12. Key Concepts Learned

* Static routes are manually configured by the administrator.
* A router needs a route to reach a remote network.
* Both directions require a valid path.
* `/30` provides a small point-to-point IPv4 network.
* Directly connected networks appear as `C` routes.
* Static routes appear as `S` routes in the routing table.
* End devices use a default gateway to reach remote networks.

## 13. Outcome

The static routing configuration was successfully implemented and verified.

Both routers have the required static routes, all required router interfaces are up/up, and connectivity between the two LANs was demonstrated.

The recorded PC1-to-PC2 test showed one initial timeout followed by successful replies, while the reverse PC2-to-PC1 test achieved 0% packet loss.

## 14. Related Files

```text
11-Static-Routing/
├── topology/
│   └── 11-Static-Routing-Lab.pkt
├── configuration/
│   ├── R1-config.txt
│   ├── R2-config.txt
│   ├── SW1-config.txt
│   └── SW2-config.txt
├── verification/
│   └── verification.md
├── screenshots/
│   ├── topology.png
│   ├── routing-verification.png
│   └── ping-test.png
└── README.md
```
