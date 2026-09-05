# STP / RSTP Verification

## 1. VLAN Verification

### SW1

Command:

```text
show vlan brief
```

Result:

* VLAN 10 `SALES` is active.
* Fa0/1 is assigned to VLAN 10.

**Status: PASS**

### SW2

Command:

```text
show vlan brief
```

Result:

* VLAN 10 `SALES` is active.
* Fa0/1 is assigned to VLAN 10.

**Status: PASS**

---

## 2. Trunk Verification

### SW1

Command:

```text
show interface trunk
```

Result:

* Fa0/23 is trunking.
* Fa0/24 is trunking.
* Encapsulation: 802.1Q.
* VLAN 10 is active on both trunks.
* Fa0/23 is forwarding VLAN 10.
* Fa0/24 is also forwarding VLAN 10 on the root bridge.

**Status: PASS**

### SW2

Command:

```text
show interfaces trunk
```

Result:

* Fa0/23 is trunking.
* Fa0/24 is trunking.
* Encapsulation: 802.1Q.
* VLAN 10 is active.
* Fa0/23 is forwarding VLAN 10.
* Fa0/24 is not forwarding VLAN 10 because RSTP has placed it in the alternate/blocking state.

**Status: PASS**

---

## 3. RSTP Verification

### SW1

Command:

```text
show spanning-tree vlan 10
```

Result:

* Spanning-tree protocol is RSTP.
* SW1 is the root bridge.
* Fa0/1 is Designated/Forwarding.
* Fa0/23 is Designated/Forwarding.
* Fa0/24 is Designated/Forwarding.

**Status: PASS**

### SW2

Command:

```text
show spanning-tree vlan 10
```

Result:

* Spanning-tree protocol is RSTP.
* SW2 identifies SW1 as the root bridge.
* Fa0/23 is the Root Port and Forwarding.
* Fa0/24 is Alternate and Blocking.
* Fa0/1 is Designated and Forwarding.

This confirms that RSTP is preventing a Layer 2 loop by keeping the redundant path in an alternate/blocking state.

**Status: PASS**

---

## 4. RSTP Mode Verification

Command:

```text
show spanning-tree summary
```

Result on both switches:

```text
Switch is in rapid-pvst mode
```

**Status: PASS**

---

## 5. Connectivity Test

From PC1:

```text
ping 192.168.10.20
```

Result:

```text
Packets: Sent = 4, Received = 4, Lost = 0 (0% loss)
Minimum = 0ms, Maximum = 1ms, Average = 0ms
```

**Status: PASS**

---

## 6. Final Verification Summary

| Test                                       | Result |
| ------------------------------------------ | ------ |
| VLAN 10 configured                         | PASS   |
| Access ports configured                    | PASS   |
| Trunk links configured                     | PASS   |
| RSTP enabled                               | PASS   |
| SW1 as Root Bridge                         | PASS   |
| SW2 Root Port                              | PASS   |
| Redundant link in Alternate/Blocking state | PASS   |
| PC-to-PC connectivity                      | PASS   |

## Final Result

The STP/RSTP lab was successfully configured and verified.

RSTP correctly identified SW1 as the root bridge and placed SW2 Fa0/24 into the Alternate/Blocking state to prevent a Layer 2 loop. End-to-end connectivity between PC1 and PC2 was successful with 0% packet loss.
