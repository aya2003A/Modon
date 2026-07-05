# Modon Developments — Project Portfolio Dashboard (Power BI)

An executive Power BI dashboard for tracking construction/development project performance across budget, schedule, and workforce metrics — built for Modon Developments to replace static spreadsheet reporting with a single interactive view.

![Power BI](https://img.shields.io/badge/Power%20BI-F2C811?style=flat&logo=powerbi&logoColor=black)
![DAX](https://img.shields.io/badge/DAX-Data%20Modeling-2185D0?style=flat)

---

## Overview

This dashboard consolidates project, finance, and HR data into one view so leadership can monitor an entire project portfolio at a glance, then drill into any single project's budget, schedule, and team performance without leaving the report.

**Live view includes:**
- Portfolio-wide KPIs (total projects, completion status breakdown, total budget/spend/variance) that stay constant regardless of filters — a fixed "big picture" panel
- Per-project drill-down (select any project from a slicer) showing completion %, schedule status, finance status, and a live cover photo
- Monthly Budget vs. Actual trend chart
- Budget vs. Actual breakdown by department
- Geographic project location map
- People & Culture panel: headcount, average performance score, medical costs, and project manager profile

## Data Model

Built as a star schema in Power BI:

| Table | Role |
|---|---|
| `DimProject` | Project attributes — dates, planned/actual %, SPI, status, location, image |
| `DimEmployee` | Employee attributes — name, role, department, performance rating |
| `FactFinance` | Monthly budget vs. actual spend, by project and department |
| `FactProjectMetrics` | Monthly schedule/completion tracking per project |
| `FactHR` | Monthly HR metrics per employee per project |
| `OverAll` | Pre-aggregated portfolio totals (intentionally left unrelated to slicers, so top-level KPIs always reflect the whole portfolio) |

## Key DAX Measures

```DAX
Overall POC % = SUM(OverAll[POC])
Actual % = AVERAGE(DimProject[Actual %])
Finance Status = IF([Variance (Project)] > 0, "Over Budget", "On Budget")
Spent % = DIVIDE([Total Spent (Project)], [Total Budget (Project)])
Avg Performance % = AVERAGE(FactHR[PerformanceScore])
```

Full measure list is documented in [`/docs/measures.dax`](docs/measures.dax).

## Skills Demonstrated

- Star-schema data modeling and relationship design in Power BI
- DAX measure authoring (aggregations, `SELECTEDVALUE`, conditional logic, ratio calculations)
- Custom theming and dashboard UX design (color system, iconography, card-based layout)
- Handling and documenting real-world data quality issues (inconsistent naming, duplicate records, mismatched values across source tables) prior to modeling
- Geographic visualization and dynamic image binding via URL data categories

## Files in This Repo

```
├── Modon_Dashboard.pbix        # Power BI report file
├── data/                       # Source Excel workbook
├── docs/measures.dax           # Full DAX measure reference
└── screenshots/                # Dashboard preview images
```


**Author:** Aya Mahmoud Abdullah · [LinkedIn]
