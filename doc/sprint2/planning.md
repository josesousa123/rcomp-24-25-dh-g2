RCOMP 2024-2025 Project - Sprint 2 planning
===========================================
### Sprint master: 1230596 ###

---

# 1. Sprint's backlog #

| Task  | Task description                                                                                                                                                                                       | Assignment |
|:-----:|:-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:----------:|
| T.2.1 | Development of a layer two and layer three Packet Tracer simulation for building 1, encompassing the campus backbone. Integration of every member’s Packet Tracer simulation into a single simulation. |  1230596   |
| T.2.2 | Development of a layer two and layer three Packet Tracer simulation for building 2, encompassing the campus backbone.                                                                                  |  1220848   |
| T.2.3 | Development of a layer two and layer three Packet Tracer simulation for building 3, encompassing the campus backbone.                                                                                  |  1230595   |

---

# 2. Technical decisions and coordination #

**Sprint 1 changes:**

- Changed the location Cabinet from Building 1 from Floor 0 to Floor 1
- Removed unnecessary patch panels from building racks
- Downsized the amount of Consolidation Points

**Sprint 2 decisions:**

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

---
## BUILDING 1 NETWORK: `10.24.32.0/22`

| VLAN ID | VLAN Name |     Network      |   Host Min   |   Host Max    |  Broadcast   |
|:-------:|:---------:|:----------------:|:------------:|:-------------:|:------------:|
|   391   |   B1-F0   | 10.24.33.192 /26 | 10.24.33.193 | 10.24.33.254  | 10.24.33.255 |
|   392   |   B1-F1   | 10.24.33.128 /26 | 10.24.33.129 | 10.24.33.190  | 10.24.33.191 |
|   393   |  B1-WIFI  | 10.24.32.128 /25 | 10.24.32.129 | 10.24.32.254  | 10.24.32.255 |
|   394   |  B1-DMZ   |  10.24.32.0 /25  |  10.24.32.1  | 10.24.32.126  | 10.24.32.127 |
|   395   |  B1-VoIP  |  10.24.33.0 /25  |  10.24.33.1  | 10.24.33.126  | 10.24.33.127 |

## **BUILDING 2 NETWORK:** `10.24.36.0/22`

| VLAN ID | VLAN Name |     Network      |   Host Min   |   Host Max    |  Broadcast   |
|:-------:|:---------:|:----------------:|:------------:|:-------------:|:------------:|
|   396   |   B2-F0   |  10.24.38.0 /25  |  10.24.38.1  | 10.24.38.126  | 10.24.38.127 |
|   397   |   B2-F1   | 10.24.37.128 /25 | 10.24.37.129 | 10.24.37.254  | 10.24.37.255 |
|   398   |  B2-WIFI  |  10.24.36.0 /24  |  10.24.36.1  | 10.24.36.254  | 10.24.36.255 |
|   399   |  B2-DMZ   | 10.24.38.128 /26 | 10.24.38.129 | 10.24.38.190  | 10.24.38.191 |
|   400   |  B2-VoIP  |  10.24.37.0 /25  |  10.24.37.1  | 10.24.37.126  | 10.24.37.127 |

## BUILDING 3 NETWORK: `10.24.40.0/22`

| VLAN ID | VLAN Name |     Network      |   Host Min   |   Host Max    |  Broadcast   |
|:-------:|:---------:|:----------------:|:------------:|:-------------:|:------------:|
|   401   |   B3-F0   |  10.24.43.0 /25  |  10.24.43.1  | 10.24.43.126  | 10.24.43.127 |
|   402   |   B3-F1   |  10.24.42.0 /24  |  10.24.42.1  | 10.24.42.254  | 10.24.42.255 |
|   403   |  B3-WIFI  |  10.24.40.0 /24  |  10.24.40.1  | 10.24.40.254  | 10.24.40.255 |
|   404   |  B3-DMZ   | 10.24.43.128 /26 | 10.24.43.129 | 10.24.43.190  | 10.24.43.191 |
|   405   |  B3-VoIP  |  10.24.41.0 /24  |  10.24.41.1  | 10.24.41.254  | 10.24.41.255 |

## BACKBONE NETWORK: `10.24.44.0/22`

| VLAN ID |    VLAN Name     |    Network     |  Host Min  |   Host Max   |  Broadcast   |
|:-------:|:----------------:|:--------------:|:----------:|:------------:|:------------:|
|   390   | CAMPUS-BACKBONE  | 10.24.44.0 /24 | 10.24.44.1 | 10.24.44.254 | 10.24.44.255 |


**Backbone nodes:**

- **RT-BK** -> `10.24.44.1`
- **RT-B1** -> `10.24.44.2`
- **RT-B2** -> `10.24.44.3`
- **RT-B3** -> `10.24.44.4`

---
