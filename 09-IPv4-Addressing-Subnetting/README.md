# 09 - IPv4 Addressing & Subnetting

## 1. Overview

This project demonstrates IPv4 addressing and basic subnetting using a `/26` subnet.

A `/24` network, `192.168.10.0/24`, is divided into `/26` subnets. Three PCs are assigned valid host addresses from the first `/26` subnet and tested for connectivity.

## 2. Objectives

* Understand IPv4 addressing.
* Calculate a `/26` subnet.
* Identify network, host, and broadcast addresses.
* Configure static IPv4 addresses on PCs.
* Verify same-subnet connectivity.
* Understand when a default gateway is required.

## 3. Network Scenario

Three PCs are connected to a Cisco 2960 switch.

All three PCs belong to the same IPv4 subnet:

```text
Network: 192.168.10.0/26
Mask:    255.255.255.192
```

IP addressing:

| Device | IPv4 Address  | Subnet Mask     | Gateway |
| ------ | ------------- | --------------- | ------- |
| PC1    | 192.168.10.10 | 255.255.255.192 | None    |
| PC2    | 192.168.10.20 | 255.255.255.192 | None    |
| PC3    | 192.168.10.30 | 255.255.255.192 | None    |

## 4. Skills Demonstrated

* IPv4 addressing
* Subnetting
* `/26` subnet calculation
* Static IP configuration
* Cisco IOS switch interface configuration
* Connectivity testing with ping

## 5. Prerequisites

* Basic IPv4 addressing knowledge
* Basic Cisco IOS knowledge
* Cisco Packet Tracer

## 6. Lab Environment

* 1 × Cisco 2960 Switch
* 3 × PCs
* Cisco Packet Tracer

## 7. Network Design

Topology:

```text
PC1 ─── SW1 ─── PC2
        │
        └────── PC3
```

Switch connections:

```text
PC1 → SW1 Fa0/1
PC2 → SW1 Fa0/2
PC3 → SW1 Fa0/3
```

## 8. IPv4 Subnet Design

Original network:

```text
192.168.10.0/24
```

Selected subnet:

```text
192.168.10.0/26
```

Subnet mask:

```text
255.255.255.192
```

The `/26` subnet provides:

```text
64 total addresses
62 usable host addresses
```

Subnet details:

```text
Network Address: 192.168.10.0
First Host:      192.168.10.1
Last Host:       192.168.10.62
Broadcast:       192.168.10.63
```

Assigned host addresses `.10`, `.20`, and `.30` are valid addresses in this range.

## 9. Configuration Approach

SW1 interfaces Fa0/1 through Fa0/3 were configured as access ports.

The PCs were manually assigned IPv4 addresses using the `/26` subnet mask.

No default gateway was configured because all three PCs are in the same subnet and the lab does not require routing.

## 10. Verification Approach

The following verification was performed:

```text
show interfaces status
```

PC IP configuration was checked using:

```text
ipconfig
```

Connectivity was tested using:

```text
ping 192.168.10.20
ping 192.168.10.30
```

## 11. Testing & Expected Behavior

PC1 successfully reached PC2:

```text
Sent = 4
Received = 4
Lost = 0 (0% loss)
```

PC1 successfully reached PC3:

```text
Sent = 4
Received = 4
Lost = 0 (0% loss)
```

This confirms that the three PCs can communicate within the same `/26` subnet.

## 12. Troubleshooting Approach

If connectivity fails:

1. Check the PC IP address.
2. Check the subnet mask.
3. Confirm that the IP addresses belong to the same subnet.
4. Check that the switch ports are connected.
5. Verify the correct physical connections.
6. Repeat the ping test.

For this lab, the most important addressing check is that the PCs use:

```text
255.255.255.192
```

and valid host addresses within:

```text
192.168.10.1 - 192.168.10.62
```

## 13. Key Concepts Learned

* `/26` means 26 network bits and 6 host bits.
* A `/26` subnet contains 64 total addresses.
* 62 addresses are usable for hosts.
* The first address is the network address.
* The last address is the broadcast address.
* Devices in the same subnet can communicate directly without a router.
* A default gateway is required when communication needs to leave the local subnet.

## 14. Outcome

The IPv4 addressing and subnetting lab was successfully completed.

The subnet calculation was correct, all three PCs received valid IPv4 configurations, and end-to-end connectivity was verified with 0% packet loss.

## 15. Related Files

```text
09-IPv4-Addressing-Subnetting/
├── topology/
│   └── 09-IPv4-Addressing-Subnetting-Lab.pkt
├── configuration/
│   └── SW1-config.txt
├── verification/
│   └── verification.md
├── screenshots/
│   ├── topology.png
│   ├── ip-addressing.png
│   └── ping-test.png
└── README.md
```
