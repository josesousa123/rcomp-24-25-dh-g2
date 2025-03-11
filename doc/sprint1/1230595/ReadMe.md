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
| 1.1.3 | Datacenter (Excluded) | |
| 1.1.4 | 4.41      | 7.11       | 6          |
| 1.1.5 | 5.92      | 7.11       | 10 (78.37m copper cable) |

**Total Outlets:** 38 + 1 for access point

# **Cross-Connects**

## **Floor 0**
Room **1.0.5** was chosen for the **Intermediate Cross-Connect (IC)** as it is directly below the datacenter (**Room 1.1.3**).

A **19" rack format** is used, housing:
- **Two 48-port patch panels**
- **One 24-port patch panel**
- **Two 48-port switches**
- **One 24-port switch**

A **24U cabinet** is used, leaving 50% space for future expansion.

## **Floor 1**
Room **1.1.3** (Datacenter) will house the **Main Cross-Connect (MC)**, linking the entire building to the **campus backbone**.

A **redundant setup** includes **four copper cables** connecting the **MC to the IC on Floor 0**, ensuring fail-safe mechanisms.
Additionally, an **8-core fiber cable** extends from the **MC to the technical ditch**, connecting to other buildings.

### **Total Cost for Building 1: 11840.52€**
