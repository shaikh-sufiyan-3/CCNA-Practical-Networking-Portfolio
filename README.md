# CCNA Practical Networking Portfolio

A hands-on Cisco networking portfolio demonstrating practical implementation, verification, troubleshooting, and documentation of core CCNA-level networking concepts using Cisco Packet Tracer.

This repository focuses on **practical networking skills rather than only theoretical knowledge**. Each completed lab contains configuration files, verification evidence, topology documentation, and a concise explanation of the concepts demonstrated.

---

## About This Portfolio

This portfolio was built to develop and demonstrate practical skills across:

* Cisco IOS configuration
* VLANs and Layer 2 segmentation
* Access and trunk ports
* Inter-VLAN routing
* EtherChannel with LACP
* STP/RSTP
* Port security
* DHCP
* IPv4 addressing and subnetting
* IPv6 configuration
* Static routing
* Default routing
* OSPF
* NAT/PAT
* Extended ACLs
* SSH remote management
* Network troubleshooting

The labs are designed progressively, starting with basic switch configuration and moving toward routing, network services, security controls, and troubleshooting.

---

## Technical Environment

**Primary Platform**

* Cisco Packet Tracer
* Cisco IOS CLI

**Networking Areas**

* Layer 2 switching
* Layer 3 routing
* IPv4
* IPv6
* Network segmentation
* Dynamic routing
* Network address translation
* Traffic filtering
* Secure remote management
* Network troubleshooting

---

## Portfolio Structure

```text
CCNA-Practical-Networking-Portfolio/
│
├── 01-Basic-Cisco-IOS-Commands/
├── 02-VLAN/
├── 03-Access-and-Trunk-Ports/
├── 04-Inter-VLAN-Routing/
├── 05-EtherChannel/
├── 06-STP-RSTP/
├── 07-Port-Security/
├── 08-DHCP/
├── 09-IPv4-Addressing-Subnetting/
├── 10-IPv6-Configuration/
├── 11-Static-Routing/
├── 12-Default-Route/
├── 13-OSPF/
├── 14-NAT-PAT/
├── 15-ACL/
├── 16-SSH-Remote-Access/
├── 17-Device-Hardening/
└── 18-Troubleshooting/
```

> Project 17 — Device Hardening — is intentionally skipped in this portfolio.

---

# Completed Projects

## 01 — Basic Cisco IOS Commands

Demonstrates fundamental Cisco IOS CLI operations and basic switch configuration.

**Skills demonstrated:**

* Cisco IOS navigation
* Hostname configuration
* Interface inspection
* VLAN inspection
* Running configuration verification
* Basic connectivity testing

**Status:** ✅ Verified

---

## 02 — VLAN

Demonstrates Layer 2 network segmentation using VLANs.

**Skills demonstrated:**

* VLAN creation
* VLAN naming
* Access port assignment
* VLAN verification
* Understanding Layer 2 isolation

**Status:** ✅ Verified

---

## 03 — Access and Trunk Ports

Demonstrates the difference between access and trunk interfaces and the use of 802.1Q trunking between switches.

**Skills demonstrated:**

* Access port configuration
* Trunk configuration
* VLAN propagation
* `show interfaces trunk`
* Same-VLAN connectivity across switches

**Status:** ✅ Verified

---

## 04 — Inter-VLAN Routing

Demonstrates router-on-a-stick inter-VLAN routing using 802.1Q subinterfaces.

**Skills demonstrated:**

* VLAN segmentation
* Router subinterfaces
* 802.1Q encapsulation
* Default gateway configuration
* Inter-VLAN communication
* Routing table verification

**Status:** ✅ Verified

---

## 05 — EtherChannel

Demonstrates link aggregation using LACP.

**Skills demonstrated:**

* EtherChannel configuration
* LACP
* Port-channel interfaces
* Physical member verification
* Trunking over Port-channel

**Status:** ✅ Verified

---

## 06 — STP/RSTP

Demonstrates Rapid PVST+ and Layer 2 loop prevention using redundant switch links.

**Skills demonstrated:**

* Rapid PVST+
* Root bridge selection
* Root port
* Designated port
* Alternate/blocking port
* STP verification

**Status:** ✅ Verified

---

## 07 — Port Security

Demonstrates Layer 2 access-port security using sticky MAC learning and violation control.

**Skills demonstrated:**

* Port security
* Maximum secure MAC addresses
* Sticky MAC learning
* Violation mode
* Secure MAC verification

**Status:** ✅ Verified

---

## 08 — DHCP

Demonstrates router-based DHCP address assignment for a client network.

**Skills demonstrated:**

* DHCP pool configuration
* Excluded addresses
* Default gateway assignment
* DNS configuration
* DHCP binding verification
* Client-side DHCP verification

**Status:** ✅ Verified


---

## 09 — IPv4 Addressing and Subnetting

