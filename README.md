# Basic Inter-VLAN Routing (Router-on-a-Stick)

To build a segmented network for three departments (HR, IT, and Guest) using a single physical router-to-switch link.

## Technical Overview
* **VLANs:** Segmented traffic into **VLAN 10** (HR), **VLAN 20** (IT), and **VLAN 30** (Guest).
* **Trunking:** Configured IEEE 802.1Q trunking on the switch-to-router uplink to allow multi-VLAN traffic over one cable.
* **Layer 3 Routing:** Created logical sub-interfaces on a Cisco 2911 router to serve as the default gateway for each subnet.

---

## Challenges and Troubleshooting
During the setup, several key issues required troubleshooting to restore connectivity:

* **Physical vs. Logical Ports:** Initially used the "Lightning Bolt" auto-connect, which mapped to the wrong physical ports. I manually re-patched the link to the Gigabit ports to ensure higher bandwidth for the trunk.
* **Syntax & Typos:** Faced common CLI challenges, such as the "Translating" hang (resolved with `Ctrl+Shift+6`) and an encapsulation spelling error on the router that temporarily broke the Guest gateway.
* **IP Logic:** Resolved a subnet mismatch where the router sub-interface was configured for the `192.168.40.x` network while the laptop was on `192.168.30.x`. Correcting the gateway address restored the "ping" path.

---

## Verification
End-to-end connectivity was verified using ICMP pings between departments. After resolving the ARP penalty and configuration errors, 100% success rate was achieved.
