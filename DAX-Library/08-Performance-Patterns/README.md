\# ⚡ Performance Patterns



\## Category Overview



Performance Patterns measures demonstrate optimization techniques that keep DAX queries fast at scale. These patterns minimize storage engine and formula engine overhead through early filtering, variable caching, efficient table scans, and deliberate avoidance of anti-patterns. Apply these techniques whenever a measure shows slow performance in DAX Studio's Server Timings.



\### P3 Alignment Notes



\- Use `VAR` to evaluate expensive expressions once and reference the variable multiple times

\- Apply filters as early as possible — inside `CALCULATE` arguments, not after aggregation

\- Prefer `REMOVEFILTERS` on specific columns over entire tables to preserve useful filters

\- Avoid `DISTINCTCOUNT` on high-cardinality text columns — pre-hash to integer keys in Power Query

\- Never use `FORMAT` or string conversion inside measures that feed other calculations



\---



\## Measures



| # | Measure | Description |

|---|---------|-------------|

| 1 | \*\*\[Optimized Sales Sum]\*\* | Baseline `SUM` with early column-level filtering inside `CALCULATE` for minimal scan |

| 2 | \*\*\[VAR-Cached Ratio]\*\* | Ratio measure computing numerator and denominator once in `VAR`, reused in `RETURN` |

| 3 | \*\*\[Early Filter Sales]\*\* | `CALCULATE` applying dimension filters before aggregation to reduce row scans |

| 4 | \*\*\[KEEPFILTERS Intersection]\*\* | Uses `KEEPFILTERS` to intersect (not replace) slicer filters for efficient context narrowing |

| 5 | \*\*\[Batch Iterator]\*\* | `SUMX` over a pre-filtered narrow table instead of the full fact table |

| 6 | \*\*\[SWITCH over Nested IF]\*\* | `SWITCH( TRUE(), … )` replacing deeply nested `IF` chains for readability and engine optimization |

| 7 | \*\*\[Divide-Safe Ratio]\*\* | `DIVIDE( numerator, denominator, 0 )` replacing manual `IF( denominator = 0, … )` checks |

| 8 | \*\*\[Pre-Filtered COUNTROWS]\*\* | `COUNTROWS( FILTER( table, condition ) )` with the narrowest possible table expression |

| 9 | \*\*\[Avoid DISTINCTCOUNT Anti-Pattern]\*\* | Integer-key based distinct count replacing high-cardinality text `DISTINCTCOUNT` |

| 10 | \*\*\[Materialized Subquery]\*\* | `VAR` capturing a `CALCULATETABLE` result once, then iterating over the cached table |

| 11 | \*\*\[SELECTEDVALUE over HASONEVALUE]\*\* | Modern `SELECTEDVALUE` with fallback replacing verbose `IF( HASONEVALUE( … ), VALUES( … ) )` |



\---



\## Usage Notes



\- Profile slow measures with \*\*DAX Studio → Server Timings\*\* to identify storage engine vs. formula engine bottlenecks

\- Storage engine queries are parallelizable; formula engine is single-threaded — push work to storage engine where possible

\- `VAR` is evaluated lazily in some contexts but always cached once evaluated — safe to use liberally

\- Test performance improvements with \*\*VertiPaq Analyzer\*\* to understand data distribution and cardinality



