# Aggregate Your Query Results | Get Started With Data 360 SQL | Data 360 Query Guide

**Source:** https://developer.salesforce.com/docs/data/data-cloud-query-guide/guide/aggregate-query-results.html

---

For large datasets, you don’t want to inspect each individual dataset. To see high-level insights across a dataset, aggregate your query.

For example, you can get the average age of customers, the total sales amount for a product, or the count of customers by geographical location. To aggregate data in the returned result set, use aggregate functions in the SELECT clause. For a list of aggregate functions, see Aggregate Functions.

This query returns the count of individuals whose first name starts with ‘E’.

The query returns one row containing the aggregated count.

count1
2

Alternatively, you can get the same count for the unified individual records by querying UnifiedIndividual__dlm.

Based on the sample data, we get the same aggregate result.

count1
2

The GROUP BY clause is often useful with aggregate results because it groups the query results by a category.

This example uses GROUP BY to return the count of addresses in ssot__ContactPointAddress__dlm by country.

This query output shows sample results.

TotalAddresses	ssot__CountryId__c
3	France
23	USA
1	Taiwan
15	Japan

To filter the results of the aggregated query to get the top counts of addresses—only the counts that are greater than 10—you can filter the aggregated result with the HAVING clause.

This example aggregates the addresses in ssot__ContactPointAddress__dlm by the country ID and returns the records whose count of addresses by country is greater than 10.

This query output shows sample results. In this case, there are more than 10 addresses for the United States and Japan.

TotalAddresses	ssot__CountryId__c
23	USA
15	Japan

Aggregate functions compute a single result from a set of input values. This section contains some commonly used aggregate functions. To see the full list of available aggregate functions, see Aggregate Functions in the Data 360 SQL Reference.

SUM(expression)

Returns the sum of <expression> of all input values.

AVG(expression)

Returns the average (arithmetic mean) of all input values.

COUNT(*)

Returns the number of input rows.

MIN(expression)

Returns the minimum value of <expression> of all input values.

MAX(expression)

Returns the maximum value of <expression> of all input values.
