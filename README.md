# 🏥 National Health Analysis Dashboard | Power BI

> A 3-page Power BI report analysing national-level patient healthcare data — covering patient demographics, key health trends, and treatment costs with YoY KPIs, custom visuals, and a multi-table DAX data model.

---

## 🛠️ Tools & Technologies

![Power BI](https://img.shields.io/badge/Power_BI-F2C811?style=flat&logo=powerbi&logoColor=black)
![DAX](https://img.shields.io/badge/DAX-0078D4?style=flat)
![Power Query](https://img.shields.io/badge/Power_Query-217346?style=flat)
![ZoomCharts](https://img.shields.io/badge/ZoomCharts_Custom_Visuals-FF6B35?style=flat)

---

## 🎯 Objective

To build a healthcare analytics report that enables hospital administrators and health analysts to:
- Understand **patient demographics** — age groups, gender, blood type distribution
- Track **key operational KPIs** — admitted patients, rooms occupied, doctors, average length of stay (LOS), and billing — with **Year-over-Year growth rates**
- Analyse **test result patterns** — Normal, Abnormal, and Inconclusive rates by medical condition
- Explore **treatment and cost breakdown** by medical condition, insurance provider, and medication
- Identify trends across **weekday vs. weekend admissions** and **monthly patterns**

---

## 🗂️ Data Model

The report is built on a **multi-table model** with the following tables:

| Table | Role | Description |
|-------|------|-------------|
| `HealthData` | Fact Table | Core patient records — admissions, gender, blood type, LOS, billing, test results |
| `DimCondition` | Dimension | Medical condition master with descriptions and URLs |
| `Billing` | Dimension / Measure support | Billing fields and breakdowns |
| `Calendar` | Date Table | Full calendar table for time intelligence |
| `DAX` | Measures Table | All calculated DAX measures centralised here |
| `KPI` | KPI Config Table | Dynamic KPI selector fields for the KPI visual |

---

## 📁 Fields & Columns

### `HealthData` (Fact Table)
| Column | Description |
|--------|-------------|
| `Admitted Patients` | Count of admitted patients |
| `Admission Type` | Emergency / Elective / Urgent |
| `Blood Type` | Patient blood group (A+, B+, O+, etc.) |
| `Gender` | Male / Female |
| `Age Group` | Age bracket of patient |
| `Average Age` | Mean patient age |
| `Insurance Provider` | Medicare, Aetna, Cigna, Blue Cross, United Health, etc. |
| `Medical Condition` | Cancer, Diabetes, Arthritis, Hypertension, Asthma, Obesity, etc. |
| `Medication` | Aspirin, Ibuprofen, Paracetamol, Penicillin, Lipitor, etc. |
| `Rooms` | Number of rooms occupied |
| `Doctors` | Number of doctors involved |
| `Avg LOS` | Average Length of Stay (days) |
| `LOS Bucket` | LOS categorised into buckets |
| `Day Type` | Weekday vs. Weekend admission |
| `Normal Results` | Count of normal test results |
| `Abnormal Results` | Count of abnormal test results |
| `Inconclusive Results` | Count of inconclusive test results |

---

## 📊 Dashboard Pages

### Page 1 — 🧑‍🤝‍🧑 Patient Demographics
Understand *who* the patients are:
- **KPI Cards:** Total Admitted Patients, Average Age, Gender split
- **Age Group Distribution** — Clustered column chart
- **Gender Breakdown** — Donut chart
- **Blood Type Distribution** — Donut chart
- **Admission Type breakdown** — Column chart (Emergency / Elective / Urgent)
- **Slicers:** Year, Month, Gender, Age Group, Blood Type, Medical Condition

### Page 2 — 📈 Key Trends
Understand *how* the health system is performing over time:
- **5 Dynamic KPI Cards with YoY Growth:**
  - Admitted Patients (`Adm YoY`)
  - Rooms Occupied (`Room YoY`)
  - Doctors (`Doc YoY`)
  - Avg. Length of Stay (`LOS YoY`)
  - Billing Amount (`Bill YoY` / `Age YoY`)
- **Monthly trend line chart** — tracks admissions and billing over time
- **Day Type Analysis** — Weekday vs. Weekend admission patterns
- **Pivot Table** — Multi-dimension cross-tab analysis
- **ZoomCharts custom visuals** — interactive drill-down combo bar and facet charts

### Page 3 — 💊 Treatment & Cost
Understand *what* treatments cost and how results vary:
- **Total Billing & Avg Billing Amount** KPI cards
- **Billing by Medical Condition** — Column chart
- **Billing by Insurance Provider** — Column chart
- **Test Result breakdown** — Normal %, Abnormal %, Inconclusive % by condition
- **Medication usage** — which drugs are prescribed most per condition
- **Billing Fields slicer** for dynamic cost view switching

---

## 🔢 Key DAX Measures

```dax
-- Admissions & Operations
Admitted Patients  = COUNTROWS(HealthData)
Avg LOS            = AVERAGE(HealthData[Length of Stay])
Rooms              = DISTINCTCOUNT(HealthData[Room Number])
Doctors            = DISTINCTCOUNT(HealthData[Doctor])

-- YoY Growth (using Calendar table)
Adm YoY   = DIVIDE([Admitted Patients] - [Admitted Patients LY], [Admitted Patients LY], 0)
Room YoY  = DIVIDE([Rooms] - [Rooms LY], [Rooms LY], 0)
LOS YoY   = DIVIDE([Avg LOS] - [Avg LOS LY], [Avg LOS LY], 0)
Bill YoY  = DIVIDE([Total Billing] - [Total Billing LY], [Total Billing LY], 0)
Doc YoY   = DIVIDE([Doctors] - [Doctors LY], [Doctors LY], 0)

-- Test Results
Normal Result %      = DIVIDE([Normal Results], [Normal Results] + [Abnormal Results] + [Inconclusive Results], 0)
AbnormalR %          = DIVIDE([Abnormal Results], [Normal Results] + [Abnormal Results] + [Inconclusive Results], 0)
Inconclusive %       = DIVIDE([Inconclusive Results], [Normal Results] + [Abnormal Results] + [Inconclusive Results], 0)

-- Billing
Total Billing        = SUM(HealthData[Billing Amount])
Avg Billing Amt      = AVERAGE(HealthData[Billing Amount])
```

---

## 📈 Key Insights the Dashboard Surfaces

- **YoY KPIs on Page 2** let administrators instantly spot whether admissions, costs, and staffing are growing or shrinking vs. the prior year — no manual calculations required
- **Admission Type split** (Emergency / Elective / Urgent) helps hospitals plan resource allocation and bed management
- **Test Result rates by Condition** reveal which medical conditions produce the most abnormal or inconclusive results — a clinical quality signal
- **Billing by Insurance Provider** highlights revenue concentration risk — if one insurer dominates, that's a dependency to manage
- **Day Type analysis** shows weekday vs. weekend admission load — useful for shift scheduling

---

## ⭐ Special Feature — ZoomCharts Custom Visuals

This report uses **3 ZoomCharts custom visuals** from the Power BI marketplace:
- **ZoomCharts Pie Chart** — animated, drill-down capable pie/donut
- **ZoomCharts Facet Chart** — faceted breakdown across dimensions
- **ZoomCharts Drill Down Combo Bar Pro** — interactive bar + line combo with drill-through

These visuals provide a more interactive experience than native Power BI visuals and demonstrate familiarity with the Power BI marketplace ecosystem.

---

## 📸 Dashboard Screenshots


![Patient Demographics] <img width="1920" height="968" alt="page1_demographics" src="https://github.com/user-attachments/assets/97e12242-46a8-4c18-aa1e-c9c7b1a3091e" />

![Key Trends] <img width="1920" height="978" alt="page2_trends" src="https://github.com/user-attachments/assets/724e84f9-f498-40e2-8895-498b7fc0380b" />

![Treatment & Cost] <img width="1920" height="970" alt="page3_treatment_cost" src="https://github.com/user-attachments/assets/a7c72018-a434-417e-8c92-306f81baf591" />


---

## 🚀 How to Open

1. Download `National_Health_Analysis.pbix`
2. Open with **Power BI Desktop** (free — [download here](https://powerbi.microsoft.com/en-us/desktop/))
3. All data is embedded — no external connection needed
4. The **ZoomCharts custom visuals** are bundled inside the file — they will load automatically
5. Use the **page navigator** to switch between the 3 report pages
6. Use slicers to filter by Year, Gender, Age Group, Medical Condition, and more

> ⚠️ Power BI Desktop is required. Free to download for Windows.

---

## 📂 Project Structure

```
national-health-analysis/
├── National_Health_Analysis.pbix       ← Main Power BI file
├── images/
│   ├── page1_demographics.png          ← Demographics page screenshot
│   ├── page2_trends.png                ← Key Trends page screenshot
│   └── page3_treatment_cost.png        ← Treatment & Cost page screenshot
└── README.md
```

---

## 💡 What I Learned

- Building a **multi-table DAX model** with a dedicated measures table (`DAX` table) — a professional Power BI best practice
- Writing **YoY growth measures** using `CALCULATE()` + `SAMEPERIODLASTYEAR()` for 5 different KPIs simultaneously
- Using **dynamic KPI fields** — a `KPI` config table that lets the slicer switch which metric is shown in the KPI card
- Integrating **ZoomCharts custom visuals** from the Power BI marketplace into a report
- Calculating **test result rates** (Normal %, Abnormal %, Inconclusive %) using `DIVIDE()` safely with fallback values
- Designing a **3-page report** with a clear narrative: Demographics → Trends → Cost

---

## 🙋 About Me

Made by **[Abhishek Jain](https://github.com/abhishekjain2004)**  
Aspiring Data Analyst | PG in Data Science & Analytics with Gen AI @ Imarticus Learning  
📧 abhishek2004.jain@gmail.com · [LinkedIn]www.linkedin.com/in/abhishek-jain-297014277
