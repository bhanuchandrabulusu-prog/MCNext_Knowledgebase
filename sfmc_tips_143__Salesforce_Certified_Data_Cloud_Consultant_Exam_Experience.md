# SFMC Tips #143 : Salesforce Certified Data Cloud Consultant Exam Experience

**Source:** https://medium.com/@marketingcloudtips/salesforce-certified-data-cloud-consultant-exam-experience-19d4f55fbc31

---

# SFMC Tips #143 : Salesforce Certified Data Cloud Consultant Exam Experience

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--19d4f55fbc31---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--19d4f55fbc31---------------------------------------)

18 min read

·

Jun 20, 2025

--

Photo by [Daniel Apodaca](https://unsplash.com/@danielapodaca96?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

## Exam Experience

I’ve never written about my experiences with Salesforce certification exams before, but as a new endeavor, I’ve decided to share insights about Salesforce certifications.

Prior to taking this exam, I had already obtained the **Agentforce Specialist** certification, so I had a decent understanding of Data Cloud. I approached this exam with the determination to achieve a perfect score. However, I fell just short, losing 4 points and failing to reach perfection. The “perfect score” barrier remains a challenging goal, as I’ve come to realize once again.

![]()

The **Data Cloud Consultant** exam primarily focuses on foundational topics related to Data Cloud. On the other hand, content related to cutting-edge technology or Agentforce is specifically covered in the **Agentforce Specialist** exam. It’s crucial to understand these differences in scope when preparing for either certification.

Additionally, Data Cloud was previously known as the **Marketing Cloud Customer Data Platform**, which explains why the exam included many questions about its integration with **Marketing Cloud Engagement**. To tackle these questions effectively, candidates need more than just standalone knowledge of Data Cloud. A basic understanding of cross-platform integration and operational processes is essential.

Given that Data Cloud receives monthly updates, you might expect these changes to impact the exam content. However, in my experience, the exam didn’t include any questions rendered obsolete by recent updates. This is likely because the exam team diligently reviews and maintains the content to account for these updates. Keeping certification exams current must be a significant effort. 👏

I won’t be discussing the exam structure, topics, or weighting here. Please refer to the [**official exam guide**](https://trailhead.salesforce.com/en/credentials/datacloudconsultant).

## **Exam Preparation**

### **1. Unlock Your Data with Data Cloud**

As a first step in your exam preparation, prioritize completing the following Trailmix:

[## Unlock Your Data with Data Cloud | Salesforce Trailhead

### Unify data from across your platforms with Data Cloud.

trailhead.salesforce.com](https://trailhead.salesforce.com/content/learn/trails/unlock-your-data-with-data-cloud?source=post_page-----19d4f55fbc31---------------------------------------)

### **2. Cert Prep: Data Cloud Consultant**

Next, make sure to complete the exam preparation module included in the Trailmix. This module features practice questions to help you assess your readiness:

[## Cert Prep: Data Cloud Consultant

### Prepare for the Salesforce Data Cloud Consultant exam with detailed resources and practice tools for each key exam…

trailhead.salesforce.com](https://trailhead.salesforce.com/content/learn/modules/cert-prep-data-cloud-consultant?trail_id=unlock-your-data-with-data-cloud&source=post_page-----19d4f55fbc31---------------------------------------)

### **3. Data Cloud Knowledge Check**

Salesforce provides official knowledge check exercises. Once you’ve completed your studies, challenge yourself with these:

**Overview of Data Cloud**

- [Knowledge Check: Overview of Data Cloud](https://rise.articulate.com/share/fK5l29AYS7GZ9btZMnZd7Iyp6ipjbo1O#/)

**Setup and Administration of Data Cloud**

- [Knowledge Check: Setting Up Data Cloud](https://rise.articulate.com/share/MYPQCk-cO-Jaz4DmNPNNF7mSxLO8jqYP#/)
- [Knowledge Check: Managing Data Cloud](https://rise.articulate.com/share/TN4fXZBEyzrVTZiRGkwNuZ0nPVx2Sd3r#/)

**Data Ingestion and Modeling**

- [Knowledge Check: Data Cloud — Data Ingestion](https://rise.articulate.com/share/NHvXKFOkcX6A9shxaBPxwOGrV_EbHO3-#/)
- [Knowledge Check: Data Cloud — Data Modeling](https://rise.articulate.com/share/zGPmf87HcpwGJsY0YZklYGvEgT8IMV_g#/)

**Identity Resolution**

- [Knowledge Check: Data Cloud — Identity Resolution](https://rise.articulate.com/share/kGzrZeirJFj91RUWV4rL9U1JHv69s8XV#/)

**Segmentation and Insights**

- [Knowledge Check: Data Cloud — Segmentation](https://rise.articulate.com/share/JeO1cJlA9GK4BGEtDpsHzHha0jDIo8AY#/)
- [Knowledge Check: Data Cloud — Insights](https://rise.articulate.com/share/5cwXgJIRwGT2RRhqVGwqxI_-wEZLqQYZ#/)

**Data Activation**

- [Knowledge Check: Data Cloud — Activation](https://rise.articulate.com/share/Zf6VgvyG6_A6ym9rBnsAca-49pjU0Wh4#/)

**Important Note**  
Some of the questions and answers in the knowledge checks may not be fully up-to-date due to maintenance status. Keep this in mind as you use them for your preparation.

### **4. Study my notes**

Now, for those of you who have read this far, I’d like to share my personal study notes.

## 1. Data Cloud Overview (11 Questions)

- Describe Data Cloud’s function, key terminology, and business value.
- Identify typical use cases for Data Cloud.
- Articulate how Data Cloud works and its dependencies.
- Describe and apply the principles of data ethics.

## Business Value

### Business Value and Key Concepts of Data Cloud

Data Cloud delivers business value through “**integration”** and “**harmonization”** of data:

- **Integration**: Links multiple datasets using identity resolution.
- **Harmonization**: Ensures consistency through data mapping.

It’s important to note that Data Cloud is not a Master Data Management (MDM) tool and is not designed for:

- Creating golden records.
- Data backup or recovery.

## Process

### 1. Data Processing Workflow in Data Cloud

Memorize the **sequence of processes**:

### **Preparation Phase**

1. Provisioning
2. Data Ingestion
3. Data Mapping (Harmonization)
4. Identity Resolution (Integration)

### **Utilization Phase**

1. Insight Analysis (e.g., generating Calculated Insights)
2. Segmentation
3. Activation

***Note****: Insight analysis is positioned at the start of the utilization phase because it directly feeds into segmentation and activation.*

### 2. Provisioning Process

1. **Set up admin users**: Additional users can be configured later.
2. **Complete provisioning of Data Cloud setup**.
3. **Configure additional users**: Assign custom permissions.
4. **Connecting Salesforce Clouds**

- Set up the “**Data Cloud Salesforce Connector” permission set**.
- Grant “**view” access** (editing permissions are not required).

***Important****: When integrating CRM data, ensure that the “****view” access*** *is properly assigned to relevant objects and fields in the* ***Data Cloud Salesforce Connector permission set****. Without this, objects and fields won’t appear in data streams, and data ingestion won’t work. Note that* ***Modify*** *or* ***Edit*** *permissions are unnecessary.*

[## SFMC Tips #82 : Data Cloud: Faster Field Access with View All Field (Global)

### In the past, when syncing newly created fields in Salesforce CRM to Data Cloud data streams, it was necessary to…

medium.com](/@marketingcloudtips/a-game-changing-update-in-data-cloud-faster-field-access-with-view-all-field-global-64614afe4a83?source=post_page-----19d4f55fbc31---------------------------------------)

## Data Ethics

### Best Practices for Data Ethics

**1. Collect and use personal information appropriately.**  
Provide mechanisms for customers to control their data settings.

**2. Offer value in exchange for data.**  
Ensure transparency so customers can recognize the benefits of sharing their data.

**3. Handle sensitive data with care.**  
Collect data only when necessary and clearly define its purpose.

**4. Minimize data collection to what is essential.**  
Avoid excessive collection and consistently reevaluate the necessity.

**5. Carefully select activation partners.**  
Confirm data usage purposes and handling methods in advance.

## Data Deletion Requests

1. **Submit data deletion requests**: Use the “**Consent API**” to delete individual data profiles in Data Cloud.
2. **Delete related records**: The request removes individual records from the **Individual DMO** and associated DMOs.
3. **Reprocessing for complete deletion**: Requests are **reprocessed after 30, 60, and 90 days** until fully deleted. Additionally, deletion requests must be sent to all connected systems and Salesforce Clouds.

## Subject Areas

### Subject Areas in the Data Model

- **Party Subject Area**: Manages information related to customers and contacts.
- **Engagement Subject Area**: Tracks interactions with customers (e.g., calls, emails).
- **Loyalty Subject Area**: Tracks and manages reward programs.
- **Product Subject Area**: Defines and tracks product or service information.
- **Sales Order Subject Area**: Manages future revenue or quantities by product family.
- **Case Subject Area**: Records and manages issues or support tickets.
- **Privacy Subject Area**: Tracks and stores data privacy settings.

With this structured approach, you can maximize the value of Data Cloud in your organization.

## **2. Data Cloud Setup and Administration** (7 Questions)

- Apply Data Cloud permissions, permission sets, and org-wide settings.
- Describe and configure the available data stream types and data bundles.
- Identify use cases for data spaces and create data spaces based on requirements.
- Manage and administer Data Cloud using reports, dashboards, flows, packaging, and data kits.
- Diagnose and explore data using Data Explorer, Profile Explorer, and APIs.

## Permissions

### Data Cloud Permissions

Here are the primary roles in Data Cloud and their responsibilities:

**1. Data Cloud Administrator**

- Manages access to all Data Cloud features.
- Handles application setup, user provisioning, and permission set assignments.

**2. Data Cloud Data Aware Specialist**

- Maps data to the data model, creates data streams, identity resolution rule sets, and calculated insights.
- Focuses on tasks related to mapping and identity resolution.

**3. Data Cloud User**

- Can view Data Cloud functionalities but cannot make changes or edits.

**4. Data Cloud Marketing Administrator**

- Similar to the administrator role but focuses on managing segmentation and activation.

**5. Data Cloud Marketing Manager**

- Oversees overall **segmentation** strategy and leads the creation of activation targets and **activations**.

**6. Data Cloud Marketing Specialist**

- Responsible for creating segments and driving marketing initiatives.
- *Note: This role does* ***not include activation tasks****.*

**Supplementary Notes**

- For segmentation and activation, the **Marketing Administrator** role is system-focused, while the **Marketing Manager** role is more execution-focused.
- It is recommended to use standard permission sets, as they are automatically updated with feature additions in Data Cloud.

## Data Categories

### Data Categories in Data Cloud

Data Cloud organizes data into three categories:

**1. Profile**

- Contains customer data.

**2. Engagement**

- **Time-series data** (e.g., purchase history, email engagement).
- Requires “**Event Time Field**” (e.g., Created Date, Purchase Date, Email Click Date).

**3. Other**

- Data related to profiles or engagements (e.g., store master data).

[## SFMC Tips #84 : Data Cloud: Understanding Event Time Field and Record Modified Field

### When creating a data stream in Salesforce Data Cloud, the Event Time Field and Record Modified Field are crucial…

medium.com](/@marketingcloudtips/data-cloud-understanding-event-time-field-and-record-modified-field-12f1ecf55126?source=post_page-----19d4f55fbc31---------------------------------------)

## Data Stream

### 1. Data Extension Synchronization (Marketing Cloud Engagement)

Regarding data extension synchronization, the exam does not cover details at a granular level. However, in practical applications, it is essential to understand the topic with the level of detail provided in the following article.

[## SFMC Tips #81 : Data Cloud: Understanding How to Update Data Extension Integrations

### One of the essential tasks after connecting Marketing Cloud to Data Cloud is linking your data extensions to data…

medium.com](/@marketingcloudtips/understanding-how-to-update-data-extensions-in-data-cloud-25a44bf180b7?source=post_page-----19d4f55fbc31---------------------------------------)

### 2. Salesforce CRM Connector Data Synchronization

**Full Sync:**

Runs bi-weekly and is also triggered by:

- **Creating a new data stream**.
- **Adding or removing columns**.
- Detecting over 600,000 deleted records.

**Incremental Sync:**

- Runs every 10 minutes after the last full sync.
- Captures data changes since the last full update.

**Notes:**

- Standard fields can stream to Data Cloud **in real time** under specific conditions.

### 3. Data Bundles

Data Bundles act as starter kits for data connections. Examples include:

**1. Marketing Cloud Engagement**

- Covers Email Studio (email), Mobile Studio (SMS), and Mobile Push (Mobile App).
- Default engagement data range: **90 days** (custom setup required for up to 2 years).

**2. Commerce Cloud**

- Default range: **30 days** of order data.

**Notes:**

- Custom integrations are needed for GroupConnect (LINE), CloudPages (web), DataViews, etc.
- Email and phone data types are **treated like text and not validated**.

[## SFMC Tips #85 : Data Cloud: A Guide to Marketing Cloud Starter Data Bundle

### Connecting Data Cloud and Marketing Cloud

medium.com](/@marketingcloudtips/data-cloud-a-guide-to-marketing-cloud-starter-data-bundle-cecea33400c4?source=post_page-----19d4f55fbc31---------------------------------------)

### 4. Amazon S3 Integration

- If no file name is specified, the first detected file is selected.
- Supported authentication types: “**Access Key**” and “**Secret Key**”.
- IAM users for S3 must have the necessary access permissions. Credential rotation errors can cause issues.

### 5. What are “Data Spaces”?

Data spaces are logical partitions for organizing data, recommended for:

- Efficiently managing a single environment across multiple brands, regions, or departments.
- Up to 50 data spaces can be created (additional licenses required).

**Example:** Separating data and customers **by brand**.

## Data Explorer

### Data Explorer Features

Displays objects such as:

- Data Lake Objects, Data Model Objects (including Unified Individuals), Calculated Insights, and Data Graphs.

\*A data graph joins the normalized table data from Data Model Objects (DMOs) and transforms it into a materialized view of new data. To create a data graph, select fields from existing DMOs.

*[Copy SOQL]* button:

- Copies the current data view as SOQL to the clipboard. **Export functionality is not available**.

[## SFMC Tips #77 : Data Cloud: Searching and Viewing Records at the Record Level

### In Data Cloud, vast amounts of data are aggregated from various sources. Typically, data is managed at the entity…

medium.com](/@marketingcloudtips/how-to-search-and-view-records-at-the-record-level-in-data-cloud-7ee19a3ae900?source=post_page-----19d4f55fbc31---------------------------------------)

## 3. Data Ingestion and Modeling (12 Questions)

- Identify the different transformation capabilities within Data Cloud.
- Describe processes and considerations for data ingestion from different sources into Data Cloud.
- Define, map, and model data using best practices and aligning to requirements for identity resolution.
- Use available tools to inspect and validate ingested and modeled data.

## Data Transform

Data transform in Data Cloud can be categorized into two types:

1. **Formula Fields**
2. **Data Transform**

### 1. Examples of Formula Field Usage

- **Creating Primary Keys**  
   Data Cloud does not support multiple primary keys. To handle this, you can create composite keys by concatenating multiple keys using the `CONCAT()` function.
- **Standardizing Data**  
   For example, if data formats vary as “abc”, “ABC”, or “a,b,c”, you can unify these into “abc” using functions like `REPLACE()` and `LOWER()`.

### Considerations for Formula Fields

Formula fields are only applied during data ingestion. Therefore, the following must be considered:

- **Full Refresh**: All data is updated, so formula fields are reapplied without issues.
- **Incremental Updates**: Formula fields are not applied to unchanged data.

### 2. Data Transform

- Splitting records.
- Performing aggregations.
- Merging data sources.
- Expanding/collapsing data arrays.

**Example: Splitting Records**  
 When mapping data to the Individual DMO in Data Cloud, only one email address can be associated per record. To comply with this, records must be split accordingly.

[## Help And Training Community

### Edit description

help.salesforce.com](https://help.salesforce.com/s/articleView?id=data.c360_a_uc_normalize_denormalized_data_from_marketing_cloud.htm&type=5&source=post_page-----19d4f55fbc31---------------------------------------)

### Batch and Streaming Transforms

**1. Batch Transform**

- Fully refreshes data.
- Can be scheduled or triggered manually.
- Uses DLOs or DMOs as source objects.
- Does not replace calculated insights.

**2. Streaming Transform**

- Processes data one row at a time during ingestion.
- Previously limited to DLOs, but since the May 2025 release, DMOs can also be used.
- Not suitable for large data volumes.
- Does not replace calculated insights.

## Data Mapping

### 1. Best Practices for Data Mapping

When dealing with fields that don’t align with the standard data model, consider the following:

**1. Balance Between Standard and Custom Models**

- Avoid forcing all fields to fit into standard DMOs.
- Similarly, designing everything as custom DMOs is inefficient.
- Use standard DMOs for compatible fields.
- Add custom DMOs only for fields that cannot fit the standard model.

**2. Leveraging Custom Fields**

- If specific requirements (e.g., for identity resolution) are necessary, add custom fields to standard DMOs.

### 2. Disconnecting Data Sources

**1. Prerequisites for Disconnecting a Data Source**

- Delete data streams (conditions outlined below).
- Delete segmentations (though this condition is automatically met if the above is completed).

[## Help And Training Community

### Edit description

help.salesforce.com](https://help.salesforce.com/s/articleView?id=data.c360_a_disconnect_a_data_source.htm&type=5&source=post_page-----19d4f55fbc31---------------------------------------)

**2. Conditions for Deleting Data Streams**

- **Must not be mapped to a DMO.**
- **Must not be used in any data transform.**
- **Must not be associated with a data kit.**

[## Help And Training Community

### Edit description

help.salesforce.com](https://help.salesforce.com/s/articleView?id=data.c360_a_delete_a_data_stream.htm&type=5&source=post_page-----19d4f55fbc31---------------------------------------)

## Web and Mobile App Connectors

- The status (e.g., active) of Web or Mobile Connectors can be checked on the app’s details page.
- Tenant-specific endpoints are automatically created when the connector setup is completed.

These connectors are also utilized in **Marketing Cloud Next** for external website tracking.

[## SFMC Tips #130 : Marketing Cloud Next: Tracking External Websites with a Consent Banner

### With Marketing Cloud Next (Marketing Cloud Growth & Advanced Editions), you can track visitor activity and engagement…

medium.com](/@marketingcloudtips/marketing-cloud-on-core-tracking-external-websites-with-a-consent-banner-2492904a799c?source=post_page-----19d4f55fbc31---------------------------------------)

## 4. Identity Resolution (8 Questions)

- Describe matching and how its rule sets are applied.
- Reconcile data and describe how its rule sets are applied.
- Describe the results of identify resolution and use cases.

## Identity Resolution

### Identity Resolution Process

Identity resolution proceeds sequentially by first applying match rules for identification, followed by reconciliation rules. This process can be executed in the following ways:

- **Manual Execution:** Can be run at any time, with a maximum of 4 executions per day.
- **Scheduled Execution:** Runs automatically once every 24 hours (schedule timing is not configurable via UI).

**Note:** Starting from Summer ’25 release, the scheduled execution frequency has been updated to once every 12 hours.

### Identity Resolution Outputs

The following artifacts are produced from the identity resolution process:

- **Unified Profile**  
  Represents the unified data but does not directly include individual IDs.
- **Unified Link**  
  Holds both the Unified Profile ID and individual IDs, acting as a “**bridge**” between them. This unified link is used when relating unified profiles to other objects.

## Match Rules and Reconciliation Rules

Identity resolution consists of two main processes:

**1. Match Rules**

- The process of grouping profiles based on common criteria.

**2. Reconciliation Rules**

- Summarize key attributes of the unified data and determine which information should take precedence.

![]()

### Rules and Rule Sets

Matching criteria are set using rules and rule sets:

- **Rule**  
   Adding more criteria lowers the unification rate. (“**AND**” condition)
- **Rule Set**  
   A collection of multiple rules; adding more conditions increases the unification rate. (“**OR**” condition)

### Rule Set Configuration

Within an account, the following four rule sets can be created:

- Unified Individual (Current Rules)
- Unified Individual (Improved Rules)
- Unified Account (Current Rules)
- Unified Account (Improved Rules)

### Reconciliation Rules

Reconciliation rules determine which information is prioritized based on these criteria:

- **Last Updated**  
   Prioritizes the most recent data.
- **Most Frequent**  
   Prioritizes the data value that appears most often.
- **Source Priority**  
   Follows a predefined priority order of data sources.

The “**Ignore Empty Values**” option can be used to exclude blank fields during reconciliation.

### Party Identification-Based Match Rules

Party Identification includes the following elements to identify individuals or accounts:

- **Party Identification ID:** The primary key of the record.
- **Party:** Foreign key linked to individual or account IDs.
- **Party Identification Type:** Represents the type of identifier, e.g., vehicle license plate, membership ID, social security number.
- **Identification Name:** A label for the identifier, e.g., driver’s license, My Number card.
- **Identification Number:** The actual ID value used for comparison.

**Important:** When using Party Identification IDs, the following elements **must match** for successful matching:

- **Party Identification Type**
- **Identification Name**
- **Identification Number**

[## Help And Training Community

### Edit description

help.salesforce.com](https://help.salesforce.com/s/articleView?id=data.c360_a_partyidentifier.htm&type=5&source=post_page-----19d4f55fbc31---------------------------------------)

## 5. Segmentation and Insights (11 Questions)

- Define basic concepts of segmentation and use cases.
- Identify scenarios for analyzing segment membership.
- Configure, refine, and maintain segments within Data Cloud.
- Identify and differentiate between calculated and streaming insights.

## Calculated Insights

### Calculated Insights — Measure Limitations

**Allowed:**

- Measures can be added to existing calculated insights.
- Only aggregatable measures can be added to aggregatable calculated insights.
- Any measure can be added to non-aggregatable calculated insights.

**Not Allowed:**

- Existing measures cannot be deleted.
- API names, data types, and roll-up behaviors cannot be changed.

### Calculated Insights Using SQL — Key Points

**Naming convention:**

- Measures and dimensions must end with `__c`.

**Requirements:**

- Measures must include aggregation functions.
- At least one measure is required.

**Restrictions:**

- Only numeric measures are supported (e.g., `MAX(Date)` is not allowed).
- Temporary tables are not supported.

### Metrics on Metrics

Calculated Insights can reference other Calculated Insights.

**Example:**

```
SELECT  
  NTILE(50) OVER (ORDER BY SUM(NTO_Email_Open_Count_cio.email_open_count_c) DESC) AS customerengagementbuckets_c,  
  NTO_Email_Open_Count_cio.customer_id_c AS customer_id_c  
FROM  
  NTO_Email_Open_Count_cio  
GROUP BY  
  customer_id_c
```

**Advantages:**

- **Reusability:** Metrics can be reused efficiently across multiple scenarios.
- **Simplification of complex insights:** By breaking down into smaller logical steps, it becomes easier to display and manage features such as “breakdowns”.

**Limitations:**

- Metrics nesting is limited to a maximum of 3 levels.

## Streaming Insights

Streaming Insights enables near-real-time construction of time-series aggregations.

**Characteristics:**

- No batch updates based on schedules.
- Aggregation timeframes can be set **from a minimum of 1 minute to a maximum of 24 hours**.

**Scope:**

- Long-term data analysis, such as over the past week exceeding 24 hours, is not supported.
- For durations longer than 24 hours, Calculated Insights must be used.

**Notes:**

- Streaming Insights cannot be used in “**Segments**” or “**Activations**”.
- Insights capable of triggering Data Actions are limited to “Web SDK”, “Mobile SDK”, and “MC Personalization”. They do not include DMO or DLO.

### SQL Considerations for Streaming Insights

Enables low-latency near real-time data analysis.

**Window Functions:**

- Required for setting aggregation time windows.
- Allowed range: 1 minute minimum to 24 hours maximum.

**Restrictions:**

- Only `SUM` and `COUNT` aggregation functions are allowed.

## Segmentation

### DMOs That Can Be Used for Segmentation

- **Profile-type DMOs:** Segments can be created on any profile-type DMO.
- **Engagement-type DMOs:** From June 2025, segmentation will also be supported on engagement-type DMOs.

### Segment Condition Settings

- **Direct Attributes:** Attributes linked 1:1 with the segmented DMO.
- **Related Attributes:** Attributes linked 1-to-many with the segmented DMO.

[## SFMC Tips #92 : Marketing Cloud Next: Basics of Segment

### When leveraging Marketing Cloud Next (Marketing Cloud Growth & Advanced Edition), designing effective segments is…

medium.com](/@marketingcloudtips/marketing-cloud-on-core-basics-of-segmentation-d240bb357d3d?source=post_page-----19d4f55fbc31---------------------------------------)

### Publishing a Segment

Creates the following DMOs in the profile DMO:

- **Segment Membership — Latest:** Profile data at the most recent segment publish time.
- **Segment Membership — History:** Profile data at past segment publish times.

### Condition Setting: Single Container vs Separate Containers

**Example conditions:**

- Color data: Yellow
- Product data: Shoes

**Single Container Condition:**

- If the condition is set as “Color = Yellow AND Product = Shoes” within the same container, the result includes only profiles who purchased **yellow shoes**.
- The color and product must be in the same purchase record. For example, customers who bought yellow shoes only qualify; those who bought blue shoes or yellow clothes do not.

**Separate Containers Condition:**

- If “Color = Yellow” and “Product = Shoes” are set in separate containers combined with AND, the result includes customers who:
- Purchased **any yellow product** AND
- Purchased **any shoes** (not necessarily yellow shoes).
- This means customers who bought yellow clothes in one record and blue shoes in another will be included.

### Key Points

- Single container: Conditions must be satisfied in the same purchase record.
- Separate containers: Conditions can be satisfied across different purchase records.

Choose the condition setting according to the objective:

- Use single container to find customers interested in **yellow shoes**.
- Use separate containers to find customers who have purchased **yellow products and shoes** at different times.

### Value Suggestion

**Overview:**

- Enables value suggestions when segmenting text attributes to prevent input errors.

**Settings:**

- Can be enabled/disabled on the DMO record home.

**Considerations for Value Suggestion:**  
1. It may take up to **24 hours** to generate the recommended value list.  
2. A maximum of 1,000 values can be displayed for a single attribute.  
3. Values exceeding 255 characters are not recommended.  
4. Impact on credit consumption:  
Enabling suggested values for text fields allows Data Cloud to periodically read selectable values from the data in the Data Model Object (DMO). This process occurs at fixed intervals of every 15 minutes and cannot be changed.

### Troubleshooting Segment Errors

**1. Error:** “Segment references too many data lake objects (DLOs).”

- Use a Calculated Insight (CI) to reduce the number of DLOs referenced by your segment.
- Split a segment into multiple smaller segments.

**2. Error:** “Segment is too complex.”

- Use a CI instead of many attributes and nested operators.
- Use a CI instead of an attribute (data model object) with many relationships.
- Combine text values into one `Is In` text operator.

[## Help And Training Community

### Edit description

help.salesforce.com](https://help.salesforce.com/s/articleView?id=data.c360_a_segmentation_troubleshooting.htm&type=5&source=post_page-----19d4f55fbc31---------------------------------------)

## 6. Act on Data (11 Questions)

- Define activations and their basic use cases.
- Use attributes and related attributes.
- Identify and analyze timing dependencies affecting the Data Cloud lifecycle.
- Troubleshoot common problems with activations including accepted/rejected counts, errors, and not seeing related attributes.
- Use data actions and identify their requirements and intended use cases.

## Activation

### Activation Process

1. **Select Segment (= Data Segment Object) (Required)**
2. **Select Activation Target (Activation Membership) (Required)**
3. **Select Contact Point (Required)**
4. **Add Attributes (Optional)**
5. **Activate Segment (Required)**

**Note:**  
When the Contact Point is set to Email, entries without an email address will be excluded during activation, reducing the number of activated entries compared to the total segment size.

### Activation Targets

The following platforms are available for activation:

- Cloud File Storage (GCS, S3, Azure)
- Marketing Cloud
- Data Cloud
- External activation platforms (Google Ads, Meta, etc.)
- B2C Commerce Cloud
- MC Personalization

**Note:**  
**Salesforce CRM is *not* included**. Do not confuse with CRM data actions.

**Commerce Cloud** and **MC Personalization** automatically set activation targets upon connection to Data Cloud. Others require manual configuration.

### Additional Attributes for Activation

The following types of attributes can be added during activation:

If Path 1 is selected, attributes from Path 2 cannot be used. \*Multiple paths are currently available.

**1. Direct Attributes:**  
Attributes that exist directly within the activation target object itself.

**2. Related Attributes:**  
Available when there is a path between the activation target object and the related object, and the relationship is either 1:1 or N:1.

**Notes:**

- (***\*Multiple paths are currently available.***) Attributes cannot be selected across multiple paths. Only attributes from a single DMO on one path can be chosen.
- Activations including related attributes are limited to a maximum of 100.
- If the limit is reached, you can either remove related attributes from existing activations or create a new activation using only direct attributes.

**3. Calculated Insights:**  
Only **metrics** can be added. **Dimensions** can be used for filtering but cannot be used as attributes for activation.

**Important:** Starting from the July 2025 new feature release, **“Multi-Path Support for Related Attributes”** is now available. With this update, you can extract attributes simultaneously from multiple Data Model Object (DMO) paths.

This enhancement enables personalized campaigns that combine data from different domains — such as purchase history and engagement data — **without needing to flatten the data or perform post-processing.**

**Note:** The number of DMOs involved in activations (including those with intermediate joins) is limited to a maximum of **8 DMOs**.

### Considerations

**1. Engagement Data Lookback:**  
A maximum lookback window of 90 days is applied, and only data within this timeframe can be used.

**2 .Segment Size Validation:**  
The size of a segment is validated during activation. Segments containing related attributes cannot be activated if they exceed 10 million records.

**3. Personalization Enablement:**  
In Marketing Cloud Engagement, JSON data can be parsed using SSJS, GTL, or AMPscript to generate messages tailored to individual users.

**Filter Function Differences**

- **Segmentation Filter**: Extracts users who meet specific conditions.
- **Activation Filter**: Selects attributes required for message personalization.

### Reactivating Activations

Do not use the “Deactivate” option if you only wish to temporarily pause activation. Once deactivated, the segment cannot be reactivated.

- Instead, change the publication schedule to “**Don’t Refresh**”.

### Customizing Attribute Names

During output, you can specify a “Preferred Attribute Name” to align with the naming conventions of the target system. However, the preferred name will not carry over to subsequent activations using the same attribute.

### Activation with Amazon S3

Two types of files are created during activation:

- **CSV file:** Contains the activated data payload (attributes and values).
- **JSON file:** Contains metadata and segment details (configuration, conditions, etc.).

**Note:**  
At first activation, an S3 subfolder named `Salesforce-c360-Segments` is automatically created.

**File naming format:**  
`YYYY/MM/DD/HH/{first 100 characters of segment name}/{20-character activation name}_{timestamp in yyyyMMddHHmmsssSSS format}`

### Other Storage Platforms

Behavior varies for Google Cloud Storage and Microsoft Azure Blob Storage. Please refer to official documentation for details.

[## Help And Training Community

### Edit description

help.salesforce.com](https://help.salesforce.com/s/articleView?id=data.c360_a_find_segments_in_cloud_file_storage.htm&type=5&source=post_page-----19d4f55fbc31---------------------------------------)

## Audience DMO

By using Audience Data Model Objects (DMO), you can analyze longitudinal changes in activated audiences.

**Features:**

- Including “**Data Cloud**” as a target allows access to segment data without connecting external systems.
- Data can be retrieved via Query API like other DMOs.

[## Help And Training Community

### Edit description

help.salesforce.com](https://help.salesforce.com/s/articleView?id=data.c360_a_create_dc_audience_dmo_activation_target.htm&type=5&source=post_page-----19d4f55fbc31---------------------------------------)

## Data Actions

**Triggerable Events:**

- Events in CRM platforms
- Email sends and journeys in Marketing Cloud
- External processes via webhook

**Note:**  
When displaying Data Cloud data on a CRM record page, one data action is consumed per setting.

[## SFMC Tips #62 : Data Cloud: Triggering Journey Builder with Data Actions

### Leveraging Data Cloud’s Data Actions allows you to send emails in Content Builder or start journeys in Journey Builder…

medium.com](/@marketingcloudtips/how-to-trigger-journey-builder-with-data-actions-73d26c5810a7?source=post_page-----19d4f55fbc31---------------------------------------)

## Closing Remarks

I hope this article has been helpful to you.

The learning and experiences gained through the exam process offer valuable opportunities for personal growth. Discovering new insights and feeling your knowledge and skills steadily improve is a great joy.

To everyone aiming for certification, please keep challenging yourself!

That’s all for this time.

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
