# 🏥 Hospital Management Dashboard | Power BI

An interactive Power BI dashboard that gives hospital administrators a single, real-time view of admissions, bed utilization, length of stay, readmissions, and revenue - broken down by department and insurance provider - to support faster, evidence-based operational decisions.

**Tools:** Power BI Desktop · Power Query · DAX · Data Modeling
**File:** `Hospital_Management_DB.pbix`

---

## 📌 Project Overview

Hospital operations teams typically pull performance numbers from multiple disconnected sources (admissions logs, billing systems, clinical records), which slows down decision-making and makes it difficult to spot cross-departmental trends. This creates a real risk: administrators can miss early warning signs of bed shortages, rising readmissions, or underperforming departments until the problem is already costly.

This dashboard consolidates admissions, clinical, financial, and insurance data into one interactive Power BI report. It allows hospital management to monitor core operational KPIs at a glance, drill into performance by department, track month-over-month admission trends, and understand how revenue breaks down by department and payer - all filterable by a custom date range.

The project was built to demonstrate the end-to-end analytics workflow of a Resource/BI Analyst: data modeling, DAX measure development, visual design, and translating raw data into decisions hospital leadership can act on.

## 🎯 Business Objectives

The dashboard was designed to answer the following operational and strategic questions:

- How many patients were admitted in a given period, and how is that trending month over month?
- How efficiently are hospital beds being utilized (bed occupancy rate)?
- How long, on average, do patients stay in the hospital, and does this vary by department?
- Which departments have the highest readmission rates, signaling potential care-quality or discharge-planning issues?
- How is patient volume distributed across departments?
- How much total revenue is the hospital generating, and how does it break down by department and by insurance provider?
- Which insurance providers contribute the most (and least) to revenue within a given department?

## 🗂️ Dataset Overview

*Note: dataset details below are based only on the fields, tables, and values visible in the Power BI data model and report visuals.*

The model is built on two core tables:

| Table | Purpose | Key Fields Used in the Report |
|---|---|---|
| **Admissions** | Patient admission-level records | `Admission_Date`, `Department` |
| **Diagnosis_Clinical** | Clinical/financial detail linked to each admission | `Department`, `Insurance_Provider`, revenue values |

**Departments covered:** Cardiology, Neurology, Pediatrics, ICU, Orthopedics, General Surgery, Emergency, Oncology (8 departments).

**Insurance providers observed:** Cigna, HealthFirst, BlueShield, Self-Pay, Aetna (at least 5 payer categories).

**Core measures (DAX):**

| Measure | What It Calculates |
|---|---|
| `Total Admissions` | Count of patient admissions in the selected period |
| `Bed Occupancy Rate%` | Percentage of available beds in use |
| `Average length of stay` | Average number of days between admission and discharge |
| `Readmission Rate %` | Percentage of admissions resulting in a readmission |
| `Total Revenue` | Sum of billed/generated revenue across admissions |

The report is filtered by a date range slicer (e.g., 7/1/2025 - 6/1/2026 on the Overview page, and a full calendar year 1/1/2025 - 12/31/2025 on the trend/revenue page), so all KPIs and visuals are dynamic based on the period selected.

## 📊 Dashboard Features

The report consists of two functional pages, accessed via the date slicer and on-canvas navigation panel.

### Page 1 - Overview

| Visual | Type | What It Measures / Shows |
|---|---|---|
| Date range slicer | Slicer | Filters the entire page by admission date range |
| Total Admissions | Card KPI | Total count of admissions in the selected period |
| Bed Occupancy Rate% | Card KPI | Share of hospital bed capacity currently in use |
| Average Length of Stay | Card KPI | Average patient stay duration, in days |
| Readmission Rate% | Card KPI | Share of admissions that resulted in readmission |
| Total Revenue | Card KPI | Total revenue generated in the selected period |
| Average Length of Stay by Department | Line chart | Compares stay duration across all 8 departments, highlighting which departments keep patients longest |
| Readmission Rate % by Department | Column chart | Flags departments with elevated readmission rates |
| Total Admissions by Department | Donut chart | Shows how patient volume is distributed across departments, with percentage share per department |

### Page 2 - Admissions Trend & Revenue Breakdown

| Visual | Type | What It Measures / Shows |
|---|---|---|
| Date range slicer | Slicer | Filters this page by admission date range |
| Total Admissions by Month | Line chart | Monthly admission volume trend across the selected year |
| Auto-generated narrative summary | Smart Narrative | Dynamically written insights (e.g., highest/lowest month, % variance) that update as filters change |
| Total Revenue decomposition | Decomposition tree | Breaks down `Total Revenue` first by **Department**, then by **Insurance Provider** within a selected department, enabling root-cause / drill-down analysis of revenue drivers |

A left-hand navigation panel (Overview, Patients, Beds, Department, Physicians) is included as a design element for the dashboard's information architecture. In this version, the Overview and the Admissions Trend/Revenue pages are the two built-out, interactive pages; the additional sections represent the intended expansion path for a multi-module hospital reporting suite (see *Future Enhancements*).

## 🔑 Key Performance Indicators (KPIs)

| KPI | Definition | Why It Matters |
|---|---|---|
| **Total Admissions** | Count of patients admitted in the period | Core volume metric for capacity planning and staffing |
| **Bed Occupancy Rate %** | Beds in use ÷ total available beds | Indicates capacity strain; too high risks overcrowding, too low signals underutilized resources |
| **Average Length of Stay** | Average days between admission and discharge | A key cost and efficiency driver; shorter stays (without compromising care) free up beds and reduce cost per patient |
| **Readmission Rate %** | Share of admissions that are readmissions | A recognized quality-of-care indicator; high rates can signal discharge or treatment issues and affect reimbursement |
| **Total Revenue** | Total billed revenue generated | Tracks financial performance and supports department/payer-level profitability analysis |

