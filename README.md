# ✈️ Airplane Crashes & Fatalities Dashboard (1908–2009)

> **"73% of people on a crashed plane never made it out."**  
> This project analyzes over 100 years of airplane crash data to uncover patterns in aviation fatalities, operator performance, aircraft safety, and crash timing.

---

## 📌 Table of Contents
- [Project Overview](#project-overview)
- [Dataset](#dataset)
- [Tools Used](#tools-used)
- [Data Preparation](#data-preparation)
- [KPI Measures](#kpi-measures)
- [Dashboard Pages](#dashboard-pages)
- [Key Insights](#key-insights)
- [Visuals](#visuals)
- [How to Use](#how-to-use)
- [Connect With Me](#connect-with-me)

---

## 📖 Project Overview

This project is a full end-to-end Power BI dashboard analyzing **5,216 recorded airplane crashes** spanning over a century of aviation history. The goal was to go beyond surface-level crash counts and dig into fatality patterns, operator accountability, aircraft type risk, and time-of-day crash behavior.

The dashboard is structured across **3 pages**:
- **Dashboard** — High-level KPIs and trend overview
- **Overview** — Crash distribution by time, aircraft type, and fatality type
- **Detail** — Geographic breakdown, yearly peaks, and per-crash averages

---

## 📂 Dataset

| Field | Description |
|---|---|
| Date | Date of the crash |
| Time | Time of crash |
| Location | City and country of crash |
| Operator | Airline or military operator |
| Flight Number | Flight identifier |
| Route | Origin to destination |
| Type | Aircraft model/type |
| Aboard | Total people on the plane |
| Fatalities | Number of deaths on the plane |
| Ground | Number of ground deaths |
| Summary | Brief description of crash cause |

- **Total Records:** 5,216 crashes
- **Time Period:** 1908 – 2009
- **Source:** Kaggle — Airplane Crashes and Fatalities Dataset

---

## 🛠️ Tools Used

- **Power BI Desktop** — Dashboard building and DAX measures
- **Power Query** — Data transformation and country extraction
- **DAX** — All KPI measures and calculated columns
- **GitHub** — Portfolio documentation

---

## 🔧 Data Preparation

### Steps taken:
1. **Loaded raw CSV** into Power BI via Get Data
2. **Created a Calendar table** with Year, Month, Quarter, Weekday, and Weekday/Weekend columns
3. **Built a Time Category column** using DAX SWITCH logic:
```DAX
Time Category = 
SWITCH(TRUE(),
    Airplane_Crashes_and_Fatalities[Time] >= TIME(18,0,0) && 
    Airplane_Crashes_and_Fatalities[Time] < TIME(12,0,0), "Night",
    Airplane_Crashes_and_Fatalities[Time] >= TIME(18,0,0), "Night",
    Airplane_Crashes_and_Fatalities[Time] < TIME(5,0,0), "Midnight",
    "Afternoon"
)
```
4. **Extracted Country** from Location column using Power Query

5. **Linked extracted location data** back to main table via primary key relationship

---

## 📊 KPI Measures

All measures were built inside a dedicated **KPIs measures** table to keep the data model clean.

| Measure | DAX Formula |
|---|---|
| Total Recorded Crashes | `COUNTA(Airplane_Crashes_and_Fatalities[index])` |
| Total Air Fatalities | `SUM(Airplane_Crashes_and_Fatalities[Fatalities])` |
| Total Ground Fatalities | `SUM(Airplane_Crashes_and_Fatalities[Ground])` |
| Total Passengers Aboard | `SUM(Airplane_Crashes_and_Fatalities[Aboard])` |
| Crashes With Ground Deaths | `CALCULATE([Total Recorded Crashes], Airplane_Crashes_and_Fatalities[Ground] > 0)` |
| Passenger Survival Rate | `DIVIDE([Total Passengers Aboard] - [Total Air Fatalities], [Total Passengers Aboard])` |
| Passenger Fatality Rate | `1 - [Passenger Survival Rate]` |
| Avg Fatalities Per Crash | `DIVIDE([Total Air Fatalities], [Total Recorded Crashes])` |
| Avg Passengers Per Crash | `DIVIDE([Total Passengers Aboard], [Total Recorded Crashes])` |

---

## 📋 Dashboard Pages

### Page 1 — Dashboard
> High-level summary for quick decision-making

- 5 KPI cards: Recorded Crashes, Survival Rate, Fatality Rate, Ground Fatalities, Air Fatalities
- **Survival Rate vs Fatality Rate** — Donut chart (27% vs 73%)
- **Top 10 Deadliest Operators** — Horizontal bar chart
- **Crashes Over Time** — Monthly line chart
- **Fatalities Over Time** — Monthly line chart

---

### Page 2 — Overview
> Pattern and distribution analysis

- **Crashes by Time Category** — Pie chart (Morning, Afternoon, Night, Midnight)
- **Air Crashes vs Ground Fatality Crashes** — Donut chart (95.8% vs 4.2%)
- **Top 10 Deadliest Aircraft Type** — Lollipop chart

---

### Page 3 — Detail
> Granular breakdown and geographic view

- **Top 10 Crash Years** — Lollipop chart
- **Avg Fatalities vs Avg Passengers Per Crash** — Clustered bar (20 vs 28)
- **Crashes by Location** — Filled map visual

---

## 💡 Key Insights

### 🔴 Fatality & Survival
- Out of every **10 people** on a crashed plane, **7 died and only 3 survived**
- **27% survival rate** across 100+ years of aviation history
- Average crash had **28 people aboard** with **20 fatalities**

### 🛩️ Operator Accountability
- **Aeroflot** is the deadliest operator with **7,200 fatalities** — more than double the next highest
- **Military - U.S. Air Force** comes second with **3,700 fatalities**
- **Air France, American Airlines, and Pan American World Airways** round out the top 5

### ✈️ Aircraft Type
- **Douglas DC-3** is the deadliest aircraft type with **331 crashes** — nearly 4x the next aircraft
- 7 of the top 10 deadliest aircraft are Douglas variants, suggesting era-specific risk concentration

### 🕐 Time of Day
- **Morning (31.2%) and Afternoon (31.0%)** together account for **62% of all crashes**
- Night crashes (26.2%) and Midnight (11.6%) are lower but still significant

### 🌍 Ground Impact
- **219 out of 5,216 crashes** also killed people on the ground
- **8,440 ground fatalities** — deaths of people who never boarded a plane
- This represents roughly **1 in 24 crashes** having ground casualties

---

## 📸 Visuals

![Dashboard](screenshot%201.png)
![Overview](screenshot%202.png)
![Detail](screenshot%203.png)
