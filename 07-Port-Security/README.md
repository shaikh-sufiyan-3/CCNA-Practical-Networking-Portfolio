# 07 - Port Security

## 1. Overview

This project demonstrates Cisco switch Port Security on access ports.

Port Security is configured on Fa0/1 and Fa0/2 to limit each port to one secure MAC address. Sticky MAC learning is used to dynamically learn the connected device MAC address.

## 2. Objectives

* Configure switch Port Security.
* Limit the number of MAC addresses on an access port.
* Use sticky MAC address learning.
* Configure a security violation action.
* Verify secure MAC addresses.
* Verify port security status.
* Test normal network connectivity.

## 3. Network Scenario

A Cisco 2960 switch connects two PCs.

Both PCs are placed in VLAN 10.

Port Security is enabled on both PC-facing access ports.

Each port is configured to allow only one secure MAC address.

## 4. Skills Demonstrated

* VLAN configuration
* Access port configuration
* Port Security
* Sticky MAC learning
* MAC address verification
* Security violation configuration
* Connectivity testing

## 5. Prerequisites

* Basic Cisco IOS CLI knowledge
* Basic VLAN knowledge
* Basic Ethernet switching knowledge
* Cisco Packet Tracer
* One Cisco 2960 switch
* Two PCs

## 6. Lab Environment

| Device | Role          |
| ------ | ------------- |
| SW1    | Access Switch |
| PC1    | End Device    |
| PC2    | End Device    |

VLAN:

```text
VLAN 10 - SALES
```

Port Security:

```text
Maximum MAC Addresses: 1
Violation Mode: Shutdown
MAC Learning: Sticky
```

## 7. Network Design

### Connections

```text
PC1 ─── Fa0/1 ─── SW1
PC2 ─── Fa0/2 ─── SW1
```

### IP Addressing

| Device | VLAN | IP Address    | Subnet Mask   |
| ------ | ---: | ------------- | ------------- |
| PC1    |   10 | 192.168.10.10 | 255.255.255.0 |
| PC2    |   10 | 192.168.10.20 | 255.255.255.0 |

Both PCs are in the same subnet, so no default gateway is required.

## 8. Configuration Approach

VLAN 10 was created and named `SALES`.

Fa0/1 and Fa0/2 were configured as access ports in VLAN 10.

Port Security was enabled on both ports.

Each port was configured with a maximum of one secure MAC address:

```text
switchport port-security maximum 1
```

Sticky MAC learning was enabled:

```text
switchport port-security mac-address sticky
```

The violation action was configured as shutdown:

```text
switchport port-security violation shutdown
```

## 9. Verification Approach

The following commands were used:

```text
show vlan brief
show port-security
show port-security interface f0/1
show port-security interface f0/2
show port-security address
```

Connectivity was tested using:

```text
ping 192.168.10.20
```

## 10. Testing & Expected Behavior

Each protected port should allow one secure MAC address.

The actual secure MAC address table confirmed:

* Fa0/1 → `0001.C709.C36A`
* Fa0/2 → `00D0.584E.7BC0`

Both addresses were learned as `SecureSticky`.

No security violation occurred during testing.

PC1 successfully communicated with PC2 with:

```text
4 packets sent
4 packets received
0% packet loss
```

## 11. Troubleshooting Approach

The following areas were checked:

1. VLAN 10 assignment.
2. Access port configuration.
3. Port Security status.
4. Maximum secure MAC address limit.
5. Sticky MAC learning.
6. Violation mode.
7. Security violation count.
8. End-to-end connectivity.

## 12. Key Concepts Learned

### Port Security

Port Security controls which MAC addresses are allowed to use a switch access port.

### Maximum MAC Address

The maximum MAC address value controls how many secure MAC addresses can be associated with the port.

In this lab, the value is:

```text
1
```

### Sticky MAC

Sticky MAC allows the switch to dynamically learn the connected device's MAC address and treat it as a secure MAC address.

### Violation Shutdown

With shutdown mode, a port can be placed into an error-disabled state when a security violation occurs.

### Secure MAC Address

A secure MAC address is an authorized MAC address associated with a port through Port Security.

## 13. Outcome

The Port Security lab was successfully completed.

The lab demonstrated:

* Access VLAN configuration
* Port Security
* One-MAC limitation
* Sticky MAC learning
* Shutdown violation mode
* Secure MAC verification
* Successful connectivity

Actual verification confirmed that both Fa0/1 and Fa0/2 had one SecureSticky MAC address and zero security violations.

## 14. Related Files

```text
topology/
    07-Port-Security-Lab.pkt

configuration/
    SW1-config.txt

verification/
    verification.md

screenshots/
    topology.png
    vlan-verification.png
    port-security-fa01.png
    port-security-fa02.png
    secure-mac-address.png
    ping-test.png
```
