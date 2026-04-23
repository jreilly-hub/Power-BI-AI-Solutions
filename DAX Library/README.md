\# 📊 DAX Pattern Library



A curated collection of \*\*100 production-ready DAX measures\*\* organized into 9 categories, designed for enterprise Power BI development.



\## Style Guide



All measures in this library follow \*\*P3 Adaptive\*\* conventions:



\- \*\*Explicit measures only\*\* — no calculated columns or precomputed summary tables in Fact tables

\- \*\*VAR for clarity\*\* — intermediate results assigned to variables for readability and debuggability

\- \*\*REMOVEFILTERS over ALL\*\* — preferred for clearing filter context

\- \*\*No EARLIER\*\* — replaced with modern iterator-safe patterns (SUMX, VAR, etc.)

\- \*\*Consistent naming\*\* — `\[Measure Name]` format with clear, descriptive names



\## Categories



| # | Category | Measures | Description |

|---|----------|----------|-------------|

| 1 | \[Time Intelligence](./01-time-intelligence/) | 12 | Period-over-period, rolling, and cumulative time calculations |

| 2 | \[Filters \& Context](./02-filters-and-context/) | 15 | Filter manipulation, context transition, and dynamic slicing |

| 3 | \[Aggregations \& Iterators](./03-aggregations-and-iterators/) | 11 | Row-by-row evaluation, ranking, and flexible aggregation |

| 4 | \[Modeling \& Relationships](./04-modeling-and-relationships/) | 10 | Virtual relationships, role-playing dimensions, and bridge patterns |

| 5 | \[KPI \& Scorecards](./05-kpi-and-scorecards/) | 12 | Target tracking, variance analysis, and conditional status indicators |

| 6 | \[Text \& Formatting](./06-text-and-formatting/) | 9 | Dynamic titles, conditional formatting values, and info measures |

| 7 | \[Row-Level Security](./07-row-level-security/) | 8 | RLS testing, dynamic security, and multi-role patterns |

| 8 | \[Performance Patterns](./08-performance-patterns/) | 11 | Optimization techniques, early filtering, and efficient aggregation |

| 9 | \[Advanced Patterns](./09-advanced-patterns/) | 12 | Cohort analysis, retention, semi-additive, and virtual tables |



\*\*Total: 100 measures\*\*



\## Folder Structure



```

dax-library/

├── README.md

├── 01-time-intelligence/

│   └── README.md

├── 02-filters-and-context/

│   └── README.md

├── 03-aggregations-and-iterators/

│   └── README.md

├── 04-modeling-and-relationships/

│   └── README.md

├── 05-kpi-and-scorecards/

│   └── README.md

├── 06-text-and-formatting/

│   └── README.md

├── 07-row-level-security/

│   └── README.md

├── 08-performance-patterns/

│   └── README.md

└── 09-advanced-patterns/

&#x20;   └── README.md

```



\## Usage



Each category README includes:

\- \*\*Category overview\*\* — purpose and when to apply these patterns

\- \*\*Measure listing\*\* — every measure with a concise description

\- \*\*P3 alignment notes\*\* — style and convention reminders specific to the category



Drop individual `.dax` files into each category folder alongside the README as you build out measure definitions.



\## Author



\*\*John Reilly\*\* — Power BI Analyst \& Developer | Enterprise Analytics Architecture



