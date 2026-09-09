# Project 14 - NAT/PAT Verification

## 1. R1 Interface Verification

`show ip interface brief`

```text
GigabitEthernet0/0     192.168.10.1    YES manual up                    up
GigabitEthernet0/1     203.0.113.2     YES manual up                    up
```

**Result: PASS**

Both NAT interfaces are operational.

* G0/0 = inside interface
* G0/1 = outside interface

---

## 2. NAT Translation Verification

`show ip nat translations`

Verified translations:

```text
Pro  Inside global     Inside local       Outside local      Outside global

icmp 203.0.113.2:29    192.168.10.10:29   203.0.113.1:29     203.0.113.1:29
icmp 203.0.113.2:30    192.168.10.10:30   203.0.113.1:30     203.0.113.1:30
icmp 203.0.113.2:31    192.168.10.10:31   203.0.113.1:31     203.0.113.1:31
icmp 203.0.113.2:32    192.168.10.10:32   203.0.113.1:32     203.0.113.1:32
```

**Result: PASS**

The inside local address:

`192.168.10.10`

was translated to the inside global address:

`203.0.113.2`

This confirms PAT is actively translating the inside host using R1's outside interface address.

---

## 3. NAT Statistics

`show ip nat statistics`

Verified:

```text
Total translations: 4 (0 static, 4 dynamic, 4 extended)

Outside Interfaces: GigabitEthernet0/1

Inside Interfaces: GigabitEthernet0/0

Hits: 14
Misses: 20

Expired translations: 12
```

**Result: PASS**

The router has 4 dynamic translations and NAT has recorded 14 hits.

The presence of dynamic translations confirms that PAT is functioning.

---

## 4. R1 Routing Verification

`show ip route`

Verified default route:

```text
Gateway of last resort is 203.0.113.1 to network 0.0.0.0

S*   0.0.0.0/0 [1/0] via 203.0.113.1
```

Connected networks:

```text
C       192.168.10.0/24 is directly connected, GigabitEthernet0/0
C       203.0.113.0/30 is directly connected, GigabitEthernet0/1
```

**Result: PASS**

R1 has a valid default route toward R2.

---

## 5. R2 Interface Verification

`show ip interface brief`

```text
GigabitEthernet0/0     203.0.113.1     YES manual up                    up
```

**Result: PASS**

R2's outside-side interface is operational.

---

## 6. PC1 Verification

### IP Configuration

```text
IPv4 Address:    192.168.10.10
Subnet Mask:     255.255.255.0
Default Gateway: 192.168.10.1
```

### Local Gateway Test

`ping 192.168.10.1`

```text
Packets: Sent = 4, Received = 4, Lost = 0 (0% loss)
Minimum = 0ms, Maximum = 10ms, Average = 2ms
```

**Result: PASS**

### Outside Network Test

`ping 203.0.113.1`

```text
Packets: Sent = 4, Received = 4, Lost = 0 (0% loss)
Minimum = 0ms, Maximum = 1ms, Average = 0ms
```

**Result: PASS**

---

## 7. Final Verification

| Verification             | Result         |
| ------------------------ | -------------- |
| R1 inside interface      | PASS           |
| R1 outside interface     | PASS           |
| R2 outside interface     | PASS           |
| NAT translation          | PASS           |
| Dynamic PAT translations | PASS           |
| NAT hits recorded        | PASS           |
| R1 default route         | PASS           |
| PC1 → R1                 | PASS — 0% loss |
| PC1 → R2                 | PASS — 0% loss |

**Project 14 Status: COMPLETE / VERIFIED**

PAT successfully translated the inside local address `192.168.10.10` to R1's outside address `203.0.113.2`.
