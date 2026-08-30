# 🚀 Space Missions Dashboard — Visual Build Guide

> **Why not auto-generate the visual JSON?** Power BI's PBIR `visual.json` format contains deeply nested internal schema references (query bindings, projection maps, visual-specific `vcObjects`, theme overrides) that are **not fully publicly documented**. Even Microsoft states: *"Direct manual editing is risky and can corrupt the report."* Building visuals in Power BI Desktop using drag-and-drop with our pre-built measures is the reliable path.

---

## 🎨 Theme Setup (Do This First)

1. **View → Themes → Customize current theme**
2. Set these colors:
   - **Background**: `#0B111E` (Deep Space Navy)
   - **Foreground/Text**: `#E2E8F0` (Silver)  
   - **Accent 1**: `#00F2FE` (Neon Cyan)
   - **Accent 2**: `#FFB800` (Cyber Amber)
   - **Accent 3**: `#FF4B4B` (Rocket Coral)
   - **Accent 4**: `#10B981` (Success Green)
   - **Accent 5**: `#8B5CF6` (Nebula Purple)
   - **Accent 6**: `#F97316` (Warning Orange)
3. **Font**: Segoe UI or DIN (if available)
4. **Apply and Save** as "Space Dark Theme"

---

## 📄 PAGE 1: "Mission Control Overview" (1920×1080)

> Rename `Page 1` → `Mission Control`

### Row 1 — KPI Cards (y: 20, height: 100)

