# VLAN Verification

## 1. VLAN Verification

Command:

```text
show vlan brief
```

Output:

```text
VLAN Name                             Status    Ports
---- -------------------------------- --------- -------------------------------
1    default                          active    Fa0/3, Fa0/4, Fa0/5, Fa0/6
                                                Fa0/7, Fa0/8, Fa0/9, Fa0/10
                                                Fa0/11, Fa0/12, Fa0/13, Fa0/14
                                                Fa0/15, Fa0/16, Fa0/17, Fa0/18
                                                Fa0/19, Fa0/20, Fa0/21, Fa0/22
                                                Fa0/23, Fa0/24, Gig0/1, Gig0/2
10   SALES                            active    Fa0/1
20   HR                               active    Fa0/2
1002 fddi-default                     active
1003 token-ring-default               active
1004 fddinet-default                  active
1005 trnet-default                    active
```

### Verification Result

* VLAN 10 (SALES) is active.
* VLAN 20 (HR) is active.
* Fa0/1 is assigned to VLAN 10.
* Fa0/2 is assigned to VLAN 20.

---

## 2. Connectivity Test

Test performed from PC1 to PC2:

```text
ping 192.168.20.10
```

Output:

```text
Pinging 192.168.20.10 with 32 bytes of data:

Request timed out.
Request timed out.
Request timed out.
Request timed out.

Ping statistics for 192.168.20.10:
    Packets: Sent = 4, Received = 0, Lost = 4 (100% loss),
```

### Verification Result

The ping failed as expected because PC1 and PC2 are in different VLANs and no Inter-VLAN Routing has been configured.

**Lab Status: Successfully Verified**
