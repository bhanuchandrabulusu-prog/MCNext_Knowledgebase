# Check Whether Related Data Exists by Using Subqueries | Get Started With Data 360 SQL | Data 360 Query Guide

**Source:** https://developer.salesforce.com/docs/data/data-cloud-query-guide/guide/subqueries-related-data.html

---

To check for the presence or absence of related data, use the EXISTS or NOT EXISTS operators. These operators are part of the WHERE clause that precedes a subquery. A subquery is a query that appears inside another query statement.

These query examples all use a subquery to check on related records to accounts.

Which accounts don’t have a phone number?
Which accounts have a phone number but no email address?
How many accounts have a phone number but no email address?

For example, this query uses a subquery to return the accounts that don’t have a phone number.

This output shows the first few rows of the sample results.

ssot__Id__c	ssot__Name__c
001Hu00002xHZJnIAO	Pyramid Construction Inc.
001Hu00002xHZJtIAO	United Oil & Gas, UK
001Hu00002xHZJuIAO	United Oil & Gas, Singapore

You can use these predicates with subqueries.

EXISTS
NOT EXISTS
IN
