# Project 13 - OSPF Verification

## 1. R1 Verification

### Interface Status

`show ip interface brief`

Required interfaces:

```text
GigabitEthernet0/0     192.168.10.1    up    up
GigabitEthernet0/1     10.0.0.1        up    up
```

**Result: PASS**

Both required R1 interfaces are operational.

### OSPF Neighbor

`show ip ospf neighbor`

```text
Neighbor ID     Pri   State           Dead Time   Address         Interface
2.2.2.2           1   FULL/BDR        00:00:35    10.0.0.2        GigabitEthernet0/1
```

**Result: PASS**

R1 has formed a **FULL OSPF adjacency** with R2.

### Routing Table

`show ip route`

Verified OSPF route:

```text
O    192.168.20.0/24 [110/2] via 10.0.0.2, GigabitEthernet0/1
```

**Result: PASS**

R1 learned the remote LAN through OSPF.

---

## 2. R2 Verification

### Interface Status

`show ip interface brief`

Required interfaces:

```text
GigabitEthernet0/0     192.168.20.1    up    up
GigabitEthernet0/1     10.0.0.2        up    up
```

**Result: PASS**

Both required R2 interfaces are operational.

### OSPF Neighbor

`show ip ospf neighbor`

```text
Neighbor ID     Pri   State           Dead Time   Address         Interface
1.1.1.1           1   FULL/DR         00:00:37    10.0.0.1        GigabitEthernet0/1
```

**Result: PASS**

R2 has formed a **FULL OSPF adjacency** with R1.

### Routing Table

`show ip route`

Verified OSPF route:

```text
O    192.168.10.0/24 [110/2] via 10.0.0.1, GigabitEthernet0/1
```

**Result: PASS**

R2 learned the remote LAN through OSPF.

---

## 3. PC1 Verification

### IP Configuration

```text
IPv4 Address:    192.168.10.10
Subnet Mask:     255.255.255.0
Default Gateway: 192.168.10.1
```

### Tests

| Test                | Result         |
| ------------------- | -------------- |
| PC1 → 192.168.10.1  | PASS — 0% loss |
| PC1 → 10.0.0.2      | PASS — 0% loss |
| PC1 → 192.168.20.10 | PASS — 0% loss |

PC1 successfully reached the remote LAN through the OSPF-routed path.

---

## 4. PC2 Verification

### IP Configuration

```text
IPv4 Address:    192.168.20.10
Subnet Mask:     255.255.255.0
Default Gateway: 192.168.20.1
```

### Tests

| Test                | Result         |
| ------------------- | -------------- |
| PC2 → 192.168.20.1  | PASS — 0% loss |
| PC2 → 10.0.0.1      | PASS — 0% loss |
| PC2 → 192.168.10.10 | PASS — 0% loss |

PC2 successfully reached the remote LAN through the OSPF-routed path.

---

## 5. Final Result

| Verification                | Status |
| --------------------------- | ------ |
| R1 interfaces up/up         | PASS   |
| R2 interfaces up/up         | PASS   |
| R1-R2 OSPF adjacency        | PASS   |
| R1 remote OSPF route        | PASS   |
| R2 remote OSPF route        | PASS   |
| PC1 end-to-end connectivity | PASS   |
| PC2 end-to-end connectivity | PASS   |

**Project 13 Status: COMPLETE / VERIFIED**

OSPF Area 0 successfully established routing between the two LANs.
