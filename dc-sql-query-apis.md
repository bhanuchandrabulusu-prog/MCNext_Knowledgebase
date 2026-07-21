# Data 360 SQL Query APIs | Query Data in Data 360 | Data 360 Query Guide

**Source:** https://developer.salesforce.com/docs/data/data-cloud-query-guide/guide/dc-sql-query-apis.html

---

Use Data 360 Query APIs with custom SQL for complex queries that don’t have an object-specific API or a supported language library. Query APIs provide the most flexible way to access your Data 360 data using Data 360 SQL syntax.

Query APIs are ideal when you need to:

Execute complex SQL queries across multiple data model objects (DMOs) and data lake objects (DLOs)
Perform advanced joins, aggregations, and data transformations
Extract large volumes of data for analytics or reporting
Build custom applications that require flexible data access
Query data that doesn’t have a dedicated object-specific API
Build custom applications in a language without supported libraries
Data 360 SQL: Enhanced SQL features specific to Data 360 objects
Complex Operations: Joins, subqueries, window functions, and aggregations
Asynchronous Execution: Handle long-running queries without blocking
Pagination: Process large result sets efficiently
Query Optimization: Automatic optimization for Data Cloud architecture
REST Endpoints: Connect REST API calls
Apex Integration: Native support in Salesforce Apex code
Multiple Data Sources: Query across unified, engagement, and profile data

Before using Query APIs, ensure you have:

Data Cloud License: Active Data Cloud licenses provisioned for your org
User Permissions: Appropriate roles and permissions assigned
Authentication Setup: Valid access tokens and external client app configuration
Data Model Knowledge: Understanding of your Data Cloud object schema
Set Up Authentication: Configure OAuth or Data Cloud authentication
Explore Your Data: Use the Metadata API to understand available objects
Write Your First Query: Start with simple SELECT statements
Handle Results: Implement pagination and error handling

See Also

Query Guide Decision Tree: Choose the right data retrieval method
Query Data with the Query API - Direct API v3 endpoints with ASYNC and ADAPTIVE modes
Object-Specific APIs: Alternatives for targeted data access
Language-Specific Libraries: Client library options
Salesforce Help: Data 360 Limits and Guidelines
Salesforce Developers Blog: Boost Data 360 Integrations with the New Query Connect API
