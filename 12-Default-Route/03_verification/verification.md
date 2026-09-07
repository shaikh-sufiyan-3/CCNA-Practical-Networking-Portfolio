# Project 12 - Default Route Verification

## 1. Objective

Verify that R1 uses a static default route to forward traffic toward R2 and that return traffic from R2 reaches the 192.168.10.0/24 network through a static route.

---

## 2. R1 Verification

### `show ip interface brief`

```text
Interface              IP-Address      OK? Method Status                Protocol
GigabitEthernet0/0     192.168.10.1    YES manual up                    up
GigabitEthernet0/1     10.0.0.1        YES manual up                    up
GigabitEthernet0/2     unassigned      YES unset  administratively down down
Vlan1                  unassigned      YES unset  administratively down down
```

**Result:** R1's required interfaces are `up/up`.

### `show ip route`

Important verified entries:

```text
Gateway of last resort is 10.0.0.2 to network 0.0.0.0

C       10.0.0.0/30 is directly connected, GigabitEthernet0/1
L       10.0.0.1/32 is directly connected, GigabitEthernet0/1
C       192.168.10.0/24 is directly connected, GigabitEthernet0/0
L       192.168.10.1/32 is directly connected, GigabitEthernet0/0
S*      0.0.0.0/0 [1/0] via 10.0.0.2
```

**Result:** The default route is correctly installed as:

`S* 0.0.0.0/0 via 10.0.0.2`

`S*` confirms that it is a static candidate default route.

---

## 3. R2 Verification

### `show ip interface brief`

```text
Interface              IP-Address      OK? Method Status                Protocol
GigabitEthernet0/0     192.168.20.1    YES manual up                    up
GigabitEthernet0/1     10.0.0.2        YES manual up                    up
GigabitEthernet0/2     unassigned      YES unset  administratively down down
Vlan1                  unassigned      YES unset  administratively down down
```

**Result:** R2's required interfaces are `up/up`.

### `show ip route`

Important verified entries:

```text
C       10.0.0.0/30 is directly connected, GigabitEthernet0/1
L       10.0.0.2/32 is directly connected, GigabitEthernet0/1
S       192.168.10.0/24 [1/0] via 10.0.0.1
C       192.168.20.0/24 is directly connected, GigabitEthernet0/0
L       192.168.20.1/32 is directly connected, GigabitEthernet0/0
```

**Result:** R2 has the required return route to `192.168.10.0/24`.

---

## 4. PC1 Verification

### `ipconfig`

```text
IPv4 Address....................: 192.168.10.10
Subnet Mask.....................: 255.255.255.0
Default Gateway.................: 192.168.10.1
```

### Gateway Test

`ping 192.168.10.1`

**Result:** 4 packets received, 0% loss.

### R2 Link Test

`ping 10.0.0.2`

**Result:** 4 packets received, 0% loss.

### End-to-End Test

`ping 192.168.20.10`

**Result:** 4 packets received, 0% loss.

Minimum = 0ms, Maximum = 11ms, Average = 3ms.

---

## 5. PC2 Verification

### `ipconfig`

```text
IPv4 Address....................: 192.168.20.10
Subnet Mask.....................: 255.255.255.0
Default Gateway.................: 192.168.20.1
```

### Gateway Test

`ping 192.168.20.1`

**Result:** 4 packets received, 0% loss.

### R1 Link Test

`ping 10.0.0.1`

**Result:** 4 packets received, 0% loss.

### End-to-End Test

`ping 192.168.10.10`

**Result:** 4 packets received, 0% loss.

---

## 6. Final Verification Result

| Test                     | Result |
| ------------------------ | ------ |
| R1 interfaces            | PASS   |
| R2 interfaces            | PASS   |
| R1 default route         | PASS   |
| R2 return route          | PASS   |
| PC1 gateway connectivity | PASS   |
| PC2 gateway connectivity | PASS   |
| PC1 → R2 connectivity    | PASS   |
| PC2 → R1 connectivity    | PASS   |
| PC1 → PC2 connectivity   | PASS   |
| PC2 → PC1 connectivity   | PASS   |

**Project 12 verification: PASS**

The default-route configuration is working correctly and end-to-end connectivity between both LANs has been successfully verified with 0% packet loss.
