# Vendor Performance Analysis

An end-to-end analysis of vendor performance, supply chain liquidity, and pricing efficiency, built by consolidating Sales, Purchases, Purchase Prices, and Vendor Invoices data into a single analytical dataset, followed by statistical validation and an interactive Power BI dashboard.

## Project Overview

This project evaluates vendor and brand performance across procurement, sales, pricing, and inventory dimensions to identify opportunities for margin optimization, freight cost containment, and supplier risk mitigation. It combines exploratory data analysis, hypothesis testing, and business intelligence dashboarding to turn raw operational data into actionable recommendations.

## Dataset

- **Source tables:** Sales, Purchases, Purchase Prices, Vendor Invoices
- **Final shape:** 10,692 rows × 18 columns
- **Missing values:** None (zero nulls across all columns)

| Column | Type | Description |
|---|---|---|
| VendorNumber | int64 | Unique vendor identifier |
| VendorName | object | Vendor name |
| Brand | int64 | Brand identifier |
| Description | object | Product description |
| PurchasePrice | float64 | Unit purchase price |
| ActualPrices | float64 | Unit selling price |
| Volume | float64 | Product volume |
| TotalPurchaseQuantity | float64 | Units purchased |
| TotalPurchaseDollars | float64 | Total purchase spend |
| TotalSalesQuantity | float64 | Units sold |
| TotalSalesDollars | float64 | Total sales revenue |
| TotalSalesPrice | float64 | Aggregate sales price |
| TotalExciseTax | float64 | Excise tax total |
| FreightCost | float64 | Freight/logistics cost |
| GrossProfit | float64 | Sales dollars minus cost |
| ProfitMargin | float64 | Gross profit as % of sales |
| StockTurnover | float64 | Inventory turnover ratio |
| SalesPurchaseRatio | float64 | Sales-to-purchase efficiency ratio |

## Key Questions Answered

1. Which brands need promotional or pricing adjustments (low sales velocity, high margin)?
2. Which vendors and brands drive the highest sales performance?
3. Which vendors contribute most to total purchase spend, and what is the supplier concentration risk?
4. Does bulk purchasing reduce unit price, and what is the optimal order volume for cost savings?
5. Which vendors show low inventory turnover (excess/slow-moving stock)?
6. How much capital is locked in unsold inventory, and which vendors hold the most?

## Key Findings

- **Margin/Velocity Tradeoff:** A distinct set of high-margin, low-volume brands were identified as strong candidates for promotional bundling rather than price cuts.
- **Vendor Concentration Risk:** A small group of top vendors account for a disproportionate share of both purchase spend and sales revenue, indicating supply chain dependency risk.
- **Price ≠ Performance:** PurchasePrice shows near-zero correlation with TotalSalesDollars (-0.012) and GrossProfit (-0.016), meaning unit price alone doesn't drive revenue or profit outcomes.
- **Turnover ≠ Profitability:** StockTurnover has a very weak negative correlation with GrossProfit (-0.038) and ProfitMargin (-0.055) — moving inventory faster doesn't necessarily mean higher profitability.
- **Outliers & Anomalies:**
  - GrossProfit minimum of **-52,002.78** flags heavily mispriced or markdown-driven stock.
  - ProfitMargin floor of **-23,730.64%** reflects edge cases where costs accrued with zero recorded sales.
  - FreightCost ranges from **$0.09 to $257,032.07**, pointing to inconsistent logistics practices or emergency shipping surcharges.

## Statistical Validation

An independent two-sample t-test was run to check whether the profit margin gap between top- and low-performing vendors is a real structural difference or just random variation.

- **H₀:** No significant difference in mean profit margin between top and low-performing vendors (μ_top = μ_low)
- **Hₐ:** Mean profit margins differ significantly between the two groups (μ_top ≠ μ_low)

| Metric | Value | Decision |
|---|---|---|
| T-Statistic | -10.7137 | Highly Significant |
| P-Value | 0.0000 (p < 0.05) | Reject H₀ |

**Conclusion:** The null hypothesis is rejected. The profit margin gap between top- and low-performing vendors is statistically significant, suggesting it stems from systematic vendor-level factors (e.g., negotiated pricing, logistics efficiency) rather than random chance.

## Dashboard

An interactive **Power BI** dashboard was built to visualize:
- Total Sales, Purchases, Gross Profit, Profit Margin, and Unsold Capital (headline KPIs)
- Purchase contribution % by vendor
- Top vendors and brands by sales
- Low-performing vendors and brands
- Profit margin vs. total sales scatter view to spot low-performer patterns
