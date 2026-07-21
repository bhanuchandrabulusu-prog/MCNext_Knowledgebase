# Query | Use Case Examples | Data 360 Connect REST API

**Source:** https://developer.salesforce.com/docs/data/connectapi/guide/query-use-case.html

---

Business Goal: Perform a comprehensive audit of data ingestion, verify data integrity, and analyze user activity related to customer interactions. This data examination ensures regulatory compliance and enables reliable, data-driven decisions regarding customer strategy.

Use Case: A data specialist needs to retrieve all campaign engagement records since January 1, 2025, from the CampaignEngagement__dll Data Lake Object (DLO). The total number of records is expected to be very large, for example, 100,000 records.

The Query Connect API is designed to make this kind of massive data retrieval manageable and efficient. First, submit the query, then check its status as it processes, and finally retrieve the full results by using pagination.

For limit information, see Data 360 Limits and Guidelines.

Use the create SQL query endpoint to initiate the query execution in Data 360.

Query parameters:

dataspace=default: The data space where the query is to be executed.
workloadName=connect-engagement-records: A description of the scenario, task, or application name that the query handles. Set this value to help Salesforce Customer Support assist with debugging issues.

In the body of the request, pass the sqlParameters array for parameterized queries. In the query, :startDate is a placeholder for the actual date value from the parameters. See Data 360 SQL Syntax for more information on SQL statements.

The API call immediately returns a queryId to track the query’s progress, metadata about the result columns, and the first chunk of data (for example, 2000 rows). The completionStatus is Running because the first chunk is ready, but rowCount indicates that more data is available.

Query results are subject to results caching, which serves identical queries submitted within a specific timeframe much faster. Cached results have a 24-hour expiration time, ensuring that they remain available for repeated access and optimized performance for frequently run queries.

Because the initial response indicated that the rowCount is 100,000 but only 2,000 rows were returned, the query is still running in the background. You need to periodically check its status using the get SQL query endpoint.

Query parameters:

dataspace=default: The data space where the query is to be executed.
workloadName=connect-engagement-records: A description of the scenario, task, or application name that the query handles. Set this value to help Salesforce Customer Support assist with debugging issues.
waitTimeMs: This parameter allows you to perform long polling. The request blocks for up to waitTimeMs (for example, 10,000 ms = 10 seconds) if the status hasn’t changed or return immediately if it has. Adjust this number as needed if you encounter Apex resource limit issues.

The client polls every five seconds until the query completionStatus is Finished. Pass the queryId obtained in the previous response as part of the URL for this status check.

The progress field indicates how much of the query has been processed.

When completionStatus is Finished (or progress is 1.0), all data is ready for retrieval.

After confirming that the initial query is complete, you fetch the remaining 98,000 rows by using the get SQL query rows endpoint.

Query parameters:

rowLimit: The maximum number of rows to return in this chunk (for example, 2000).
offset: The row number at which to start retrieving the next chunk of query results.
omitSchema=true: This parameter, when set to true, tells the request not to return the metadata (metadata array) with each subsequent chunk. Omitting the metadata reduces the amount of data returned for faster performance.

Get the next 2000 rows, starting from row 2000 (since you already received the first 2000 rows).

The response contains the next chunk of data.

For queries that are no longer needed due to user cancellation or to cancel a long-running query, use the cancel SQL query endpoint.
