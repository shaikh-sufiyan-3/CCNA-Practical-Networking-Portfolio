# Access & Trunk Ports Verification

## 1. SW1 VLAN Verification

Command:

```text
show vlan brief
```

Result:

```text
VLAN 10 - SALES - Active
Fa0/1 assigned to VLAN 10
```

---

## 2. SW1 Trunk Verification

Command:

```text
show interfaces trunk
```

Result:

```text
Port        Mode         Encapsulation  Status        Native vlan
Fa0/24      on           802.1q         trunking      1
```

VLANs active on the trunk:

```text
Fa0/24      1,10
```

Spanning Tree forwarding:

```text
Fa0/24      1,10
```

---

## 3. SW2 VLAN Verification

Command:

```text
show vlan brief
```

Result:

```text
VLAN 10 - SALES - Active
Fa0/1 assigned to VLAN 10
```

---

## 4. SW2 Trunk Verification

Command:

```text
show interfaces trunk
```

Result:

```text
Port        Mode         Encapsulation  Status        Native vlan
Fa0/24      on           802.1q         trunking      1
```

VLANs active on the trunk:

```text
Fa0/24      1,10
```

Spanning Tree forwarding:

```text
Fa0/24      1,10
```

---

## 5. Connectivity Test

Test performed from PC1 to PC2:

```text
ping 192.168.10.20
```

Result:

```text
Packets: Sent = 4, Received = 4, Lost = 0 (0% loss)
```

### Result

Ping was successful.

PC1 and PC2 are in VLAN 10 and can communicate across the trunk link between SW1 and SW2.

---

## 6. Final Verification

* VLAN 10 is active on both switches.
* PC1 and PC2 are assigned to VLAN 10.
* Fa0/24 is operating as an 802.1Q trunk on both switches.
* VLAN 10 is allowed and forwarding across the trunk.
* PC1 successfully communicates with PC2.

**Lab Status: Successfully Verified**
