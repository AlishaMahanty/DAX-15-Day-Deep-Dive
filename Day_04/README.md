# Day 04 - Row Context vs Filter Context

## 📌 Problem:

Yesterday, `SUMX` "walked each row" and multiplied Quantity by Price. But how does it know which Quantity and Price belong to the row it's on?

This works as a calculated column:

`Profit = sales[Revenue] - sales[Cost]`

But writing the same formula as a measure causes an error.

### ❓ The question is:

Why does Revenue - Cost work in a calculated column but break in a measure? What does the column have that the measure doesn't?

**Bonus Question:**

What's the one-word name for the context that lets a formula see a single row's values?

## 💡 Solution:

Row Context: The Thing a Measure Doesn't Have

DAX has two evaluation contexts:

Row Context: It means the formula is working on one specific row and can access that row's values.

It is active in calculated columns, `SUMX`, and `FILTER`. That's why Revenue minus Cost works as a calculated column: DAX evaluates it row by row.

Filter Context: It determines which rows are visible during a calculation. It comes from visuals, slicers, and `CALCULATE`.

A measure has no row context. It only has filter context. So, when a measure uses `sales[Revenue]`, DAX has no current row to identify which Revenue value to use.

The measure can be written as:

`Total Profit = SUM(sales[Revenue]) - SUM(sales[Cost])`

Or using `SUMX` to perform the calculation row by row:

`Total Profit = SUMX(sales, sales[Revenue] - sales[Cost])`

**The bonus:**

The one-word answer is Row Context.

## ⭐ Key Takeaways:

- DAX has two evaluation contexts: Row Context and Filter Context.
- Row context lets a formula access values from the current row.
- Calculated columns, `SUMX`, and `FILTER` use row context.
- Filter context determines which rows are visible during a calculation.
- Measures do not have row context by default.
- `SUMX` can perform row-by-row calculations within a measure.
