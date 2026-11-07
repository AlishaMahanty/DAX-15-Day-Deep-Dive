# Day 02 - Calculated Columns vs Measures

## 📌 Problem:

A junior analyst builds a Profit calculation. It works perfectly in the table.

Six months later, the same report has 40 such calculations. The .pbix file is now 600 MB, refreshes take 12 minutes, and nobody knows why.

Every one of those 40 calculations was created as a calculated column, even though most should have been measures.

### ❓ The question is:

Why does a calculated column increase file size and refresh time, while a measure costs almost nothing to store, even though both produce the same number on screen?

**Bonus Question:**

Name one situation where a calculated column is genuinely the right choice.

## 💡 Solution:

Calculated Column vs Measure: Where the Cost Hides

The main difference is when each one is calculated.

A calculated column is computed during data refresh. Its result is physically stored in the data model, with one value for every row. It increases file size and memory usage and is recomputed on every refresh.

A measure, on the other hand, is calculated at query time. Its result is not physically stored in the model. It runs only when a visual requests it and calculates based on the visual's filter context.

Therefore:
- 40 calculated columns = 40 stored columns increasing the model size.
- 40 measures = 40 small formulas calculated when needed.

**The bonus:**

A calculated column is useful when you need a row-level value for slicing or relating data, such as a Customer Segment, Date key, or category flag.

Rule of thumb:

- Aggregating? → Measure.
- Slicing or relating on a per-row value? → Calculated Column.

## ⭐ Key Takeaways:
- Calculated columns are computed during data refresh.
- Calculated column results are physically stored in the data model.
- Too many calculated columns can increase file size, memory usage and refresh time.
- Measures are calculated at query time and do not store their results in the model.
- Measures respond dynamically to the filter context of visuals.
- Use calculated columns for row-level values needed for slicing, filtering, or relationships.
- Use measures for aggregations and calculations that should respond to report interactions.
