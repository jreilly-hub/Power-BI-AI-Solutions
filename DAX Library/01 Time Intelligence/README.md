\# 📅 Time Intelligence



\## Category Overview



Time Intelligence measures handle period-over-period comparisons, running totals, rolling windows, and cumulative calculations. These patterns depend on a properly configured \*\*Date table\*\* marked as the model's date dimension, with a contiguous range of dates and no gaps.



All measures in this category use `DATEADD`, `DATESYTD`, `DATESINPERIOD`, and related Time Intelligence functions — never manual date arithmetic on raw columns.



\### P3 Alignment Notes



\- Use `VAR` to capture the current-period result before calculating the prior period

\- Wrap time-shift logic in `CALCULATE` + `DATEADD` or equivalent — never filter on year/month number columns

\- Prefer `REMOVEFILTERS` over `ALL` when clearing date filters for cumulative patterns



\---



\## Measures



| # | Measure | Description |

|---|---------|-------------|

| 1 | \*\*\[Total Sales YTD]\*\* | Year-to-date running total of sales using `DATESYTD` |

| 2 | \*\*\[Total Sales PY]\*\* | Prior year total sales shifted via `DATEADD( …, -1, YEAR )` |

| 3 | \*\*\[Total Sales YoY %]\*\* | Year-over-year percentage change comparing current to prior year |

| 4 | \*\*\[Total Sales QTD]\*\* | Quarter-to-date accumulation using `DATESQTD` |

| 5 | \*\*\[Total Sales MTD]\*\* | Month-to-date accumulation using `DATESMTD` |

| 6 | \*\*\[Total Sales PM]\*\* | Prior month total sales via `DATEADD( …, -1, MONTH )` |

| 7 | \*\*\[Total Sales MoM %]\*\* | Month-over-month percentage change |

| 8 | \*\*\[Rolling 3M Sales]\*\* | Trailing 3-month rolling sum using `DATESINPERIOD` |

| 9 | \*\*\[Rolling 12M Sales]\*\* | Trailing 12-month rolling sum for trend smoothing |

| 10 | \*\*\[Sales PYTD]\*\* | Prior-year-to-date sales for aligned YTD comparison |

| 11 | \*\*\[YTD Growth %]\*\* | YTD vs. PYTD percentage growth |

| 12 | \*\*\[Days in Current Period]\*\* | Count of dates in the active filter context for daily-rate calculations |



\---



\## Usage Notes



\- Ensure the Date table is marked as a \*\*Date Table\*\* in the model (`MARK AS DATE TABLE`)

\- These measures assume a single, unbroken Date dimension with a `Date\[Date]` column

\- Rolling measures use `DATESINPERIOD` anchored to `MAX( Date\[Date] )` for slicer-safe behavior



