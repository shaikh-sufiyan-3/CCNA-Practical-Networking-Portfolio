# 16 - SSH Remote Access Verification

## 1. Verification Objective

The purpose of this lab is to verify secure remote management of SW1 using SSH.

The verification confirms:

* Management VLAN 10 is configured.
* SW1 has management IP address `192.168.10.2`.
* SSH version 2 is enabled.
* A local administrative user is configured.
* VTY lines use local authentication.
* VTY lines accept SSH only.
* PC1 can reach the switch management IP.
* PC1 can successfully establish an SSH session with SW1.

## 2. VLAN Verification

Command:

```text
show vlan brief
```

Actual relevant result:

```text
10   MANAGEMENT    active    Fa0/1
```

Fa0/1 is correctly assigned to the management VLAN.

## 3. SSH Verification

Command:

```text
show ip ssh
```

Actual result:

```text
SSH Enabled - version 2.0
Authentication timeout: 120 secs; Authentication retries: 3
```

SSH version 2 is enabled.

## 4. Local User Verification

Command:

```text
show running-config | section username
```

Actual result:

```text
username admin secret 5 $1$mERr$Pq3/lr0agnISq0fxb9TUZ0
```

A local administrative user named `admin` is configured.

The password hash is recorded as shown by IOS and the plaintext password is not documented in verification output.

## 5. VTY Verification

Command:

```text
show running-config | section line vty
```

Actual result:

```text
line vty 0 4
 login local
 transport input ssh
line vty 5 15
 login local
 transport input ssh
```

All VTY lines use local authentication and accept SSH as the remote-access protocol.

## 6. Management IP Connectivity

PC1 tested connectivity to SW1:

```text
ping 192.168.10.2
```

Actual result:

```text
Packets: Sent = 4, Received = 4, Lost = 0 (0% loss)
```

The management IP is reachable from PC1.

## 7. SSH Login Test

PC1 initiated an SSH session:

```text
ssh -l admin 192.168.10.2
```

After password authentication, the session reached:

```text
SW1#
```

This proves that the SSH remote-access session was successfully established.

## 8. Final Verification Result

| Verification              | Result |
| ------------------------- | ------ |
| Management VLAN 10        | PASS   |
| Fa0/1 assigned to VLAN 10 | PASS   |
| SSH version 2             | PASS   |
| Local user configured     | PASS   |
| VTY local authentication  | PASS   |
| SSH-only VTY access       | PASS   |
| PC1 → SW1 management IP   | PASS   |
| Actual SSH login          | PASS   |

**Final Status: PROJECT 16 COMPLETE / VERIFIED**
