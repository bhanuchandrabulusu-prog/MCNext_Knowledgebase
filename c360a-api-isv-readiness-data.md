# Data 360 Extensibility Readiness Matrix | Model Data in Data 360 | Data 360 DMO and Mapping Guide

**Source:** https://developer.salesforce.com/docs/data/data-cloud-dmo-mapping/guide/c360a-api-isv-readiness-data.html

---

Data 360 provides two types of data kits to deploy your metadata and process definitions. Choosing the right data kit depends on your use case and deployment environment. Use the guidelines to determine the best option for your needs.

Salesforce offers two types of data kits to package and deploy Data 360 solutions.

Standard Data Kit

Create a standard data kit to package and share your Data 360 features and solutions with customers. You can create the data kit from the default data space and deploy it to any data space in the target org. With a standard data kit, you can distribute Data 360 solutions tailored to your customers’ needs.

Local Sandbox Deployment

Use standard data kits in a Data 360 sandbox to replicate metadata and process definitions from a default data space to a non-default data space. Add the assets into a data kit and use the local data kit deploy feature to install them in the target space. See Replicate Data 360 Configurations Using Local Data Kits.

Supported components for local deployment:

Calculated insight
CRM data stream
Data action target
Data lake object
Ingestion API stream
Market segment
Streaming app (web and mobile)

DevOps Data Kit

Use a DevOps data kit to migrate Data 360 metadata from a sandbox org to a production org. You can create the DevOps data kit from any data space. But you must deploy it to the same data space in the target org.

The table lists Data 360 configuration elements that you can deploy using each type of data kit. To deploy Data 360 features, first add them to a data kit, and then add the data kit to a managed package.

Data 360 Feature	Standard Data Kit	DevOps Data Kit
Activation target: Amazon S3	Yes	Yes
Activation target: Strategic partners (Google Ads, Amazon Ads, Meta, LinkedIn)	No	No
Activation target: SFTP, Microsoft Azure, GCS	Yes	Yes
Activation target: Marketing Cloud Engagement	Yes	Yes
Activation target: Native—Data 360	Yes	Yes
Activation target: Commerce Cloud, Loyalty	No	No
Activation Target: AppExchange Partners (Liveramp, Criteo, Tradedesk)	No	No
Activations: AmazonS3	Yes	Yes
Activations: SFTP, Microsoft Azure, GCS	Yes	Yes
Activations: Marketing Cloud Engagement	Yes	Yes
Activations: Native—Data 360	Yes	Yes
Activations: Commerce Cloud, Loyalty	No	No
Activations: AppExchange Partners (Liveramp, Criteo, Tradedesk)	Yes	Yes
Activations: Strategic partners (Google Ads, Amazon Ads, Meta, LinkedIn)	No	No
Advertising Audiences: Marketing Cloud Advertising	No	No
Bring Your Own Model (BYOM)	No	No
Calculated Insights: SQL	Yes	Yes
Calculated Insights: Builder	Yes	Yes
Calculated Insights: Streaming	Yes	Yes
Code Extension	No	Yes
Connector: Amazon Kinesis	Yes	Yes
Connector: Amazon S3	Yes	Yes
Connector: Azure	Yes	Yes
Connector: B2C	Yes	Yes
Connector: CRM	Yes	Yes
Connector: Google Cloud Platform	Yes	Yes
Connector: Google Cloud Storage	Yes	Yes
Connector: Ingestion API	Yes	Yes
Connector: Marketing Cloud Account Engagement	No	No
Connector: Marketing Cloud Engagement	Yes	Yes
Connector: Marketing Cloud Personalization	No	No
Connector: Mobile SDK	Yes	Yes
Connector: Snowflake	Yes	Yes
Connector: Web SDK	Yes	Yes
Data 360 Reports	Yes	Yes
Data Governance - Tags	No	Yes
Data Action: CRM	Yes	Yes
Data Action: Marketing Cloud Engagement	Yes	Yes
Data Action: Webhook	Yes	Yes
Data Action Target: Marketing Cloud Engagement	Yes	Yes
Data Action Target: Salesforce Platform	Yes	Yes
Data Action Target: Webhook	Yes	Yes
Data Graph	Yes	Yes
Data Lake Object (DLO)	Yes	Yes
Data Model Mappings	Yes	Yes
Data Model Object (DMO)	Yes	Yes
Data Share	Yes	Yes
Data Share Target: Snowflake	No	No
Data Space: Custom	Yes	Yes
Data Space: Default	Yes	Yes
Data Transform: Batch	Yes	Yes
Data Transform: Streaming	Yes	Yes
Einstein Studio: Connected Predictive AI Models (BYOM)	Yes	Yes
Einstein Studio: Connected Large Language Models (BYO-LLM)	Yes	Yes
Einstein Studio: Predictive AI Models Created from Scratch (No-code)	No	Yes
Identity Resolution	Yes	Yes
Private Connect	No	No
Related List Enrichments Based on Identity Resolution	No	Yes
Retrievers: Ensemble	No	No
Retrievers: No-code	Yes	Yes
Retrievers: Pro-code/ADL	No	No
Salesforce Platform: Apex	Yes	Yes
Salesforce Platform: Data Clean Room	Yes	Yes
Salesforce Platform: Data 360 Enrichments - Copy Fields	No	No
Salesforce Platform: Data 360 Enrichments - Related Lists	Yes	Yes
Salesforce Platform: Flow	Yes	Yes
Salesforce Platform: Lightning Web Components	Yes	Yes
Search Index Configurations	Yes	Yes
Segment: Real-Time	Yes	Yes
Segment: Waterfall	Yes	Yes
Standard Data Model (SSOT)	Yes	Yes
Standard Segment: DBT	Yes	Yes
Standard Segment: Visual Builder	Yes	Yes
Unstructured Data Lake Object (DLO)	Yes	Yes
Unstructured Data Model Object (UDMO)	Yes	Yes
Web SDK	Yes	Yes
Zero Copy Data Federation: BigQuery	Yes	Yes
Zero Copy Data Federation: Databricks	Yes	Yes
Zero Copy Data Federation: Redshift	Yes	Yes
Zero Copy Data Federation: Snowflake	Yes	Yes
Zero Copy Data Sharing: BigQuery	Yes	Yes
Zero Copy Data Sharing: Databricks	Yes	Yes

Data Kit doesn’t support unstructured data streams.

See Also

Data Cloud Developer Guide: Packages and Data Kits
First-Generation Managed Packages
Second-Generation Managed Packages
Connect REST API Developer Guide: Data 360 Resources
Build and Deploy Related List Enrichments from a Data 360 Sandbox
