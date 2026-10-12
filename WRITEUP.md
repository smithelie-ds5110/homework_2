# Homework 2 — Write-Up

## Task 0 — Descriptive Analysis

The revenue dataset contains 5 rows and 13 columns. It is not tidy because the quarterly revenue values are represented by separate column headers rather than a single quarter variable. This violates the rule that each variable should have its own column. The orders dataset contains 20 rows and 5 columns and the shipments data set contains 35 rows and 2 columns. Both of these datasets are tidy because they adhere to the rules of a tidy dataset - each variable is represented with a column, each observation is represented with a row and each value occupies a single cell.
Before applying any transformations, I applied visualizations to each of the raw data sets - barplots for revenue and orders, a countplot for shipments.

## Task 1 — Revenue Table

The revenue data set is not tidy because it violates the rule that each variable must be represented by a single column. In this case, the quarterly values are represented as column headers when instead, we should have a quarters column with those headers as values. This is the reason why it is wide. I used the melt method of the pandas dataframe object to reshape the data into long format, producing 60 rows with 3 columns: company, quarter and revenue. With this, each row now represents one observation of revenue across company and quarter, which satisfies the tidy rule that was previously being violated.

## Task 2 — Duplicate Keys

I checked order_id for duplicates in the orders and shipments data sets. It is unique in orders but not in shipments so this produces a one-to-many relationship. In other words, one order can produce multiple rows after joining, depending on the matching number of shipments.

## Task 3 — Join Orders and Shipments

I performed an inner join using order_id and calculated the mean order amount per customer using both the joined table as well as the original orders table.
The results differed because joining duplicated an order's amount when it had multiple shipments. As a result, the joined table weights orders with more shipments more heavily, thus distorting the mean.
The mean calculated directly from orders is correct because each order contributes once.

## Task 4 — Analysis Ready Table

I joined orders and shipments and then joined the tidy version of revenue to it using company and quarter. I validated the relationship as many-to-one because multiple shipment records
can correspond to the same company-quarter, while revenue has only one record per combination.
The resulting table has meaningful column names as I accounted for that when I applied the tidy transformation to my revenue table.
I also reset the index after the join operation. In summary, the net result is a table with meaningful column names, no index artifacts, one row per shipment and context from the order and revenue tables. 


## Task 5 — Visualization

I placed the original "2023-Q1" revenue chart alongside a chart comparing revenue by company and quarter.
Tidying made it possible to simply pass quarter as a hue rather than hardcoding individual quarterly columns as I did with the first chart.
The joined table also reveals which company-quarter combinations have matching order and shipment records. As a result, some quarters present in the original revenue data are absent from the final visualization.
