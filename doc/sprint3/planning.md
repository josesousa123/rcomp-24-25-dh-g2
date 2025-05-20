RCOMP 2024-2025 Project - Sprint 3 planning
===========================================
### Sprint master: 1220848 ###

---

# 1. Sprint's backlog #

| Task  | Task description                                                                                                                                                                                                                                                  | Assignment |
|:-----:|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:----------:|
| T.3.1 | Update the **building1.pkt** layer three Packet Tracer simulation from the previous sprint, to include the described features in this sprint for building one.                                                                                                    |  1230596   |
| T.3.2 | Update the **building2.pkt** layer three Packet Tracer simulation from the previous sprint, to include the described features in this sprint for building two. Final integration of each member’s Packet Tracer simulation into a single simulation (campus.pkt). |  1220848   |
| T.3.3 | Update the **building3.pkt** layer three Packet Tracer simulation from the previous sprint, to include the described features in this sprint for building three.                                                                                                  |  1230595   |
- Task T.3.4 is to be ignored because the team only have three members.

---

# 2. Technical decisions and coordination #

- **Packet Tracer version:** `8.2.2.0400`
- **VTP Domain Name:** `r2425dhg2`
- **VLAN ID Range:** `390 – 411`
- **IPv4 Address Block Assigned:** `10.24.32.0 /20`
- **ISP Router IPv4 Node Address:** `87.5.127.205 /30`
- **Switch Model:** `Pt-Empty`
- **Phone Model:** `7960`
- **Router Model:** `2811`
- **Default vlan id:** `1`
- **Default gateway** will be the Host Min for every network
- **Hardware names format:** `[DeviceType][Number]-B[BuildingNumber]-F[FloorNumber]`

### **Sprint 2 changes:**
- Backbone router changed to act as a "MAIL".

### **Sprint 3 decisions:**

- Add one server and one phone to each building.

1. **Servers & Phones**
    - Add one server and one IP phone to each building.
   

2. **OSPF Areas**
    - Area 0: Backbone
    - Area 1: Building 1
    - Area 2: Building 2
    - Area 3: Building 3
   

3. **VoIP Dial Plans**
    - Building 1: Extensions starting with `1…`
    - Building 2: Extensions starting with `2…`
    - Building 3: Extensions starting with `3…`
   

4. **DNS Zones**
    - Building 1: `rcomp-24-25-dh-g2`
    - Building 2: `building-2.rcomp-24-25-dh-g2`
    - Building 3: `building-3.rcomp-24-25-dh-g2`

**More Detailed Information**

- [Building 1 Details](1230596/README.md)
- [Building 2 Details](1220848/README.md)
- [Building 3 Details](1230595/README.md)
- [Firewall Details](1220848/README(Firewall).md)
---
