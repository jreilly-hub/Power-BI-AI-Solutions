\# 🎯 KPI \& Scorecards



\## Category Overview



KPI \& Scorecards measures power executive dashboards, operational scorecards, and target-tracking visuals. These patterns compare actuals to targets, calculate variance (absolute and percentage), assign status indicators (RAG — Red/Amber/Green), and support conditional formatting logic driven entirely by measures.



\### P3 Alignment Notes



\- Keep target values in a dedicated Targets table joined to the Date and/or Product dimension — never hardcode thresholds in measures

\- Use `VAR` to compute Actual and Target once, then derive Variance and Status from those variables

\- Return numeric status codes (1/2/3) for KPI visuals and conditional formatting rules — not text strings

\- Prefer `SWITCH( TRUE(), … )` over nested `IF` for multi-threshold status logic



\---



\## Measures



| # | Measure | Description |

|---|---------|-------------|

| 1 | \*\*\[Actual Sales]\*\* | Core sales aggregation serving as the "Actual" leg of all KPI comparisons |

| 2 | \*\*\[Target Sales]\*\* | Target value pulled from the Targets table, aligned by date and category |

| 3 | \*\*\[Variance to Target]\*\* | Absolute difference: Actual − Target |

| 4 | \*\*\[Variance to Target %]\*\* | Percentage variance: (Actual − Target) ÷ Target, with divide-safe handling |

| 5 | \*\*\[KPI Status]\*\* | Numeric RAG indicator (1 = Red, 2 = Amber, 3 = Green) using `SWITCH( TRUE(), … )` |

| 6 | \*\*\[KPI Status Label]\*\* | Text label ("Below Target", "Near Target", "On Target") for tooltip display |

| 7 | \*\*\[Forecast Sales]\*\* | Simple linear forecast extending current-period trend into remaining periods |

| 8 | \*\*\[Forecast vs Target %]\*\* | Projected attainment: Forecast ÷ Target as a percentage |

| 9 | \*\*\[Attainment %]\*\* | Actual ÷ Target expressed as a percentage — the core attainment metric |

| 10 | \*\*\[Pacing Indicator]\*\* | Compares daily run-rate to required daily rate to hit target by period end |

| 11 | \*\*\[YoY Variance]\*\* | Current-year actual minus prior-year actual for year-over-year KPI tracking |

| 12 | \*\*\[Conditional Format Value]\*\* | Returns a value mapped to conditional formatting rules in Power BI visuals |



\---



\## Usage Notes



\- KPI visuals in Power BI expect numeric status values — use `\[KPI Status]` (1/2/3), not text

\- Threshold values (e.g., 90%, 100%) should come from a parameter table or the Targets table, not hardcoded

\- Pacing measures assume a linear distribution of target across the period — adjust for seasonality if needed



