# Verification - IPv6 Configuration

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
```

Fa0/1 and Fa0/2 are connected and operating in VLAN 1.

## 2. IPv6 Address Verification

### PC1

```text
IPv6 Address: 2001:DB8:10:10::10
IPv4 Address: 0.0.0.0
Default Gateway: ::
                  0.0.0.0
```

PC1 also has an automatically generated link-local IPv6 address:

```text
FE80::20B:BEFF:FE57:ACD0
```

### PC2

```text
IPv6 Address: 2001:DB8:10:10::20
IPv4 Address: 0.0.0.0
Default Gateway: ::
                  0.0.0.0
```

PC2 also has an automatically generated link-local IPv6 address:

```text
FE80::201:43FF:FE66:4B92
```

## 3. IPv6 Network

The lab uses:

```text
Network: 2001:DB8:10:10::/64
```

Configured global unicast addresses:

```text
PC1: 2001:DB8:10:10::10
PC2: 2001:DB8:10:10::20
```

Both addresses belong to the same `/64` IPv6 network.

## 4. IPv6 Connectivity Test

Command from PC1:

```text
ping 2001:DB8:10:10::20
```

Actual result:

```text
Reply from 2001:DB8:10:10::20: bytes=32 time<1ms TTL=128
Reply from 2001:DB8:10:10::20: bytes=32 time=1ms TTL=128
Reply from 2001:DB8:10:10::20: bytes=32 time<1ms TTL=128
Reply from 2001:DB8:10:10::20: bytes=32 time<1ms TTL=128
```

Ping statistics:

```text
Packets: Sent = 4, Received = 4, Lost = 0 (0% loss)
Minimum = 0ms, Maximum = 1ms, Average = 0ms
```

Result: **Successful**

## 5. Final Verification

The IPv6 configuration was successfully verified.

* SW1 Fa0/1 and Fa0/2 are connected.
* PC1 and PC2 have valid global IPv6 addresses.
* Both addresses belong to the same IPv6 `/64` network.
* IPv6 connectivity was confirmed with 0% packet loss.
* No default gateway is required for this same-subnet connectivity test.
* IPv4 is unused in this IPv6-focused lab.
