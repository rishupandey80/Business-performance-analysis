# Business-performance-analysis
Business Performance Analysis using Python, SQL, and data visualization to explore sales and vendor performance.

 Vendor Profitability, Product Pricing & Inventory Analysis

## Project Overview
This end-to-end Data Analytics project uses Python/Jupyter Notebook and Power BI to analyse vendor sales and profitability, product-level sales/pricing, and inventory movement. It transforms six CSV source tables into summarized analysis datasets and a three-page interactive dashboard.

> **Metric definition:** Gross Profit in this project is calculated as `TotalSalesDollars - TotalPurchaseDollars`. `ProfitAfterFreight` is `GrossProfit - TotalFreight`. These are analytical proxies, not audited accounting profit.

## Dashboard Pages
1. **Sales, Inventory & Profitability Insights** — vendor KPIs, top vendors by sales/gross profit, performance-category sales, and sales-versus-profit comparisons.
2. **Product and Pricing Analysis** — product sales and gross profit leaders, performance-category split, and selling-versus-purchase-price comparison.
3. **Inventory Analysis** — beginning/ending stock, inventory value, inventory value change, stock movement status, and city/product inventory views.

## Tech Stack
- **Python:** Pandas, NumPy, os
- **Visualisation:** Matplotlib, Seaborn
- **Notebook / data processing:** Jupyter Notebook
- **BI:** Microsoft Power BI (KPI cards, bar/column charts, donut chart, slicer, Top-N filters, data labels, multi-page report)
- **SQLAlchemy:** imported in the notebook; the displayed final workflow uses Pandas-based aggregation and CSV export.

## Source Data
| File | Rows | Columns |
|---|---:|---:|
| `sales.csv` | 12,825,363 | 14 |
| `purchases.csv` | 2,372,474 | 16 |
| `begin_inventory.csv` | 206,529 | 9 |
| `end_inventory.csv` | 224,489 | 9 |
| `purchase_prices.csv` | 12,261 | 9 |
| `vendor_invoice.csv` | 5,543 | 10 |

## Workflow
1. Load the six CSV files with Pandas.
2. Aggregate sales and purchases at vendor and product levels.
3. Merge summaries and calculate gross-profit, margin, and freight-adjusted measures.
4. Compare beginning and ending inventory by `InventoryId`; calculate stock and estimated inventory-value changes.
5. Create performance categories using the notebook’s margin rules.
6. Run descriptive statistics, correlation analysis and IQR-based outlier detection.
7. Export summarized tables for Power BI and build three dashboard pages.

## Key Notebook / Dashboard Outputs
- **Total Sales:** `$598.06M`
- **Total Purchase:** `$420.33M`
- **Gross Profit (calculated proxy):** `$177.73M`
- **Profit After Freight:** `$175.58M`
- **Profit Margin:** `29.72%`
- **Product Sales shown on Page 2:** `$452.06M`
- **Product Gross Profit shown on Page 2:** `$130.47M`
- **Average Selling Price card:** `$34.77`
- **Average Purchase Price card:** `$21.81`
- **Inventory Value card:** `$65.21M`
- **Inventory Value Change card:** `-$2.84M`
- **Inventory movement:** 128,639 increased; 110,157 decreased; approximately 17,246 unchanged inventory IDs.
- **Product performance categories in notebook:** 8,250 high-margin rows; 1,077 low-margin rows; 1,950 loss/negative-profit rows.
- **IQR outlier detection:** 23 gross-profit rows flagged.
- **Correlations:** Sales vs Gross Profit `0.708`; Sales vs Purchase Dollars `0.775`; Gross Profit vs Profit After Freight 0.999985.

## Statistical Analysis
The notebook includes descriptive statistics, a correlation matrix, a gross-profit boxplot and IQR-based outlier detection. The attached notebook does **not** show an executed hypothesis test with p-values; statistical significance is therefore not claimed.

## Important Data-Quality Notes
- The notebook reports 127 distinct `VendorNo` values but the final vendor table has 148 rows; repeated vendor IDs/names and sales figures appear after merging invoice data. Investigate the vendor/invoice join and ensure one row per vendor before treating vendor totals and rankings as final.
- On Product & Pricing, the price chart axis reaches thousands while the KPI cards show average prices of $34.77 and $21.81; verify chart aggregation (use Average or a correctly defined measure).
- The Product Margin chart currently uses a sum of percentage values; use a properly defined margin measure for meaningful ranking.
- On Inventory Analysis, the right-hand chart title says “Inventory Value by City” while its axes show product description and inventory value change; fix the title or fields.
- Inventory value is estimated using stock quantity multiplied by the Price field and may not equal accounting inventory valuation.

## Setup
Install the Python packages used for the notebook:
bash
pip install pandas numpy matplotlib seaborn sqlalchemy jupyter

Open the notebook in Jupyter and update the source folder path to your local CSV directory. The raw CSV files are not included in this repository by default because of their size. The final summarized CSV outputs can be exported from the notebook for Power BI.

## Repository Structure 
business-performance-analytics/
├── notebook/
│   └── vendor_performance.ipynb
├── powerbi/
│   └── business_performance_analytics.pbix
├── outputs/
│   ├── final_vendor_analysis.csv
│   ├── final_product_analysis.csv
│   ├── inventory_analysis.csv
│   ├── vendor_category_summary.csv
│   └── product_category_summary.csv
├── screenshots/
│   ├── vendor-overview.png
│   ├── product-pricing.png
│   └── inventory-analysis.png
└── README.md

