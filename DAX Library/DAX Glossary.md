.



📘 DAX Glossary / Dictionary

A reference guide for enterprise‑grade semantic modeling in Power BI \& Fabric



🔍 Purpose

This glossary provides clear, business‑friendly definitions of the most important DAX functions, patterns, and modeling concepts used throughout this repository.

It is designed to support:



BI developers



Analytics engineers



Data modelers



Architects



Power BI governance teams



🧠 Core DAX Concepts

Measure

A reusable calculation evaluated at query time. Measures respect filter context and do not store data.



Row Context

The concept of “current row” when iterating over a table (e.g., inside SUMX).

Measures do not have row context unless created by an iterator.



Filter Context

The set of filters applied to a calculation.

CALCULATE modifies filter context.



Context Transition

When CALCULATE converts row context into filter context.

Used carefully to avoid performance issues.



🧮 Aggregation Functions

SUM()

Adds up numeric column values.



AVERAGE()

Returns the arithmetic mean of a numeric column.



MIN() / MAX()

Returns the smallest or largest value in a column.



COUNT() / COUNTA()

Counts rows or non‑blank values.



DISTINCTCOUNT()

Counts unique values in a column.



🔁 Iterator Functions (X‑Functions)

Iterators evaluate an expression row‑by‑row.



SUMX()

Iterates a table and sums the expression result.



AVERAGEX()

Iterates a table and averages the expression result.



MINX() / MAXX()

Returns min/max of an expression evaluated row‑by‑row.



COUNTX()

Counts rows where the expression returns non‑blank.



RANKX()

Ranks values in a table based on an expression.



📅 Time Intelligence Functions

DATESYTD() / DATESMTD() / DATESQTD()

Returns a date range for year‑to‑date, month‑to‑date, or quarter‑to‑date.



DATEADD()

Shifts dates forward or backward (e.g., prior month).



SAMEPERIODLASTYEAR()

Returns the same date range one year earlier.



DATESINPERIOD()

Returns a rolling window (e.g., last 12 months).



TOTALYTD()

A wrapper for YTD calculations (less flexible than DATESYTD).



🧩 Filter \& Context Functions

CALCULATE()

Modifies filter context and evaluates an expression.

The most important function in DAX.



FILTER()

Returns a table filtered by a logical expression.



REMOVEFILTERS()

Clears filters from a table or column.



ALL()

Removes filters but keeps table structure.



ALLSELECTED()

Respects user selections but removes visual‑level filters.



ALLEXCEPT()

Removes all filters except those on specified columns.



KEEPFILTERS()

Adds filters without overwriting existing ones.



VALUES()

Returns a one‑column table of distinct values.



SELECTEDVALUE()

Returns the selected value or a default.



🔗 Relationship \& Modeling Functions

USERELATIONSHIP()

Activates an inactive relationship for a calculation.



CROSSFILTER()

Temporarily changes relationship direction (use sparingly).



TREATAS()

Applies a virtual relationship between tables.



RELATED()

Pulls a value from a related table (row context required).



RELATEDTABLE()

Returns rows from a related table.



🧱 Table Construction Functions

SUMMARIZE()

Groups data by columns (use carefully — can be misused).



SUMMARIZECOLUMNS()

Optimized grouping function for measure evaluation.



ADDCOLUMNS()

Adds calculated columns to a table expression.



GROUPBY()

Groups data using CURRENTGROUP() for advanced aggregations.



TOPN()

Returns the top N rows based on an expression.



UNION() / INTERSECT() / EXCEPT()

Set‑based table operations.



🧬 Advanced Modeling Functions

PATH()

Builds a parent‑child hierarchy path.



PATHITEM()

Returns a specific level from a PATH.



ISINSCOPE()

Detects the current hierarchy level in visuals.



HASONEVALUE()

Checks if a column has exactly one value in context.



ISFILTERED()

Checks if a column or table is filtered.



🔐 Row‑Level Security Functions

USERPRINCIPALNAME()

Returns the logged‑in user’s email.



USERNAME()

Returns the user identity (varies by environment).



LOOKUPVALUE()

Finds a value in a table based on search conditions.



🎨 Formatting \& UX Functions

FORMAT()

Converts a value to text using a format string.



UNICHAR()

Returns a Unicode character (arrows, bullets, icons).



CONCATENATEX()

Concatenates text values from a table.



🧮 Math \& Statistical Functions

DIVIDE()

Safe division that avoids divide‑by‑zero errors.



PERCENTILEX.INC() / PERCENTILEX.EXC()

Percentile calculations over a table.



MEDIANX()

Median of an expression evaluated row‑by‑row.



🧠 Calculation Groups (Conceptual)

SELECTEDMEASURE()

Returns the measure currently being evaluated.



SELECTEDMEASURENAME()

Returns the name of the active measure.



Format String Expression

Defines dynamic formatting for a calculation item.



🧭 Best Practices Summary

Prefer measures over calculated columns.



Use REMOVEFILTERS instead of ALL when clearing context.



Use SUMMARIZECOLUMNS instead of SUMMARIZE for measure logic.



Avoid bi‑directional relationships unless required.



Use VAR to improve readability and performance.



Avoid row context unless necessary (prefer aggregators).



Use TREATAS for virtual relationships.



Use USERELATIONSHIP for role‑playing date tables.