Demonstrates IPv4 subnetting by dividing a `/24` network into `/26` subnets.

**Skills demonstrated:**

* Subnet calculation
* Network and broadcast identification
* Usable host range calculation
* IPv4 host configuration
* Connectivity testing

**Status:** ✅ Verified

---

## 10 — IPv6 Configuration

Demonstrates basic IPv6 host addressing and Layer 2 connectivity.

**Skills demonstrated:**

* IPv6 addressing
* IPv6 link-local addressing
* IPv6 host configuration
* IPv6 connectivity testing

**Status:** ✅ Verified

---

## 11 — Static Routing

Demonstrates communication between two LANs through two routers using manually configured static routes.

**Skills demonstrated:**

* Router interface addressing
* Point-to-point addressing
* Static route configuration
* Routing table verification
* End-to-end routing tests

**Status:** ✅ Verified

---

## 12 — Default Route

Demonstrates the use of a default route for forwarding traffic toward a remote network.

**Skills demonstrated:**

* Default route configuration
* Next-hop routing
* Gateway of last resort
* Routing table verification
* End-to-end connectivity

**Status:** ✅ Verified

---

## 13 — OSPF

Demonstrates dynamic routing using OSPF Area 0.

**Skills demonstrated:**

* OSPF process configuration
* Router ID
* OSPF network statements
* Neighbor adjacency
* FULL OSPF state
* Dynamic route installation

**Status:** ✅ Verified

---

## 14 — NAT/PAT

Demonstrates Port Address Translation using a router interface as the inside-global address.

**Skills demonstrated:**

* NAT inside/outside interfaces
* NAT ACL
* PAT overload
* Default routing
* NAT translation verification
* NAT statistics

**Status:** ✅ Verified

---

## 15 — ACL

Demonstrates an Extended ACL used to control traffic between two VLANs.

**Policy implemented:**

```text
PC1 192.168.10.10 → PC2 192.168.20.10
BLOCK

PC2 192.168.20.10 → PC1 192.168.10.10
ALLOW
```

**Skills demonstrated:**

* Extended ACL
* Source and destination matching
* ACL sequence processing
* ACL direction
* Inbound ACL application
* ACL match counters
* Traffic filtering verification

**Status:** ✅ Verified

---

## 16 — SSH Remote Access

Demonstrates secure remote management of a Cisco switch using SSH.

**Skills demonstrated:**

* Management VLAN
* Switch management SVI
* Local user authentication
* SSH version 2
* VTY configuration
* SSH-only remote access
* Actual SSH session verification

**Status:** ✅ Verified

---

# Verification Philosophy

This portfolio follows a simple rule:

> **Configuration is not considered verified just because the command was entered successfully.**

Where possible, each lab is verified using:

1. Configuration/state commands
2. Interface status
3. Routing or protocol state
4. Connectivity testing
5. Actual command output
6. Expected versus observed behavior

Intentional failures are documented as intentional failures.

If a test was not performed, it is not presented as performed.

If a result contains packet loss, the documented result reflects the actual observation rather than being replaced with an idealized result.

---

# Documentation Standard

Each project follows a consistent structure:

```text
Project/
├── topology/
├── configuration/
├── verification/
├── screenshots/
└── README.md
```

Typical contents:

* `topology/` — Packet Tracer topology
* `configuration/` — device configuration files
* `verification/` — verification commands and observed results
* `screenshots/` — key visual evidence
* `README.md` — project explanation and technical summary

Screenshots are intentionally limited to the most useful evidence rather than filling the repository with unnecessary captures.

---

# Skills Demonstrated Across the Portfolio

### Switching

* VLANs
* Access ports
* Trunking
* 802.1Q
* EtherChannel
* LACP
* STP
* RSTP
* Port security

### Routing

* Inter-VLAN routing
* Static routing
* Default routing
* OSPF
* Routing table analysis

### Addressing

* IPv4 addressing
* IPv4 subnetting
* IPv6 addressing
* Default gateways

### Network Services

* DHCP
* NAT
* PAT

### Security and Management

* Extended ACLs
* SSH
* Local authentication
* Secure remote management

### Troubleshooting

* Interface-state analysis
* VLAN verification
* Trunk verification
* Routing-table analysis
* Protocol-state verification
* Connectivity testing
* ACL counter analysis

---

# Career Focus

This portfolio is intended to demonstrate practical readiness for entry-level networking roles such as:

* Network Support Engineer
* NOC Engineer
* Junior Network Administrator
* IT Support / Network Support
* Network Operations roles
* Entry-level Cisco networking positions

The portfolio complements CCNA study by demonstrating that networking concepts can be implemented, verified, tested, and documented in a practical lab environment.

---

# Author

**Shaikh Sufiyan**

CCNA Practical Networking Portfolio

Built with Cisco Packet Tracer and Cisco IOS CLI.

Focus: **Practical networking, verification, troubleshooting, and technically accurate documentation.**
