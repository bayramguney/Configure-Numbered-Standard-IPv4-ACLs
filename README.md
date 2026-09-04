# Configure-Numbered-Standard-IPv4-ACLs

# Packet Tracer – Configure Numbered Standard IPv4 ACLs

## Overview

This lab demonstrates how to configure and verify **numbered Standard IPv4 Access Control Lists (ACLs)** in Cisco Packet Tracer. The objective is to restrict network access based on **source IP addresses** while allowing all other network traffic.

## Objectives

* Plan ACL implementation based on network security policies.
* Configure numbered Standard ACLs on Cisco routers.
* Apply ACLs to router interfaces.
* Verify ACL functionality using ping tests and ACL statistics.

## Network Topology

* **3 Routers:** R1, R2, R3
* **3 PCs:** PC1, PC2, PC3
* **1 Web Server**
* Routing Protocol: **EIGRP**

### Networks

* 192.168.10.0/24 – PC1
* 192.168.11.0/24 – PC2
* 192.168.20.0/24 – Web Server
* 192.168.30.0/24 – PC3

## Security Policies

### R2 ACL

* Deny hosts from **192.168.11.0/24** access to the **Web Server (192.168.20.254)**.
* Permit all other traffic.

### R3 ACL

* Deny hosts from **192.168.10.0/24** access to the **192.168.30.0/24** network.
* Permit all other traffic.

## Configuration Summary

### R2

```plaintext
access-list 1 deny 192.168.11.0 0.0.0.255
access-list 1 permit any

interface GigabitEthernet0/0
 ip access-group 1 out
```

### R3

```plaintext
access-list 1 deny 192.168.10.0 0.0.0.255
access-list 1 permit any

interface GigabitEthernet0/0
 ip access-group 1 out
```

## Verification Commands

```plaintext
show access-lists
show running-config
show ip interface gigabitethernet0/0
```

## Expected Results

| Test             | Expected Result |
| ---------------- | --------------- |
| PC1 → PC2        | ✅ Success       |
| PC1 → Web Server | ✅ Success       |
| PC2 → Web Server | ❌ Blocked       |
| PC1 → PC3        | ❌ Blocked       |
| PC2 → PC3        | ✅ Success       |
| PC3 → Web Server | ✅ Success       |

## Skills Learned

* Standard IPv4 ACL configuration
* Numbered ACL syntax
* Wildcard mask usage
* Applying ACLs to interfaces
* Verifying ACL operation with Cisco IOS commands
* Testing network connectivity and access restrictions

## Conclusion

This lab demonstrates how Standard ACLs can effectively control network access using source IP addresses. Proper ACL placement and verification ensure that security policies are enforced without disrupting permitted network communication.
