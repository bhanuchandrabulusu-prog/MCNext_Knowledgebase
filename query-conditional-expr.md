# Use a Conditional Expression | Get Started With Data 360 SQL | Data 360 Query Guide

**Source:** https://developer.salesforce.com/docs/data/data-cloud-query-guide/guide/query-conditional-expr.html

---

For example, the Account Type ID field of ssot__Account__dlm has the values 'Customer - Direct' and 'Customer - Channel'. You don’t want the 'Customer - ' prefix. Use the CASE conditional expression to return a different value for the Account Type Id field based on the original value. The ELSE expression covers the field values that don’t match the conditions and returns the field value unchanged.

In the condition, you can use all the same operators (=, <, <=, LIKE, BETWEEN, ...) that you can use in WHERE clauses.
