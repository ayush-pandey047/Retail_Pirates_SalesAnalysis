# Section 10: Tableau Dashboard Design
# Retail Pirates — Sales Analysis

---

## 10.1 Dashboard Objective

The Tableau dashboards are designed to support two distinct decision-making contexts:

**Executive Summary Dashboard** answers the question: *"How is the business performing overall, and what are the biggest drivers of revenue?"* It is built for the CEO or business owner who needs a quick, high-level health check — total revenue, average order value, top categories, and channel performance — all in one view with global year and category filters.

**Operational Drill-Down Dashboard** answers the question: *"Where exactly should we focus our operational attention?"* It serves the store/operations manager who needs to compare quarterly momentum, identify which category-channel combinations are underperforming, understand customer concentration risk, and evaluate whether the discount strategy is working.

Together, the two dashboards form a complete analytics layer — executives see the summary; managers can drill into causes.

---

## 10.2 Data Source

- **File:** `data/processed/tableau_ready.csv`
- **Rows:** 12,418 transactions
- **Columns:** 23 (11 original + 12 ETL-derived: txn_year, txn_month, txn_month_name, txn_quarter, txn_quarter_label, txn_day_of_week, txn_day_name, revenue_per_unit, is_bulk, spent_segment, discount_applied, discount_flag, category_code)
- **Date Range:** January 2022 – January 2025 (2025 excluded from main analysis — only 210 partial-year transactions)

---

## 10.3 View Structure

### Dashboard 1 — Executive Summary

| Zone | Sheet | Chart Type | Purpose |
|---|---|---|---|
| Top row (4 tiles) | KPI Summary | Big Number / Text | At-a-glance scorecard: Total Revenue ($1.56M), AOV ($125.27), Transactions (12,418), Discount Rate (66.9%) |
| Middle left (wide) | Revenue Trend | Line Chart | Monthly revenue 2022–2024, one line per year, colour-coded, reference line at average |
| Middle right | Category Revenue | Horizontal Bar | Ranked revenue by all 8 product categories |
| Bottom left | Channel Split | Donut/Pie Chart | Online (50.9%) vs In-store (49.1%) revenue share |
| Bottom right | Payment Method | Bar Chart | Revenue by Cash, Credit Card, Digital Wallet |

### Dashboard 2 — Operational Drill-Down

| Zone | Sheet | Chart Type | Purpose |
|---|---|---|---|
| Top (full width) | Quarterly Trend | Multi-line Chart | Quarterly revenue by year — spot seasonal dips and recovery |
| Middle left | Category × Channel | Stacked Bar | Which categories over-index online vs in-store |
| Middle right | Spend Segment | Bar Chart | Volume of Low / Medium / High spend transactions |
| Bottom left | Customer Leaderboard | Horizontal Bar | Top 10 customers ranked by lifetime spend |
| Bottom right | Discount Impact | Grouped Bar | Average order value — discounted vs non-discounted, by category |

---

## 10.4 Filters and Interactive Elements

### Global Filters (both dashboards)

| Filter | Field | Type | Options |
|---|---|---|---|
| Year | txn_year | Single Value Dropdown | 2022, 2023, 2024 |
| Category | category | Multi-Value Checkbox | All 8 categories |
| Channel | location | Radio Button | All / Online / In-store |
| Payment Method | payment_method | Multi-Value List | Cash, Credit Card, Digital Wallet |

All filters are configured with **"Apply to worksheets → All using this data source"** so selecting a year or category on one dashboard instantly updates every chart simultaneously.

### Dashboard Actions (Interactivity)

1. **Highlight-to-Filter:** Clicking any category bar on the Executive Summary's Category Revenue chart filters all other charts on both dashboards to show only that category's data. Built via Dashboard → Actions → Filter Action (Source: Category Revenue, Target: All Sheets).

2. **Tooltip Drill-Down:** Every chart has a customised tooltip showing the exact values on hover — e.g., hovering a bar in Category Revenue shows: Category name, Total Revenue, % of total revenue, Transaction count.

3. **Year Slider (Operational Dashboard):** The Year filter appears as a slider on Dashboard 2 to allow quick year-over-year toggling while exploring quarterly trends.

---

