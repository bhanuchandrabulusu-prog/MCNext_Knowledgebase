# Simplify Queries with CTEs | Get Started With Data 360 SQL | Data 360 Query Guide

**Source:** https://developer.salesforce.com/docs/data/data-cloud-query-guide/guide/common-table-expressions.html

---

Common Table Expressions (CTEs) are a powerful feature that allows you to create temporary named result sets within your query. Think of them as temporary tables that exist only for the duration of your query execution. CTEs make complex queries more readable and help you break down complicated logic into manageable pieces.

A CTE is defined using the WITH clause followed by a name and a query. Here’s the basic structure:

Let’s say you want to analyze high-value customers from your Individual DMO. First, create a CTE to identify customers with more than 5 contact points, then use that CTE in your main query:

This query creates a temporary result set called high_activity_customers and then selects from it in the main query.

You can define multiple CTEs in a single query by separating them with commas:

Improved Readability: Break complex queries into logical, named components
Reusability: Reference the same subquery multiple times without repeating code
Debugging: Test each CTE individually to isolate issues

For comprehensive syntax details, advanced features like recursive CTEs, and additional examples, see the complete WITH Clause reference.

CTEs are particularly useful when you need to:

Calculate intermediate results that you’ll use multiple times
Make complex joins more readable
Replace complex subqueries with named, reusable components
Perform multi-step data transformations

In the next sections, you’ll learn about other advanced querying techniques that work well with CTEs, such as subqueries and joins.