## 💡 Key Insights

*Analysis based strictly on the values visible in the dashboard for the selected reporting periods.*

- **Admissions volume is stable with a mild seasonal dip.** Monthly admissions ranged narrowly between 29 and 32 across the year, with January the strongest month (32) and February the weakest (29, 10.34% lower) - a pattern worth monitoring for staffing/scheduling alignment rather than a cause for concern.
- **Bed occupancy (12.00%) is comfortably low**, suggesting the hospital has meaningful spare bed capacity in the selected period - room to absorb demand spikes, but also a potential signal to revisit resourcing or bed allocation efficiency.
- **Readmissions are concentrated in two departments.** ICU and Oncology are the only departments showing a visible readmission rate (~2%) while all others sit near 0%. Given the clinical severity of ICU and Oncology cases, this is plausible, but it is the clearest actionable flag in the dataset - a natural starting point for a discharge-planning or post-care follow-up review.
- **Length of stay is highest in acute-care departments.** Cardiology through ICU cluster around 6 days, while Orthopedics, General Surgery, Emergency, and Oncology trend down toward 5 days. This aligns with clinical expectations but is worth tracking, since ALS directly impacts bed availability and cost per case.
- **Patient volume is evenly distributed across departments** (each department represents roughly 12-13% of total admissions), indicating balanced demand rather than one department dominating capacity - useful context when planning staffing across departments.
- **Revenue is diversified but Emergency and General Surgery lead.** Of the ~$10.2M in total revenue analyzed on the decomposition tree, Emergency (~$1.30M) and General Surgery (~$1.30M) are the top-contributing departments, with the remaining departments (ICU, Pediatrics, Orthopedics, Oncology) close behind - no single department dominates, which reduces financial risk concentration.
- **Payer mix within a department is fairly balanced**, with Cigna and HealthFirst as leading contributors in the department drilled into, followed by BlueShield, Self-Pay, and Aetna - useful for negotiating payer contracts or evaluating self-pay exposure.

**Recommendation for leadership:** prioritize a readmission root-cause review for ICU and Oncology, and use the low bed occupancy rate to evaluate whether elective admissions or capacity-sharing agreements could better utilize available beds.

## 🛠️ Tools & Technologies Used

- **Power BI Desktop** - report development and data visualization
- **Power Query** - data shaping and preparation
- **DAX (Data Analysis Expressions)** - custom measures (Bed Occupancy Rate%, Readmission Rate %, Average Length of Stay, Total Revenue, Total Admissions)
- **Data Modeling** - relationships between Admissions and Diagnosis_Clinical tables
- **Power BI Smart Narrative** - AI-generated natural-language insights
- **Power BI Decomposition Tree** - AI-assisted, drillable root-cause analysis
- **Custom theming** - dark-blue hospital-branded theme with custom iconography

## 🧠 Skills Demonstrated

- Data modeling and relationship design across multiple tables
- Writing and validating DAX measures for rate-based and aggregate KPIs (%, averages, sums)
- Dashboard/UX design: KPI card layout, color theming, iconography, and information hierarchy
- Use of advanced Power BI visuals (Decomposition Tree, Smart Narrative) for AI-assisted analysis
- Translating raw healthcare operations data into executive-ready insights and recommendations
- Time-intelligence filtering via dynamic date-range slicers
- Business storytelling - framing dashboard output as decisions, not just numbers

## ▶️ How to Use the Dashboard

1. **Set the reporting period:** use the date slicer at the top of either page to define the start and end dates. All KPIs, charts, and the narrative update automatically.
2. **Review KPIs at a glance:** the five KPI cards on the Overview page (Page 1) give an immediate operational snapshot.
3. **Compare departments:** use the line chart, column chart, and donut chart on the Overview page to compare length of stay, readmission rate, and admission volume across departments.
4. **Explore trends:** on Page 2, review the monthly admissions line chart and read the auto-generated narrative summary for a plain-language explanation of the trend.
5. **Drill into revenue:** on the Decomposition Tree, click "+" on **Total Revenue** to expand by **Department**, then expand a department to break it down further by **Insurance Provider** - useful for identifying which payers drive revenue within a specific service line.

## 📈 Project Outcomes

This dashboard replaces manual, static reporting with a single interactive source of truth for hospital operations and finance stakeholders. It enables leadership to:

- Monitor capacity (bed occupancy, length of stay) and quality (readmission rate) indicators without waiting on manual reports
- Identify underperforming or at-risk departments (e.g., elevated readmissions) early enough to act
- Understand revenue composition by department and payer to support financial planning and payer negotiations
- Make faster, data-backed decisions on staffing, bed allocation, and discharge-planning priorities

## 🚀 Future Enhancements

- Build out the remaining navigation modules (Patients, Beds, Department, Physicians) referenced in the sidebar into fully interactive pages
- Add row-level security so department heads only see data relevant to their unit
- Incorporate patient satisfaction or clinical outcome metrics alongside operational KPIs
- Add year-over-year and forecast comparisons for admissions and revenue
- Introduce drill-through pages from the department and donut visuals for deeper department-level detail
- Automate data refresh via a scheduled gateway connection if/when connected to a live hospital data source

---

*This project is part of a Business Intelligence / Data Analytics portfolio. Feedback and suggestions are welcome.*
