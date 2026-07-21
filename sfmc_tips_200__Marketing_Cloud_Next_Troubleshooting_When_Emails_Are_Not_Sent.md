# SFMC Tips #200 : Marketing Cloud Next: Troubleshooting When Emails Are Not Sent

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-next-troubleshooting-when-emails-are-not-sent-647e5ccb2d40

---

# SFMC Tips #200 : Marketing Cloud Next: Troubleshooting When Emails Are Not Sent

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--647e5ccb2d40---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--647e5ccb2d40---------------------------------------)

5 min read

·

Nov 7, 2025

--

Photo by [Lazar Gugleta](https://unsplash.com/@lazargugleta?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

In **Marketing Cloud Next Growth & Advanced Edition**, there may be cases where emails are not sent to certain recipients even though the flow status shows as **“Completed”.**

This article summarizes the key points to check and the specific steps to investigate such situations.

![]()

🪄 **Important Concept to Understand First**  
Although flows can return many types of errors, situations such as **“segments not being properly published”** or **“data graphs not being refreshed”** are not detected as errors.  
Therefore, it’s crucial to proactively **manage and verify** these items beforehand.

🔍 **Four Key Points to Verify**  
 If emails are not being sent, check data consistency in the following order — this sequence matters:

1. Confirm that the record import into **Data Cloud** has been completed.
2. Ensure that **Identity Resolution** has been performed after step 1.
3. Verify that the target **segment** has been published after step 2.
4. Confirm that the **data graph update** has been completed after step 2.

Finally, the most efficient way to verify is to check whether any errors occur during **preview and test sends**.  
If an error appears during preview, the actual send will also fail.

### ① Confirm record ingestion into Data Cloud

Run the following query in Query Editor to verify whether the data has been ingested. Specify the Individual Id to narrow the results.

```
SELECT   
    a.ssot__Id__c AS Id,  
    a.ssot__FirstName__c AS FirstName,  
    a.ssot__LastName__c AS LastName,  
    b.ssot__EmailAddress__c AS Email,  
    a.ssot__DataSourceObjectId__c AS DataSource,  
    a.ssot__IsAnonymous__c AS IsAnonymous,  
    a.ssot__LastModifiedDate__c + interval '9 hour' AS LastModifiedDate,  
    a.ssot__CreatedDate__c + interval '9 hour' AS CreatedDate  
FROM ssot__Individual__dlm a  
LEFT JOIN (  
    SELECT ssot__PartyId__c,  
           ssot__EmailAddress__c,  
           ROW_NUMBER() OVER (PARTITION BY ssot__PartyId__c ORDER BY ssot__LastModifiedDate__c DESC) AS rn  
    FROM ssot__ContactPointEmail__dlm  
) b ON a.ssot__Id__c = b.ssot__PartyId__c  
   AND b.rn = 1  
WHERE a.ssot__Id__c = '******************' /* Individual Id Filter */  
-- WHERE a.ssot__IsAnonymous__c = '1'  
ORDER BY a.ssot__LastModifiedDate__c DESC  
LIMIT 10
```

\*This query adds 9 hours to align with Japan Standard Time, so please adjust it according to your own time zone.

### ② Verify Identity Resolution

Run the query below with the Individual Id to confirm that a Unified Individual Id has been obtained. Also check whether `IRUpdatedDate` (the timestamp when Identity Resolution ran) is up to date.

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
        b.CreatedDate__c + interval '9 hour' AS IRUpdatedDate,  
        ROW_NUMBER() OVER (  
            PARTITION BY b.SourceRecordId__c, c.ssot__EmailAddress__c  
            ORDER BY c.ssot__LastModifiedDate__c DESC  
        ) AS rn  
    FROM  
        IndividualIdentityLink__dlm a /* ← Change to your Unified Link Individual DMO API name */  
    LEFT OUTER JOIN IndividualIdentityLink__dlm b /* ← Change to your Unified Link Individual DMO API name */  
        ON a.UnifiedRecordId__c = b.UnifiedRecordId__c  
    LEFT OUTER JOIN ssot__ContactPointEmail__dlm c   
        ON b.SourceRecordId__c = c.ssot__PartyId__c  
    LEFT OUTER JOIN UnifiedIndividual__dlm d /* ← Change to your Unified Individual DMO API name */  
        ON a.UnifiedRecordId__c = d.ssot__Id__c  
    WHERE a.SourceRecordId__c = '******************' /* Individual Id Filter */  
) t  
WHERE rn = 1  
ORDER BY Id  
LIMIT 10
```

\*This query adds 9 hours to align with Japan Standard Time, so please adjust it according to your own time zone.

### ③ Confirm the segment is published

Use the following query to check whether the Individual Id in question has been published to the segment. Check that `PublishDateTime` (the publish timestamp) is recent.

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
FROM Individual_Unified_SM_1755567709613__dlm a /* ← Change to your Unified Individual - Latest DMO API name */  
JOIN ssot__MarketSegment__dlm b  
    ON a.Segment_Id__c = SUBSTRING(b.ssot__Id__c, 1, 15)  
JOIN UnifiedIndividual__dlm c /* ← Change to your Unified Individual DMO API name */  
    ON a.Id__c = c.ssot__Id__c  
LEFT JOIN ssot__ContactPointEmail__dlm d  
    ON c.ssot__ExternalRecordId__c = d.ssot__PartyId__c  
-- WHERE b.ssot__Name__c = '***' /* Segment Name Filter */  
WHERE c.ssot__ExternalRecordId__c = '******************' /* Individual ID Filter */  
-- WHERE c.ssot__FirstName__c = '***' AND c.ssot__LastName__c = '***' /* Full Name Filter */  
ORDER BY a.Timestamp__c DESC, a.Delta_Type__c DESC  
LIMIT 10
```

\*This query adds 9 hours to align with Japan Standard Time, so please adjust it according to your own time zone.

### ④ Check data graph update status

For data graphs, rather than using a query, the most reliable method is to search using the Unified Id obtained in step ② from the Data Graph-specific UI inside Query Editor.

### ✅ Final check: preview and test sends

After completing the above checks, go to Preview and Test and confirm that no errors appear in the preview. If you see errors like the examples below, it likely means Identity Resolution or the Data Graph refresh has not completed.

**Notes on Unified Individual ID behavior**  
The Unified Individual ID can change depending on circumstances and therefore should not be treated as a fixed identifier for a given Individual Id. It is important to regularly refresh and operate using the most recent Unified Individual ID.

## Conclusion

Troubleshooting is difficult without correctly understanding the flow that produces the sendable data. Other factors may also cause errors, but start by following the steps in this article and verify them one by one.

That’s all for this time.

Stay tuned for more Salesforce Marketing Cloud tips! 😎

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
