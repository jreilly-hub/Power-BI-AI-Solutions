\# 🔒 Row-Level Security



\## Category Overview



Row-Level Security (RLS) measures support dynamic, role-based data access control within Power BI. These patterns enable testing, validation, and flexible security models — from simple single-dimension filtering to complex multi-role and hierarchy-based security. RLS logic lives in DAX filter expressions on tables, but these companion measures help you \*\*validate, debug, and extend\*\* your security implementation.



\### P3 Alignment Notes



\- RLS filter expressions should be as simple as possible — push complexity into the data model, not the DAX filter

\- Use `USERPRINCIPALNAME()` for Azure AD–backed security; use `USERNAME()` only for on-premises models

\- Test all RLS roles with `VIEW AS ROLE` in Power BI Desktop before publishing

\- Never use `REMOVEFILTERS` to bypass RLS in production measures — RLS filters are engine-enforced and cannot be overridden by DAX



\---



\## Measures



| # | Measure | Description |

|---|---------|-------------|

| 1 | \*\*\[Current User Email]\*\* | Returns `USERPRINCIPALNAME()` for display in a test card visual to verify identity resolution |

| 2 | \*\*\[RLS Active Flag]\*\* | Boolean indicator showing whether any RLS role is currently filtering the model |

| 3 | \*\*\[Accessible Rows Count]\*\* | `COUNTROWS` of the primary fact table — verifies the scope of data visible under the active role |

| 4 | \*\*\[Accessible Region List]\*\* | `CONCATENATEX` listing all regions visible to the current user under RLS |

| 5 | \*\*\[Dynamic RLS Lookup]\*\* | Checks the security mapping table for the current user's allowed dimension values |

| 6 | \*\*\[Hierarchy-Based Access]\*\* | Navigates a manager hierarchy via `PATH` to determine inherited data access |

| 7 | \*\*\[Multi-Role Intersection]\*\* | Validates behavior when a user belongs to multiple RLS roles (union of access) |

| 8 | \*\*\[RLS Test — Expected vs Actual]\*\* | Compares expected row count for a role against actual filtered row count for automated validation |



\---



\## Usage Notes



\- RLS is enforced by the Analysis Services engine — DAX measures \*\*cannot override\*\* RLS filters, even with `REMOVEFILTERS`

\- Dynamic RLS requires a security mapping table (User → Dimension Key) joined to the model

\- Always validate RLS with both "View as Role" in Desktop and the Power BI Service security testing feature

\- Hierarchy-based RLS (manager sees all direct reports' data) requires a `PATH`-based security filter on the fact table