| # | Visual Type | Measure | Position (x, width) | Format |
|---|------------|---------|---------------------|--------|
| 1 | **Card** | `Total Launches` | x:20, w:220 | Title: "TOTAL LAUNCHES", Font 28pt bold, Accent 1 (#00F2FE) |
| 2 | **Card** | `Success Rate %` | x:260, w:220 | Title: "SUCCESS RATE", Font 28pt, Accent 4 (#10B981) |
| 3 | **Card** | `Unique Countries` | x:500, w:220 | Title: "COUNTRIES", Font 28pt, Accent 5 (#8B5CF6) |
| 4 | **Card** | `Unique Rockets` | x:740, w:220 | Title: "ROCKETS USED", Font 28pt, Accent 2 (#FFB800) |
| 5 | **Card** | `Total Spend ($M)` | x:980, w:220 | Title: "TOTAL SPEND", Font 28pt, display as "$162.3B" |
| 6 | **Card** | `Active Rockets` | x:1220, w:220 | Title: "ACTIVE ROCKETS", Font 28pt, Accent 1 |

> [!TIP]
> Add a subtle rounded rectangle shape behind each card with 5% opacity fill for glassmorphism effect.

---

### Row 2 — Launch Trend + Success Rate (y: 140, height: 340)

| # | Visual Type | Fields | Position | Notes |
|---|------------|--------|----------|-------|
| 7 | **Line & Clustered Column Chart** | **Column Y-axis**: `Total Launches`, **Line Y-axis**: `Success Rate %`, **X-axis**: `Date Table[Year]` | x:20, w:940, h:340 | Title: "Launch Cadence & Reliability Trend (1957–2022)". Add a constant line at 90% on secondary axis. |
| 8 | **Ribbon Chart** | **Y-axis**: `Total Launches`, **X-axis**: `Date Table[Decade]`, **Legend**: `Space Mission[HistoricalSovereign]` | x:980, w:920, h:340 | Title: "Global Space Dominance Shifts by Decade". Shows rank changes between USSR→USA→China. Filter to Top 6 countries by launches. |

---

### Row 3 — Country & Company Breakdown (y: 500, height: 280)

| # | Visual Type | Fields | Position | Notes |
|---|------------|--------|----------|-------|
| 9 | **Bar Chart (Horizontal)** | **Y-axis**: `Space Mission[HistoricalSovereign]`, **X-axis**: `Total Launches`, **Tooltips**: `Success Rate %` | x:20, w:460, h:280 | Title: "Top Countries by Launches". Add **data bars** conditional formatting. Top N filter = 10. Sort descending by Total Launches. |
| 10 | **Treemap** | **Category**: `Space Mission[Company]`, **Values**: `Total Launches`, **Tooltips**: `Success Rate %` | x:500, w:460, h:280 | Title: "Companies by Launch Volume". Top N = 12. Color by Success Rate % (conditional formatting green→red). |
| 11 | **Donut Chart** | **Legend**: `Space Mission[CompanySector]`, **Values**: `Total Launches` | x:980, w:440, h:280 | Title: "Government vs Commercial vs Military". Use Accent colors for each segment. |

---

### Row 4 — Mission Status & Era (y: 800, height: 250)

| # | Visual Type | Fields | Position | Notes |
|---|------------|--------|----------|-------|
| 12 | **Stacked Bar Chart** | **Y-axis**: `Space Mission[Decade]`, **X-axis**: `Total Launches`, **Legend**: `Space Mission[MissionStatus]` | x:20, w:620, h:250 | Title: "Mission Outcomes by Decade". Colors: Success=#10B981, Failure=#FF4B4B, Partial=#F97316, Prelaunch=#EF4444 |
| 13 | **Slicer** | `Space Mission[SpaceEra]` | x:660, w:300, h:250 | Style: **Tile/Button**, Multi-select, Title: "FILTER BY ERA" |
| 14 | **Matrix** | **Rows**: `Date Table[Decade]`, **Columns**: `Space Mission[HistoricalSovereign]`, **Values**: `Success Rate %` | x:980, w:920, h:250 | Title: "Success Rate Heatmap". Apply conditional formatting background color (red→yellow→green) on Success Rate %. |

---

## 📄 PAGE 2: "Rocket Arsenal" (1920×1080)

> Insert → New Page → Rename to `Rocket Arsenal`

### Row 1 — Rocket KPI Cards (y: 20, height: 100)

| # | Measure | Notes |
|---|---------|-------|
| 1 | `Top Rocket by Launches` | Card, title "ALL-TIME #1 ROCKET" |
| 2 | `Top Rocket Launch Count` | Card, title "ITS LAUNCH COUNT" |
| 3 | `Active Share %` | Card, title "ACTIVE FLEET %" |
| 4 | `Rocket Families Count` | Card, title "ROCKET FAMILIES" |

### Row 2 — Rocket Leaderboard (y: 140, height: 380)

| # | Visual Type | Fields | Position | Notes |
|---|------------|--------|----------|-------|
| 5 | **Table** | **Columns**: `Space Mission[Rocket]`, `Total Launches`, `Success Rate %`, `Space Mission[RocketStatus]`, `Space Mission[RocketFamily]` | x:20, w:940, h:380 | Title: "Rocket Leaderboard". Sort by Total Launches desc. Add **Rocket Rank** as first column. Conditional format Success Rate % (data bars green). Top N = 20. Icon set on RocketStatus (✅ Active / ⛔ Retired). |
| 6 | **Clustered Bar Chart** | **Y-axis**: `Space Mission[RocketFamily]`, **X-axis**: `Total Launches`, **Legend**: `Space Mission[RocketStatus]` | x:980, w:920, h:380 | Title: "Launch Volume by Rocket Family". Sort desc. Stacked by Active (Cyan) vs Retired (Grey). |

### Row 3 — Rocket Deep Dive (y: 540, height: 280)

| # | Visual Type | Fields | Position | Notes |
|---|------------|--------|----------|-------|
| 7 | **Line Chart** | **X-axis**: `Date Table[Year]`, **Values**: `Active Share %` | x:20, w:620, h:280 | Title: "Active vs Retired Fleet % Over Time". Shows the shift toward newer rockets. |
| 8 | **Scatter Chart** | **X-axis**: `Total Launches`, **Y-axis**: `Success Rate %`, **Size**: `Avg Cost per Launch ($M)`, **Details**: `Space Mission[Rocket]` | x:660, w:620, h:280 | Title: "Launch Volume vs Reliability vs Cost". Play axis: `Date Table[Year]`. Top N filter by Total Launches >= 10. |
| 9 | **Slicer** | `Space Mission[RocketFamily]` | x:1300, w:600, h:280 | Style: Tile/Button, multi-select |

---

## 📄 PAGE 3: "Launchpad Geography" (1920×1080)

> Insert → New Page → Rename to `Launchpad Geography`

### Row 1 — Geographic KPIs (y: 20, height: 100)

| # | Measure | Notes |
|---|---------|-------|
| 1 | `Unique Launch Sites` | Card |
| 2 | `Unique Countries` | Card |
| 3 | `Top Country by Launches` | Card |

### Row 2 — Map + Site Breakdown (y: 140, height: 420)

| # | Visual Type | Fields | Position | Notes |
|---|------------|--------|----------|-------|
| 4 | **Filled Map** or **Azure Map** | **Location**: `Space Mission[Country]`, **Size**: `Total Launches`, **Tooltips**: `Success Rate %`, `Total Spend ($M)` | x:20, w:940, h:420 | Title: "Global Launch Distribution". Bubble size = launches, color saturation = success rate. |
| 5 | **Bar Chart** | **Y-axis**: `Space Mission[LaunchSite]`, **X-axis**: `Total Launches`, **Tooltips**: `Success Rate %`, `Space Mission[Country]` | x:980, w:920, h:420 | Title: "Top Spaceports Worldwide". Top N = 12. Sort desc. Data labels ON. |

### Row 3 — Launch Timing & Patterns (y: 580, height: 280)

| # | Visual Type | Fields | Position | Notes |
|---|------------|--------|----------|-------|
| 6 | **Heatmap (Matrix)** | **Rows**: `Space Mission[TimeOfDay]`, **Columns**: `Date Table[DayName]`, **Values**: `Total Launches` | x:20, w:620, h:280 | Title: "When Do Rockets Launch? (Day × Time)". Conditional format with background color gradient. |
| 7 | **Column Chart** | **X-axis**: `Date Table[MonthShort]`, **Y-axis**: `Total Launches` | x:660, w:620, h:280 | Title: "Seasonality of Launches". Sort by MonthNumber. |
| 8 | **Slicer** | `Space Mission[Country]` | x:1300, w:600, h:280 | Dropdown style, multi-select |

---

## 🏁 Final Polish Checklist

- [ ] **Page Navigator**: Insert → Buttons → Navigator → Page Navigator (for tab-style navigation across pages)
- [ ] **Report Title**: Add a text box at top of each page: `🚀 SPACE MISSIONS 1957–2022` in 18pt bold, Accent 1 color
- [ ] **Subtitle**: Use the `KPI Subtitle` measure in a card below the title
- [ ] **Interactions**: Edit Interactions → ensure slicers filter all visuals on their page
- [ ] **Tooltips**: Enable enhanced tooltips in Format → Tooltip for all chart visuals
- [ ] **Mobile Layout**: View → Mobile Layout → rearrange key KPIs and charts for mobile
- [ ] **Bookmarks**: Create bookmarks for each "Era" preset (Space Race, Cold War, New Space)
