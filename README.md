# Pharmaceutical Sales Performance Analytics

**An end-to-end Excel analytics system built for a multinational pharmaceutical distributor's field sales team in Ghana.**

> ⚠️ **Privacy Note:** This tool is built on real, production data. Product names, facility names, and exact revenue figures have been anonymized or omitted to protect commercial confidentiality. All percentages, patterns, and methodologies described below are real.

---

## Business Context

As a Medical Sales Representative at a multinational pharma distributor, I managed a portfolio of 4 product SKUs across 300+ healthcare facilities — hospitals, pharmacies, and wholesalers — spanning multiple territories in Ghana.

The sales team had no standardized way to track performance trends, customer purchasing behavior, or upcoming stockout risk. Reporting was manual, fragmented, and reactive: reps compiled numbers at month-end, and by the time a stockout was spotted, the customer had already gone days or weeks without product — revenue leaked during the gap, and in the worst cases, competitors moved in.

**A few months into the role, I built this system to answer three primary questions:**
1. Are we on track to hit our annual targets — by product, by customer, by territory?
2. Which customers are slowing down, and why?
3. Where is the next stockout going to happen before it happens?

But it grew beyond that. Each rep adopted their own version of the system to self-serve insights across their territory — some managing portfolios of 10, 12, even 20 SKUs. Senior leadership used it for weekly check-ins, monthly business reviews, quarterly performance assessments, and year-over-year comparisons, gaining direct visibility into each rep's territory management

---
## Executive Summary

This system has tracked performance across three full fiscal years (2023–2025), covering 4 products and 160+ active customers. Key findings:
- **Total portfolio volume nearly quadrupled — even as targets were raised each year**. As the business grew, leadership increased targets to match. The system gave reps the visibility to consistently meet or exceed those moving goalposts
- **The stockout prediction model became the team's most valuable early warning system**. By tracking consumption rates across 400+ facility-SKU combinations, the system didn't just flag upcoming stockouts — it surfaced dormant customers. Facilities that had purchased in the past but silently stopped reordering were flagged automatically, giving reps a concrete call list of lapsed accounts to investigate and re-engage before those customers were completely lost
- **Every product grew in absolute volume year over year**. The top-performing product grew nearly 8x over the period. Even the slowest-growing product in the portfolio still more than tripled its volume
- **Revenue concentration remains a key risk.** The top 5 customers account for nearly 50% of total revenue. Losing a single key account would create a significant gap that dozens of smaller customers couldn't fill.

---

## Insights Deep Dive

### 1. Seasonal Patterns & 2026 Q1 Strategy

Across all three years (2023–2025), Q1 consistently underperformed — driven by key hospital accounts making large purchases in December to build stock ahead of the tender review period in January–February. This front-loading of orders created a predictable Q1 revenue dip each year.

The system also revealed a disparity between volume and revenue; Q4 2025 was the highest revenue quarter despite lower total units — because the highest-priced SKU delivered 234% of its quarterly target, pulling revenue disproportionately upward.

By surfacing these patterns, I implemented a targeted strategy going into 2026 to break the cycle and ensure a stronger start to the year. Early indicators suggest the approach is working.

### 2. Product Growth
Every product in the portfolio grew year over year from 2023 to 2025, with total volume nearly quadrupling. The standout is Product A, which grew nearly 8x over the period and now accounts for the majority of portfolio volume — up from roughly a quarter of the mix in 2023.

The portfolio mix has shifted significantly: what was once a relatively balanced spread across four SKUs is now heavily led by one product. This isn't necessarily a problem — but it means revenue is increasingly sensitive to that product's performance in any given period.

Diversifying growth across the remaining SKUs is a priority for 2026

### 3. Customer Concentration
The top 5 customers account for roughly half of total revenue, with the top 2 alone contributing nearly 30%. The remaining 150+ customers share the other half. This isn't unusual in pharma sales — large teaching hospitals and government facilities naturally drive volume — but it creates real risk.

