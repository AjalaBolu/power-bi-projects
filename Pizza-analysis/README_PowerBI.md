# Pizza Sales — Power BI Dashboard

Interactive dashboard built on the same `pizza_sales` dataset used in the SQL analysis, rebuilding each SQL finding as a visual and cross-checking the numbers match.

## File
`Pizza-sales.pbix`

## KPI Cards
| Metric | Value |
|---|---|
| Total Revenue | $817.86K |
| Total Orders | 21,350 |
| Total Pizza Sold | 49,574 |
| Avg Order Value | $38.31 |
| Avg Pizza Per Order | 2.32 |

## Visuals
- **Total Orders by Day** — column chart, Sunday–Saturday
- **Total Orders by Month** — area/trend chart, January–December
- **% of Sales by Category** — donut chart (Classic, Supreme, Chicken, Veggie)
- **% of Sales by Size** — donut chart (Small, Medium, Large, Extra-Large, Extra-Extra-Large)
- **Total Orders by Category** — horizontal bar chart

All visuals reconcile with the SQL findings from `README.md` (main SQL analysis) — e.g. Friday as the busiest day, July as the busiest month, Classic leading both revenue and volume, Large driving size revenue.

## Key DAX Measures

```dax
Avg Order Value = 
DIVIDE(
    SUM(pizza_sales[total_price]),
    DISTINCTCOUNT(pizza_sales[order_id])
)

Avg Pizza Per Order = 
DIVIDE(
    SUM(pizza_sales[quantity]),
    DISTINCTCOUNT(pizza_sales[order_id])
)
```

> `DISTINCTCOUNT` is the DAX equivalent of SQL's `COUNT(DISTINCT order_id)` — summing `order_id` directly (rather than distinct-counting it) was an early mistake caught during development, same class of bug as the SQL integer-division issue in Q5.

> `DIVIDE()` used instead of `/` for safe division — returns blank instead of erroring on a divide-by-zero, which matters once slicers/filters can produce empty subsets.

## Formatting Notes
- KPI cards default to "Auto" display units, which abbreviates values (e.g. `21.35K` instead of `21,350`). Fixed via **Format pane → Callout value → Display units → None**, plus setting the underlying field/measure format to **Whole Number** for thousands-separator commas.

## Tools
- Power BI Desktop
- DAX measures
- Power Query (data type corrections, imported from the same cleaned dataset used in SQL/Excel)
