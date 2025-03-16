Building 1
==========

Building 1 will house the **datacenter (Room 1.1.3)** and will also serve as the **main cross-connect** for the structured cabling system.

# **Building Features**

- **Dimensions:** 20 x 20 meters
- **Floors:** 2
  1. **Floor 0:**
     - Underground cable raceway connected to the external technical ditch
     - Ceiling height: 4 meters
     - Shared areas (entrance hall, restrooms, stairs) require no network outlets.
  2. **Floor 1:**
     - Dropped ceiling 2.5 meters from the ground
     - Ceiling height: 3 meters (2.5 effective)
     - No underfloor cable raceways
     - No network outlets required in restrooms or shared areas (corridors, halls)
     - The **datacenter (1.1.3) is out of scope** for this project, so no network outlets are included there.

# **Network Outlets**

The standard ratio of **2 network outlets per 10 square meters** was applied for each room. Outlets are placed **1 meter above floor level** for ease of access.

## **Floor 0**

A single **25m range (radius) access point** is used to cover the entire floor. The AP is connected through a wall in **Room 1.0.3**, extending to the ceiling with a connection to a **double outlet**. It is positioned in the entrance hall, near **Rooms 1.0.3 and 1.0.4**, as these areas have the highest expected user density.

Cables run through the **underground raceway** and rise **1 meter** above floor level to connect to outlets on the walls.

### **Outlets per Room**
| Room  | Width (m) | Length (m) | No. Outlets |
|:-----:|:---------:|:----------:|:----------:|
| 1.0.1 | 3.00      | 4.89       | 4          |
| 1.0.2 | 3.00      | 4.89       | 4          |
| 1.0.3 | 3.00      | 4.89       | 4          |
| 1.0.4 | 3.00      | 4.89       | 4 + CP     |
| 1.0.5 | 5.89      | 7.11       | 10 + HC + IC |
| 1.0.6 | 4.32      | 5.89       | 6 + CP + AP |
| 1.0.7 | 7.14      | 7.11       | 8 (80m copper cable) |

**Total Outlets:** 40 + 1 for access point

## **Floor 1**

A **25m range access point** is positioned near **Rooms 1.1.3 and 1.1.4**, as these areas require the most connectivity. Cabling follows a **raceway above the floor**, descending **1 meter** to the outlets.

### **Outlets per Room**
| Room  | Width (m) | Length (m) | No. Outlets |
|:-----:|:---------:|:----------:|:----------:|
| 1.1.1 | 3.62      | 7.23       | 6          |
| 1.1.2 | 3.62      | 7.23       | 6          |
| 1.1.4 | 4.41      | 7.11       | 6          |
| 1.1.5 | 5.92      | 7.11       | 10  |

**Total Outlets:** 38 + 1 for access point


## Enclosed Rack (Cabinet) for Consolidation Points

total_size: 6U

| Component                                 | Size |
|-------------------------------------------|------|
| Copper Patch Panel (CAT7, 24 ports)       | 1U   |
| Consolidation Point (24 ports)            | 1U   |
| Free Space for Future Expansion           | 2U   |

### Enclosed Rack (Cabinet) - Total 15U

- IC Fiber Patch Panel (Multimode, 12 Ports) - 1U
- IC Cooper Patch Panel (CAT7, 24 ports) - 1U
- IC Switch (24 ports) - 1U
- HC Fiber Patch Panel (Multimode, 12 Ports) - 1U
- HC Cooper Patch Panel (CAT7, 24 ports) - 1U
- HC Switch (24 ports) - 1U
- UPS - 1U
- Free Space for Future expansion - 7U (additional 100% over dimensioning)

Commercially available size above 14U is usually 15U, so we will use one.


## Floor 0

Rack: 20U

| Component                                | Size |
|------------------------------------------|------|
| UPS                                      | 1U   |
| Fiber Patch Panel (Multimode, Backbone)  | 3U   |
| Copper Patch Panel (CAT7, 48 ports)      | 2U   |
| Switch 48 ports (3)                      | 2U   |
| Cable Management                         | 1U   |
| Free Space for Future Expansion          | 9U   |

### Copper Cable CAT7 Calculations

| Room    | Cable Length |
|---------|--------------|
| 1.0.1   | 92.96m       |
| 1.0.2   | 41.08m       |
| 1.0.3   | 28.96m       |
| 1.0.4   | 16.84m       |
| 1.0.5   | 113.3m       |
| 1.0.6   | 84.6m        |
| 1.0.7   | 205.92m      |
| **Total** | **583.66m** |

---

## Floor 1

Rack: 6U

| Component                                 | Size |
|-------------------------------------------|------|
| Copper Patch Panel (CAT7, 48 ports)       | 1U   |
| Fiber Patch Panel (Multimode, Backbone) (2) | 1U   |
| Switch 48 ports                           | 1U   |
| Free Space for Future Expansion           | 3U   |

| Room    | Copper CAT7 Cable Length |
|---------|----------------------------|
| 1.1.1   | 70.32m                       |
| 1.1.2   | 51.6m                        |
| 1.1.4   | 104.82m                      |
| 1.1.5   | 268.8m                       |
| **Total** | **495.54m**                 |

---

## Inventory

## INVENTORY

|                **ITEM**                 | **FLOOR 0** | **FLOOR 1** |  **TOTAL**  |
|:---------------------------------------:|:-----------:|:-----------:|:-----------:|
|           Copper Cable (CAT7)           |   583.66m   |   495.54m   |  1079.20m   |
|     Optical Fiber Cable (Multimode)     |      6      |     1.5     |     7.5     |
|          Network Outlet (RJ45)          |     40      |     38      |     78      |
| Fiber Patch Panel (Multimode, 12 Ports) |      1      |      0      |      1      |
|   Copper Patch Panel (CAT7, 24 Ports)   |      0      |      0      |      0      |
|   Copper Patch Panel (CAT7, 48 Ports)   |      1      |      1      |      2      |
|            Switch (48 Ports)            |      1      |      1      |      2      |
|                   UPS                   |      1      |      0      |      1      |
|        Access Point (25m radius)        |      1      |      1      |      2      |
|     Consolidation Point (24 Ports)      |      2      |      1      |      3      |
|           Enclosed Rack (12U)           |      1      |      0      |      1      |
|            Enclosed Rack (6U)           |      0      |      1      |      1      |
|      Copper CAT7 Patch Cord (0.5m)      | 40 (+1 AP)  | 38 (+1 AP)  | 78 (+2 APs) |
|   Fiber (Multimode) Patch Cord (0.5m)   |      36      |     12      |     48      |
|       Copper CAT7 Patch Cord (5m)       |     40      |     38      |     78      |

_*_ Campus Backbone Optical Fiber Cable (Multimode) not included in this Inventory.

