\# 🧠 Advanced Patterns



\## Category Overview



Advanced Patterns measures tackle the most complex analytical scenarios in Power BI — cohort analysis, customer retention, semi-additive aggregations (balances, inventory), virtual tables, and dynamic segmentation. These patterns combine multiple DAX techniques (iterators, context manipulation, time intelligence) into sophisticated, production-grade calculations.



Many of these measures originated from real-world cohort modeling and retention analytics work, refined to be \*\*cohort-safe, context-leak-free, and stable\*\* inside matrices, tooltips, and drill-through pages.



\### P3 Alignment Notes



\- Use `VAR` extensively to isolate each logical stage — acquisition context, retention window, and aggregation

\- Never use `EARLIER` — replace with `VAR` captured outside the iterator or explicit `CALCULATE` context transitions

\- Use `REMOVEFILTERS` for semi-additive measures that must ignore date filters and re-apply a single date point

\- Prefer `SELECTEDVALUE` with a fallback over `HASONEVALUE` + `VALUES` for cleaner single-value extraction

\- Test all cohort measures in a matrix visual with cohort on rows and period offset on columns



\---



\## Measures



| # | Measure | Description |

|---|---------|-------------|

| 1 | \*\*\[Cohort Customers]\*\* | Counts distinct customers whose first transaction falls within the selected cohort period |

| 2 | \*\*\[Cohort Retention %]\*\* | Percentage of cohort customers who returned in a given offset period relative to acquisition |

| 3 | \*\*\[Cohort Revenue]\*\* | Total revenue attributed to customers acquired in the cohort period, across all subsequent periods |

| 4 | \*\*\[Returned Customers]\*\* | Distinct count of customers from the acquisition cohort who transacted in the offset period |

| 5 | \*\*\[New Customers]\*\* | Customers whose earliest transaction date falls within the current filter context |

| 6 | \*\*\[Lost Customers]\*\* | Customers active in the prior period but absent in the current period |

| 7 | \*\*\[Customer Lifetime Value]\*\* | Cumulative revenue per customer from acquisition through the current period |

| 8 | \*\*\[Semi-Additive Balance]\*\* | Closing balance using `LASTDATE` — ignores date aggregation to return the period-end snapshot |

| 9 | \*\*\[Opening Balance]\*\* | Balance as of the first date in the current filter context using `FIRSTDATE` |

| 10 | \*\*\[Dynamic Segmentation]\*\* | Assigns customers to value segments (High / Medium / Low) based on measure results, not static columns |

| 11 | \*\*\[Virtual Table Aggregation]\*\* | Builds an in-memory table via `SUMMARIZE` + `ADDCOLUMNS`, then aggregates over it |

| 12 | \*\*\[ABC Classification]\*\* | Pareto-based classification (A/B/C) using cumulative percentage of total, calculated via `RANKX` and running totals |



\---



\## Usage Notes



\- \*\*Cohort measures\*\* require a clean acquisition-date column on the customer dimension — compute this in Power Query, not DAX

\- Semi-additive measures (`\[Semi-Additive Balance]`, `\[Opening Balance]`) must use `LASTDATE` / `FIRSTDATE` inside `CALCULATE` — never `MAX` / `MIN` on the date column

\- Test `\[Cohort Retention %]` in a matrix with Cohort Month on rows and Offset on columns to verify no context leaks

\- `\[Dynamic Segmentation]` recalculates in every filter context — for performance-critical scenarios, consider materializing segments in Power Query

\- Virtual table measures using `SUMMARIZE` + `ADDCOLUMNS` should reference only dimension columns in `SUMMARIZE` and add measures via `ADDCOLUMNS`



