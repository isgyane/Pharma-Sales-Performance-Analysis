# Pharmaceutical Sales Performance Analytics

**An end-to-end Excel analytics system built for a multinational pharmaceutical distributor's field sales team in Ghana.**

> ⚠️ **Privacy Note:** This tool is built on real, production data. Product names, facility names, and exact revenue figures have been anonymized or omitted to protect commercial confidentiality. All percentages, patterns, and methodologies described below are real.

---

## Business Context

As a Senior Medical Sales Representative at a multinational pharma distributor, I managed a portfolio of 4 product SKUs across 300+ healthcare facilities — hospitals, pharmacies, and wholesalers — spanning multiple territories in Ghana.

The sales team had no standardized way to track performance trends, customer purchasing behavior, or upcoming stockout risk. Reporting was manual, fragmented, and reactive: reps compiled numbers at month-end, and by the time a stockout was spotted, the customer had already gone days or weeks without product — revenue leaked during the gap, and in the worst cases, competitors moved in.

**A few months into the role, I built this system to answer three primary questions:**
1. Are we on track to hit our annual targets — by product, by customer, by territory?
2. Which customers are slowing down, and why?
3. Where is the next stockout going to happen before it happens?

But it grew beyond that. Each rep adopted their own version of the system to self-serve insights across their territory — some managing portfolios of 10, 12, even 20 SKUs. Senior leadership used it for weekly check-ins, monthly business reviews, quarterly performance assessments, and year-over-year comparisons, gaining direct visibility into each rep's territory management

---
## Executive Summary

Key findings from FY2025 (~25,000 units sold across 160+ active customers and 4 products):

- **Revenue concentration is dangerously high.** The top 5 customers account for ~47% of total revenue. Losing a single key account would create a significant gap that dozens of smaller customers couldn't fill.

- **Monthly performance swings are extreme.** Target achievement ranged from as low as 31% in the weakest months to 158% in the strongest — a 5x variance that makes forecasting unreliable and creates cash flow pressure.

- **Product performance is uneven.** Two products exceeded annual targets (one reaching 133%), while one product landed at just 56% of target — suggesting either a pricing issue, a prescriber engagement gap, or an allocation mismatch.

- **The stockout prediction model flagged opportunities the team was missing.** By tracking consumption rates across 400+ facility-SKU combinations, the system identified customers whose purchasing had silently dropped — often a signal that prescribers had switched away from our products before the rep was even aware.

---

## Insights Deep Dive

### 1. Sales Trends & Target Achievement

The system tracks monthly achievement against annual targets for each product, using a traffic-light indicator system (on track / behind / critical).

**Key findings:**
- **Q3 consistently outperforms other quarters**, driven by hospital procurement cycles that align with government budget releases. July and August regularly exceed 130% of monthly targets.
- **Q4 drops sharply** — December achievement fell below 50%, partly due to holiday closures at key facilities but also because annual budgets are exhausted at major hospital accounts.
- **February is a persistent weak spot** across all products (~35-44% achievement), suggesting a structural gap in early-year demand that marketing campaigns could address.

The YTD vs. Full Year view gives reps a real-time read on whether current pace will hit the annual number, or whether acceleration is needed in remaining months.

<!-- Dashboard screenshot placeholder -->
<!-- ![Overview Dashboard](images/Dashboard%20Page.gif) -->

### 2. Product Performance

Four SKUs are tracked, each with distinct performance profiles:

| Product | FY Target Achievement | Insight |
|---------|----------------------|---------|
| Product A (Injectable) | ~133% | Star performer. High-volume hospital accounts drive consistent demand. |
| Product B (Capsule) | ~56% | Significantly underperforming. Low prescriber awareness or therapeutic competition likely. |
| Product C (Sachet) | ~81% | Mid-range. Growth potential in pediatric-focused facilities. |
| Product D (Ear drops) | ~111% | Exceeded target. Niche but reliable — steady demand from ENT departments. |

