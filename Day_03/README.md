# Day 03 - SUM vs SUMX

## 📌 Problem:

Your sales table has two columns: Quantity and Price. There is no line total column.

Your manager asks: "What's our total revenue?"

You try:

`Total Revenue = SUM(sales[Quantity]) * SUM(sales[Price])`

The number comes back, but it's wrong by a lot.

### ❓ The question is:

Why does summing the two columns and then multiplying give the wrong revenue, and which DAX function fixes it by doing the calculation row by row first?

**Bonus Question:**

Write the correct one-line formula.

## 💡 Solution:

`SUM` vs `SUMX`: Why the Order of Operations Matters

`SUM(Quantity) * SUM(Price)` multiplies two grand totals. It does not calculate revenue for each sale separately, so it mixes values from unrelated rows.

Imagine two sales:
- 10 units × ₹50 = ₹500
- 2 units × ₹500 = ₹1,000
Correct revenue = ₹1,500.

But `SUM(Quantity) * SUM(Price)` gives:

(10 + 2) × (50 + 500) = ₹6,600.

The correct function is SUMX.

`SUMX` is an iterator. It performs the calculation row by row and then adds all the results.

**The bonus:**

`Total Revenue = SUMX(sales, sales[Quantity] * sales[Price])`

The same row-by-row logic applies to other iterator functions such as `AVERAGEX`, `MAXX`, `MINX`, and `COUNTX`.

You could also create a calculated column for Quantity × Price and then use `SUM`, but `SUMX` performs the calculation directly without storing an additional column in the model.

## ⭐ Key Takeaways:

- `SUM` adds values from a single column.
- `SUMX` performs an expression row by row and then aggregates the results.
- Multiplying two column totals does not give the correct row-level revenue.
- Use an X function when each row needs its own calculation before aggregation.
- `SUMX` avoids creating an additional calculated column for this calculation.
