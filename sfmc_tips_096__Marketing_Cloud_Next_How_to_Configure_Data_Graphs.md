# SFMC Tips #96 : Marketing Cloud Next: How to Configure Data Graphs

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-on-core-personalization-1af8d9aa9026

---

# SFMC Tips #96 : Marketing Cloud Next: How to Configure Data Graphs

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--1af8d9aa9026---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--1af8d9aa9026---------------------------------------)

7 min read

·

Apr 3, 2025

--

Photo by [Nathan Lee](https://unsplash.com/@nhathongle?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

In Marketing Cloud Next (Marketing Cloud Growth & Advanced Edition), when selecting fields for **dynamic content** or **merge fields** in content, or when specifying fields for **decision splits** in flows, you can leverage the **Data Cloud data graph**. This enables you to deliver personalized messages tailored to each individual contact.

The data graph is extremely powerful — it allows you to reference not only **direct attributes** tied to leads or contacts, but also **related attributes** from objects associated with them. This makes it possible to flexibly use these attributes for merge fields in emails or as branching conditions in flows.

### Personalization Features Covered in This Article

- ✖️ Unified Individual Data Model Object (Direct Attributes)
- ⭕ **Data Graph (Direct & Related Attributes)**
- ✖️ [Event Data](/@marketingcloudtips/marketing-cloud-on-core-personalization-part-2-8d0efb6402af)
- ️✖️ [Personalization Recommender](/@marketingcloudtips/marketing-cloud-next-repeater-component-and-recommender-fb41b9c72ad0) (Salesforce Personalization)

## The Role of a Data Graph

A Data Graph visually represents the relationships between Data Model Objects (DMOs) centered around the **Unified Individual** object.

![]()

## Data Graph Considerations

Because it is difficult to make significant changes to a Data Graph after it has been built, it is recommended to carefully design it in advance before creating it.

### Limits on Available Objects and Fields

Data Graphs have limits on the number of data models that can be used.

- Data Model Objects (DMOs): Maximum 25
- Fields: Maximum 200

**Note:** Only include the objects and fields that are truly required.

### Objects and Fields Cannot Be Removed After Saving

- Once you click **Save & Build** in a Data Graph, any objects and fields that you added **cannot be removed** later.
- If the Data Graph is built with an incorrect design, you may need to recreate it from scratch. While the **Data Graph itself can be deleted**, rebuilding it may require significant effort.

### Relationships Are Limited to Six Levels

- A Data Graph supports relationships of up to **six levels** starting from the primary DMO.
- If your data model requires chaining many related objects together, be sure to consider this hierarchy limitation during the design phase.

### Increased Number of Available Data Graphs

- As of **April 14, 2026**, the maximum number of Data Graphs that can be created in a single organization has increased from **10** to **25**.
- Please note that **SDO (demo environments)** are still limited to a maximum of **three** Data Graphs.

***Tip:*** *Because Data Graphs offer limited flexibility after they are built, it is recommended to start with a minimal configuration and expand incrementally as you validate your design.*

## Steps to Configure the Data Graph

**1.** In the Marketing Cloud app, make the **Data Graphs** tab visible and click **New**.

**2.** For a new Data Graph, click **Start from Scratch** and proceed.

*\*If you are editing an existing Data Graph, skip to Step 5.*

**3.** Select **Standard Data Graph** as the Data Graph type.

**4.** Specify a name for the Data Graph and select **Unified Individual** as the Primary Data Model Object. It will not appear unless Identity Resolution has been completed.

**5.** First, select the fields from Unified Individual that are required for display and personalization. These fields become the available **direct attributes**.

**6.** Click the plus (+) icon on the right side of Unified Individual.

**7.** Related objects and Calculated Insights are displayed. Select **Unified Link Individual**.

***Tip:*** *Unified Link Individual serves as a bridge between Unified Individual and Individual.*

**8.** Next, connect the **Individual** object. You can continue connecting additional objects using the same process.

***Tip:*** *Fields associated with the Individual DMO can easily be used as* ***Attribute*** *values within flows.*

**9.** After connecting the related objects, select the fields you want to use. Since objects and fields that have been built cannot be removed later, select only the minimum required fields.

**10.** Click **Save & Build**.

**11.** Choose a Data Graph refresh schedule and click **Save & Build**. The Data Graph will then be saved and created.

### Available Refresh Schedules

- Every 30 Minutes
- Every Hour
- Every 4 Hours
- Daily
- Weekly
- Monthly

*Note: At this time, there is no* ***No Refresh*** *option.*

## Adding Ad Hoc Filters

With the Data Cloud feature release in October 2025, each DMO can use:

- Sort & Limit Filters (ascending/descending and record limits)
- Filter Conditions

These capabilities allow you to sort data, limit the number of records retrieved, and define retrieval conditions within the Data Graph.

### ⚠️ Be Aware of Engagement DMO Limitations

- Record Limit: Up to 10 records (expandable to 100)
- Time Limit: Most recent 7 days (expandable to 30 days)

[## SFMC Tips #211 : Marketing Cloud Next: Ad Hoc Filters for Data Graphs

### With the October 2025 release of Data Cloud, Ad Hoc Filters have been added to Data Graphs.

medium.com](/@marketingcloudtips/marketing-cloud-next-ad-hoc-filters-for-data-graphs-466c231740fe?source=post_page-----1af8d9aa9026---------------------------------------)

## Configuring the Default Data Graph

After creating your first Data Graph, navigate to:

**Setup → Reports and Optimization → Customer Engagement → Configure Basic Personalization**

Then select the Data Graph you created.

This establishes the system’s **Default Data Graph**.

***Tip:*** *By configuring a Default Data Graph, it is automatically assigned when opening the email editor, allowing you to start using it immediately.*

## Adding Fields to a Data Graph

### Manual Addition Required

Even if new fields are added to a DMO, they are not automatically added to the Data Graph.

To use newly added fields, edit the Data Graph from the location shown below and add them manually.

## Configuration for Einstein Send Time Optimization

To enable Einstein Send Time Optimization, add the following path to the Data Graph:

Unified Individual  
 → Unified Link Individual  
 → Individual  
 → Contact Point Email  
 → Email Send Time Optimization

Then select:

- **Hourly Scores By Week**

and enable its checkbox.

[## SFMC Tips #91 : Marketing Cloud Next: Einstein Send Time Optimization (STO)

### Marketing Cloud Next (Marketing Cloud Growth & Advanced Edition) enables you to execute various marketing scenarios…

medium.com](/@marketingcloudtips/marketing-cloud-on-core-einstein-send-time-optimization-sto-3cd4c104b162?source=post_page-----1af8d9aa9026---------------------------------------)

## Viewing Data Graph Refresh History

With the Data Cloud feature release in June 2026, a new capability was introduced to view Data Graph refresh history.

You can access it from the action menu of each Data Graph as shown below.

## Automatically Scheduling Data Graph Publication

For information on how to automatically schedule Data Graph publication, please refer to the following article.

[## SFMC Tips #208 : Marketing Cloud Next: Scheduling Identity Resolution and Data Graph

### In Marketing Cloud Next Growth & Advanced Edition, Identity Resolution and Data Graph cannot be executed on a schedule…

medium.com](/@marketingcloudtips/marketing-cloud-next-scheduling-identity-resolution-and-data-graph-a63aecf1904a?source=post_page-----1af8d9aa9026---------------------------------------)

## **Delete the Data Graph Itself**

To delete the data graph itself, you must first remove its dependencies, such as **Flow Versions**, **Personalization Points**, and **Managed Content Resources**.

[## Salesforce Help

### Edit description

help.salesforce.com](https://help.salesforce.com/s/articleView?id=004693444&type=1&source=post_page-----1af8d9aa9026---------------------------------------)

**Managed Content Resources** refer to assets such as email content. However, as shown in the screenshot above, locating them manually can be challenging because you need to search by the **Content Key**, **Created By**, and **Created Date**.

Instead, go to **Query Editor** and use the **Content Key** to find the corresponding email content name. You can use the following query:

```
SELECT "Name__c"  
FROM "ManagedContent_Home__dll"   
WHERE "ContentKey__c" = 'MCZNENJZC7HNEO7LSTN2VWFQL4VI'
```

*\*For* ***Managed Content Resources only****, even after you delete them from the UI, it may take up to* ***48 hours*** *for the deletion to be fully reflected in the system.*

## Conclusion

Keep in mind that Data Graph data is refreshed according to its configured schedule.

As a result, the latest real-time data is not always available at the moment of message delivery. Instead, the data retrieved during the most recent scheduled refresh is used.

Because of this, it is important to understand both the **Data Graph refresh schedule** and the **flow delivery schedule**. Otherwise, there is a risk that messages may be delivered using outdated data.

That’s all for this article.

Stay tuned for more Salesforce Marketing Cloud tips! 😊

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
