# `NovaHome_Dataset.xlsx`

Synthetic 2-year transactional dataset (Jan 2024 – Dec 2025) for a home-goods retailer, used as the single source of truth for the Power BI model and the presentation in this repository.

## Sheets

| Sheet | Rows | Description |
|---|---|---|
| `Sales_2024` | 1,210 | Order-line transactions for 2024 |
| `Sales_2025` | 1,810 | Order-line transactions for 2025 |
| `Customers` | 240 | Customer master data (segment, city) |
| `Products` | 30 | Product master data (category, brand, unit cost) |
| `Regions` | 8 | City/zone mapping |
| `Targets` | 24 | Monthly company-wide sales target |
| `Dictionary` | — | Column definitions and business rules |

`Sales_2024` and `Sales_2025` share an identical schema and are appended into one transaction table before analysis.

## Key columns (Sales sheets)

| Column | Notes |
|---|---|
| `OrderID`, `OrderDate`, `CustomerID`, `ProductID`, `RegionID` | Keys |
| `Quantity`, `UnitPrice`, `UnitCost` | `UnitPrice` is **not** a fixed product attribute — it varies across orders for the same product (price changes over time / promotions) |
| `DiscountRate` | Decimal (e.g. `0.10` = 10%), already a fraction — do not divide by 100 again |
| `ReturnedQty` | Units returned; always ≤ `Quantity` |
| `ShippingCost` | Per-order shipping cost; not refunded on a return |
| `Channel` | Online / Store / B2B |
| `Status` | Completed / Cancelled / Pending |
| `Campaign` | No Campaign / Black Friday / Weekend / Return to Office |

## Data quality notes (found during cleaning)

- **20 exact duplicate rows** across the combined 2024+2025 data — removed via `Remove Duplicates`.
- **Leading/trailing whitespace** in `Channel`, `Status`, and `Campaign` text values (e.g. `" B2B "`) — cleaned via `Text.Trim`.
- **14.3% of all orders** are `Cancelled` or `Pending` — excluded from every financial measure per the project's business rules (only `Completed` orders count toward revenue, cost, or profit).
- `UnitPrice` has **6 distinct values per product** on average — it is a transactional fact, not a product dimension attribute (do not move it into the `Products`/`Dim_Products` table without preserving order-level history).

## Business rules used throughout this project

- **Net Sales** = `(Quantity − ReturnedQty) × UnitPrice × (1 − DiscountRate)` — a fully returned order therefore nets to `0`.
- **Net Cost** = `(Quantity − ReturnedQty) × UnitCost`.
- **Gross Profit** = `Net Sales − Net Cost`.
- **Contribution** = `Gross Profit − ShippingCost` (shipping is never refunded, even on a full return).
- **Weighted Discount %** = `total discount amount ÷ total original sales amount` (not a simple average of `DiscountRate`).
- `Targets` is company-wide only (no breakdown by region/segment/product) and applies at year/month grain.

## License / disclaimer

Synthetic data generated for a training/portfolio exercise. Not representative of any real company.
