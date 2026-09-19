# NovaHome — Sales & Profitability Analysis

A retail analytics project built on a synthetic 2-year sales dataset for **NovaHome**, a home-goods retailer (electronics, appliances, furniture, kitchen, accessories). The project answers a single core question for management:

> **"If sales grow, does the company's profit grow at the same rate?"**

Built as part of the **DataCube Power BI Capstone Project**.

## Repository contents

| File | Description | README |
|---|---|---|
| `NovaHome_Dataset.xlsx` | Raw source data — 7 sheets (Sales 2024, Sales 2025, Customers, Products, Regions, Targets, Dictionary) | [README_dataset.md](README_dataset.md) |
| `Ədalət_Sadıqov_NovaHome.pbix` | Power BI data model, DAX measures, and 3-page interactive report | [README_pbix.md](README_pbix.md) |
| `Ədalət_Sadıqov_NovaHome.pptx` | 17-slide executive presentation of findings and recommendations | [README_pptx.md](README_pptx.md) |

## Tech stack

- **Microsoft Power BI Desktop** — data modeling, DAX, report pages, What-If parameter
- **Power Query** — data cleaning (deduplication, whitespace trimming, table append)
- **Microsoft PowerPoint** — executive summary deck

## The 10 business questions

1. Does sales growth match profit growth (2024 → 2025)?
2. Is the best-selling product also the most profitable one?
3. Which category has strong sales but a weak margin?
4. Which products/channels have the highest return rates?
5. How did the Black Friday campaign perform — sales vs. profit?
6. Which region sells the most, and which has the best margin?
7. Which customer segment has the highest AOV and repeat-purchase rate?
8. Which months missed the sales plan, and by how much?
9. How would an extra 5%/10% discount affect profit?
10. Which 2 products and which channel should the business prioritize going forward?

## Key findings

| # | Question | Finding |
|---|---|---|
| 1 | Growth alignment | Net Sales grew **+53.9%** (2024→2025) but Gross Profit grew only **+35.0%** — profit is not keeping pace with sales |
| 2 | Best-seller vs. most profitable | **Laptop** is the #1 product by revenue but has only a **13.4%** gross margin; **Wardrobe** ranks #4 in revenue but has a **38.5%** margin |
| 3 | Category margin | **Electronics** is the 2nd-largest category by revenue (1.37M ₼) but has the **weakest margin (14.1%)** of all 5 categories |
| 4 | Returns | **Online** channel has the highest return rate (4.98% vs. 2.86% for B2B); **Sofa** is the riskiest product by both return value (25.7K ₼) and rate (7.8%) |
| 5 | Black Friday | Generates 507.6K ₼ in sales but only **-355 ₼** in Gross Profit — a weighted discount of 29.1% erases the campaign's profitability |
| 6 | Regional performance | **Absheron** zone leads in sales (1.95M ₼); **Sumgait** leads in contribution margin (26.0%) despite lower volume than Baku |
| 7 | Customer segments | **Corporate** has the highest AOV (3,893 ₼, ~4× Retail) and the most consistent repeat-purchase behavior |
| 8 | Plan adherence | **18 of 24 months (75%)** missed the sales target, with a combined shortfall of **-335,940 ₼** in the missed months |
| 9 | Discount sensitivity | A flat +5% discount cuts Gross Profit by **-20.2%**; +10% cuts it by **-40.4%** — profit is highly discount-sensitive |
| 10 | Forward focus | Prioritize **Wardrobe** and **Sofa** (high margin) and the **Corporate** channel (highest AOV + retention); rework Black Friday's discount depth first |

## Data & methodology notes

- All revenue figures use only **Completed** orders (Cancelled/Pending orders are excluded from financial metrics per the project's business rules).
- **Net Sales** = (Quantity − Returned Qty) × Unit Price × (1 − Discount Rate); a fully returned order nets to zero.
- **Gross Profit** = Net Sales − Net Cost (COGS); **Contribution** = Gross Profit − Shipping Cost.
- Discount % is **weighted** (discount amount ÷ original sales amount), not a simple average.
- Two questions (repeat-purchase rate, discount scenario) required measures/parameters not originally in the model; these were added (see `README_pbix.md`) so every question is answered from the model itself.

## Suggested repo structure

```
NovaHome-Sales-Profitability-Analysis/
├── README.md                          ← this file
├── data/
│   ├── NovaHome_Dataset.xlsx
│   └── README_dataset.md
├── powerbi/
│   ├── Ədalət_Sadıqov_NovaHome.pbix
│   └── README_pbix.md
└── presentation/
    ├── Ədalət_Sadıqov_NovaHome.pptx
    └── README_pptx.md
```

## Author

Ədalət Sadıqov — Data Analyst Intern, Baku, Azerbaijan
[GitHub](https://github.com/edaletsadigov) · [LinkedIn](https://linkedin.com/in/edaletsadigov)

## Disclaimer

The dataset is synthetic and generated for training/portfolio purposes. Findings should not be interpreted as facts about any real business.
