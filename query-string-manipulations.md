# Perform String Manipulations | Get Started With Data 360 SQL | Data 360 Query Guide

**Source:** https://developer.salesforce.com/docs/data/data-cloud-query-guide/guide/query-string-manipulations.html

---

To modify the string values that a query returns, such as when a query returns only part of a string, use string manipulation functions. For example, if the first-name field includes a middle name, such as Edna Martha, you want to return only the middle name, Martha.

To extract the portion of a string value after a starting position, use substring(string, startPosition). The startPosition argument starts from 1. In the name Edna Martha, the position of the first letter in Martha is 6. The substring function in this query returns Martha.

However, the position of the middle name isn’t always the same, depending on the length of the first name. A better way to get the position of the middle name is to call the strpos() function. Because the first name and middle name are always delimited by a space, you can use strpos() to get the position of the space. Then add 1 so the position references the start of the middle name. This query combines strpos() and substring() to return the middle name.