Product C makes this particularly visible. Its volume is concentrated in just 3 facilities. For 2026, the goal is to **onboard 10+ new customers** for this product specifically, reducing over-reliance and building a more resilient revenue base.


### 4. Dormant Customer Detection & Stockout Prediction

This is the most operationally impactful feature. For every facility-SKU combination, the system calculates:

- **Last order date** — when did this customer last buy?
- **Consumption rate** — how fast are they going through stock, based on order history?
- **Predicted current stock** — estimated units remaining today
- **Days to depletion** — when will they run out?

Of the 400+ facility-SKU combinations tracked, a significant number show deeply negative predicted stock — meaning the customer has long passed their expected reorder date. Some facilities haven't placed an order in over 18 months.

These aren't just late orders. A facility whose predicted stock has been negative for months has almost certainly stopped using the product (or purchasing through a third-party). The prescribers in some of those hospital may have switched to a competitor, or the product may have been removed from the hospital's formulary. Without this system, a rep might not notice for months. With it, these accounts surface automatically as a prioritized re-engagement list

This shifts the rep's workflow from reactive ("why didn't they order?") to proactive ("they'll need stock next week — let me follow up now").

---

## System Architecture

The system consists of two linked Excel workbooks:

**Sales Entry Workbook** — the data capture layer
- Reps enter daily sales transactions (facility, product, quantity, date)
- Power Query cleans and structures entries for the reporting layer
- Validates against master customer and product lists

**Reporting Dashboard Workbook** — the analytics layer, with 8 interactive views:

| View | Purpose |
|------|---------|
| **Overview** | Performance vs. target at a glance — achievement % and deficit by product |
| **YTD vs Full Year** | Are we on track to hit annual targets, or do we need to accelerate? |
| **Growth Analysis** | How is each product trending for the current year vs previous year? |
| **Customer Analysis** | Which facilities are driving revenue, and volumes and which are falling behind? |
| **Customer Budget vs Achieved** | Are key accounts buying at the volumes we targetted for them? |
| **Territory Breakdown** | Which geographic areas are performing and where are the gaps? |
| **Stockout Prediction** | Who needs to reorder soon — and who has silently stopped buying? |
| **Weekly Report** | Snapshot view for weekly team meetings |

👋I've also built this same analytical framework in Power BI and SQL. The insights are the same

### Technical Implementation

- **Data Model:** Excel Data Model with relationships between sales transactions, customers, product targets, and calendar tables
- **Data Preparation:** Power Query (M language) for ETL — cleaning, type conversion, and merging across workbooks
- **Custom Calendar:** Built to align with the company's non-standard fiscal calendar for accurate period-over-period comparisons
- **Consumption Rate Engine:** Calculates rolling consumption rates per facility-SKU based on order frequency and quantity, then projects forward to estimate current stock levels and next purchase dates
- **Pivot Tables:** 15+ pivot tables powering the backend calculations, feeding into dashboard visualizations via structured ranges
- **Interactive Filtering:** Slicers for period selection (year, quarter, month, week) across most views

---

## Impact

This system replaced a process where reps manually compiled numbers into a spreadsheet at month-end. Now:

- **Daily visibility** into sales performance against targets
- **Weekly reports** generated in seconds instead of hours
- **Proactive stockout prevention** — reps contact customers before they run out, not after
- **Prescriber drop-off detection** — consumption slowdowns surface weeks before a missed reorder would
- **Adopted by the entire sales team** as the standard reporting tool for the Ghana operation
- **Contributed to a 157% revenue increase** as part of a broader data-driven sales strategy

---

## Tools

Excel (Power Query, Data Model, Pivot Tables, Slicers) · M Language · Data Modeling

---

*Built by [Isaac G. Somuah](https://www.linkedin.com/in/isaacsomuah) — Pharmacist, Commercial Analytics, Data Skills Trainer.*
*Founder @ [Verken IT & Analytics](https://verkenitandanalytics.com)*
