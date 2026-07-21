# SFMC Tips #85 : Data Cloud: A Guide to Marketing Cloud Starter Data Bundle

**Source:** https://medium.com/@marketingcloudtips/data-cloud-a-guide-to-marketing-cloud-starter-data-bundle-cecea33400c4

---

# SFMC Tips #85 : Data Cloud: A Guide to Marketing Cloud Starter Data Bundle

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--cecea33400c4---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--cecea33400c4---------------------------------------)

8 min read

·

Feb 25, 2025

--

Photo by [Alice Donovan Rouse](https://unsplash.com/@alicekat?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

## **Connecting Data Cloud and Marketing Cloud**

By connecting **Marketing Cloud** to **Data Cloud**, you can import data stored in Marketing Cloud into Data Cloud.

During the connection setup, you can choose from the following two types of data sources:

- **Data Extensions**
- **Starter Data Bundle**

### About Data Extensions

Data Extensions are often custom-created, so you likely already have a good understanding of their structure and contents.

### About the Starter Data Bundle

On the other hand, the **Starter Data Bundle**, which is automatically configured by Data Cloud, may be less familiar.  
 This article will help you understand its contents so that you can decide whether to connect it as needed.

> ***Note:*** *Previously, connecting data from* ***Marketing Cloud Engagement*** *required an additional fee. However, since* ***August 12, 2025****, this connection has become* ***free of charge****. Therefore, unless you are concerned about data storage capacity, it is generally recommended to establish this connection.*

[## SFMC Tips #158 : Data Cloud: Data Pipeline Credit Charges Now Free

### Previously, I posted an article about the credit charges for Data Cloud Data Pipelines (ingestion into data streams)…

medium.com](/@marketingcloudtips/data-cloud-data-pipeline-credit-charges-now-free-891916c58c1f?source=post_page-----cecea33400c4---------------------------------------)

## Overview of Data Integration with Data Cloud

### Creating Data Streams and Data Lake Objects (DLOs)

When integrating Marketing Cloud data into Data Cloud, the system automatically generates corresponding **Data Streams** and **Data Lake Objects (DLOs)** for each Starter Bundle.

### Mapping to Data Model Object (DMOs)

After creating DLOs, the system automatically maps them to **Data Model Objects (DMOs)**. However, not all fields are mapped.

The fields mapped to DMO are critical because they are used in subsequent segments, calculated insights, and other processes. It’s essential to:

1. Identify which data is automatically mapped to DMO.
2. Evaluate whether that data is truly necessary for your use case.

## Three Main Data Categories

The Starter Data Bundle is classified into the following three categories:

- **Contact-related data**
- **Journey-related data**
- **Engagement-related data**

### Update Frequencies of Data Streams

Understanding the update frequencies for data streams in the Marketing Cloud Starter Data Bundle is essential, as these vary depending on the **object category**:

- **Profile and Other Categories:** Full Refresh are performed once daily.
- **Engagement Category:** Upserts occur every hour.
- **Insights (limited to SFMC Einstein Email Scores):** Upserts occur once daily. This frequency depends on the source data, which is updated in Marketing Cloud only once a week.

By keeping these details in mind, you can effectively manage data integration and avoid unnecessary costs or data processing inefficiencies.

### Contact-Related Data

1. **SFMC Subscriber** (Category: Profile)
2. **SFMC Contact Point Email** (Category: Other)
3. **SFMC Ent Profile Attribute** (Category: Profile)

### Journey-Related Data

1. **SFMC Campaign** (Category: Other)
2. **SFMC Email Publication** (Category: Other)
3. **SFMC Email Template** (Category: Other)
4. **SFMC Journey** (Category: Other)
5. **SFMC Journey Activity** (Category: Other)
6. **SFMC Journey Activity Run (**Category: Engagement**)**

### Engagement-Related Data

1. **SFMC Email Engagement Send** (Category: Engagement)
2. **SFMC Email Engagement Open** (Category: Engagement)
3. **SFMC Email Engagement Click** (Category: Engagement)
4. **SFMC Email Engagement Bounce** (Category: Engagement)
5. **SFMC Email Unsubscribe** (Category: Engagement)
6. **SFMC Email Complaint** (Category: Engagement)

### Additional Data

1. **SFMC EES Email Snapshot** (Category: Other)
2. **SFMC Einstein Email Scores** (Category: Insights)

## Contact-Related Data

This contact-related data includes importing subscriber keys, email addresses, and attribute data.

### **1. SFMC Subscriber (Category: Profile)**

This object is used to import the “Contact Key” from “All Contacts”.

- **Subscriber Key**: Contact Key (PK)
- **Party Identification ID**: PersonIdentifier\_MCSubKey\_[Subscriberkey]
- **Party Identification Name**: Fixed Value: “MC Subscriber Key”
- **Party Identification Type**: Fixed Value: “Person Identifier”

Note: Includes the association between “Contact Key” and “Contact Id”.

> *The association between “Contact Key” and “Contact Id” represents mappings such as “Contact Key ○○○ corresponds to Contact Id △△△”. Currently, this mapping cannot be retrieved from Marketing Cloud, which can be useful in some scenarios. For example, the data view “\_PushAddress” is known to retrieve only the Contact Id, not the Contact Key.*

### **2. SFMC Contact Point Email (Category: Other)**

This object is used to import “Subscriber Key”, “Email Address”, and “Email Domain” from “All Subscribers”, not “All Contacts”.

- **Subscriber Key**: Subscriber Key (PK)
- **Email Address**: Email Address
- **Email Domain**: Email Domain
- **Is Primary Email Address**: Fixed Value: “1”

### **3. SFMC Ent Profile Attribute (Category: Profile)**

This object is used to import “Attribute” and “Preference” fields registered in “All Subscribers”.

- **Subscriber Key**: Contact Key (PK)
- **Party Identification ID**: PersonIdentifier\_MCSubKey\_[Subscriberkey]
- **Party Identification Name**: Fixed Value: “MC Subscriber Key”
- **Party Identification Type**: Fixed Value: “Person Identifier”

If you have customized customer attributes (e.g., First Name, Last Name), you need to manually map them to the DMO.

Note: HTML Email Preferences are not included in the data integration.

> ***Key Considerations****: If an attribute name is changed on the Marketing Cloud side, the data import will* ***fail****.  
> To avoid issues, avoid renaming attributes in Marketing Cloud after integration. Instead, create new attributes.  
> If renaming is absolutely necessary, recreate the “old attribute name” in Marketing Cloud. This will allow mapping to resume and resolve the import error.*

## Journey-Related Data

This journey-related data involves importing components of send jobs and Journey Builder configurations.

### **4. SFMC Campaign (Category: Other)**

Properties of the “Campaign” feature in Marketing Cloud Classic.

- **ID**: Campaign ID
- **Name**: Campaign Name
- **Start Date**: Typically NULL
- **End Date**: Typically NULL
- **Created Date**: The date the campaign was created
- **Modified Date**: The date the campaign was modified

Note: The **Is Active** field is not mapped. A value of “0” for **Is Active** indicates a deleted past campaign.

### **5. SFMC Email Publication (Category: Other)**

Records at the “job” level for email sends. Think of it as the equivalent of the “Job” data view. These are mapped to the Email Publication DMO.

- **ID**: Job ID
- **Name**: Sender Name
- **From Email**: Sender Email Address
- **Created Date**: The date the job was created
- **Modified Date**: The date the job was modified

Only the above fields are automatically mapped to the DMO. The following require custom mapping:

- **Email ID**: Email ID (not the Asset ID)
- **Email Name**: Email definition name (prone to garbled characters in Japanese)
- **Email Name 2**: Email definition name (not garbled in Japanese)
- **Send Time**: Send execution date
- **Subject Line**: Email subject
- **Email Pre Header**: Email preheader

### **6. SFMC Email Template (Category: Other)**

Property information for emails stored in Content Builder. These are mapped to the Email Template DMO.

- **ID**: Email ID (not the Asset ID)
- **Email Name**: Email definition name
- **Email Subject**: Email subject
- **Asset Type**: Fixed Value: “EmailTemplate”
- **Created Date**: The date the email was created
- **Modified Date**: The date the email was modified

### **7. SFMC Journey (Category: Other)**

Data for each “Journey Version” saved in Journey Builder. Think of it as the equivalent of the “Journey” data view. These are mapped to the Market Journey DMO.

- **ID**: Journey Version ID
- **Name**: Journey Version Name
- **Version ID**: ID of the Journey Version
- **Created Date**: The date the journey version was created
- **Modified Date**: The date the journey version was modified

The following information is available but not automatically mapped:

- **Version Number**: The version number of the journey
- **Description**: Description of the journey version
- **Status**: Current status of the journey version
- **Original Definition ID**: Journey ID
- **Last Published Date**: Last published date

Note: The Journey ID typically matches the Journey Version ID when the version is “1”.

### **8. SFMC Journey Activity (Category: Other)**

Data for each “Journey Activity” saved in Journey Builder. Think of it as the equivalent of the “Journey Activity” data view. These are mapped to the Market Journey Activity DMO.

- **ID**: Journey Activity ID
- **Name**: Journey Activity Name
- **Journey ID**: ID of the Journey Version
- **Created Date**: The date the activity was created
- **Modified Date**: The date the activity was modified

If **Name** is NULL or details are unclear, additional information can be supplemented by referring to **Type Name**.

Note: The help documentation lists this as being in the “Profile” category, but it actually falls under “Other”.

### **SFMC Journey Activity Run was added in Winter ’26.**

[## SFMC Tips #201 : Data Cloud: Journey Activity Run Added to Starter Data Bundle

### With the Winter ’26 release, the integration between Data Cloud and Marketing Cloud Engagement has been further…

medium.com](/@marketingcloudtips/data-cloud-journey-activity-run-added-to-starter-data-bundle-bbbe73434dd0?source=post_page-----cecea33400c4---------------------------------------)

## Engagement-Related Data

This engagement-related data includes user behavior data after delivery and delivery result data. When the Starter Data Bundle is activated, only data from the past 90 days will be ingested, and subsequent data will be accumulated incrementally.

Since engagement data is mapped to various fields in the DMO, please refer to the following help documentation for details. If you require the Is\_Unique field, which is also present in Data Views, you will need to map it manually.

[## Marketing Cloud Engagement: Engagement Mappings

### After a data stream is deployed, the Marketing Cloud Engagement starter data bundle automatically maps data from…

developer.salesforce.com](https://developer.salesforce.com/docs/atlas.en-us.c360a_api.meta/c360a_api/c360dm_mce_engagement.htm?source=post_page-----cecea33400c4---------------------------------------)

### **9. SFMC Email Engagement Send (Category: Engagement)**

Data equivalent to the “Sent” data view can be retrieved.

### **10. SFMC Email Engagement Open (Category: Engagement)**

Data equivalent to the “Open” data view can be retrieved.

### **11. SFMC Email Engagement Click (Category: Engagement)**

Data equivalent to the “Click” data view can be retrieved.

### **12. SFMC Email Engagement Bounce (Category: Engagement)**

Data equivalent to the “Bounce” data view can be retrieved.

### **13. SFMC Email Unsubscribe (Category: Engagement)**

Data equivalent to the “Unsubscribed” data view can be retrieved.

### **14. SFMC Email Complaint (Category: Engagement)**

Data equivalent to the “Complaint” data view can be retrieved.

## Einstein Engagement Scoring Data

### **15. SFMC EES Email Snapshot (Category: Other)**

This data is built based on the “Subscriber Key” and links email addresses currently stored in the Marketing Cloud **Einstein MC Predictive Scores** data extension with email addresses registered in **SFMC Contact Point Email** via a JOIN.

Only subscribers for whom the linkage is successful are included, and their Einstein Engagement Scores are listed. This enables subscriber key-based usage for various segments and insights.

### **16. SFMC Einstein Email Scores (Category: Insights)**

This data retains a history of updates from the **Einstein MC Predictive Scores** data extension in Marketing Cloud.

- **Einstein MC Predictive Scores** are evaluated weekly, with the latest subscriber data overwriting previous data, which is then deleted.
- In contrast, **SFMC Einstein Email Scores** accumulates historical records of deleted data, preserving past data as a history.

### Important Notes

- **SFMC Einstein Email Scores** is intended for **insights** and is not automatically mapped to the DMO.
- **Einstein Engagement Scoring** is traditionally evaluated based on “Email Address”. Therefore, a representative Subscriber Key is stored. Avoid mapping this data by Subscriber Key, as it is not meant for segmentation.
- The record with the most recent **Created Date** reflects the data currently stored in Marketing Cloud’s **Einstein MC Predictive Scores**.

## Conclusion

From my perspective, the **Starter Data Bundle** essentially provides **“Data Views”** and **“Einstein Engagement Scoring”**, which are standard features in Marketing Cloud, within **Data Cloud**.

As for **SFMC EES Email Snapshot**, it doesn’t exist as a standard feature in Marketing Cloud, but you can still retrieve the same data using **SQL queries** within Marketing Cloud. Therefore, the only data that can be obtained exclusively through this Starter Data Bundle is likely the **association between “Contact Key” and “Contact ID”** available in **SFMC Subscriber**. I hope this serves as a useful reference.

That’s all for now.

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
