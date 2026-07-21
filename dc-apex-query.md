# Query Data 360 Data with Apex | Query Data in Data 360 | Data 360 Query Guide

**Source:** https://developer.salesforce.com/docs/data/data-cloud-query-guide/guide/dc-apex-query.html

---

Use Apex to query Data 360 data directly from your Salesforce org. Access unified customer insights and act on them immediately within your Salesforce automations.

Use the sfsqlquery namespace when you need an easy and intuitive way to execute queries with iterators and typed row accessors.

When to use: Run SQL queries on Data 360

Synchronous iteration over query results
Typed column value accessors (getString, getInteger, etc.)
Asynchronous processing of large datasets with SqlQueueable
Resume queries from saved query IDs

Common workflows:

The namespace provides five classes that support three primary workflows:

Execute a new query synchronously:
SqlStatement → SqlRowIterator → Row

Fetch results of a previously executed query:
QueryHandle → SqlRowIterator → Row

Process large datasets asynchronously:
SqlQueueable → SqlRowIterator → Row

See sfsqlquery Namespace in the Apex Reference.

Apex methods use the current user’s session context and permissions automatically. Ensure users have appropriate Data 360 permissions assigned through permission sets or profiles.

See Getting Started with Apex in the Apex Developer Guide.

Use asynchronous patterns: For long-running queries, implement polling logic to avoid governor limits
Handle errors: Check query status for failures and implement retry logic
Test with smaller datasets: Validate your query logic with LIMIT clauses before processing full datasets

Build a query with SqlStatement, execute it synchronously with SqlRowIterator, and access typed column values using the Row class. The SqlStatement.create() method builds the query, the execute() method runs it synchronously, and Row provides typed accessor methods like getString() to retrieve column values.

Resume a query from a saved query ID using QueryHandle. The QueryHandle.create() method takes a saved query ID and uses withOffset() to skip already-processed results. This is useful when you need to retrieve additional results from a previously executed query.

Process large datasets asynchronously using SqlQueueable. The custom class extends SqlQueueable and implements two key methods: processDataChunk() to handle each page of results, and chainNextJob() to automatically continue processing subsequent pages. This pattern prevents governor limit issues when working with large result sets.

For backward compatibility, the ConnectApi.CdpQuery class remains available as a low-level interface that directly mirrors the Connect REST API. We recommend using the sfsqlquery namespace for all new development.

See ConnectApi.CdpQuery Methods in the Apex Reference.

Query Data 360 Data using Query API - Complete API reference
Data 360 SQL Query APIs - Overview of query API options
Get Started With Data 360 SQL - SQL syntax and examples
