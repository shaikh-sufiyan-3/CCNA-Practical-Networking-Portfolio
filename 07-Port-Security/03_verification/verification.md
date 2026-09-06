# Port Security Verification

## 1. VLAN Verification

Command:

```text
show vlan brief
```

Result:

* VLAN 10 `SALES` is active.
* Fa0/1 is assigned to VLAN 10.
* Fa0/2 is assigned to VLAN 10.

**Status: PASS**

---

## 2. Port Security Verification

Command:

```text
show port-security
```

Result:

* Fa0/1: Maximum secure addresses = 1.
* Fa0/2: Maximum secure addresses = 1.
* Current secure addresses = 1 on both ports.
* Security violations = 0.
* Security action = Shutdown.

**Status: PASS**

---

## 3. Fa0/1 Port Security

Command:

```text
show port-security interface f0/1
```

Result:

* Port Security: Enabled
* Port Status: Secure-up
* Violation Mode: Shutdown
* Maximum MAC Addresses: 1
* Security Violation Count: 0

The interface-specific output reports zero current/sticky MAC addresses, while the secure MAC address table confirms the sticky MAC learned on Fa0/1.

**Status: PASS**

---

## 4. Fa0/2 Port Security

Command:

```text
show port-security interface f0/2
```

Result:

* Port Security: Enabled
* Port Status: Secure-up
* Violation Mode: Shutdown
* Maximum MAC Addresses: 1
* Security Violation Count: 0

The secure MAC address table confirms the sticky MAC learned on Fa0/2.

**Status: PASS**

---

## 5. Secure MAC Address Verification

Command:

```text
show port-security address
```

Result:

```text
Vlan    Mac Address       Type             Ports
10      0001.C709.C36A    SecureSticky     Fa0/1
10      00D0.584E.7BC0    SecureSticky     Fa0/2
```

This confirms that both access ports have learned their connected device MAC addresses as SecureSticky addresses.

**Status: PASS**

---

## 6. Security Violation Verification

Current security violation count:

* Fa0/1: 0
* Fa0/2: 0

No unauthorized MAC address violation was generated during the lab.

**Status: PASS**

---

## 7. Connectivity Test

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

## 8. Final Verification Summary

| Test                      | Result |
| ------------------------- | ------ |
| VLAN 10 configured        | PASS   |
| Fa0/1 assigned to VLAN 10 | PASS   |
| Fa0/2 assigned to VLAN 10 | PASS   |
| Port Security enabled     | PASS   |
| Maximum MAC = 1           | PASS   |
| Sticky MAC configured     | PASS   |
| Sticky MAC learned        | PASS   |
| Violation mode = Shutdown | PASS   |
| Security violations       | 0      |
| PC-to-PC connectivity     | PASS   |
| Ping packet loss          | 0%     |

## Final Result

The Port Security lab was successfully configured and verified.

Both access ports are protected with a maximum of one secure MAC address. Sticky MAC learning is active, the violation mode is set to shutdown, no security violations occurred, and PC-to-PC connectivity was successful with 0% packet loss.
