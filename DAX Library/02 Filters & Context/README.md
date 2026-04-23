\# 🔍 Filters \& Context



\## Category Overview



Filters \& Context measures manipulate the filter context surrounding a calculation. These patterns are the backbone of dynamic, slicer-safe reporting — enabling measures that ignore, override, or reshape the filters applied by visuals, slicers, and row context.



Mastering context transition (`CALCULATE` converting row context to filter context) and explicit filter removal (`REMOVEFILTERS`) is essential for every production DAX model.



\### P3 Alignment Notes



\- Always use `REMOVEFILTERS` instead of `ALL` when the intent is to clear filters

\- Use `CALCULATE` + filter arguments — never rely on implicit context transition

\- Wrap complex filter expressions in `VAR` for readability and to avoid repeated evaluation

\- Prefer `KEEPFILTERS` when adding filters that should intersect (not replace) existing context



\---



\## Measures



| # | Measure | Description |

|---|---------|-------------|

| 1 | \*\*\[Total Sales All Regions]\*\* | Sales with all region filters removed via `REMOVEFILTERS( Dim\_Region )` |

| 2 | \*\*\[Total Sales Selected Category]\*\* | Sales filtered to the user's active category selection using `CALCULATE` + `KEEPFILTERS` |

| 3 | \*\*\[% of Grand Total]\*\* | Current-context sales divided by `CALCULATE( \[Total Sales], REMOVEFILTERS() )` |

| 4 | \*\*\[% of Parent]\*\* | Current value as a share of the parent group total using partial `REMOVEFILTERS` |

| 5 | \*\*\[% of Column Total]\*\* | Percentage contribution within the column's filter context in a matrix |

| 6 | \*\*\[Sales for Selected Customer]\*\* | Dynamic single-customer measure using `SELECTEDVALUE` with fallback |

| 7 | \*\*\[Sales Ignoring Date Filter]\*\* | Sales with date dimension filters removed for cross-period comparison |

| 8 | \*\*\[Has Selection]\*\* | Boolean flag detecting whether a slicer has an active selection via `ISFILTERED` |

| 9 | \*\*\[Dynamic Measure Selector]\*\* | Switch measure driven by a disconnected parameter table using `SELECTEDVALUE` + `SWITCH` |

| 10 | \*\*\[Filtered Customer Count]\*\* | Distinct customer count respecting all active visual and slicer filters |

| 11 | \*\*\[Cross-Filter Sales]\*\* | Sales calculated across a bidirectional relationship using `CROSSFILTER` |

| 12 | \*\*\[Sales with Context Transition]\*\* | Iterator-based measure demonstrating explicit `CALCULATE` inside `SUMX` for row-to-filter transition |

| 13 | \*\*\[Unfiltered Row Count]\*\* | Total row count ignoring all filters — baseline for filter-impact analysis |

| 14 | \*\*\[Slicer-Safe Average]\*\* | Average that responds correctly to multi-select slicers without double-counting |

| 15 | \*\*\[USERELATIONSHIP Override]\*\* | Sales calculated through an inactive relationship via `USERELATIONSHIP` in `CALCULATE` |



\---



\## Usage Notes



\- `REMOVEFILTERS` is preferred over `ALL` — same engine behavior, clearer intent

\- Always test context transition measures inside both card visuals and iterating visuals (matrix, table) to verify correct behavior

\- Disconnected parameter tables should have no relationships to the data model



