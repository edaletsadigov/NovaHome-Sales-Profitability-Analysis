# `Ədalət_Sadıqov_NovaHome.pptx`

A 17-slide executive presentation summarizing the NovaHome Sales & Profitability analysis for a non-technical audience. Built from the same figures as the Power BI model (`Ədalət_Sadıqov_NovaHome.pbix`) and the underlying dataset (`NovaHome_Dataset.xlsx`).

## Structure

| Slide(s) | Section |
|---|---|
| 1 | Title |
| 2 | Business Overview — company context and the central question |
| 3 | Business Questions — all 10 questions at a glance |
| 4 | Key KPIs — Net Sales, Gross Profit, Contribution, Orders, Active Customers, AOV, Discount %, Return % |
| 5–13 | Analysis & Findings — one slide per business question (Q1–Q9), each with a chart and a one-line takeaway |
| 14 | Trends & Comparisons — 2025 YTD cumulative sales |
| 15 | Key Insights — 5 headline findings |
| 16 | Recommendations — 3 concrete actions (observation → evidence → action → metric to track) |
| 17 | Final Conclusion |

Question 10 (which products/channel to prioritize going forward) is a strategic question rather than a standalone metric — it is answered across the Recommendations and Final Conclusion slides instead of getting its own analysis slide.

## Design

- Custom "Warm Slate" palette (deep navy/purple `#1E1B4B`/`#3B2F6E`, orange accent `#EA580C`) matching the Power BI report theme for visual continuity between the deck and the dashboard.
- Native, editable PowerPoint charts (line, bar, combo, area) — not images — so every number can be re-checked or restyled directly in PowerPoint.
- Two slides (Q7 — repeat purchase, Q9 — discount scenario) include a methodology note because those measures were not yet built into the Power BI model at the time the deck was generated; the figures were computed from the same underlying `Fact_Orders` data and rules. As of the current `.pbix`, both are now implemented as real DAX measures (`Repeat Customer Rate`, `Scenario Gross Profit`), so the model and the deck are fully aligned.

## Data honesty

Every number in this deck traces back to `NovaHome_Dataset.xlsx` under the business rules documented in `README_dataset.md` (Completed orders only, returns/discount-adjusted Net Sales, weighted discount %, etc.). No figure was estimated or invented.

## How to open

Microsoft PowerPoint 2016+, or any OOXML-compatible viewer (Google Slides, LibreOffice Impress, Keynote via import). Charts are native and remain editable after opening.
