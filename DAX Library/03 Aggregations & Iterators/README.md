\# 🔢 Aggregations \& Iterators



\## Category Overview



Aggregations \& Iterators measures go beyond simple `SUM` and `AVERAGE` by evaluating expressions \*\*row by row\*\* across a table. Iterator functions (`SUMX`, `AVERAGEX`, `MINX`, `MAXX`, `RANKX`, `COUNTX`) enable calculations that depend on per-row logic — weighted averages, conditional counts, rankings, and flexible aggregations that simple aggregators cannot express.



\### P3 Alignment Notes



\- Use `VAR` inside iterators to capture intermediate row-level results before the final aggregation

\- Never use `EARLIER` — use `VAR` outside the iterator or nest `CALCULATE` for context transitions

\- Prefer `DISTINCTCOUNT` over `COUNTROWS( DISTINCT( … ) )` for cleaner syntax

\- Use `SUMX` over calculated columns for row-level multiplication (e.g., Quantity × Price)



\---



\## Measures



| # | Measure | Description |

|---|---------|-------------|

| 1 | \*\*\[Total Revenue]\*\* | `SUMX` over line items calculating Quantity × Unit Price per row |

| 2 | \*\*\[Weighted Average Price]\*\* | Revenue-weighted average unit price using `SUMX` ÷ `SUM` |

| 3 | \*\*\[Distinct Customer Count]\*\* | `DISTINCTCOUNT` of customer key across all transactions |

| 4 | \*\*\[Conditional Sales Count]\*\* | `COUNTX` + `IF` counting only rows meeting a threshold condition |

| 5 | \*\*\[Rank by Sales]\*\* | Dense rank of the current item by total sales using `RANKX` with `DENSE` |

| 6 | \*\*\[Top N Sales]\*\* | Sales filtered to the top N items via `TOPN` inside `CALCULATE` |

| 7 | \*\*\[Running Total]\*\* | Cumulative sum across a sorted dimension using iterator + filter pattern |

| 8 | \*\*\[Median Sales]\*\* | `MEDIANX` over a dimension to find the midpoint value |

| 9 | \*\*\[Product of Values]\*\* | `PRODUCTX` across rows — useful for compound growth calculations |

| 10 | \*\*\[Concatenated List]\*\* | `CONCATENATEX` building a comma-separated list of dimension values |

| 11 | \*\*\[Max Transaction Amount]\*\* | `MAXX` returning the single largest transaction value in context |



\---



\## Usage Notes



\- Iterators scan every row of the table expression — keep the table as narrow as possible for performance

\- `RANKX` defaults to `SKIP` tie-handling; use `DENSE` explicitly when rank gaps are undesirable

\- `TOPN` returns a table — wrap it in `CALCULATE` + `KEEPFILTERS` or use inside `SUMX` for the aggregated result



