# Data 360 Features Brief Overview | Get Started with Data 360 Development | Data 360 Developer Guide

**Source:** https://developer.salesforce.com/docs/data/data-cloud-dev/guide/dc-features-overview.html

---

If you’re new to Data 360, this section provides a brief overview of what Data 360 is used for. It also provides resources so that you can learn more about Data 360.

Data about the same customer can originate from disparate sources and have a different record structure. For example, a customer on an ecommerce site can also be a shopper on a mobile app. But the fields and relationships of the shopper record from the site and the app don’t always match. You can standardize, or harmonize, the structure and relationships of the customer record using the Customer 360 Data Model. Because there can be many instances of the same customer, such as Joe Doe and Joseph Doe with the same email, you can reconcile the differences using identity reconciliation rulesets.

The benefit of unified customer data and insights is that you can learn more about your customers and meet their needs better. You can also act on the unified data. For example, a unified profile of a customer in Data 360 can be linked to cases in Service Cloud. If a customer is filing many cases, a trigger can ask a customer service representative to follow up with the customer, or you can a create marketing cloud journey for the customer.

A significant amount of enterprise knowledge originates from unstructured data. Unlike structured data that is stored in an easily searchable format, such as a relational database, unstructured data does not have a predefined format and is typically large in size. Unstructured data can contain both textual and non-textual data such as PDFs, web content, or audio and video files. Harnessing the enterprise knowledge stored in unstructured data is the key to supporting use cases for Agentforce agents, retrieval augmented generation (RAG), automation, and analytics.

With Data 360, you can ingest and index unstructured data, and then retrieve it in workflows with AI agents, automation flows, or analytics queries. Data 360 has connectors built for ingesting unstructured data from third-party applications or sources, such as Amazon S3, Azure, Google Drive, Microsoft Sharepoint, and more. You can use the Salesforce CRM connector to ingest knowledge article data stored in Salesforce records.

Data 360 supports two types of search index: vector search and hybrid search. Create the right search index with advanced builders in Data 360 to finely tune and retrieve the most relevant response. Use the responses to ground prompts with accurate, current, and pertinent information for agents or RAG queries.

If you have purchased Segmentation and Activation, you can:

Group customers using segmentation to create targeted business logic and communications
Build segments using calculated insights generated in Data 360
Create personalized customer engagements based on segment characteristics

A typical use case is creating marketing campaigns using Marketing Cloud engagements. For example:

Generate a calculated insight for average customer spending
Build segments for different spending levels (low, medium, high)
Create targeted email campaigns:
Promote lower-priced products to budget-conscious segments
Highlight premium products to high-spending segments
Query segments to create personalized site experiences for VIP customers
Trailhead: Customer 360 Data Model for Data Cloud
Trailhead: Data Cloud Insights
Trailhead: Segmentation and Activation
Trail: Explore Data Cloud
Salesforce Help: Data Cloud Features
