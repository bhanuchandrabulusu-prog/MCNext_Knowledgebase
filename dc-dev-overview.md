# Data 360 Development Overview | Get Started with Data 360 Development | Data 360 Developer Guide

**Source:** https://developer.salesforce.com/docs/data/data-cloud-dev/guide/dc-dev-overview.html

---

This diagram shows the API and object integration points within Data 360 and the Salesforce Platform. The diagram separates the components that relate to a Data 360 tenant from the components within the Salesforce Platform.

Here’s what the diagram covers in detail.

After the data is ingested from data sources, it’s represented as a set of data lake objects (DLOs). Using the Customer 360 data model, an administrator maps the DLO fields to a data model object (DMO). Next, an administrator unifies the data by using identity resolution rules, which results in a Unified DMO.
The Data 360 API is part of the Data 360 tenant, and the API calls access the tenant-specific endpoint in the tenant. The Data 360 API includes REST resources for running queries, accessing profiles, calculated insights, identity resolution rulesets, data source records, and metadata.
The Connect API is part of the Salesforce Platform. Like the Data 360 API, Connect API includes REST resources for running queries, accessing profiles, calculated insights, identity resolution rulesets, data source records, and metadata. Connect API also provides Apex classes through the ConnectApi namespace so that you can perform a subset of these operations.
Using data actions, calculated insights and engagement data can trigger automation in the Salesforce Platform using Platform Events, in Marketing Cloud, or in an external system using a webhook.

See Also

Data Cloud Reference Guide
Data Cloud Connect REST API
Salesforce Help: Data Cloud Features
Custom App Development
Integration with External Systems Using Data Actions
