\# ✏️ Text \& Formatting



\## Category Overview



Text \& Formatting measures produce dynamic titles, labels, tooltips, and conditional formatting values that make reports self-documenting and context-aware. These "info measures" respond to slicer selections, filter context, and user interactions — eliminating hardcoded text boxes and static labels.



\### P3 Alignment Notes



\- Use `VAR` to build components of dynamic strings before concatenating in `RETURN`

\- Use `SELECTEDVALUE` with a fallback string (e.g., `"All"`) for slicer-aware titles

\- Return `BLANK()` instead of empty strings `""` to avoid visual clutter

\- Format numbers inside measures using `FORMAT` only for display-only measures — never for measures used in calculations



\---



\## Measures



| # | Measure | Description |

|---|---------|-------------|

| 1 | \*\*\[Dynamic Report Title]\*\* | Concatenates selected dimension values into a context-aware page title |

| 2 | \*\*\[Selected Period Label]\*\* | Returns a human-readable label for the active date filter (e.g., "Q2 2025") |

| 3 | \*\*\[Last Refreshed Timestamp]\*\* | Displays the data model's last refresh date/time for report transparency |

| 4 | \*\*\[Formatted Sales]\*\* | Sales value pre-formatted with currency symbol and thousands separator via `FORMAT` |

| 5 | \*\*\[Conditional Icon]\*\* | Returns a Unicode icon (✅ ⚠️ ❌) based on KPI status thresholds |

| 6 | \*\*\[Tooltip Summary]\*\* | Multi-line text measure combining key metrics for rich tooltip display |

| 7 | \*\*\[No Data Message]\*\* | Returns a user-friendly message when the current context yields `BLANK()` |

| 8 | \*\*\[Slicer Instruction Text]\*\* | Dynamic instruction text that disappears once the user makes a slicer selection |

| 9 | \*\*\[Rank Label]\*\* | Ordinal rank text (e.g., "1st", "2nd", "3rd") derived from `\[Rank by Sales]` |



\---



\## Usage Notes



\- Display-only measures (titles, labels, tooltips) should \*\*never\*\* be used in calculations or other measures

\- `FORMAT` returns text — any measure using `FORMAT` loses numeric sorting and aggregation capability

\- Test dynamic titles with multiple slicer combinations to ensure clean output in all states