**The gap between Product A (133%) and Product B (56%) represents the single largest revenue opportunity.** If Product B reached even 80% of target through focused prescriber engagement at top facilities, total portfolio revenue would increase meaningfully.

### 3. Customer Concentration & Territory Analysis

The customer analysis breaks down performance by individual facility and territory, revealing where revenue actually comes from:

- **Top 5 facilities contribute ~47% of total revenue.** These are large teaching hospitals and military/government facilities with high patient volumes.
- **The long tail is wide but thin.** Over 100 facilities contribute individually small amounts. Many ordered only once or twice across the year.
- **Territory performance varies significantly**, with urban territories (Accra, Kumasi) driving the majority of volume while regional territories show untapped potential.

The Customer Budget vs. Achieved view tracks each key account's progress against their individual allocation, making it immediately visible which accounts are falling behind their committed volumes.

### 4. Stockout Prediction & Prescriber Drop-Off Detection

This is the most operationally impactful feature. For every facility-SKU combination, the system calculates:

- **Last order date** — when did this customer last buy?
- **Consumption rate** — how fast are they going through stock, based on order history?
- **Predicted current stock** — estimated units remaining today
- **Days to depletion** — when will they run out?

**What makes this more than inventory tracking:** a customer whose predicted stock goes deeply negative isn't just "out of stock" — they've likely stopped using the product entirely. This is the early warning signal that a prescriber has switched to a competitor or a hospital formulary committee has dropped the product. By the time a rep notices the customer hasn't reordered, it may be months too late.

The system tracks 400+ facility-SKU combinations and flags:
- 🔴 **Overdue** — predicted stock is negative; customer should have reordered but hasn't
- 🟡 **Due soon** — stock is running low; rep should proactively reach out
- 🟢 **Healthy** — adequate stock based on consumption rate

This shifts the rep's workflow from reactive ("why didn't they order?") to proactive ("they'll need stock next week — let me call now").

---

## Recommendations

Based on the patterns surfaced by this system:

**Revenue Concentration**
- Develop a "Next 10" growth plan targeting mid-tier facilities with the highest potential to become top accounts, reducing dependence on the current top 5.

**Product B Underperformance**
- Investigate prescriber awareness at high-potential facilities. Cross-reference with facilities that buy Product A (same call points) but not Product B — these are warm leads where the rep relationship already exists.

**Seasonal Gaps**
- Pre-position stock and run targeted outreach campaigns in January–February and December to smooth the achievement curve and reduce the 5x monthly variance.

**Prescriber Drop-Off**
- Flag any facility-SKU combination where predicted stock has been negative for 60+ days as a "prescriber risk" for immediate field visit and investigation.

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
| **Overview** | North Star KPIs: total revenue, units sold, customer count, products on target |
| **YTD vs Full Year** | Pace tracking — will current run rate hit annual targets? |
| **Growth Analysis** | Month-over-month and year-over-year trends by product |
| **Customer Analysis** | Revenue and volume breakdown by individual facility |
| **Customer Budget vs Achieved** | Key account allocation tracking with achievement % |
| **Territory Breakdown** | Geographic performance comparison across territories |
| **Stockout Prediction** | Consumption-based reorder forecasting for 400+ facility-SKU pairs |
| **Weekly Report** | Snapshot view for weekly team meetings |

### Technical Implementation

- **Data Model:** Excel Data Model with relationships between sales transactions, customer master, product master, and calendar tables
- **Data Preparation:** Power Query (M language) for ETL — cleaning, type conversion, and merging across workbooks
- **Custom Calendar:** Built to align with the company's non-standard fiscal calendar for accurate period-over-period comparisons
- **Consumption Rate Engine:** Calculates rolling consumption rates per facility-SKU based on order frequency and quantity, then projects forward to estimate current stock levels and next purchase dates
- **Pivot Tables:** 15+ pivot tables powering the backend calculations, feeding into dashboard visualizations via structured ranges
- **Interactive Filtering:** Slicers for period selection (year, quarter, month, week) across all views

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
