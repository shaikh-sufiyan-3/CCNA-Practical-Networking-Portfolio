# 08 - DHCP Configuration

## 1. Overview

This project demonstrates Dynamic Host Configuration Protocol (DHCP) using a Cisco router as the DHCP server.

The router automatically assigns IP addressing information to a client in VLAN 10.

## 2. Objectives

* Configure a router as a DHCP server.
* Create a DHCP address pool.
* Exclude reserved IP addresses.
* Automatically assign an IP address to a client.
* Verify DHCP bindings.
* Verify the router LAN interface.
* Test client connectivity.

## 3. Network Scenario

A Cisco router is connected to a switch.

The switch connects one PC.

The router provides DHCP services for the `192.168.10.0/24` network.

VLAN 10 is used for the LAN.

## 4. Skills Demonstrated

* VLAN configuration
* Access port configuration
* IPv4 addressing
* DHCP server configuration
* DHCP address exclusion
* DHCP lease verification
* Basic connectivity testing

## 5. Prerequisites

* Basic Cisco IOS CLI knowledge
* Basic VLAN knowledge
* Basic IPv4 knowledge
* Cisco Packet Tracer
* One Cisco 2960 switch
* One router
* One PC

## 6. Lab Environment

| Device | Role                          |
| ------ | ----------------------------- |
| R1     | DHCP Server / Default Gateway |
| SW1    | Access Switch                 |
| PC1    | DHCP Client                   |

DHCP Pool:

```text id="m9b3s2"
SALES
```

Network:

```text id="j3p8kf"
192.168.10.0/24
```

## 7. Network Design

### Connections

```text id="x5v2cq"
PC1 ─── SW1 ─── R1
```

### Addressing

| Device  | Addressing      |
| ------- | --------------- |
| R1 G0/0 | 192.168.10.1/24 |
| PC1     | DHCP            |

The addresses `192.168.10.1` through `192.168.10.10` are excluded from DHCP allocation.

The observed DHCP client received `192.168.10.11`.

## 8. Configuration Approach

VLAN 10 named `SALES` was configured on SW1.

The PC-facing port and router-facing port were configured as access ports in VLAN 10.

R1 G0/0 was configured with:

```text id="yr5t2k"
192.168.10.1/24
```

A DHCP pool named `SALES` was created.

The addresses `192.168.10.1` through `192.168.10.10` were excluded.

The DHCP pool provides:

* Network: `192.168.10.0/24`
* Default gateway: `192.168.10.1`
* DNS server: `8.8.8.8`

## 9. Verification Approach

The following commands were used on R1:

```text id="5m5h9f"
show ip dhcp pool
show ip dhcp binding
show ip interface brief
```

The DHCP client was checked to confirm automatic IP assignment.

## 10. Testing & Expected Behavior

The DHCP client should automatically receive an IP address from the configured pool.

The actual DHCP binding confirmed:

```text id="u6d4rx"
192.168.10.11
```

The router interface was confirmed as:

```text id="n2x7ca"
GigabitEthernet0/0
192.168.10.1
up/up
```

This confirms that the DHCP server successfully allocated an address to the client.

## 11. Troubleshooting Approach

The following areas were checked:

1. VLAN configuration.
2. Access port configuration.
3. Router interface addressing.
4. Router interface status.
5. DHCP pool configuration.
6. Excluded address range.
7. DHCP binding.
8. Client IP assignment.
9. Client-to-router connectivity.

## 12. Key Concepts Learned

### DHCP

DHCP automatically provides network configuration to clients.

### DHCP Pool

A DHCP pool defines the network and parameters from which clients receive their configuration.

### Excluded Addresses

Excluded addresses are prevented from being dynamically assigned by DHCP.

### DHCP Binding

The DHCP binding table shows the relationship between an assigned IP address and the client.

### Default Gateway

The DHCP server provides `192.168.10.1` as the default gateway for clients in this lab.

## 13. Outcome

The DHCP configuration was successfully implemented.

The actual verification confirmed that:

* The `SALES` DHCP pool exists.
* One DHCP address has been leased.
* The client received `192.168.10.11`.
* R1 G0/0 is `192.168.10.1` and operational.

The final client-to-router ping should be recorded separately using the actual Packet Tracer result.

## 14. Related Files

```text id="r7k2mp"
topology/
    08-DHCP-Lab.pkt

configuration/
    SW1-config.txt
    R1-config.txt

verification/
    verification.md

screenshots/
    topology.png
    dhcp-verification.png
    ping-test.png
```
