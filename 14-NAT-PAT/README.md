# 14 - NAT/PAT

## 1. Overview

This project demonstrates Network Address Translation using PAT (Port Address Translation), also known as NAT Overload.

A private inside host uses the R1 router to reach an outside network. R1 translates the private source address to its outside interface address.

---

## 2. Objectives

* Configure inside and outside NAT interfaces.
* Configure an access list for the inside network.
* Configure PAT using NAT overload.
* Configure a default route toward the outside network.
* Verify NAT translations.
* Verify NAT statistics.
* Test connectivity from the inside host to the outside network.

---

## 3. Network Scenario

```text
PC1 ── SW1 ── R1 ───── R2
```

R1 acts as the NAT/PAT router.

PC1 belongs to the private inside network `192.168.10.0/24`.

R1 translates traffic from the inside network to its outside interface address `203.0.113.2`.

R2 represents the outside network endpoint.

---

## 4. Skills Demonstrated

* NAT configuration
* PAT / NAT Overload
* Inside and outside NAT interfaces
* Standard ACL for NAT matching
* Static default route
* NAT translation verification
* NAT statistics verification
* Connectivity testing

---

## 5. Prerequisites

* Basic Cisco IOS CLI knowledge
* Understanding of IPv4 addressing
* Basic routing knowledge
* Basic understanding of NAT
* Cisco Packet Tracer

---

## 6. Lab Environment

| Device | Role                     |
| ------ | ------------------------ |
| R1     | NAT/PAT router           |
| R2     | Outside network endpoint |
| SW1    | Inside LAN switch        |
| PC1    | Inside host              |

---

## 7. Network Design

### Inside Network

* Network: `192.168.10.0/24`
* PC1: `192.168.10.10`
* R1 G0/0: `192.168.10.1`
* Gateway: `192.168.10.1`

### Outside Network

* Network: `203.0.113.0/30`
* R1 G0/1: `203.0.113.2`
* R2 G0/0: `203.0.113.1`

### NAT Translation

```text
Inside Local:   192.168.10.10
Inside Global: 203.0.113.2
```

R1 uses its outside interface address for PAT.

---

## 8. Configuration Approach

The inside network was permitted through a standard access list:

```text
access-list 1 permit 192.168.10.0 0.0.0.255
```

PAT was then configured using R1's outside interface:

```text
ip nat inside source list 1 interface GigabitEthernet0/1 overload
```

R1 G0/0 was configured as the NAT inside interface and R1 G0/1 as the NAT outside interface.

A default route was configured toward R2:

```text
ip route 0.0.0.0 0.0.0.0 203.0.113.1
```

---

## 9. Verification Approach

The following R1 commands were used:

```text
show ip interface brief
show ip nat translations
show ip nat statistics
show ip route
```

R2 was verified using:

```text
show ip interface brief
```

PC1 was verified using:

```text
ipconfig
ping 192.168.10.1
ping 203.0.113.1
```

---

## 10. Testing & Expected Behavior

The NAT translation table successfully showed traffic from:

```text
192.168.10.10
```

being translated to:

```text
203.0.113.2
```

NAT statistics showed:

```text
Total translations: 4
Dynamic translations: 4
Hits: 14
```

PC1 successfully reached both its local gateway and the outside endpoint with **0% packet loss**.

---

## 11. Troubleshooting Approach

If NAT is not working:

1. Verify R1 interfaces are `up/up`.
2. Confirm G0/0 is configured as `ip nat inside`.
3. Confirm G0/1 is configured as `ip nat outside`.
4. Verify the NAT access list matches the inside network.
5. Verify the PAT command is configured.
6. Check the routing table for a valid outside route.
7. Generate traffic from the inside host.
8. Check `show ip nat translations`.
9. Check `show ip nat statistics`.

The translation table should be checked **after generating traffic**, because dynamic NAT/PAT entries are created when matching traffic occurs.

---

## 12. Key Concepts Learned

* NAT translates IP addresses between inside and outside networks.
* PAT allows multiple inside hosts to share one global address by using transport-layer port information.
* `ip nat inside` identifies the private-side interface.
* `ip nat outside` identifies the external-side interface.
* `overload` enables PAT.
* `Inside Local` represents the original private address.
* `Inside Global` represents the translated address used outside.
* NAT verification should include both the translation table and NAT statistics.

---

## 13. Outcome

PAT was successfully configured on R1.

The private host `192.168.10.10` was dynamically translated to R1's outside address `203.0.113.2`.

NAT translations and statistics were successfully verified, and connectivity to the outside endpoint was confirmed with **0% packet loss**.

**Project Status: COMPLETE / VERIFIED**

---

## 14. Related Files

```text
14-NAT-PAT/
├── topology/
│   └── 14-NAT-PAT-Lab.pkt
├── configuration/
│   ├── R1-config.txt
│   ├── R2-config.txt
│   └── SW1-config.txt
├── verification/
│   └── verification.md
├── screenshots/
│   ├── topology.png
│   ├── nat-verification.png
│   └── ping-test.png
└── README.md
```
