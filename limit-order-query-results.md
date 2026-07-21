# Limit and Order Your Query Results | Get Started With Data 360 SQL | Data 360 Query Guide

**Source:** https://developer.salesforce.com/docs/data/data-cloud-query-guide/guide/limit-order-query-results.html

---

A query result set can be large if your Data 360 org contains a lot of data. To limit the query result, use the LIMIT clause. The LIMIT clause returns the first n rows that the data store returns, where n is the number of rows specified.

This query returns 20 unified individuals only.

The LIMIT clause doesn’t guarantee the order of the rows returned. You can get different results if you run the query at different times. A more reproducible query combines the LIMIT clause with the ORDER BY clause so that the results returned are in the same order in each query execution.

This query returns the top 20 oldest unified individuals based on the birth date.

This query output shows the first few rows returned for unified individuals from the result set of 20 rows. The rows are ordered by birth date.

ssot__FirstName__c	ssot__LastName__c	ssot__BirthDate__c
Avi	Green	1937-03-12T00:00:00.000Z
Babara	Levy	1940-07-20T00:00:00.000Z
Edna	Frank	1945-10-23T00:00:00.000Z
Stella	Pavlova	1946-12-04T00:00:00.000Z
...	...	...

The ORDER BY clause orders in ascending order by default. To order the result in descending order, use the DESC keyword. This ORDER BY clause in the query returns the top 20 youngest individuals.

To retrieve a subset of the returned result set, use OFFSET to return the row after the specified row number. Use OFFSET with ORDER BY to get the same result set in subsequent queries.

Suppose you already displayed the first two rows of the oldest individuals. You want the next two rows. You can use this query with an offset of 2 and a limit of 2.

This query returns rows 3 and 4 from the previous output. The rows are ordered by birth date.

ssot__FirstName__c	ssot__LastName__c	ssot__BirthDate__c
Edna	Frank	1945-10-23T00:00:00.000Z
Stella	Pavlova	1946-12-04T00:00:00.000Z
