# 01 - Basic Cisco IOS Commands

## 1. Overview

This lab demonstrates the fundamentals of working with Cisco IOS through the Command-Line Interface (CLI).

The lab focuses on basic switch configuration, IOS navigation, interface identification, configuration verification, and basic connectivity testing. These skills form the foundation for configuring and troubleshooting Cisco network devices.

---

## 2. Objectives

* Understand the basic Cisco IOS CLI environment.
* Practice navigating between different IOS configuration modes.
* Configure a hostname and interface descriptions.
* Use essential `show` commands to verify device configuration and interface status.
* Understand the difference between running and startup configurations.
* Perform a basic connectivity test between two end devices.

---

## 3. Network Scenario

A small LAN environment is used to simulate the initial configuration of a Cisco access switch.

A network administrator needs to access the switch through the console, configure basic device settings, identify connected interfaces, verify the switch configuration, and confirm connectivity between two PCs.

This represents the type of initial configuration and verification commonly performed when deploying or preparing a network switch.

---

## 4. Skills Demonstrated

* Cisco IOS CLI navigation
* IOS configuration modes
* Basic switch configuration
* Hostname configuration
* Interface description configuration
* Interface and VLAN verification
* Running configuration verification
* Basic network connectivity testing
* Use of Cisco IOS `show` commands

---

## 5. Prerequisites

* Cisco Packet Tracer
* Basic Cisco IOS knowledge
* Basic networking knowledge
* Basic understanding of IPv4 addressing and ping

---

## 6. Lab Environment

| Component     | Details             |
| ------------- | ------------------- |
| Simulator     | Cisco Packet Tracer |
| Switch        | Cisco 2960          |
| End Devices   | PC0, PC1, PC2       |
| Network Type  | LAN                 |
| Access Method | Console             |
| Technology    | Cisco IOS CLI       |

---

## 7. Network Design

The lab consists of one Cisco switch and three PCs.

* **PC0** is connected to the console port of SW1 and is used for CLI access.
* **PC1** is connected to FastEthernet0/1 of SW1.
* **PC2** is connected to FastEthernet0/2 of SW1.
* PC1 and PC2 are used for basic network connectivity testing.

### Topology

```text
                 Console Connection
              ┌─────────────────────┐
              │                     │
            PC0                    SW1
          Console              Cisco 2960
                                  │   │
                                  │   │
                               Fa0/1 Fa0/2
                                  │   │
                                 PC1 PC2
```

The console connection is used for device management, while PC1 and PC2 provide the end-device connectivity test.

---

## 8. Configuration Approach

The switch was accessed through the console connection and configured using Cisco IOS CLI.

The configuration process included:

1. Accessing the switch CLI through the console.
2. Identifying Cisco IOS configuration modes.
3. Configuring the switch hostname as `SW1`.
4. Adding descriptions to the interfaces connected to PC1 and PC2.
5. Reviewing the switch configuration.
6. Verifying interface and VLAN information.
7. Saving the configuration for persistence.

The complete configuration is available in the `configuration/` folder.

---

## 9. Verification Approach

The configuration was verified using essential Cisco IOS verification commands.

The following commands were used:

```text
show ip interface brief
show vlan brief
show running-config
```

These commands were used to verify interface status, VLAN information, and the active switch configuration.

A connectivity test was also performed between PC1 and PC2 using `ping`.

Complete verification evidence is available in the `verification/` folder.

---

## 10. Testing & Expected Behavior

The following tests were performed:

* Verified the status of switch interfaces.
* Verified VLAN information on the switch.
* Verified the active running configuration.
* Tested connectivity between PC1 and PC2.

### Expected Behavior

* PC1 and PC2 should be able to communicate when correctly connected and configured within the same LAN.
* The switch should display the configured hostname and interface descriptions.
* `show ip interface brief` should provide the operational status of the switch interfaces.
* `show vlan brief` should display the VLAN information and port membership.
* `show running-config` should display the active configuration.

---

## 11. Troubleshooting Approach

A structured troubleshooting methodology was followed rather than making assumptions.

1. Check the physical connections and link status.
2. Confirm that the correct switch interfaces are being used.
3. Verify interface status using `show ip interface brief`.
4. Verify VLAN and port information using `show vlan brief`.
5. Review the active configuration using `show running-config`.
6. Verify the IP configuration of the end devices.
7. Test connectivity using `ping`.
8. Identify and correct configuration or connectivity issues based on the verification results.

---

## 12. Key Concepts Learned

* Cisco IOS CLI navigation
* User EXEC, Privileged EXEC, and Global Configuration modes
* Basic switch configuration
* Hostname configuration
* Interface descriptions
* Interface status verification
* VLAN verification
* Running configuration
* Basic LAN connectivity
* Systematic troubleshooting

---

## 13. Outcome

Successfully configured and verified the basic Cisco IOS environment on SW1, including hostname and interface descriptions, and demonstrated basic connectivity between PC1 and PC2.

---

## 14. Related Files

* `topology/` → Packet Tracer topology and lab file
* `configuration/` → SW1 configuration
* `verification/` → Combined verification evidence
* `screenshots/` → Visual evidence of the lab and testing

