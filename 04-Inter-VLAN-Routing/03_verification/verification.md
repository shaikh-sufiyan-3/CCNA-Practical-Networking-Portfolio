# Inter-VLAN Routing Verification

## 1. VLAN Verification - SW1

Command used:

```text
show vlan brief
```

Result:

* VLAN 10 `SALES` is active.
* Fa0/1 is assigned to VLAN 10.
* VLAN 20 `HR` is active.
* Fa0/2 is assigned to VLAN 20.

**Status: PASS**

---

## 2. Trunk Verification - SW1

Command used:

```text
show interface trunk
```

Result:

* Fa0/24 is operating in trunking status.
* Encapsulation is `802.1q`.
* VLAN 10 and VLAN 20 are allowed and active on the trunk.
* VLAN 10 and VLAN 20 are in STP forwarding state and are not pruned.

**Status: PASS**

---

## 3. Router Interface Verification - R1

Command used:

```text
show ip interface brief
```

Result:

| Interface | IP Address   | Status | Protocol |
| --------- | ------------ | ------ | -------- |
| G0/0.10   | 192.168.10.1 | up     | up       |
| G0/0.20   | 192.168.20.1 | up     | up       |

Both router subinterfaces are operational.

**Status: PASS**

---

## 4. Routing Table Verification - R1

Command used:

```text
show ip route
```

Result:

```text
C 192.168.10.0/24 is directly connected, GigabitEthernet0/0.10
C 192.168.20.0/24 is directly connected, GigabitEthernet0/0.20
```

The router has both VLAN networks as directly connected routes.

**Status: PASS**

---

## 5. Inter-VLAN Connectivity Test

Test performed from PC1:

```text
ping 192.168.20.10
```

Observed result:

```text
Packets: Sent = 4, Received = 3, Lost = 1 (25% loss)
```

The first packet timed out, while the following three packets received replies successfully.

This behavior can occur during the initial ARP resolution in a Packet Tracer lab. The successful subsequent replies confirm that traffic is being routed between VLAN 10 and VLAN 20.

**Status: PARTIAL — Initial ping showed 25% loss**

A second ping should ideally be performed to confirm `0% packet loss` before marking end-to-end connectivity as fully verified.

---

## 6. Final Verification

| Test                       | Result                           |
| -------------------------- | -------------------------------- |
| VLAN 10 configured         | PASS                             |
| VLAN 20 configured         | PASS                             |
| PC1 access port in VLAN 10 | PASS                             |
| PC2 access port in VLAN 20 | PASS                             |
| SW1-R1 trunk operational   | PASS                             |
| 802.1Q trunking            | PASS                             |
| R1 VLAN 10 subinterface    | PASS                             |
| R1 VLAN 20 subinterface    | PASS                             |
| Routing table              | PASS                             |
| Inter-VLAN communication   | Working, first ping had 25% loss |

## Lab Status

**Configuration: Successfully Verified**

**End-to-End Connectivity: Working, but final 0% loss confirmation is recommended.**

