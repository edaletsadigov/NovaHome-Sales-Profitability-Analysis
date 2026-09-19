# `Ədalət_Sadıqov_NovaHome.pbix`

The Power BI data model and interactive report for the NovaHome Sales & Profitability analysis. Built on `NovaHome_Dataset.xlsx`.

## Data model

| Table | Role | Source |
|---|---|---|
| `Fact_Orders` | Fact table — one row per order line | `Sales_2024` + `Sales_2025` appended in Power Query, deduplicated, trimmed |
| `Dim_Customers` | Customer dimension (segment, city) | `Customers` |
| `Dim_Products` | Product dimension (category, brand) | `Products` |
| `Dim_Regions` | Region dimension (city, zone) | `Regions` |
| `Dim_Targets` | Monthly company-wide sales target | `Targets` |
| `DimTarix` | Date table, marked as the model's Date table | Generated (`Jan 2024 – Dec 2025`) |
| `Əlavə Endirim %` | Disconnected What-If parameter table (0–15%) | Generated via `Modeling → New Parameter` |
| `Summary stats` | Manual data-cleaning log (rows before/after dedup) | Manual entry |

**Relationships:** `Fact_Orders` connects to `Dim_Customers`, `Dim_Products`, and `Dim_Regions` on their respective IDs (single-direction, M:1). `DimTarix` and `Dim_Targets` are linked into calculations through `TREATAS`/`CALCULATE` filter logic inside the measures rather than always relying on a physical relationship — this is intentional so that year/month filtering works without cross-filter ambiguity.

## Report pages

1. **Sales Overview** — KPI cards, monthly Net Sales vs. Target trend, category/channel/segment breakdown, zone map
2. **Product Analysis** — Top products by sales and by profit, category margin comparison, product-in-category share
3. **Regional Breakdown** — City/zone sales and margin, full regional table
4. **Customer Breakdown** — Segment AOV, Active Customers, Repeat Customer count/rate
5. **What if** — Interactive discount scenario page using the `Əlavə Endirim %` parameter

## Measures (grouped)

**Core financials:** `Net Sales`, `Gross Sales`, `Net Cost`, `Gross Profit`, `Gross Profit Margin %`, `Contribution`, `Margin %`, `Shipping Cost (Completed)`, `Total Revenue (000)`

**Orders & customers:** `Orders (Completed)`, `AOV`, `Active Customer Count`, `Repeat Customer Count`, `Repeat Customer Rate`, `Avg Discount Rate`, `Cancel Rate`, `Return Rate`, `Return Value`

**Time intelligence:** `Net Sales YTD`, `Revenue YoY %`, `Gross Profit YoY %`, `Completed Orders YoY %`, `Cancel Rate YoY %`, `Return Rate YoY (pp)`, plus fixed-year variants (`Revenue 2024/2025`, `Completed Orders 2024/2025`, `Returned Qty 2024/2025`) used for side-by-side year cards

**Plan vs. actual:** `Sales Target` (+ 2024/2025 variants), `Target var`, `Target Var % 2024/2025`, `Target Status` (+ 2024/2025 variants)

**Share & ranking:** `Category Revenue Share %`, `Product Category Share %`, `Channel Revenue Share %`, `Zone Revenue Share %`, `City Revenue Share %`, `Campaign Revenue Share %`, `City Rank`, `City vs Top City %`, `Category Rank`, `Zone City Count`

**What-If scenario:** `Əlavə Endirim % Value`, `Scenario Net Sales`, `Scenario Gross Profit`, `Profit Impact %`

**Tooltips:** dedicated multi-measure tooltip strings per dimension (`Tooltip Text Category/Channel/City/Segment/Zone/Campaign/2024/2025`)

## Business rules encoded in the measures

- All financial measures filter to `Status = "Completed"` — Cancelled/Pending orders never enter Net Sales, Cost, or Profit.
- `Net Sales` accounts for returns and discount in one formula: `(Quantity − ReturnedQty) × UnitPrice × (1 − DiscountRate)`.
- `Avg Discount Rate` is **weighted** (discount amount ÷ original sales amount), not a plain average of the `DiscountRate` column.
- Year-over-year measures return blank automatically for 2024 (no prior year exists in the 2024–2025 date table).
- The What-If discount scenario keeps `Quantity`, `ReturnedQty`, cost, and shipping constant — only the discount applied to existing Net Sales changes.

## Known limitation

Automated relationship extraction (used to audit this model) does not surface the `DimTarix ↔ Fact_Orders` link, even though it is active in the model and confirmed working in the report (year/month filters correctly change every card and chart). This appears to be a limitation of the auditing tool rather than the model — worth double-checking directly in Power BI's Model View if you fork this project.

## How to open

1. Requires Power BI Desktop (free) — File → Open → select the `.pbix`.
2. If prompted, point the data source to your local copy of `NovaHome_Dataset.xlsx`.
