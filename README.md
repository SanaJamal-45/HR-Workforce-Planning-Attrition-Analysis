# HR-Workforce-Planning-Attrition-Analysis

An interactive Power BI dashboard analyzing workforce growth, employee attrition, and recruitment planning across a global organization — built to help HR and business leaders monitor headcount health, identify attrition risk, and track hiring performance against plan.

## Project Overview
This project is an end-to-end **HR Analytics dashboard** built in **Microsoft Power BI**, covering workforce data from **January 2023 to December 2025** for **1,200 employees** across 6 global locations.
The objective of this project is to transform raw HR data into meaningful workforce insights that help leadership monitor headcount health, understand attrition drivers, evaluate recruitment performance, and support proactive, data-driven people decisions.

## Problem Statement
The company wanted to analyze its workforce data to uncover key insights regarding:
- Overall headcount and FTE growth
- Attrition rate and its root causes
- Voluntary vs. involuntary turnover
- Recruitment funnel efficiency
- Departmental and level-based retention risk
- Employee engagement and performance trends

The dashboard was created to answer important HR questions and support data-driven workforce planning.

## Dashboard Objectives
The dashboard addresses the following business questions:
1. Identify the **Ending Headcount and FTE** for the latest period.
2. Track **Headcount Growth %** month-over-month.
3. Analyze **Workforce Growth Trend** from 2023–2025.
4. Compare **Actual vs. Planned Headcount** by department.
5. Calculate the **Overall Attrition Rate**.
6. Break down **Voluntary vs. Involuntary Attrition**.
7. Identify **Top Termination Reasons**.
8. Analyze **Attrition by Department, Role, and Level**.
9. Measure **Engagement Score at Exit** vs. active employees.
10. Track **Average Performance Rating by Department**.
11. Monitor **Open Requisitions and Fill Rate**.
12. Calculate the **Average Days to Fill** a role.

## Tools Used
- **Microsoft Power BI**
  - Power Query (data cleaning & transformation)
  - Data Modeling (star schema, relationships)
  - DAX (55+ calculated measures)
  - ZoomCharts custom visuals (drill-down line, facet, pie, combo bar, scatter, timeline)
  - Slicers and interactive filtering
  - Dashboard design across 3 report pages

## Key Performance Indicators (KPIs)
- Ending Headcount / Ending FTE
- Headcount & FTE Growth %
- New Hires / Terminations
- Attrition Rate %
- Voluntary Attrition % / Involuntary Attrition %
- Average Engagement at Exit
- Average Performance Rating
- Open Requisitions / Fill Rate %
- Average Days to Fill
- Headcount Variance vs. Plan

## Dashboard Features
- Interactive slicers for Department, Location, Level, and Date
- Executive Overview page with real-time headcount and FTE KPIs
- Attrition & Retention page with drill-down by department, role, and level
- Planning & Recruitment page tracking requisitions and fill performance
- Actual vs. planned headcount/FTE comparisons with variance indicators
- Color-coded MoM comparison cards (green/red) for quick trend reading
- Engagement-at-exit analysis to flag retention risk

## Dashboard Preview
![Dashboard Preview](dashboard-1.png)

## Business Insights
- **Headcount is 999 (Dec 2025)**, up 1.3% MoM, but still **80 heads (-7.4%) below the staffing plan** of 1,079.
- A sharp **8% headcount drop occurred in July 2025**, aligned with a company restructuring event.
- **Overall attrition rate is ~24.3%**, and terminations skew involuntary (61% involuntary vs. 39% voluntary).
- **"Company Restructuring" is the top exit driver**, accounting for 46% of all terminations.
- **Sales (28.5%) and Customer Success (22.5%)** have the highest attrition rates; **Finance (9.1%) and Engineering (10.4%)** are the most stable.
- **Engagement score predicts attrition risk**, employees who left averaged 3.27 vs. 3.59 for those who stayed.
- **Performance ratings are consistent across departments (3.32–3.61/5)**, showing attrition isn't driven by low performance.
- **Recruitment fill rate is only 34.7%**, with an average time-to-fill of 53 days, directly contributing to the headcount shortfall.
- **Engineering (385 employees) is the largest department**, and **Riga (470 employees) is the largest location hub**.

## Data Model
| Table | Purpose |
|---|---|
| DimEmployee | Employee master — department, role, level, location, hire/term dates, demographics |
| DimDepartment / DimLocation / DimDate | Lookup/dimension tables |
| FactMonthlySnapshot | Point-in-time headcount & FTE by department/location/level |
| FactEmployeeEvents | Hire and termination events with type/reason |
| FactEngagement | Periodic engagement survey scores |
| FactPerformance | Performance review ratings |
| FactCompensation | Salary history |
| FactAbsence | Sick/unpaid leave records |
| FactRecruitment | Requisitions opened/filled/cancelled, days-to-fill |
| WorkforceTargets | Planned headcount/FTE/budget by scenario |

## Key DAX Measures
```DAX
Attrition Rate % = DIVIDE([Terminations], [Average Headcount], 0)

Ending Headcount =
VAR LatestMonth = MAX(FactMonthlySnapshot[Month])
RETURN CALCULATE(SUM(FactMonthlySnapshot[Headcount]), FactMonthlySnapshot[Month] = LatestMonth)

Fill Rate % = DIVIDE([Filled Requisitions], [Open Requisitions] + [Filled Requisitions], 0)

Headcount Variance % = DIVIDE([Headcount Variance], [Planned Headcount (Latest Month)], 0)

Average Engagement at Exit =
CALCULATE(AVERAGE(FactEngagement[EngagementScore]), DimEmployee[EmploymentStatus] = "Terminated")
```

## How to Use
1. Clone or download this repository.
2. Open `HR_Analytics.pbix` in **Power BI Desktop**.
3. Use the slicers (Department, Location, Level, Date) to filter each page.
4. Click into any visual to drill down by department, role, or level.

## Conclusion
The workforce grew steadily through 2025 but remains 7.4% below staffing plan, primarily because recruitment fill rates (35%) and time-to-fill (53 days) haven't kept pace with demand. Attrition is concentrated in Sales and Customer Success, driven mainly by restructuring and involuntary exits rather than performance, and declining engagement scores are a measurable early warning sign ahead of an employee leaving.
