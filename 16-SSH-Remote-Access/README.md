# 16 - SSH Remote Access

## 1. Overview

This project demonstrates secure remote management of a Cisco switch using Secure Shell (SSH).

SW1 is configured with a dedicated management VLAN and management IP address. A local administrative account is used for authentication, and the VTY lines are configured to accept SSH connections.

## 2. Objectives

* Configure a management VLAN.
* Configure a switch management SVI.
* Configure a local administrative user.
* Enable SSH version 2.
* Configure VTY lines for local authentication.
* Allow SSH remote access.
* Verify successful SSH connectivity.

## 3. Network Scenario

The lab contains:

* One Cisco 2960 switch.
* One PC.
* One management VLAN.

PC1 connects to SW1 through Fa0/1.

SW1 uses VLAN 10 as the management VLAN.

## 4. Skills Demonstrated

* Management VLAN configuration
* Switch Virtual Interface configuration
* IPv4 management addressing
* Local user authentication
* SSH configuration
* VTY line configuration
* Remote device management
* SSH verification

## 5. Prerequisites

* Cisco Packet Tracer
* Basic Cisco IOS knowledge
* Basic IPv4 addressing
* Basic VLAN knowledge
* Basic understanding of remote access protocols

## 6. Lab Environment

| Device     | Role           |
| ---------- | -------------- |
| Cisco 2960 | Managed switch |
| PC1        | SSH client     |

## 7. Network Design

| Device | Interface | VLAN | IP Address       |
| ------ | --------- | ---: | ---------------- |
| PC1    | Fa0/1     |   10 | 192.168.10.10/24 |
| SW1    | VLAN 10   |   10 | 192.168.10.2/24  |

The management connection is within the same IPv4 subnet, so a default gateway is not required for this local SSH test.

## 8. Configuration Approach

VLAN 10 was created as the management VLAN.

SW1 Fa0/1 was configured as an access port in VLAN 10.

The VLAN 10 SVI was assigned:

```text
192.168.10.2/24
```

A local administrative user was configured and SSH version 2 was enabled.

The VTY lines were configured with:

```text
login local
transport input ssh
```

This ensures that VTY access uses the local user database and accepts SSH rather than Telnet.

## 9. Verification Approach

The following commands were used:

```text
show ip interface brief
show vlan brief
show ip ssh
show running-config | section username
show running-config | section line vty
```

PC1 was also used to test:

```text
ping 192.168.10.2
ssh -l admin 192.168.10.2
```

## 10. Testing & Expected Behavior

### Management Connectivity

PC1 successfully reached SW1's management IP.

Result:

```text
4/4 replies
0% packet loss
```

### SSH Authentication

PC1 initiated:

```text
ssh -l admin 192.168.10.2
```

The SSH session successfully reached the SW1 privileged EXEC prompt:

```text
SW1#
```

Therefore, SSH remote access was successfully established.

## 11. Troubleshooting Approach

The following areas were verified:

1. Management VLAN membership.
2. Management IP reachability.
3. SSH version.
4. Local username configuration.
5. VTY authentication method.
6. VTY transport protocol.
7. Actual SSH login.

## 12. Key Concepts Learned

* SSH provides secure remote management.
* SSH version 2 is preferred over older SSH versions.
* A switch can be remotely managed through an SVI.
* `login local` uses locally configured usernames.
* `transport input ssh` restricts VTY access to SSH.
* Successful ping proves IP reachability but does not by itself prove SSH functionality.
* An actual successful SSH session is the strongest verification for this lab.

## 13. Outcome

SW1 was successfully configured for secure remote management using SSH.

The management VLAN and SVI were operational, SSH version 2 was enabled, VTY authentication was configured, and an actual SSH login from PC1 was successfully completed.

**Project Status: COMPLETE / VERIFIED**

## 14. Related Files

```text
16-SSH-Remote-Access/
├── topology/
│   └── 16-SSH-Remote-Access-Lab.pkt
├── configuration/
│   └── SW1-config.txt
├── verification/
│   └── verification.md
├── screenshots/
│   ├── topology.png
│   ├── ssh-verification.png
│   └── ssh-login.png
└── README.md
```
