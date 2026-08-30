# 🚀 65 Years of Space Missions (1957–2022) | Power BI Analytics Report

[![Power BI](https://img.shields.io/badge/Power_BI-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)](https://powerbi.microsoft.com/)
[![DAX](https://img.shields.io/badge/DAX-Measures_37+-blue?style=for-the-badge)](https://learn.microsoft.com/dax/)
[![TMDL](https://img.shields.io/badge/TMDL-Semantic_Model-purple?style=for-the-badge)](https://learn.microsoft.com/power-bi/developer/projects/projects-dataset)
[![Maven Analytics](https://img.shields.io/badge/Maven_Challenge-Space_Missions-orange?style=for-the-badge)](https://mavenanalytics.io/challenges)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg?style=for-the-badge)](LICENSE)

> An enterprise-grade, developer-mode Power BI project analyzing **4,630 space missions** from the dawn of spaceflight (Sputnik 1 in 1957) to August 2022. Built for the **Maven Space Challenge**.

---

## 🌌 Project Overview & Key Highlights

This Business Intelligence report explores the global evolution of space exploration across 65 years, tracking launch volumes, mission reliability, global geopolitical leadership shifts, rocket family lifecycles, launchpad physics, and commercial space economics.

```
========================================================================================================================
                                     HISTORICAL SPACE FLIGHT AT A GLANCE (1957 – 2022)
========================================================================================================================
Total Missions: 4,630     | Overall Success Rate: 89.89% (4,162 Successes) | Active Rockets Today: 21.8% (1,010 Missions)
Total Known Cost: $162.3B | Peak Volume Decade: 1970s (1,012 Launches)     | Fastest Growing: 2020s (150+ launches/year pace)
========================================================================================================================
```

---

## 🎯 Recommended Analysis & Core Insights

### 1. Launch Volume Trends & Success Rate Evolution
* **1950s (Trial & Error Era):** 51 launches total, 31.37% success rate. The space age began with heavy experimentation and high failure rates.
* **1960s–1970s (Cold War Space Race Peak):** Cadence surged to an all-time 20th-century high of **1,012 launches in the 1970s**, with reliability maturing rapidly to **92.69%**.
* **1980s–2000s (Post-Cold War Contraction):** Cadence dropped to a low of 475 launches in the 2000s following the Soviet collapse.
* **2010s–2020s (New Space Renaissance):** Driven by commercial mega-constellations (SpaceX Starlink) and China's program expansion, launch cadence reached ~150 launches/year in 2020–2022 with sustained **~92%–94% reliability**.

### 2. Global Space Hegemony & Leadership Shifts
* **1957–1990 (Soviet Era):** USSR led global spaceflight volume by a wide margin (1,770 total missions, 1,608 successes). In the 1970s, USSR launched **815 missions** vs. USA's **143**.
* **1991–2009 (American & European Commercial Dominance):** USA took the #1 spot, while Arianespace (Europe/France) led commercial geostationary satellite launches.
* **2010s–2020s (US Commercial vs. China Duopoly):** The USA (144 launches) and China (121 launches) represent **72% of all launches in the 2020s**.

### 3. All-Time Most Used vs. Active Workhorses
* **All-Time Most Used:** **Cosmos-3M (11K65M)** with **446 launches** (93.95% success rate, 1967–2010) — *Retired*.
* **Most Used Active Rocket:** **Falcon 9 Block 5 (SpaceX)** with **111 launches** and a **100.0% mission success rate** up to August 2022 — the most reliable high-cadence booster in aerospace history.

### 4. Launchpad Physics & Geographic Orbit Corridors
* **Equatorial Sites (e.g. Guiana Space Centre at 5.2°N):** Leverages Earth's ~1,670 km/h rotational boost for efficient Geostationary Transfer Orbits (GTO).
* **High-Latitude Polar Sites (e.g. Plesetsk Cosmodrome at 62.9°N, 1,278 launches):** Optimized for polar, sun-synchronous, and high-inclination Molniya military orbits.
* **Coastal Drop Corridors (Cape Canaveral Eastward / Vandenberg Southward):** Ensures discarded stages fall safely over open oceans.

---

## 🏗️ Architecture & Star Schema Data Model

The data model follows an optimized **Star Schema** architecture designed for maximum DAX performance:

```
┌──────────────────────────────────────────────────────────┐
│                       Date Table                         │
│ (Date, Year, Decade, SpaceEra, Quarter, Month, Day, ...) │
└────────────────────────────┬─────────────────────────────┘
                             │ 1
                             │
                             │ *
┌────────────────────────────┴─────────────────────────────┐
│                      Space Mission                       │
│  (Company, Rocket, Location, Date, Time, RocketStatus,   │
│   MissionStatus, Country, LaunchSite, LaunchPad,         │
│   RocketFamily, CompanySector, IsSuccess, Price_M_USD)   │
└──────────────────────────────────────────────────────────┘
                             │
                             ▼
┌──────────────────────────────────────────────────────────┐
│                       01 Measures                        │
│ (37 Structured DAX Measures organized in Display Folders)│
└──────────────────────────────────────────────────────────┘
```

---

## 📊 DAX Measures Catalog (37 Measures)

Measures are organized into 7 structured **Display Folders**:

| Display Folder | Key Measures Included |
|---|---|
| **Core KPIs** | `Total Launches`, `Successful Missions`, `Failed Missions`, `Success Rate %`, `Failure Rate %`, `Unique Rockets`, `Unique Companies`, `Unique Countries`, `Active Rockets`, `Retired Rockets` |
| **Mission Status** | `Partial Failures`, `Prelaunch Failures`, `Full Failures` |
| **Financial** | `Total Spend ($M)`, `Avg Cost per Launch ($M)`, `Max Mission Cost ($M)`, `Min Mission Cost ($M)`, `Missions with Price Data`, `Price Coverage %`, `Cost of Failures ($M)` |
| **Time Intelligence** | `Launches PY`, `YoY Launch Growth`, `Success Rate PY`, `YoY Success Rate Change`, `Running Total Launches`, `Running Total Successes`, `Cumulative Success Rate %`, `Launches per Year (Avg)`, `Best Year by Launches` |
| **Rocket Analytics** | `Top Rocket by Launches`, `Top Rocket Launch Count`, `Active Rocket Launches`, `Retired Rocket Launches`, `Active Share %`, `Rocket Families Count` |
| **Geographic & Sector** | `Top Country by Launches`, `Government Launches`, `Commercial Launches`, `Military Launches`, `Commercial Share %`, `Unique Launch Sites` |
| **Formatting & Helpers**| `Country Rank`, `Rocket Rank`, `Success Rate Color`, `KPI Subtitle` |

---

## 🎨 Theme & UI/UX Design

* **Theme:** Custom Deep Space Dark Theme (`#0B111E` background) with high-contrast neon accents:
  * 🔹 **Neon Cyan (`#00F2FE`):** Primary KPIs & Active Fleet
  * 🔸 **Cyber Amber (`#FFB800`):** Rockets & Costs
  * 🔺 **Rocket Coral (`#FF4B4B`):** Failures & Anomalies
  * ❇️ **Emerald Green (`#10B981`):** Success Metrics (≥95%)
  * 🟣 **Nebula Purple (`#8B5CF6`):** Geographic & Era Slicers

---

## 📁 Repository Structure

```
├── space_missions.pbip            # Power BI Project Entry Point
├── space_missions.csv             # Source dataset (4,630 records)
├── space_missions_data_dictionary.csv # Data dictionary
├── README.md                      # Project documentation & insights
├── .gitignore                     # Power BI developer mode exclusions
├── space_missions.Report/         # Power BI Report Definition (PBIR)
│   ├── definition/
│   │   ├── pages/                 # Report Pages & Visual Containers
│   │   ├── report.json            # Report Configuration
│   │   └── version.json           # Version metadata
│   └── StaticResources/
│       └── SharedResources/
│           └── RegisteredResources/
│               └── SpaceDarkTheme.json  # Custom Space Dark Theme
└── space_missions.SemanticModel/  # Tabular Model Definition (TMDL)
    └── definition/
        ├── model.tmdl             # Model & table references
        ├── relationships.tmdl     # Model relationships
        └── tables/
            ├── Space Mission.tmdl # Fact Table & M-Query
            ├── Date Table.tmdl    # Dim_Date Calendar Table
            └── 01 Measures.tmdl   # 37 DAX Measures in Folders
```

---

## 🚀 How to Run Locally

1. **Clone the repository:**
   ```bash
   git clone https://github.com/YOUR_USERNAME/space-missions-powerbi-analytics.git
   ```
2. **Open in Power BI Desktop:**
   * Double-click `space_missions.pbip` (requires Power BI Desktop with PBIP / Developer Mode enabled).
3. **Data Refresh:**
   * If paths differ, update the source file path in Power Query (`Transform Data` > `Data source settings`).

---

## 📜 Credits & Acknowledgments
* **Dataset:** Maven Analytics Space Challenge
* **Author:** Power BI & BI Engineering Portfolio
* **Tools:** Power BI Desktop, TMDL, DAX, Power Query (M Language), Tabular Editor
