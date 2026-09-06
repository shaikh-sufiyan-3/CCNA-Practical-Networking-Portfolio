# DHCP Verification

## 1. DHCP Pool Verification

Command:

```text id="j6f5n0"
show ip dhcp pool
```

Result:

* DHCP pool: `SALES`
* Total addresses: 254
* Leased addresses: 1
* Excluded addresses: 1
* Network range: `192.168.10.0/24`

**Status: PASS**

---

## 2. DHCP Binding Verification

Command:

```text id="7hjx9n"
show ip dhcp binding
```

Actual result:

```text id="9u1v4k"
IP address       Client-ID/              Lease expiration        Type
192.168.10.11    0060.70C7.B32C           --                     Automatic
```

The DHCP server successfully assigned `192.168.10.11` to the client.

**Status: PASS**

---

## 3. Router Interface Verification

Command:

```text id="4c6k2p"
show ip interface brief
```

Actual result confirms:

```text id="y9c7tm"
GigabitEthernet0/0     192.168.10.1    YES manual    up    up
```

The router interface connected to the LAN is operational.

**Status: PASS**

---

## 4. DHCP Addressing

The DHCP configuration reserves the addresses:

```text id="a1h2s7"
192.168.10.1 - 192.168.10.10
```

The first observed DHCP client received:

```text id="t5k3n8"
192.168.10.11
```

This confirms that the DHCP server is assigning addresses outside the excluded range.

**Status: PASS**

---

## 5. Connectivity Test

The DHCP-assigned PC should be tested against the router:

```text id="c4m7vx"
ping 192.168.10.1
```

The actual ping result should be recorded from Packet Tracer.

**Status: Pending actual ping output**

---

## 6. Final Verification Summary

| Test                              | Result                         |
| --------------------------------- | ------------------------------ |
| DHCP pool created                 | PASS                           |
| DHCP network configured           | PASS                           |
| Excluded address range configured | PASS                           |
| DHCP lease assigned               | PASS                           |
| Client received 192.168.10.11     | PASS                           |
| R1 G0/0 192.168.10.1              | PASS                           |
| R1 G0/0 up/up                     | PASS                           |
| PC-to-Router ping                 | Verify from actual ping output |

## Conclusion

The DHCP server configuration is working correctly based on the observed DHCP pool and binding outputs.

The router successfully assigned `192.168.10.11` to the client, while R1's LAN interface is operational at `192.168.10.1`.
