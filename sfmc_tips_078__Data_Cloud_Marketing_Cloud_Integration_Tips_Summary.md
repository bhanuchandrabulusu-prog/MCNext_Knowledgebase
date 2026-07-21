# SFMC Tips #78 : Data Cloud: Marketing Cloud Integration Tips Summary

**Source:** https://medium.com/@marketingcloudtips/data-cloud-marketing-cloud-engagement-integration-tips-9e160167cda8

---

# SFMC Tips #78 : *Data Cloud: Marketing Cloud Integration Tips Summary*

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--9e160167cda8---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--9e160167cda8---------------------------------------)

8 min read

·

Feb 5, 2025

--

Photo by [Alex Sheldon](https://unsplash.com/@slavewire?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

In this article, I will share tips for integrating **Data Cloud** and **Marketing Cloud Engagement**. I plan to update this post regularly as I discover new information.

## How to Create a Free Demo Environment

To set up a demo environment for **Data Cloud** that you can use freely as an individual, the easiest way is to create a **Playground** from Trailhead. While there is a time limit, it’s straightforward to set up.

[## Deploy the Coral Cloud Sample App | Salesforce Trailhead

### Trailhead, the fun way to learn Salesforce

trailhead.salesforce.com](https://trailhead.salesforce.com/content/learn/projects/quick-start-explore-the-coral-cloud-sample-app/deploy-the-coral-cloud-sample-app?source=post_page-----9e160167cda8---------------------------------------)

After creating a Playground, you can follow the steps outlined in the **Agentforce Workshop** below. Even if you are a beginner in **Data Cloud**, this will guide you through the basic setup efficiently step by step.

If you only want to learn about Data Cloud, completing **Workshop 1** should suffice. Please skip all sections related to setting up Experience Cloud in the initial configuration, as well as the installation of Salesforce CLI and Visual Studio Code.

[## Agentforce Workshop | Salesforce Developers

### Get Started with Data 360 and Agentforce!

developer.salesforce.com](https://developer.salesforce.com/workshops/agentforce-workshop?source=post_page-----9e160167cda8---------------------------------------)

\*If you are a partner company, it is possible to connect to the **Marketing Cloud Engagement demo environment**. However, it takes approximately 30 minutes before the data becomes usable in the Data Stream. During this time, the data will not be displayed in the Data Stream.

## Tips Summary

If you encounter issues while configuring **Data Cloud**, refer to the tips below. They might help you find a solution.

### ① Subscriber Key Integration Logic for Marketing Cloud

When integrating a Unified ID with **Marketing Cloud**, the logic for determining the subscriber key depends on the contact points:

- **Email only**: The Individual ID linked to the record with the smallest **Contact Point Email ID** in the **Contact Point Email** object is used.
- **Phone only**: The Individual ID linked to the record with the smallest **Contact Point Phone ID** in the **Contact Point Phone** object is used.
- **Both Email and Phone**: The Individual ID linked to the record with the smallest **Contact Point Email ID** in the **Contact Point Email** object is used.

\*I’ve verified this behavior, and indeed, the Individual ID associated with the smaller **Contact Point Email ID** was adopted.

[## Help And Training Community

### Edit description

help.salesforce.com](https://help.salesforce.com/s/articleView?language=en_US&id=000396882&type=1&source=post_page-----9e160167cda8---------------------------------------)

### ② How Long It Takes for Published Segment Data to Sync with Marketing Cloud

When a segment is “published”, a shared folder and a shared data extension are created on the Marketing Cloud side, followed by the addition of records.

Depending on timing, it typically takes **about 15 to 30 minutes** from the start of publication for the records to appear. This timeframe applies not only to the initial publication but also to cases where records are updated.

\*In some cases, the synchronization was completed in under 10 minutes.

### **③ Synchronization Timeline for DEs Connected to Data Streams**

When selecting a “Data Extension” for the first time in a Data Stream, you may need to wait up to **24 hours** for the records in that Data Extension to be extracted to Data Cloud.

- During this time, the execution status will remain as **“Pending”**.
- Mapping to the DMO can be started in advance.

From the Help Documentation:  
“When the data extension is extracted for the first time, it takes up to 24 hours for data to be available in the system.”

[## Help And Training Community

### Edit description

help.salesforce.com](https://help.salesforce.com/s/articleView?id=sf.c360_a_create_marketing_cloud_data_extension.htm&type=5&source=post_page-----9e160167cda8---------------------------------------)

**Note:**  
If you want to quickly import and test data in Data Cloud, consider using **Amazon S3** or **Google Cloud Storage**.

### ④ Character Limits for Data Cloud Objects

- **Data Stream Name:** Up to **238 characters**
- **Data Stream API Name:** Not applicable
- **Data Lake Object Name:** Up to **40 characters**
- **Data Lake Object API Name:** Up to **40 characters**
- **Data Model Object Name:** Up to **40 characters**
- **Data Model Object API Name:** Up to **40 characters**

\*Data Model Objects may display an error stating “maximum of 36 characters” if the name exceeds 36 characters; however, **up to 40 characters can actually be entered**.

![]()

### ⑤ Unmapping Primary Key Fields: What You Need to Know

When unmapping fields, primary key fields cannot be removed.  
Refer to the **Help and Training Community** ([help.salesforce.com](https://help.salesforce.com/s/articleView?id=001993463&type=1)) for detailed guidance.

In short, you need to delete all associated Calculated Insights, Segments, Activations, ID Resolutions, and their display on Lightning Pages.

Be cautious, as this could lead to **reconfiguring** **the entire Data Cloud**. 😱

### ⑥ Handling Problem Records

You can **audit problematic records from “Data Stream Ingestion”** using **Data Lake Objects (DLOs)** prefixed with `PR_`.

These DLOs are created when data is ingested via connectors like **Amazon S3, Google Cloud Storage, Microsoft Azure Storage or Ingestion API**.

### Error Code Types

- **NOT\_NULL\_CONSTRAINT\_VIOLATION:**  
  The record was not ingested because a required field contains a null value, such as a null primary key.
- **TRANSFORM\_EVALUATION\_ERROR:**  
  The record was partially rejected due to errors during the field transformation process. A single record processing multiple fields may encounter multiple errors.
- **UNHANDLED\_ERROR:**  
  The record was not ingested due to an error occurring during row processing.
- **DUPLICATE\_ROW:**  
  The record was not ingested because multiple records in the batch share the same primary key.

Notes:

- **Data Cloud** retains Problem Records for **30 days**. However, if you delete a data stream containing Problem Records before the 30-day period expires, the associated Problem Records DLO will also be deleted.
- You can query the Problem Records DLO using **Data Explorer, Query Editor, or Query API**.

[## Help And Training Community

### Edit description

help.salesforce.com](https://help.salesforce.com/s/articleView?id=sf.c360_a_datastream_dlo_problem_record.htm&type=5&source=post_page-----9e160167cda8---------------------------------------)

### ⑦ Common Email Paths for Activation

*Note: This assumes that the ID fields are mapped for each “****Party”****.*

### For individuals:

`Contact Point Email.Party > Individual.Individual Id`

### For unified individuals:

`Contact Point Email.Party > Individual.Individual Id`  
`Individual.Individual Id > Unified Link Individual xxxx.Individual Id`  
`Unified Link Individual xxxx.Individual Id > Unified Individual ccid.Unified Individual Id`

Note:

- xxxx refers to your **Ruleset ID**.
- The object **Unified Link Individual ccid** acts as a bridge.
- Although the path for unified individuals is quite long, only part of it is displayed, as shown below:

\*If the correct path is not selected, a shared folder may be created in Marketing Cloud, **but the shared data extension might not be generated**. If this occurs, consider this as a potential cause.

### ⑧ Points to Note When Changing Update Methods in Activation Editing

There are two types of updates for activation: **Full Refresh** and **Incremental Refresh**.

**You can switch between these**, but note that a new data extension will be created within the same folder. As shown in the image below, two data extensions will be created.

- If you switch back to the original setting, such as **Incremental Refresh → Full Refresh → Incremental Refresh**, the initially created data extension will be **reused**.

\*Additionally, when changing the update method in activation settings, it is recommended to review the considerations in the following help document:

[## Help And Training Community

### Edit description

help.salesforce.com](https://help.salesforce.com/s/articleView?id=sf.c360_a_activation_publish_types.htm&type=5&source=post_page-----9e160167cda8---------------------------------------)

### ⑨ Data Extensions Not Cleared After a Full Refresh with Zero Segment Population

When performing a full refresh with zero records in a segment, the status will display as “Success” in Data Cloud. However, the Marketing Cloud Engagement side will not retain any import history.

To ensure that Data Extensions are cleared after sending zero records following a full refresh, you can enable a setting for your Data Cloud tenant. To request this change, please create a case with Data Cloud Support.

[## Help And Training Community

### Edit description

help.salesforce.com](https://help.salesforce.com/s/articleView?id=000578149&type=1&source=post_page-----9e160167cda8---------------------------------------)

\*If you have created a data stream from a Data Extension in Marketing Cloud Engagement, clearing the contents of the Data Extension does not empty the data stream records. For example, if you reduce the Data Extension to 1 record, the data stream will also reflect only 1 record.

### ⑩ Risks of Missing Deletions with Incremental Activation Over 30 Days

If there is a gap of more than 30 days since the last publication, there may be cases where deletions are missed during incremental activation.

*Note: This has not been personally tested. Please refer to the following help document for details.*

[## Help And Training Community

### Edit description

help.salesforce.com](https://help.salesforce.com/s/articleView?id=001397973&type=1&source=post_page-----9e160167cda8---------------------------------------)

### ⑪ Deleting Marketing Cloud Data is Not Supported in ‘Upsert’ Data Streams

### Current Limitations

- **Upsert Mode**: Deleting data within a data extension is **not supported** in this mode.
- **Full Refresh Mode**: Since all content is replaced, deletion is possible with this option.

If deletion of data from a data extension is still necessary, the only option is to delete unwanted records from the data extension within Marketing Cloud and then create a new data stream.

[## Help And Training Community

### Edit description

help.salesforce.com](https://help.salesforce.com/s/articleView?id=000396417&type=1&source=post_page-----9e160167cda8---------------------------------------)

## Addition

Additionally, I have shared other articles related to **Data Cloud** in the past, so feel free to check them out.

[## SFMC Tips #62 : How to Trigger Journey Builder with Data Actions

### Leveraging Data Cloud’s Data Actions allows you to send emails in Content Builder or start journeys in Journey Builder…

medium.com](/@marketingcloudtips/how-to-trigger-journey-builder-with-data-actions-73d26c5810a7?source=post_page-----9e160167cda8---------------------------------------)

[## SFMC Tips #81 : Understanding How to Update Data Extensions in Data Cloud

### One of the essential tasks after connecting Marketing Cloud to Data Cloud is linking your data extensions to data…

medium.com](/@marketingcloudtips/understanding-how-to-update-data-extensions-in-data-cloud-25a44bf180b7?source=post_page-----9e160167cda8---------------------------------------)

[## SFMC Tips #83 : Date vs. DateTime: Key Configuration Insights for Data Cloud Users

### This article builds on the insights shared in my earlier post, Data Cloud: Marketing Cloud Integration Tips Summary…

medium.com](/@marketingcloudtips/date-vs-datetime-key-configuration-insights-for-data-cloud-users-71bfcc6a62e3?source=post_page-----9e160167cda8---------------------------------------)

[## SFMC Tips #85 : Data Cloud: A Guide to Marketing Cloud Starter Data Bundle

### Connecting Data Cloud and Marketing Cloud

medium.com](/@marketingcloudtips/data-cloud-a-guide-to-marketing-cloud-starter-data-bundle-cecea33400c4?source=post_page-----9e160167cda8---------------------------------------)

## **Closing Remarks**

For those who are already operating Data Cloud, much of the content might have seemed quite basic. However, I hope this information proves helpful, even in a small way, for those who are just beginning to explore Data Cloud.

Please note that **Data Cloud is constantly evolving**. As a result, the features introduced in this article may change or be replaced with others in the future. Additionally, discrepancies between the described functionality and actual behavior may arise due to bug fixes or updates, so please keep this in mind.

Thank you for reading!!

Stay tuned for more Salesforce Marketing Cloud tips! 😊

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
