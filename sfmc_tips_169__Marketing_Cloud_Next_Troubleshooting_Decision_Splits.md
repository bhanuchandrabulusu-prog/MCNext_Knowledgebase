# SFMC Tips #169 : Marketing Cloud Next: Troubleshooting Decision Splits

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-next-troubleshooting-decision-splits-73e2ab3ac40f

---

# SFMC Tips #169 : Marketing Cloud Next: Troubleshooting Decision Splits

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--73e2ab3ac40f---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--73e2ab3ac40f---------------------------------------)

6 min read

·

Sep 4, 2025

--

Photo by [Angelo Pantazis](https://unsplash.com/@angelopantazis?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

When using decision splits (decision element) in flows in **Marketing Cloud Next (Marketing Cloud Growth & Advanced Edition)**, leveraging the **data graph** is a prerequisite. If the split does not work as expected, first check the contents of the data graph. If the required data does not exist, the split will not be executed.

For instructions on how to configure the data graph, please refer to the article below.

[## SFMC Tips #96 : Marketing Cloud Next: How to Configure Data Graphs

### In Marketing Cloud Next (Marketing Cloud Growth & Advanced Editions), you can deliver personalized messages to…

medium.com](/@marketingcloudtips/marketing-cloud-on-core-personalization-1af8d9aa9026?source=post_page-----73e2ab3ac40f---------------------------------------)

## Access Permissions for Query Editor

The most efficient way to check the contents of the data graph is by using the **Query Editor**. However, access to the Query Editor requires specific permissions.

**Required Permission Sets:**

- Data Cloud Administrator
- Data Cloud Data Aware Specialist

On the other hand, if a user does not have the above permission sets but has either the **Data Cloud Marketing Manager** or **Data Cloud Marketing Specialist** permission set, the following additional steps are required to use Query Editor:

1. Create a custom permission set with **Data Explorer** access enabled.
2. Assign the created permission set to the user.

> ***Note:*** *“Data Explorer” is the data search function within Query Editor. Normally, only Data Cloud Administrators and Data Aware Specialists have access. For details on how to create a custom permission set, please refer to the* [*help documentation*](https://help.salesforce.com/s/articleView?id=data.c360_a_enable_data_explorer_permissions.htm&type=5)*.*

## Steps to Check the Contents of a Data Graph

1. Open **Query Editor** and select **Data Graphs** from the menu on the left.

2. Select the data graph currently being used in Marketing Cloud.

3. The object tree within the data graph will be displayed. Open the **Data Explorer** tab here.

4. Up to 20 unified individual IDs are displayed. Click any ID to view the contents of the data graph in JSON format.

5. Use the unified individual ID you want to investigate to locate the target record.

## If the Unified Individual ID Is Unknown

6. If you don’t know the unified individual ID, open a new tab.

7. Copy the following custom SQL query, replace the `***` with the individual ID (the 18-digit Salesforce ID of a contact, lead, prospect, etc.), and run it.

```
SELECT UnifiedId, Id, FirstName, LastName, Email, DataSource, IRUpdatedDate  
FROM (  
    SELECT  
        b.UnifiedRecordId__c AS UnifiedId,  
        b.SourceRecordId__c AS Id,  
        d.ssot__FirstName__c AS FirstName,  
        d.ssot__LastName__c AS LastName,  
        c.ssot__EmailAddress__c AS Email,  
        b.ssot__DataSourceObjectId__c AS DataSource,  
        DATE_ADD('hour', 9, b.CreatedDate__c) AS IRUpdatedDate,  
        -- b.CreatedDate__c + interval '9 hour' AS IRUpdatedDate, /*for Unified Data Cloud SQL*/  
        ROW_NUMBER() OVER (  
            PARTITION BY b.SourceRecordId__c, c.ssot__EmailAddress__c  
            ORDER BY c.ssot__LastModifiedDate__c DESC  
        ) AS rn  
    FROM  
        IndividualIdentityLink__dlm a /* ← Replace with the API name of your Unified Link Individual DMO */  
    LEFT OUTER JOIN IndividualIdentityLink__dlm b /* ← Replace with the API name of your Unified Link Individual DMO */  
        ON a.UnifiedRecordId__c = b.UnifiedRecordId__c  
    LEFT OUTER JOIN ssot__ContactPointEmail__dlm c   
        ON b.SourceRecordId__c = c.ssot__PartyId__c  
    LEFT OUTER JOIN UnifiedIndividual__dlm d /* ← Replace with the API name of your Unified Individual DMO */  
        ON a.UnifiedRecordId__c = d.ssot__Id__c  
    WHERE a.SourceRecordId__c = '***' /* Individual Id Filter */  
) t  
WHERE rn = 1  
ORDER BY Id  
LIMIT 10
```

> *\*The system time in* ***Query Editor is displayed in UTC****. In my country, Japan, I need to add 9 hours, so I have adjusted it accordingly. Please make adjustments based on your own time zone.*

8. The unified individual ID will be displayed in the leftmost column. Copy this value.

9. Go back to the **Data Graphs** tab in Query Editor and search using the unified individual ID.

## Checkpoints for Data Required in Decision Splits

From the search results, for example, if you can confirm that the **Company Industry** equals **Technology**, then a decision split (decision element) based on “Industry = Technology” can be executed.

If the value in the data graph is **blank** or if the target field does not exist at the “time of sending”, the split will not be executed, and the flow will proceed along the **default path**.

**Example of a blank value in the data graph**

Possible reasons for being unable to retrieve values include:

- The CRM field value is **NULL**
- The mapping between the DLO and DMO is incorrect
- The data graph has not been updated

First, check whether the value of the target field for the split is being retrieved correctly. If the value is retrieved as expected, the decision split will generally function correctly.

## Additional Checkpoints When Decision Splits Do Not Work Correctly

Even so, decision splits (decision element) may fail due to timing mismatches such as:

- The timing of **identity resolution**
- The timing of **data graph updates**
- The timing of when **data is sent in the flow**

Verify that these are executed in the correct sequence. If not, adjust accordingly to ensure the split functions properly.

## Confirming with the Flow Debug Feature

After checking the contents of the data graph using the steps above, you can easily verify whether a decision split (decision element) works correctly by using the **Flow Debug** feature.

For the basics of the Debug feature, please refer to the article below.

[## SFMC Tips #157 : Marketing Cloud Next: Debugging Segment Trigger Flows

### In Marketing Cloud Next (Marketing Cloud Growth & Advanced Edition), the flow debugging feature is equivalent to the…

medium.com](/@marketingcloudtips/marketing-cloud-next-debugging-segment-trigger-flows-80efef3c4e7a?source=post_page-----73e2ab3ac40f---------------------------------------)

### **Steps**

1. Open the flow and create a split based on “Industry = Technology”.

2. Click the **Debug** button.

3. Click **Select Data Cloud Record.**

4. Set a filter using the unified individual ID obtained from Query Editor earlier, and select the displayed unified individual ID.

5. Run without test sending.

6. Confirm that the split executed correctly.

By knowing this quick way to inspect the contents of a data graph, you can troubleshoot issues much faster.

And this method is not only useful for troubleshooting **decision splits (decision element)**, but also when problems occur with **content personalization fields** and similar features.

That’s all for this time.

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
