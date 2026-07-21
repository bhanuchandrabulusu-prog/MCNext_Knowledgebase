# Best Practices for Optimizing Usage | Get Started with Data 360 Development | Data 360 Developer Guide

**Source:** https://developer.salesforce.com/docs/data/data-cloud-dev/guide/best-practices-usage.html

---

Write optimized code that’s inexpensive, such as queries. You can write SQL queries to fetch only the data that you need. Queries are preferable over GET API requests because they offer more flexibility in choosing the data that you want to retrieve. To write efficient queries, add a WHERE clause to filter the returned results and retrieve the smallest set of required records. Also, specify only the fields that you need in the SELECT statement.

For example, this query is efficient because it gets one Individual record for a specific Individual ID value.

Connect REST API resource:

SQL query:

You can query data via Connect REST API. See the Query Library section in Data Cloud Resources in the Data Cloud Connect REST API Guide. Or see Query Data using Query API and Query Customer Profile Information with Profile API in the Data Cloud Query Guide. Alternatively, you can use SOQL to query data. For more information, see Data Cloud Query Profile Parameters in the REST API Developer Guide.

As part of your data ingestion strategy, ensure that you import relevant data records into Data 360 and that you don’t import more data than what’s needed. Sometimes it’s better to aggregate data before ingesting it rather than ingesting every data point, especially if not all attributes are relevant.

When testing a custom app, limit the amount of testing data in the test org. Use a sample of records that’s sufficient to meet your functional testing needs.