## 10.5 Individual Sheet Explanations

### Sheet 1 — Monthly Revenue Trend

**What it shows:** Three lines (one per year) trace monthly revenue from January to December. The X-axis is the calendar month (Jan–Dec); the Y-axis is SUM(total_spent) in USD. A horizontal reference line marks the overall monthly average (~$43,000/month).

**Business interpretation:** 2022 started unusually strong (January: $52,548) then declined through the year. 2023 was the weakest year overall (-3.3% YoY). 2024 recovered significantly (+6.7% YoY), with Q4 2024 approaching 2022 Q1 levels, suggesting the business is back on a growth trajectory. The consistent dip in mid-year months (May–July across all years) points to a predictable seasonal softness that could be addressed with targeted promotions.

---

### Sheet 2 — Revenue by Category

**What it shows:** A horizontal bar chart with 8 bars, sorted from highest to lowest revenue. Each bar represents the total revenue (SUM of total_spent) for one product category over the full 2022–2024 period.

**Business interpretation:** Butchers ($204,140) and Electric Household Essentials ($203,261) lead all categories, while Milk Products ($182,741) and Patisserie ($184,615) trail. The spread between highest and lowest is only $21,400 (10.5% gap), meaning no single category dominates — the business has a healthy, diversified revenue base. However, Milk Products and Patisserie represent an opportunity for targeted promotion to close the gap.

---

### Sheet 3 — Channel Split

**What it shows:** A donut chart divided into two segments: Online (50.9%, $791,592) and In-store (49.1%, $763,968).

**Business interpretation:** The near-perfect 51/49 online-to-in-store split indicates a well-balanced omnichannel operation. Neither channel is dominant, which reduces concentration risk. However, Computers & Electric Accessories skew more heavily online (54.5%), while Food and Furniture skew in-store, suggesting category-specific channel optimisation opportunities.

---

### Sheet 4 — Payment Method Revenue

**What it shows:** Three bars representing Cash ($541,679), Digital Wallet ($507,475), and Credit Card ($506,406).

**Business interpretation:** Cash slightly leads digital payment methods (34.8% of revenue), suggesting a significant customer segment that remains offline or prefers physical payment. Digital Wallet and Credit Card are nearly equal. As the business grows online, digital wallet adoption is likely to rise — monitoring this trend annually will indicate the pace of digital shift.

---

### Sheet 5 — Quarterly Revenue Trend

**What it shows:** Quarterly revenue plotted as connected lines, with colour separation by year (2022 blue, 2023 orange, 2024 green). X-axis shows Q1–Q4 labels.

**Business interpretation:** Q4 is the weakest quarter in every year — a counter-intuitive finding for retail (usually strongest in Q4 due to holiday shopping). This suggests the store's product mix (grocery, essentials, furniture) is not driven by gift-buying seasonality. Q1 is consistently the strongest quarter. The 2024 Q3–Q4 recovery trend ($128,705 → $137,025) is the most promising signal — it means the business ended 2024 at its highest quarterly run-rate.

---

### Sheet 6 — Category × Channel (Stacked Bar)

**What it shows:** Stacked horizontal bars for each category, split into Online (blue) and In-store (orange) sub-segments.

**Business interpretation:** Computers & Electric Accessories and Electric Household Essentials have the strongest online skew, consistent with consumers preferring online browsing for high-consideration electronics purchases. Butchers and Milk Products show stronger in-store presence, consistent with fresh food purchase behaviour. This insight directly informs inventory and staffing allocation by channel.

---

### Sheet 7 — Customer Leaderboard

**What it shows:** Top 10 customer IDs ranked by total lifetime spend (2022–2024), displayed as horizontal bars.

**Business interpretation:** The top 25 customers account for 100% of revenue (the dataset has only 25 unique customers, averaging ~$62,222 each). CUST_24 leads at $67,896. The narrow spread between customers (~8% from top to bottom) suggests no single customer is a concentration risk, but also that there is no "whale" customer to retain above all others — the business likely serves a regular, stable wholesale or B2B client base.

---

### Sheet 8 — Spend Segment Distribution

**What it shows:** Three bars for Low (≤$55), Medium ($55–$182), and High (>$182) spend buckets, showing transaction count and average spend per segment.

