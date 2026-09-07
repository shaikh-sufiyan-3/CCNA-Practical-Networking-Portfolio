# Verification - Static Routing

## 1. R1 Interface Verification

Command:

```text
show ip interface brief
```

Actual result:

```text
GigabitEthernet0/0     192.168.10.1    YES manual up                    up
GigabitEthernet0/1     10.0.0.1        YES manual up                    up
```

Both required R1 interfaces are up/up.

## 2. R1 Routing Table

Command:

```text
show ip route
```

Relevant routes:

```text
C       10.0.0.0/30 is directly connected, GigabitEthernet0/1
C       192.168.10.0/24 is directly connected, GigabitEthernet0/0
S       192.168.20.0/24 [1/0] via 10.0.0.2
```

R1 has a static route to the remote LAN `192.168.20.0/24` through R2 at `10.0.0.2`.

## 3. R2 Interface Verification

Command:

```text
show ip interface brief
```

Actual result:

```text
GigabitEthernet0/0     192.168.20.1    YES manual up                    up
GigabitEthernet0/1     10.0.0.2        YES manual up                    up
```

Both required R2 interfaces are up/up.

## 4. R2 Routing Table

Command:

```text
show ip route
```

Relevant routes:

```text
C       10.0.0.0/30 is directly connected, GigabitEthernet0/1
S       192.168.10.0/24 [1/0] via 10.0.0.1
C       192.168.20.0/24 is directly connected, GigabitEthernet0/0
```

R2 has a static route to the remote LAN `192.168.10.0/24` through R1 at `10.0.0.1`.

## 5. PC1 IP Verification

```text
IPv4 Address:    192.168.10.10
Subnet Mask:     255.255.255.0
Default Gateway: 192.168.10.1
```

## 6. PC2 IP Verification

```text
IPv4 Address:    192.168.20.10
Subnet Mask:     255.255.255.0
Default Gateway: 192.168.20.1
```

## 7. PC1 to Local Gateway

Command:

```text
ping 192.168.10.1
```

Result:

```text
Sent = 4, Received = 4, Lost = 0 (0% loss)
```

Result: **Successful**

## 8. PC1 to R2

Command:

```text
ping 10.0.0.2
```

Result:

```text
Sent = 4, Received = 4, Lost = 0 (0% loss)
```

Result: **Successful**

## 9. PC1 to Remote PC2

Command:

```text
ping 192.168.20.10
```

Recorded result:

```text
Packets: Sent = 4, Received = 3, Lost = 1 (25% loss)
```

The first request timed out, followed by three successful replies.

## 10. PC2 to Remote PC1

Command:

```text
ping 192.168.10.10
```

Result:

```text
Sent = 4, Received = 4, Lost = 0 (0% loss)
```

Result: **Successful**

## 11. Final Verification

The static routing configuration is correct.

Evidence:

* R1 and R2 interfaces are up/up.
* R1 has a static route to `192.168.20.0/24`.
* R2 has a static route to `192.168.10.0/24`.
* PC1 can reach R1.
* PC1 can reach R2.
* PC2 can reach PC1 with 0% packet loss.
* The recorded PC1-to-PC2 test had one initial timeout and then three successful replies.

The routing tables confirm that both remote networks are reachable through the correct next-hop routers.
