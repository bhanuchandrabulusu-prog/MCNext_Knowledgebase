# SFMC Tips #289 : Marketing Cloud Next: Analysis Features Using CRM Analytics Lenses

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-next-analysis-features-using-crm-analytics-lenses-ec76f8886356

---

# SFMC Tips #289 : Marketing Cloud Next: Analysis Features Using CRM Analytics Lenses

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--ec76f8886356---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--ec76f8886356---------------------------------------)

5 min read

·

May 8, 2026

--

Photo by [Agence Olloweb](https://unsplash.com/@olloweb?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

When using Marketing Cloud Next Growth & Advanced Editions, there may be situations where **you want to download and analyze Data 360 data in Excel**.

Previously, [I introduced methods for exporting data to spreadsheets](/p/cb672a47228a), but as an easier way to perform analysis, you can use CRM Analytics Lenses.

- **A separate CRM Analytics license is required.**
- **You can download up to 50,000 rows at one time.**

In this article, I will explain the basic analysis methods using “**CRM Analytics Direct Data for Data 360**”.

## Basic Usage

1. Open the “Data Model” tab in Data Cloud. If you see the “Explore in Analytics” button in the upper-right corner, this feature is available.

2. Clicking this button will navigate to the “**Analytics**” tab and open a screen called a “**Lens**”.

Analysis of the target DMO starts automatically, but initially it only displays the “Record Count” (example below: 3,900 records), so **first switch to** “**Table View**”.

3. At this point, there may be low-value fields included, so remove unnecessary fields.  
(\*Note: The final remaining field cannot be removed.)

4. After that, add the required fields.

The user experience feels very similar to Salesforce CRM Reports.

5. The required fields have now been prepared.

Currently, only a single DMO is referenced, but it is also possible to easily join with other DMOs. Click “**Manage**”.

6. Then, objects related to the current DMO (in this case, the Email Engagement DMO) will be displayed, allowing you to specify how to join them.

- **Left Join**
- **Right Join**
- **Inner Join**
- **Outer Join**

7. Once a DMO is added, **fields from the joined DMO also become available**.

## Data 360 SQL Is Available

1. The biggest advantage of this feature is that **you can directly use Data 360 SQL**.   
Open “**Query Mode**”.

2. Then, the contents currently displayed in the table view are automatically generated as SQL.

3. Delete the generated SQL and, for example, rewrite and execute the query as shown below.  
This example retrieves data based on Email Engagement while joining multiple DMOs.

```
SELECT  
    a.ssot__IndividualId__c AS Id,  
    a.ssot__SendtimeEmailAddress__c AS Email,  
    i.ssot__FirstName__c AS FirstName,  
    i.ssot__LastName__c AS LastName,  
    a.ssot__EngagementDateTm__c + interval '9 hour' AS EngagementDateTime,  
    a.ssot__EngagementChannelActionId__c AS ActionName,  
    a.ssot__EmailRecipientSendStatus__c AS SendStatus,  
    c.ssot__Name__c AS EmailElementAPIName,  
    e.ssot__Name__c AS FlowName,  
    d.ssot__VersionNumber__c AS VersionNumber,  
    h.ssot__Name__c AS SegmentName,  
    a.ssot__EngagementActionReasonText__c AS ActionReason,  
    a.ssot__EmailBounceType__c AS BounceType,  
    a.ssot__BounceReasonText__c AS BounceReason,  
    a.ssot__UnsubscribeSourceText__c AS UnsubscribeSource,  
    a.ssot__ResolvedURL__c AS LinkURL,  
    g.ssot__Subject__c AS EmailSubject,  
    g.ssot__FromAddress__c AS FromAddress,  
    g.ssot__MessagePurpose__c AS MessagePurpose  
FROM ssot__EmailEngagement__dlm a  
JOIN ssot__FlowElementRun__dlm b ON a.ssot__FlowElementRunId__c = b.ssot__Id__c  
JOIN ssot__FlowElement__dlm c ON b.ssot__FlowElementId__c = c.ssot__Id__c  
JOIN ssot__FlowVersion__dlm d ON c.ssot__FlowVersionId__c = d.ssot__Id__c  
JOIN ssot__Flow__dlm e ON d.ssot__FlowId__c = e.ssot__Id__c  
JOIN ssot__BulkEmailMessage__dlm g ON a.ssot__BulkEmailMessageId__c = g.ssot__Id__c  
LEFT OUTER JOIN ssot__MarketSegment__dlm h ON g.ssot__MarketSegmentId__c = h.ssot__Id__c  
LEFT OUTER JOIN ssot__Individual__dlm i ON a.ssot__IndividualId__c = i.ssot__Id__c  
-- WHERE a.ssot__EngagementChannelActionId__c != 'OPEN' /*Action Name Filter*/  
-- WHERE a.ssot__IndividualId__c = '***' /*Individual Id Filter*/  
-- WHERE a.ssot__SendtimeEmailAddress__c = '***' /*Email Filter*/  
-- WHERE i.ssot__FirstName__c = '***' AND i.ssot__LastName__c = '***' /*Name Filter*/  
-- WHERE e.ssot__Name__c = '***' /*Flow Name Filter*/  
-- WHERE h.ssot__Name__c = '***' /*Segment Name Filter*/  
-- WHERE c.ssot__Name__c = '***' /*Email Element API Name Filter*/  
ORDER BY a.ssot__EngagementDateTm__c DESC  
LIMIT 10
```

4. Then, the DMOs joined within the SQL are automatically recognized, and the results are displayed directly.

*Tips: As another example,* ***I will also include a sample SQL query for “retrieving audiences included in each segment”****.  
\*You need to modify the API name of the Unified Individual — Latest DMO.*

```
SELECT  
    a.Id__c AS UnifiedId,  
    c.ssot__ExternalRecordId__c AS Id,  
    c.ssot__FirstName__c AS FirstName,  
    c.ssot__LastName__c AS LastName,  
    d.ssot__EmailAddress__c AS CurrentEmail,  
    b.ssot__Name__c AS SegmentName,  
    a.Delta_Type__c AS DeltaType,  
    a.Timestamp__c + interval '9 hour' AS PublishDateTime  
FROM Individual_Unified_SM_1755567709613__dlm a /* ← Change to your own Unified Individual - Latest DMO API name */  
JOIN ssot__MarketSegment__dlm b  
    ON a.Segment_Id__c = SUBSTRING(b.ssot__Id__c, 1, 15)  
JOIN UnifiedIndividual__dlm c /* ← Change to your own Unified Individual DMO API name */  
    ON a.Id__c = c.ssot__Id__c  
LEFT JOIN ssot__ContactPointEmail__dlm d  
    ON c.ssot__ExternalRecordId__c = d.ssot__PartyId__c  
-- WHERE b.ssot__Name__c = '***' /*Segment Name Filter*/  
-- WHERE c.ssot__ExternalRecordId__c = '***' /*Individual ID Filter*/  
-- WHERE c.ssot__FirstName__c = '***' AND c.ssot__LastName__c = '***' /*Full Name Filter*/  
ORDER BY a.Timestamp__c DESC, a.Delta_Type__c DESC  
LIMIT 10
```

## Downloading Data 360 Data

1. Downloading data using this feature is also very easy.  
From the action menu in the upper-right corner, select “Download”.

2. You can download data in the following formats:

- **PNG**
- **Excel**
- **Excel with Metadata**
- **CSV**

3. The data currently displayed on the screen can be downloaded directly as-is.

How was it?

In Salesforce official help documentation, not only simple data downloads but also more advanced analysis use cases are introduced, **such as visualizing Calculated Insights on CRM Analytics dashboards**.

Therefore, consider using this feature not only as a simple “data export tool”, but also **as an analytics foundation for Marketing Cloud Next**.

In addition, Marketing Cloud Next also includes the following standard analytics tools, so please make use of them as well.

### Marketing Cloud Next Analytics Features

- [Standard Reports and Dashboards](/@marketingcloudtips/marketing-cloud-on-core-exploring-standard-reports-and-dashboards-3fdd7ec3194c)
- [Marketing Performance Basics](/@marketingcloudtips/marketing-cloud-on-core-transforming-campaign-insights-with-marketing-performance-7c3f91f77304)
- [Marketing Performance New Features — Summer ‘25](/@marketingcloudtips/marketing-cloud-next-enhanced-marketing-performance-features-a8f691195c91)
- [Marketing Performance New Features — Winter ‘26](/@marketingcloudtips/marketing-cloud-next-marketing-performance-new-features-winter-26-bb3ed37ea55a)
- [Flow Performance](/@marketingcloudtips/marketing-cloud-next-flow-performance-analytics-feature-8301c6431cb3?postPublishedType=repub)
- [Conversion Analytics Dashboard](/@marketingcloudtips/marketing-cloud-next-conversion-analytics-dashboard-ae03ba6cb890?postPublishedType=repub)

That’s all for this time.

Stay tuned for more Salesforce Marketing Cloud tips! 😎

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
