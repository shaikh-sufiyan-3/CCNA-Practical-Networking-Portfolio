# EtherChannel Verification

## 1. SW1 VLAN Verification

Command used:

```text
show vlan brief
```

Result:

* VLAN 10 `SALES` is active.
* Fa0/1 is assigned to VLAN 10.

**Status: PASS**

---

## 2. SW1 EtherChannel Verification

Command used:

```text
show etherchannel summary
```

Result:

```text
Group  Port-channel  Protocol    Ports
1      Po1(SU)       LACP        Fa0/23(P) Fa0/24(P)
```

Verification:

* EtherChannel group 1 is configured.
* Port-channel 1 is Layer 2 and in use.
* LACP is the active protocol.
* Fa0/23 is successfully bundled.
* Fa0/24 is successfully bundled.

**Status: PASS**

---

## 3. SW1 Trunk Verification

Command used:

```text
show interfaces trunk
```

Result:

* Po1 is in `trunking` status.
* Encapsulation is `802.1q`.
* VLAN 10 is allowed and active.
* VLAN 10 is in STP forwarding state and not pruned.

**Status: PASS**

---

## 4. SW2 VLAN Verification

Command used:

```text
show vlan brief
```

Result:

* VLAN 10 `SALES` is active.
* Fa0/1 is assigned to VLAN 10.

**Status: PASS**

---

## 5. SW2 EtherChannel Verification

Command used:

```text
show etherchannel summary
```

Result:

```text
Group  Port-channel  Protocol    Ports
1      Po1(SU)       LACP        Fa0/23(P) Fa0/24(P)
```

Verification:

* EtherChannel group 1 is configured.
* Port-channel 1 is Layer 2 and in use.
* LACP is the active protocol.
* Fa0/23 is successfully bundled.
* Fa0/24 is successfully bundled.

**Status: PASS**

---

## 6. SW2 Trunk Verification

Command used:

```text
show interfaces trunk
```

Result:

* Po1 is in `trunking` status.
* Encapsulation is `802.1q`.
* VLAN 10 is allowed and active.
* VLAN 10 is in STP forwarding state and not pruned.

**Status: PASS**

---

## 7. End-to-End Connectivity Test

Test performed from PC1:

```text
ping 192.168.10.20
```

Result:

```text
Packets: Sent = 4, Received = 4, Lost = 0 (0% loss)
```

All four packets were successfully received.

**Status: PASS**

---

## 8. Final Verification

| Verification                  | Result |
| ----------------------------- | ------ |
| VLAN 10 active on SW1         | PASS   |
| VLAN 10 active on SW2         | PASS   |
| SW1 Fa0/23 bundled            | PASS   |
| SW1 Fa0/24 bundled            | PASS   |
| SW2 Fa0/23 bundled            | PASS   |
| SW2 Fa0/24 bundled            | PASS   |
| LACP operational              | PASS   |
| Port-channel 1 in use         | PASS   |
| Port-channel trunking         | PASS   |
| 802.1Q encapsulation          | PASS   |
| VLAN 10 forwarding across Po1 | PASS   |
| PC1 → PC2 connectivity        | PASS   |
| Packet loss                   | 0%     |

## Lab Status

**Successfully Verified**
