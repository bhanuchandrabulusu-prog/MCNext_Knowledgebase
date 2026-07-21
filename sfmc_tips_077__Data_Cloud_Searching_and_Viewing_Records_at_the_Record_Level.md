# SFMC Tips #77 : Data Cloud: Searching and Viewing Records at the Record Level

**Source:** https://medium.com/@marketingcloudtips/how-to-search-and-view-records-at-the-record-level-in-data-cloud-7ee19a3ae900

---

# SFMC Tips #77 : Data Cloud: Searching and Viewing Records at the Record Level

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--7ee19a3ae900---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--7ee19a3ae900---------------------------------------)

7 min read

·

Feb 4, 2025

--

Photo by [Simon Berger](https://unsplash.com/@simon_berger?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

In Data Cloud, vast amounts of data are aggregated from various sources. Typically, data is managed at the entity level, but working with data at the record level might feel unfamiliar to some.

However, if you don’t carefully examine data at the record level before starting operations, **there’s a risk of unexpected delivery errors or aggregation mistakes**. To avoid these risks, it’s essential to understand methods for visualizing and reviewing data at the record level.

Salesforce Marketing Cloud has similar tools, such as the **Email Studio filter function** and **Query Studio**. When data is imported, these tools are used for thorough data review, and it’s the same concept here.

In this article, I’ll explain how to search and view records in Data Cloud using four tools.

## Table of Contents:

1. Data Explorer
2. Query Editor
3. Standard Reports
4. Profile Explorer

## Access Permissions

Before diving into the tools, let’s touch on access permissions.

To view and use the **Data Explorer** (1) and **Profile Explorer** (4), you need the “**Data Cloud Administrator**” or “**Data Cloud Data Warehouse Specialist**” permission set.

If someone assigned the “Data Cloud Marketing Manager” or “Data Cloud Marketing Specialist” permission set needs to use these tools, a **custom permission set must be created** and permissions granted.

You can find instructions on how to create these permission sets in the help documentation.

[## Help And Training Community

### Edit description

help.salesforce.com](https://help.salesforce.com/s/articleView?id=data.c360_a_enable_data_explorer_permissions.htm&type=5&source=post_page-----7ee19a3ae900---------------------------------------)

Additionally, the **Query Editor** (2) can be used when you have the access rights for **Data Explorer** (1).

\*You cannot access it with just the Profile Explorer permissions.

**This is because the Query Editor and Data Explorer are integrated**. When you open the Query Editor workspace, Data Explorer is included by default, so lacking access to Data Explorer will cause issues.

Now, let’s look at an overview of each tool.

## 1. Data Explorer

The **Data Explorer** is the simplest tool to review data stored in Data Cloud. The objects you can search for are limited to the following four:

- Data Lake Objects
- Data Model Objects
- Calculated Insights
- Data Graphs

By using the “Edit Columns” function, you can easily display the necessary data in a list by specifying up to 10 columns. You can view a maximum of 100 rows.

Note:

- Currently, **column edits cannot be saved**.
- The “Copy SOQL” button only fetches the maximum of 10 columns displayed.

You can also filter the data using the **built-in filter function**.

Additionally, for **Calculated Insights**, you can visualize the data through **graphs** for analysis.

## 2. Query Editor

Unlike Data Explorer, which uses filters to search and manipulate data, the **Query Editor** uses SQL to perform data searches and operations. The objects you can search for are the same as in the Data Explorer, i.e.,

- Data Lake Objects
- Data Model Objects
- Calculated Insights
- Data Graphs

The Query Editor has an autocomplete feature for field names, making it efficient to write queries. To use this feature, you need to drag and drop the relevant object to the top of the screen.

Note:

- Query timeout is limited to 5 minutes.
- There is no paging for query results, so all rows are displayed. If the result exceeds 10,000 rows, the page may crash, so it’s recommended to use a **LIMIT of 10000**.

You can also **save queries** for future reuse, making it an ideal tool for data analysis or specific extractions.

The Query Editor integrates **Data Explorer** in the workspace, so rather than using **Data Explorer** separately, you can open the workspace in the Query Editor and use Data Explorer from there.

Here’s an example of a query that can be used in the Query Editor:

- Query sample for extracting merged data after creating Unified Individuals. (Email-based)

```
SELECT UnifiedssotIndividualCcid__dlm.ssot__Id__c AS UnifiedId__c  
, ssot__Individual__dlm.ssot__Id__c AS IndividualId__c  
, ssot__ContactPointEmail__dlm.ssot__Id__c AS ContactPointEmailId__c  
, ssot__Individual__dlm.ssot__DataSourceId__c AS DataSourceId__c  
, ssot__Individual__dlm.ssot__DataSourceObjectId__c AS DataSourceObjectId__c  
, ssot__Individual__dlm.ssot__FirstName__c AS FirstName__c  
, ssot__Individual__dlm.ssot__LastName__c AS LastName__c  
, ssot__Individual__dlm.ssot__Birthdate__c AS Birthdate__c  
, ssot__ContactPointEmail__dlm.ssot__EmailAddress__c AS EmailAddress__c  
  
FROM UnifiedssotIndividualCcid__dlm   
JOIN UnifiedLinkssotIndividualCcid__dlm  
ON (UnifiedssotIndividualCcid__dlm.ssot__Id__c = UnifiedLinkssotIndividualCcid__dlm.UnifiedRecordId__c)  
JOIN ssot__Individual__dlm  
ON (UnifiedLinkssotIndividualCcid__dlm.SourceRecordId__c = ssot__Individual__dlm.ssot__Id__c)  
JOIN ssot__ContactPointEmail__dlm  
ON (ssot__Individual__dlm.ssot__Id__c = ssot__ContactPointEmail__dlm.ssot__PartyId__c)  
  
WHERE (SELECT COUNT(*) FROM UnifiedssotIndividualCcid__dlm AS UnifiedssotIndividualCcid__dlm2  
JOIN UnifiedLinkssotIndividualCcid__dlm AS UnifiedLinkssotIndividualCcid__dlm2  
ON (UnifiedssotIndividualCcid__dlm2.ssot__Id__c = UnifiedLinkssotIndividualCcid__dlm2.UnifiedRecordId__c)  
JOIN ssot__Individual__dlm AS ssot__Individual__dlm2  
ON (UnifiedLinkssotIndividualCcid__dlm2.SourceRecordId__c = ssot__Individual__dlm2.ssot__Id__c)  
  
WHERE UnifiedssotIndividualCcid__dlm.ssot__Id__c = UnifiedssotIndividualCcid__dlm2.ssot__Id__c) >= 2  
  
ORDER BY UnifiedId__c ASC, IndividualId__c ASC, ContactPointEmailId__c ASC  
LIMIT 10000
```

- Query sample for extracting merged data after creating Unified Individuals. (Email & Phone Number-based)

```
SELECT UnifiedssotIndividualCcid__dlm.ssot__Id__c AS UnifiedId__c  
, ssot__Individual__dlm.ssot__Id__c AS IndividualId__c  
, ssot__ContactPointEmail__dlm.ssot__Id__c AS ContactPointEmailId__c  
, ssot__ContactPointPhone__dlm.ssot__Id__c AS ContactPointPhoneId__c  
, ssot__Individual__dlm.ssot__DataSourceId__c AS DataSourceId__c  
, ssot__Individual__dlm.ssot__DataSourceObjectId__c AS DataSourceObjectId__c  
, ssot__Individual__dlm.ssot__FirstName__c AS FirstName__c  
, ssot__Individual__dlm.ssot__LastName__c AS LastName__c  
, ssot__Individual__dlm.ssot__Birthdate__c AS Birthdate__c  
, ssot__ContactPointEmail__dlm.ssot__EmailAddress__c AS EmailAddress__c  
, ssot__ContactPointPhone__dlm.ssot__FormattedE164PhoneNumber__c AS PhoneNumber__c  
  
FROM UnifiedssotIndividualCcid__dlm   
JOIN UnifiedLinkssotIndividualCcid__dlm  
ON (UnifiedssotIndividualCcid__dlm.ssot__Id__c = UnifiedLinkssotIndividualCcid__dlm.UnifiedRecordId__c)  
JOIN ssot__Individual__dlm  
ON (UnifiedLinkssotIndividualCcid__dlm.SourceRecordId__c = ssot__Individual__dlm.ssot__Id__c)  
JOIN ssot__ContactPointEmail__dlm  
ON (ssot__Individual__dlm.ssot__Id__c = ssot__ContactPointEmail__dlm.ssot__PartyId__c)  
JOIN ssot__ContactPointPhone__dlm  
ON (ssot__Individual__dlm.ssot__Id__c = ssot__ContactPointPhone__dlm.ssot__PartyId__c)  
  
WHERE (SELECT COUNT(*) FROM UnifiedssotIndividualCcid__dlm AS UnifiedssotIndividualCcid__dlm2  
JOIN UnifiedLinkssotIndividualCcid__dlm AS UnifiedLinkssotIndividualCcid__dlm2  
ON (UnifiedssotIndividualCcid__dlm2.ssot__Id__c = UnifiedLinkssotIndividualCcid__dlm2.UnifiedRecordId__c)  
JOIN ssot__Individual__dlm AS ssot__Individual__dlm2  
ON (UnifiedLinkssotIndividualCcid__dlm2.SourceRecordId__c = ssot__Individual__dlm2.ssot__Id__c)  
WHERE UnifiedssotIndividualCcid__dlm.ssot__Id__c = UnifiedssotIndividualCcid__dlm2.ssot__Id__c) >= 2  
  
ORDER BY UnifiedId__c ASC, IndividualId__c ASC, ContactPointEmailId__c ASC, ContactPointPhoneId__c ASC  
LIMIT 10000
```

\*Replace the “Ccid” part with your own **Ruleset ID (4 digits)**.

## 3. Standard Reports

You can create reports based on objects within Data Cloud using Salesforce’s standard reporting features.

By utilizing the relationship model of Data Cloud, you can create reports using pre-joined objects (e.g., **Individual related to Unified Individual**). This allows for efficient reporting even with slightly complex data structures.

**■ Data Cloud Reports and Dashboards: Limitations**

[## Help And Training Community

### Edit description

help.salesforce.com](https://help.salesforce.com/s/articleView?id=analytics.rd_dc_reports_dashboards_limits.htm&type=5&source=post_page-----7ee19a3ae900---------------------------------------)

Additionally, for Calculated Insights, reports can be easily created through the following link, so it’s useful to keep this in mind.

**■ Considerations for Data Cloud Reports on Calculated Insights**

[## Help And Training Community

### Edit description

help.salesforce.com](https://help.salesforce.com/s/articleView?id=analytics.rd_dc_reports_calculated_insights_limits.htm&type=5&source=post_page-----7ee19a3ae900---------------------------------------)

## 4. Profile Explorer

It is limited to searches focused on the “**Unified Account**” and “**Unified Individual**” objects. It is ideal for deeply analyzing and visualizing unified data through ID resolution and is used to gain a deeper understanding of customer profiles.

Similar to the Data Explorer (1), you can select up to 10 columns to display.

A key point to note when searching is that **“fuzzy search” is not available**. For example, in the case above, searching for “Nobuyuki” as the First Name will not return results if you search with just “Nobu” as shown below.

Keep in mind that **only “exact matches” will be displayed**.

On this point, the Standard Reports feature (3) allows you to set search criteria like “contains”, so if you need a “fuzzy search”, try using the search in Standard Reports.

## Conclusion

I introduced four tools for searching and displaying Data Cloud records. Each tool has specific features and uses, so please use them according to your needs:

- For simple checks: **Data Explorer**
- For complex queries and extractions: **Query Editor**
- For efficiently analyzing related data: **Standard Reports**
- For deep diving into customer profiles: **Profile Explorer**

By leveraging these tools, let’s efficiently analyze and utilize Data Cloud data.

That’s all for this article.

Stay tuned for more Salesforce Marketing Cloud tips! 😊

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
