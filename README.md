# 2025-Miami-HEAT-Data-Analyst-Challenge
Data‑driven breakdown of Miami Heat ticket sales—SQL Server analytics + Power BI dashboard for revenue, utilization, and game insights.
\
<!-- ──────────────────────────────────────────────────────────────────────────────── -->
<h3 align="center">
  📊🔥 <strong>Miami Heat Ticket‑Sales Analysis</strong> 🔥📊
</h3>
<p align="center">
  <img src="https://img.shields.io/badge/SQL%20Server-2019%2B-CC2927?logo=microsoftsqlserver&logoColor=white">
  <img src="https://img.shields.io/badge/Power%20BI-DAX%20⚡-F2C811?logo=powerbi&logoColor=black">
  <img src="https://img.shields.io/badge/Status-Completed-brightgreen">
  <img src="https://img.shields.io/badge/License-MIT-blue">
</p>

> **A two‑part analytics deep‑dive** into Miami Heat game attendance & ticket revenue —  
> **Part ①**: Data modelling + interactive visuals (Power BI).  
> **Part ②**: SQL Server segmentation & KPI discovery.

<!-- ───────────────────────────────────────────────────────────────────── -->

<!-- ──────────────────────────────────────────────────────────────── -->

<h3 align="center">📊🔥 Miami Heat Ticket‑Sales Project 🔥📊</h3>

---

## 📁 Repository Structure

```text
🔹 part1_powerbi/
├─ Miami Heat.pbix                     ← Power BI file with full dashboard
├─ My Dax Measures.docx                ← All DAX measures used
├─ Part 1 Answers PDF version.pdf      ← PDF write-up of insights
├─ Part 1 Answers txt Version.txt      ← Text version of Part 1 insights
├─ M Code for my Model Creation ( Table ).txt ← Power Query M-code for dimensions and fact table
├─ Miami Heat Dashboard.pdf            ← Exported visuals for quick view

🔹 part2_sql/
├─ PART 2 ANSWERS.txt                  ← SQL-based analysis answers
├─ analyst_project_p2.xlsx             ← Raw SQL tables + insert data

🔹 challenge_docs/
├─ 2025 Miami HEAT Data Analyst.pdf    ← Challenge instructions
├─ analyst_project_p1.xlsx             ← Game ticket sales dataset

🔹 README.md   ← you are here
```

---

Built with SQL Server 2022, Power Query, DAX, and Power BI. 🏀

---

## 🚀 Quick Start

1. **Clone**

```bash
git clone https://github.com/<you>/2025-Miami-HEAT-Data-Analyst-Challenge.git
cd heat-ticket-analysis
```

2. **SQL Server (Express 2022)**

* Install ➞ `SQLEXPR_x64_ENU.exe`
* Open **SSMS** → run `part2_sql/create_tables.sql`
* Execute `INSERT` blocks in **analyst\_project\_p2.xlsx** (sheet 3)

3. **Power BI**

* Open `part1_powerbi/Miami Heat.pbix`
* Click **Refresh** → explore the visuals!

---

## ✨ Analytical Approach

| Stage                   | What I did                                                                                                                      | 🔧 Tools    |
| ----------------------- | ------------------------------------------------------------------------------------------------------------------------------- | ----------- |
| **Ingest & Clean**      | Removed nulls, parsed opponent/date, converted `GroupFlag` ➞ `BIT`.                                                             | Power Query |
| **Model**               | Built 🚀 star‑schema (DateDim, EventDim, SectionDim, PlanDim, FactTicketSales).                                                 | Power BI    |
| **DAX Layer**           | Authored **36+ reusable measures** (YTD, Rolling‑30‑day, Premium %, Opponent Index …).                                          | DAX         |
| **Visual Storytelling** | 5‑page dashboard ➞ Exec Snapshot, Pricing, Demand Curve, Product, Geo.                                                          | Power BI    |
| **SQL Deep‑Dive**       | Utilisation tiers, game ranking, forwarding behaviour, segmentation CTEs.                                                       | SQL Server  |
| **Insights**            | • Premium seats < 2 revenue ➞ re‑price<br>• Large‑group orders scan 9 pts lower<br>• Mid‑week utilisation higher than weekends. | Narrative   |

---

## 🏆 Key Findings

| KPI             | Best Game                             | Worst Game                           |
| --------------- | ------------------------------------- | ------------------------------------ |
| **Revenue**     | **\$2.69 M** vs Mavericks (Apr 1 ’23) | **\$2.37 M** vs Clippers (Dec 8 ’22) |
| **Utilisation** | **99 %**                              | **78 %**                             |
| **Premium Mix** | **1.7 %**                             | **1.4 %**                            |

> Season plans drive 77 % of revenue, while premium inventory remains under‑leveraged.

---

## 🛠️ SQL Snippets

```sql
/* High / Medium / Low utilisation buckets */
SELECT  u.AccountKey,
        Utilisation = CAST(TicketsScanned * 1.0 / NULLIF(TicketsSold,0) AS DECIMAL(4,2)),
        Segment = CASE
                    WHEN Utilisation >= .95 THEN 'High'
                    WHEN Utilisation >= .80 THEN 'Medium'
                    ELSE                       'Low'
                  END
FROM    dbo.fn_AccountUtilisation() AS u;

/* Rank games by utilisation then revenue */
SELECT EventKey,
       Utilisation,
       GameRevenue,
       RANK() OVER (ORDER BY Utilisation DESC, GameRevenue DESC) AS GameRank
FROM   #GameStats;
```

---

## 👋 About Me

|              |                                                                                   |
| ------------ | --------------------------------------------------------------------------------- |
| **💼 Name**  | **Shadrack Kumi** — Data Analyst & Full‑Stack Dev                                 |
| **⚙️ Stack** | Python • SQL Server • Power BI • React • Node                                     |
| **🎯 Focus** | Converting raw sports & SaaS data into high‑impact dashboards & stories           |
| **🏅 Wins**  | Built **Brackify** 🏆 (event‑management platform) • Miami Heat challenge finalist |

---

## 🙌 Acknowledgements

* Miami Heat Analytics Team — for the data
* Microsoft SQL Server & Power BI communities — for open docs
* Supportive mentors & the FGC community — for caffeine ☕️ + play‑testing

