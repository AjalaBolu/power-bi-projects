# Sales Performance Analysis — Power BI

Part of the **Sales Performance Analysis** portfolio project (Phase 1: Data Analysis Foundations).
Built from the `Data` table in `Sales_Performance_Analysis.xlsx` (raw flat order-level data).

## Dashboard contents

**KPI Cards**
- Total Revenue — `SUM(sales)`
- Total Profit — `SUM(profit)`
- Order Count — distinct count of `order_id`
- Average Order Value — DAX measure: `SUM(sales) / DISTINCTCOUNT(order_id)`
- Profit Margin — DAX measure: `SUM(profit) / SUM(sales)`

**Visuals**
- Bar chart — Sales by Category, with drill-down to Sub-Category
- Line chart — Monthly Sales Trend (Year/Month hierarchy)

**Filters**
- Region slicer

## DAX measures

```dax
Avg Order Value = SUM(Data[sales]) / DISTINCTCOUNT(Data[order_id])

Profit Margin = SUM(Data[profit]) / SUM(Data[sales])
```

## Data prep notes

- `order_date` initially imported as a numeric type rather than a Date — fixed via **Transform Data** (Power Query) → right-click column → **Change Type** → **Date**, then **Close & Apply**. Without this fix, the date-based line chart won't render correctly.
- Only the raw `Data` table was loaded into Power BI (not the pre-aggregated Excel summary sheets) — Power BI does its own aggregation natively, so pivoted/summarized sheets aren't needed as a source.

## Files

- `Sales_Performance_Dashboard.pbix` — the Power BI report described above

## Possible next iterations

- Add a filled map visual (state/region) for geographic sales distribution
- Add a category or date-range slicer alongside the region slicer
- Formatting pass: consistent color theme, aligned card layout, page title