**Business interpretation:** The equal thirds split (by design of the tertile segmentation) confirms the data is well-distributed. High-segment transactions (>$182 average spend) are where bulk-buying (qty ≥ 7) concentrates. Targeting these high-segment customers with loyalty incentives would have the greatest revenue-per-customer impact.

---

### Sheet 9 — Discount Impact

**What it shows:** Grouped bars showing AVG(total_spent) for Discounted vs Non-Discounted transactions, coloured by category.

**Business interpretation:** The critical finding is that the average order value for discounted transactions ($125.04) is virtually identical to non-discounted transactions ($125.73). This means the current discount strategy (applied to 66.9% of transactions) is not increasing basket size — it is simply giving away margin. The business should test reducing discount frequency and reallocating that budget to category-specific promotions where discounts do shift behaviour.

---

## 10.6 Dashboard Screenshots

All screenshots saved in `tableau/screenshots/`.

| View | File |
|---|---|
| Executive Summary (full view) | `screenshots/dashboard_executive_summary.png` |
| Operational Drill-Down (full view) | `screenshots/dashboard_operational.png` |
| Sheet 1 — Revenue Trend | `screenshots/sheet_revenue_trend.png` |
| Sheet 2 — Category Revenue | `screenshots/sheet_category_revenue.png` |
| Sheet 3 — Channel Split | `screenshots/sheet_channel_split.png` |
| Sheet 4 — Payment Method | `screenshots/sheet_payment_method.png` |
| Sheet 5 — Quarterly Trend | `screenshots/sheet_quarterly_trend.png` |
| Sheet 6 — Category x Channel | `screenshots/sheet_category_x_channel.png` |
| Sheet 7 — Customer Leaderboard | `screenshots/sheet_customer_leaderboard.png` |
| Sheet 8 — Spend Segment | `screenshots/sheet_spend_segment.png` |
| Sheet 9 — Discount Impact | `screenshots/sheet_discount_impact.png` |

---

## 10.7 Tableau Public URLs

**Published:** 27 April 2026 | **Author:** Pranay Chitare

### Dashboards

| Dashboard | URL |
|---|---|
| Executive Summary | https://public.tableau.com/app/profile/pranay.chitare/viz/RetailPiratesSalesAnalysis/ExecutiveSummary |
| Operational Drill-Down | https://public.tableau.com/app/profile/pranay.chitare/viz/RetailPiratesSalesAnalysis/OperationalDrill-Down |

### Individual Sheet Views

| Sheet | URL |
|---|---|
| Sheet 1 — Revenue Trend | https://public.tableau.com/app/profile/pranay.chitare/viz/RetailPiratesSalesAnalysis/RevenueTrend |
| Sheet 2 — Category Revenue | https://public.tableau.com/app/profile/pranay.chitare/viz/RetailPiratesSalesAnalysis/CategoryRevenue |
| Sheet 3 — Channel Split | https://public.tableau.com/app/profile/pranay.chitare/viz/RetailPiratesSalesAnalysis/ChannelSplit |
| Sheet 4 — Payment Method | https://public.tableau.com/app/profile/pranay.chitare/viz/RetailPiratesSalesAnalysis/PaymentMethod |
| Sheet 5 — Quarterly Trend | https://public.tableau.com/app/profile/pranay.chitare/viz/RetailPiratesSalesAnalysis/QuarterlyTrend |
| Sheet 6 — Category x Channel | https://public.tableau.com/app/profile/pranay.chitare/viz/RetailPiratesSalesAnalysis/CategoryxChannel |
| Sheet 7 — Customer Leaderboard | https://public.tableau.com/app/profile/pranay.chitare/viz/RetailPiratesSalesAnalysis/CustomerLeaderboard |
| Sheet 8 — Spend Segment | https://public.tableau.com/app/profile/pranay.chitare/viz/RetailPiratesSalesAnalysis/SpendSegment |
| Sheet 9 — Discount Impact | https://public.tableau.com/app/profile/pranay.chitare/viz/RetailPiratesSalesAnalysis/DiscountImpact |

**Reference:** Dashboard links and screenshot index — `tableau/dashboard_links.md`
