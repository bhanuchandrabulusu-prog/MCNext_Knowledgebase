# Query Data in Data 360 | Data 360 Query Guide

**Source:** https://developer.salesforce.com/docs/data/data-cloud-query-guide/guide/query-guide-get-started.html

---

As of October 14, 2025, Data Cloud has been rebranded to Data 360. During this transition, you may see references to Data Cloud in our application and documentation. While the name is new, the functionality and content remains unchanged.

Salesforce Data 360 enables you to collect, store, and process data from Salesforce clouds and external systems. After harmonizing and unifying your data, you can create metrics that span all data sources, providing comprehensive insights. To extract valuable insights from your Data 360 data, you can query it using integrated apps, object-specific APIs, client libraries, and Data 360 query APIs. This guide focuses on how to retrieve data from Data 360.

Review this decision flow diagram to determine which data retrieval method works best for you.

To help you choose the most suitable data retrieval method based on your specific needs, consider the following:

To explore and query data using a visual interface, use integrated apps. For more information, see Data 360 Integrated Apps.
For object-oriented queries, use the Data 360 Connect REST API or the Data Cloud REST API. See Data 360 Object-Specific APIs for details.
To seamlessly integrate your applications with Data 360 data, use a language-specific client library. The available libraries include JDBC, Python, and the Connect API for Apex. For more information, see Language-Specific Client Libraries.
To query Data 360 data using custom SQL queries REST API calls, you can use the Data 360 Connect API (REST API and Apex). See Data 360 SQL Query APIs for more information. For Apex-specific workflows and the sfsqlquery namespace, see Query Data 360 Data with Apex.

As an admin, you’ll likely focus on data exploration, reporting, and user enablement:

Start with Data Explorer: Use Salesforce’s built-in Data Explorer tool to explore your data
Understand Your Data Model: Review available data objects and relationships
Set Up User Permissions: Configure user roles and permissions for data access
Create Reports and Dashboards: Build analytics using integrated apps
Monitor Usage: Track API limits and performance

Quick Start: Begin with Query Editor to run your first Data 360 SQL queries.

As a developer, you’ll focus on programmatic access and application integration:

Choose Your Integration Method: Review Language-Specific Client Libraries or Data Cloud SQL Query APIs to select the right approach
Set Up Authentication: Configure External Client Apps and OAuth
Explore the Data Model: Use the Metadata API to understand available objects
Start with Simple Queries: Follow Get Started With Data Cloud SQL examples

Quick Start: Try the Data 360 Quick Start to make your first API call.

Write a Simple Query
Filter Your Query Results
Join Records from Different DMOs and DLOs
Set up JDBC for Java applications
Use the Python Connector for data analysis
Build with Connect API in Apex

Calculated insight and data transformation creation use a different SQL dialect than described in this guide. See Calculated Insights and Streaming Data Transforms in Salesforce Help for more information about the different SQL dialect.

Understanding Data 360:
Data Objects in Data 360
Data Model Concepts
User Roles and Permissions
Development Resources:
Data Cloud Developer Guide
Data 360 Quick Start
API Limits and Guidelines
Working with Data:
Unify Source Profiles
Query Editor
