# 15 - ACL Verification

## 1. Verification Objective

The purpose of verification is to confirm that:

* VLAN 10 and VLAN 20 are correctly configured.
* The router-on-a-stick interfaces are operational.
* Extended ACL 100 is correctly configured.
* ACL 100 is applied inbound on VLAN 10.
* PC1 (`192.168.10.10`) is blocked from reaching PC2 (`192.168.20.10`).
* PC2 can still reach PC1.

## 2. R1 Interface Verification

Command:

```text
show ip interface brief
```

Relevant result:

```text
GigabitEthernet0/0.10  192.168.10.1    up    up
GigabitEthernet0/0.20  192.168.20.1    up    up
```

Both router subinterfaces are operational.

## 3. ACL Verification

Command:

```text
show access-lists
```

Actual result:

```text
Extended IP access list 100
    10 deny ip host 192.168.10.10 host 192.168.20.10 (4 match(es))
    20 permit ip any any (4 match(es))
```

The deny statement has 4 matches, proving that traffic from PC1 to PC2 matched the ACL.

The `permit ip any any` statement also has 4 matches, confirming permitted traffic is being processed by the ACL.

## 4. ACL Interface Application

Command:

```text
show ip interface GigabitEthernet0/0.10
```

Relevant result:

```text
Outgoing access list is not set
Inbound  access list is 100
```

ACL 100 is correctly applied in the inbound direction on VLAN 10.

## 5. Switch VLAN Verification

Command:

```text
show vlan brief
```

Actual relevant result:

```text
10   SALES   active    Fa0/1
20   HR      active    Fa0/2
```

Therefore:

* Fa0/1 belongs to VLAN 10.
* Fa0/2 belongs to VLAN 20.

## 6. Trunk Verification

Command:

```text
show interfaces trunk
```

Actual result:

```text
Fa0/24      on      802.1q      trunking      1
```

VLANs allowed and active:

```text
1,10,20
```

VLANs forwarding and not pruned:

```text
1,10,20
```

The SW1-to-R1 link is correctly operating as an 802.1Q trunk.

## 7. PC1 Connectivity Test

### PC1 → R1 Gateway

Command:

```text
ping 192.168.10.1
```

Result:

```text
Sent = 4, Received = 4, Lost = 0 (0% loss)
```

The PC1-to-gateway connection is working.

### PC1 → PC2

Command:

```text
ping 192.168.20.10
```

Actual result:

```text
Reply from 192.168.10.1: Destination host unreachable.
```

Statistics:

```text
Sent = 4, Received = 0, Lost = 4 (100% loss)
```

This failure is expected because ACL 100 explicitly denies traffic from `192.168.10.10` to `192.168.20.10`.

The 4 matches on the ACL deny statement provide direct evidence of this behavior.

## 8. PC2 Connectivity Test

### PC2 → R1 Gateway

Command:

```text
ping 192.168.10.1
```

Result:

```text
Sent = 4, Received = 4, Lost = 0 (0% loss)
```

### PC2 → PC1

Command:

```text
ping 192.168.20.10
```

Result:

```text
Sent = 4, Received = 4, Lost = 0 (0% loss)
```

PC2 can communicate successfully in the reverse direction because ACL 100 is applied inbound only on VLAN 10.

## 9. Final Verification Result

| Verification                       | Result              |
| ---------------------------------- | ------------------- |
| R1 subinterfaces up/up             | PASS                |
| VLAN 10 configured                 | PASS                |
| VLAN 20 configured                 | PASS                |
| SW1-R1 trunk operational           | PASS                |
| ACL 100 configured                 | PASS                |
| ACL 100 applied inbound on G0/0.10 | PASS                |
| PC1 → Gateway                      | PASS                |
| PC1 → PC2                          | BLOCKED as intended |
| PC2 → PC1                          | PASS                |

**Final Status: PROJECT 15 COMPLETE / VERIFIED**
