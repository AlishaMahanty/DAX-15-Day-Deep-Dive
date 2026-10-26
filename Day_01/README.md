# Day 01 - Filter Context

## 📌 Problem:

You drag a Total Sales measure into a card. It shows ₹4.2 crore.

Then you drag that same measure into a table next to City. Now Mumbai shows ₹80 lakh, Delhi ₹65 lakh, and Pune ₹40 lakh.

Same formula. Different numbers in every row. You never wrote any filter.

### ❓ The question is:

What invisible thing is changing the number, and why does this make a DAX measure fundamentally different from an Excel formula?

**Bonus Question:**

In one line, when would you build a calculated column instead of a measure?

## 💡 Solution:

Why one measure shows a different number in every row

The invisible thing is **Filter Context**.

An Excel formula evaluates using its cell references. For example, `=SUM(B2:B100)` always sums the same fixed range.

A DAX measure does not have a fixed range. It calculates based on the filters applied to the data.

For example: `Total Sales = SUM(sales[amount])`

The measure calculates the sum of the amount column, but the rows included in that calculation depend on where the measure is used.

- In a card: With no filters, it sums all sales → ₹4.2 crore.
- In a table beside City: The row filters sales to that city before calculating the total → Mumbai ₹80 lakh.

You never wrote the city filter. The visual created it.

That set of active filters is called **Filter Context**. A measure recalculates within the context in which it is evaluated.

This is one of the fundamental concepts behind DAX.

**The bonus:**

Use a measure for aggregations that should respond to slicers and visual filters. Use a calculated column for row-level values that need to be stored and used for filtering or relationships.

For example,

DAX Measure

`Total Sales = SUM(sales[amount])`

The same measure returns different values depending on the filter context in which it is evaluated.

Calculated Column

`Profit = sales[revenue] - sales[cost]`

This calculates profit for each row and stores the result as a calculated column.

## ⭐ Key Takeaways:

- Filter context determines which rows are included in a DAX calculation.
- The same measure can return different values depending on the visual and its filters.
- A card and a table can display different results from the same measure.
- DAX measures are evaluated dynamically based on their filter context.
- Measures are useful for aggregations that respond to slicers and filters.
- Calculated columns store row-level values that can be used for filtering and relationships.
- If a number needs to change when placed in different charts, a measure is generally the right choice.
