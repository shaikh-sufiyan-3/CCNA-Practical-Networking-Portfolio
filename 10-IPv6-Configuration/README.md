# 10 - IPv6 Configuration

## 1. Overview

This project demonstrates basic IPv6 addressing and connectivity using a Cisco switch and two PCs.

Both PCs are configured with IPv6 global unicast addresses from the same `/64` network and tested using IPv6 ping.

## 2. Objectives

* Understand basic IPv6 addressing.
* Configure IPv6 addresses on end devices.
* Understand IPv6 `/64` prefix notation.
* Identify IPv6 link-local addresses.
* Verify IPv6 connectivity.
* Understand same-subnet IPv6 communication.

## 3. Network Scenario

Two PCs are connected to a Cisco 2960 switch.

```text
PC1 ─── SW1 ─── PC2
```

IPv6 network:

```text
2001:DB8:10:10::/64
```

Addressing:

| Device | IPv6 Address       | Prefix |
| ------ | ------------------ | ------ |
| PC1    | 2001:DB8:10:10::10 | /64    |
| PC2    | 2001:DB8:10:10::20 | /64    |

No default gateway is configured because both PCs are in the same IPv6 subnet.

## 4. Skills Demonstrated

* IPv6 addressing
* Global unicast IPv6 addresses
* IPv6 `/64` prefix
* IPv6 link-local addresses
* Static IPv6 configuration
* IPv6 connectivity testing
* Basic Cisco IOS interface configuration

## 5. Prerequisites

* Basic networking knowledge
* Basic IPv6 addressing knowledge
* Basic Cisco IOS knowledge
* Cisco Packet Tracer

## 6. Lab Environment

* 1 × Cisco 2960 Switch
* 2 × PCs
* Cisco Packet Tracer

## 7. Network Design

Connections:

```text
PC1 → SW1 Fa0/1
PC2 → SW1 Fa0/2
```

IPv6 network:

```text
2001:DB8:10:10::/64
```

PC addressing:

```text
PC1 → 2001:DB8:10:10::10/64
PC2 → 2001:DB8:10:10::20/64
```

## 8. Configuration Approach

SW1 Fa0/1 and Fa0/2 were configured as access ports.

The PCs were manually assigned IPv6 global unicast addresses from the same `/64` network.

No IPv4 addressing or routing was required for this lab.

No default gateway was configured because the connectivity test remains within the local IPv6 subnet.

## 9. Verification Approach

Switch interfaces were checked using:

```text
show interfaces status
```

IPv6 addressing on the PCs was checked using:

```text
ipconfig
```

IPv6 connectivity was tested using:

```text
ping 2001:DB8:10:10::20
```

## 10. Testing & Expected Behavior

PC1 successfully reached PC2 using the IPv6 address:

```text
2001:DB8:10:10::20
```

Actual ping result:

```text
Packets: Sent = 4
Received = 4
Lost = 0 (0% loss)
```

Average round-trip time was `0ms`.

This confirms successful IPv6 communication between the two PCs.

## 11. Troubleshooting Approach

If IPv6 connectivity fails:

1. Check the IPv6 address on both PCs.
2. Confirm both PCs use the same `/64` network.
3. Check that the switch interfaces are connected.
4. Verify the physical connections.
5. Check for typing errors in the IPv6 addresses.
6. Repeat the IPv6 ping test.

## 12. Key Concepts Learned

* IPv6 uses hexadecimal addressing.
* `/64` is commonly used for IPv6 LAN prefixes.
* Global unicast addresses can be manually configured.
* IPv6 devices automatically have link-local addresses.
* Link-local addresses begin with `FE80::/10`.
* Devices on the same IPv6 subnet can communicate without a router.
* A default gateway is required when communication must leave the local subnet.

## 13. Outcome

The IPv6 configuration lab was successfully completed.

Both PCs were configured with IPv6 addresses from the same `/64` network, and end-to-end IPv6 connectivity was verified with 0% packet loss.

## 14. Related Files

```text
10-IPv6-Configuration/
├── topology/
│   └── 10-IPv6-Configuration-Lab.pkt
├── configuration/
│   └── SW1-config.txt
├── verification/
│   └── verification.md
├── screenshots/
│   ├── topology.png
│   ├── ipv6-addressing.png
│   └── ping-test.png
└── README.md
```
