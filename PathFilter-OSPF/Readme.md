# OSPF Path Filtering with Prefix-List (Cisco Routers)

This lab demonstrates how to filter specific OSPF routes **between different areas** using a `prefix-list` and the `area filter-list` command on Cisco routers.

---

## 🧠 Key Concept

- OSPF uses **LSA Type 3 (Summary LSAs)** to advertise inter-area routes.
- The `area filter-list prefix` command **only works on ABR routers**, affecting **inter-area routes**.
- **Intra-area routes** (LSA Type 1 and 2) **cannot be filtered** using this method.
- Filtering is applied **when a route is advertised across area boundaries**, not within a single area.

---

## 🧪 Lab Topology

```
R1 --- R2 --- R3
     (ABR)
```

- **R1**: OSPF Area 0  
- **R2**: Area Border Router (connected to both Area 0 and Area 1)  
- **R3**: OSPF Area 1

---

## 🎯 Objective

Prevent the network `192.168.10.0/24` (originating on R1) from being advertised to R3 (in Area 1) via OSPF.

---

## ⚙️ Configuration Summary

### ▶️ R1
```bash
interface Loopback0
 ip address 1.1.1.1 255.255.255.255

router ospf 10
 router-id 1.1.1.1
 network 192.168.10.0 0.0.0.255 area 0
 network 192.168.20.0 0.0.0.255 area 0
 network 192.168.30.0 0.0.0.255 area 0

```

---

### ▶️ R2 (ABR)
```bash
interface Loopback0
 ip address 2.2.2.2 255.255.255.255

ip prefix-list BLOCK_R1_NET seq 5 deny 192.168.20.0/24
ip prefix-list BLOCK_R1_NET seq 10 permit 0.0.0.0/0 le 32

router ospf 10
 router-id 2.2.2.2
 network 192.168.30.0 0.0.0.255 area 0
 network 192.168.40.0 0.0.0.255 area 1
 area 0 filter-list prefix BLOCK_R1_NET out
```

---

### ▶️ R3
```bash
interface Loopback0
 ip address 3.3.3.3 255.255.255.255

router ospf 1
 router-id 3.3.3.3
 network 192.168.40.0 0.0.0.255 area 1
 network 192.168.50.0 0.0.0.255 area 1
```

---

## ✅ Expected Result

- R2 learns `192.168.10.0/24` from R1 in Area 0.
- R2 **does not** advertise it to R3 in Area 1 due to the prefix-list filter.
- On **R3**, `show ip route ospf` should **not** contain `192.168.10.0/24`.

---

## 🔍 Verification Commands

Run these on R3 to verify filtering:

```bash
show ip route ospf
show ip ospf database summary
```

If needed, reset OSPF process:

```bash
clear ip ospf process
```

---

## 💡 Notes

- The `distribute-list` command works only for redistributed routes (e.g., static or connected injected into OSPF).
- The `area filter-list prefix` command is only applicable to **ABRs**, and **only filters Type 3 LSAs**.

---

## 🧰 Tools

- Tested on **GNS3** using Cisco IOS image (e.g., `c7200-adventerprisek9-mz.152-4.M7.bin`)
- Minimum 3 routers required (R1, R2 as ABR, R3)

---

## 📁 License

This lab and documentation are released under the [MIT License](LICENSE).

---

Happy Networking! 🚀
