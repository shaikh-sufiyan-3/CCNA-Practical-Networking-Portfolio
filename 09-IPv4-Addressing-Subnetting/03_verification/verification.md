# Verification - IPv4 Addressing & Subnetting

## 1. Switch Interface Verification

Command:

```text
show interfaces status
```

Actual result:

```text
Port      Name               Status       Vlan       Duplex  Speed Type
Fa0/1                        connected    1          a-full  a-100 10/100BaseTX
Fa0/2                        connected    1          a-full  a-100 10/100BaseTX
Fa0/3                        connected    1          a-full  a-100 10/100BaseTX
```

Fa0/1, Fa0/2, and Fa0/3 are connected and operating in VLAN 1.

## 2. IPv4 Address Verification

### PC1

```text
IPv4 Address: 192.168.10.10
Subnet Mask: 255.255.255.192
Default Gateway: 0.0.0.0
```

### PC2

```text
IPv4 Address: 192.168.10.20
Subnet Mask: 255.255.255.192
Default Gateway: 0.0.0.0
```

### PC3

```text
IPv4 Address: 192.168.10.30
Subnet Mask: 255.255.255.192
Default Gateway: 0.0.0.0
```

All three PCs are correctly configured with a `/26` subnet mask.

## 3. Subnet Calculation

Network:

```text
192.168.10.0/26
```

Subnet mask:

```text
255.255.255.192
```

Address range:

```text
Network Address: 192.168.10.0
Usable Hosts:    192.168.10.1 - 192.168.10.62
Broadcast:       192.168.10.63
```

The assigned addresses `.10`, `.20`, and `.30` are valid host addresses within this subnet.

## 4. PC1 to PC2 Connectivity

Command:

```text
ping 192.168.10.20
```

Actual result:

```text
Packets: Sent = 4, Received = 4, Lost = 0 (0% loss)
Minimum = 0ms, Maximum = 1ms, Average = 0ms
```

Result: **Successful**

## 5. PC1 to PC3 Connectivity

Command:

```text
ping 192.168.10.30
```

Actual result:

```text
Packets: Sent = 4, Received = 4, Lost = 0 (0% loss)
Minimum = 0ms, Maximum = 1ms, Average = 0ms
```

Result: **Successful**

## 6. Final Verification

The lab is successfully verified.

* Correct `/26` subnet mask configured.
* All assigned IP addresses belong to the same subnet.
* PC1 can communicate with PC2.
* PC1 can communicate with PC3.
* No default gateway is required for this same-subnet connectivity test.
* No packet loss was observed.
