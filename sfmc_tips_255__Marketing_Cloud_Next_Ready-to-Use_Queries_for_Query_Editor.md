# SFMC Tips #255 : Marketing Cloud Next: Ready-to-Use Queries for Query Editor

**Source:** https://medium.com/@marketingcloudtips/sfmc-tips-255-marketing-cloud-next-ready-to-use-queries-for-query-editor-72d1675c06d8

---

# SFMC Tips #255 : Marketing Cloud Next: Ready-to-Use Queries for Query Editor

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--72d1675c06d8---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--72d1675c06d8---------------------------------------)

7 min read

·

Feb 22, 2026

--

Photo by [Alvan Nee](https://unsplash.com/@alvannee?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

The Query Editor in Marketing Cloud Next Growth & Advanced Edition is useful for investigating data within Data Cloud. This time, I am publishing the investigative queries that I frequently use.

If you are unsure how to use the Query Editor, it would be a good idea to enter and save the following seven queries. There is a possibility that you will be able to use them somewhere.

> *※ 9 hours are added to adjust from UTC to Japan Standard Time (JST).*

## Check Email Engagement

This is useful for retrieving the latest Email Engagement information. By using the WHERE clause, you can filter by Salesforce ID, flow name, email element API name, and so on.

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

### Email Engagement

- `ssot__IndividualId__c`: Individual ID
- `ssot__SendtimeEmailAddress__c`: Email address
- `ssot__EngagementDateTm__c`: Engagement date and time (UTC)  
   ※ To match Japan time, 9 hours are added
- `ssot__EngagementChannelActionId__c`: Engagement type
- `ssot__EmailRecipientSendStatus__c`: Send status
- `ssot__EngagementActionReasonText__c`: Reason for not sending
- `ssot__EmailBounceType__c`: Bounce type
- `ssot__BounceReasonText__c`: Bounce reason
- `ssot__UnsubscribeSourceText__c`: Unsubscribe source
- `ssot__ResolvedURL__c`: Clicked link URL

### Flow Element Run

- None: for joining

### Flow Element

- `ssot__Name__c`: Email element API name

### Flow Version

- `ssot__FlowId__c`: Flow ID
- `ssot__VersionNumber__c`: Flow version number

### Flow

- `ssot__Flow__dlm`: Flow name

### Bulk Email Message

- `ssot__Subject__c`: Email subject
- `ssot__FromAddress__c`: From email address
- `ssot__MessagePurpose__c`: Commercial or transactional classification

### Market Segment

- `ssot__Name__c`: Segment name used

### Individual

- `ssot__FirstName__c`: First name
- `ssot__LastName__c`: Last name

## Check Website Engagement

This is useful for retrieving the latest Website Engagement information.

> *※ Items with UTM can be used when configuring an external website.*

```
SELECT  
    ssot__IndividualId__c AS Id,   
    ssot__EngagementDateTm__c + interval '9 hour' AS EngagementDateTime,  
    ssot__PagePublicTitleName__c AS PageTitle,   
    ssot__EngagementChannelActionId__c AS ActionName,   
    ssot__LinkURL__c AS ClickLinkURL,  
    ssot__AnchorLinkLabelText__c AS ClinkLinkText,  
    -- ssot__UtmMediumName__c AS Medium,  
    -- ssot__UtmTermDescription__c AS Term,  
    -- ssot__UtmContentDescription__c AS Content,  
    -- ssot__UtmCampaignName__c AS Campaign,  
    -- ssot__UtmId__c AS CampaignId,  
    -- ssot__UtmSourcePlatformName__c AS SourcePlatform,  
    ssot__ReferrerURL__c AS ReferrerURL,  
    ssot__OSName__c AS OSName,  
    ssot__OSModelName__c AS OSVersion,   
    ssot__BrowserName__c AS BrowserName  
FROM ssot__WebsiteEngagement__dlm   
-- WHERE ssot__IndividualId__c = '***' /*Individual Id Filter*/  
ORDER BY ssot__EngagementDateTm__c DESC   
LIMIT 10
```

### Website Engagement

- `ssot__IndividualId__c`: Individual ID (anonymous identifier)
- `ssot__EngagementDateTm__c`: Engagement date and time
- `ssot__PagePublicTitleName__c`: Web page name
- `ssot__EngagementChannelActionId__c`: Action type
- `ssot__LinkURL__c`: Click link URL
- `ssot__AnchorLinkLabelText__c`: Link text
- `ssot__UtmMediumName__c`: UTM medium
- `ssot__UtmTermDescription__c`: UTM keyword
- `ssot__UtmContentDescription__c`: UTM content
- `ssot__UtmCampaignName__c`: UTM campaign name
- `ssot__UtmId__c`: UTM campaign ID
- `ssot__UtmSourcePlatformName__c`: Source platform
- `ssot__ReferrerURL__c`: Referrer URL
- `ssot__OSName__c`: OS name
- `ssot__OSModelName__c`: OS version number
- `ssot__BrowserName__c`: Browser name

> *※ If the computer or browser is different, it will be treated as a different anonymous identifier.  
> ※ If the cache is deleted, it will also be treated as a different anonymous identifier.*

## Check Unified Record from Individual ID

When you enter an Individual ID, you can see the Unified Individual ID associated with it. If multiple Individual IDs are linked to that Unified ID, all of them will be displayed.

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
    WHERE a.SourceRecordId__c = '***' /* Individual Id Filter */  
    -- WHERE c.ssot__EmailAddress__c = '***' /*Email Address Filter*/  
) t  
WHERE rn = 1  
ORDER BY Id  
LIMIT 10
```

### Unified Link Individual

- `UnifiedRecordId__c`: Unified Individual ID (32 digits)
- `SourceRecordId__c`: Individual ID (Salesforce ID or anonymous identifier)
- `ssot__DataSourceObjectId__c`: Data source name
- `CreatedDate__c`: Last update date of ID resolution

### Contact Point Email

- `ssot__EmailAddress__c`: Current email address

### Unified Individual

- `ssot__FirstName__c`: First name
- `ssot__LastName__c`: Last name

## Check Unified Record from Unified Individual ID

When you enter a Unified Individual ID, you can see the associated Individual IDs. If multiple Individual IDs are linked, all of them will be displayed.

```
SELECT UnifiedId, Id, FirstName, LastName, Email, DataSource, IRUpdatedDate  
FROM (  
    SELECT  
        a.UnifiedRecordId__c AS UnifiedId,  
        a.SourceRecordId__c AS Id,  
        c.ssot__FirstName__c AS FirstName,  
        c.ssot__LastName__c AS LastName,  
        b.ssot__EmailAddress__c AS Email,  
        a.ssot__DataSourceObjectId__c AS DataSource,  
        a.CreatedDate__c + interval '9 hour' AS IRUpdatedDate,  
        ROW_NUMBER() OVER (  
            PARTITION BY a.SourceRecordId__c, b.ssot__EmailAddress__c  
            ORDER BY b.ssot__LastModifiedDate__c DESC  
        ) AS rn  
    FROM  
        IndividualIdentityLink__dlm a /* ← Change to your Unified Link Individual DMO API name */  
    LEFT OUTER JOIN ssot__ContactPointEmail__dlm b  
        ON a.SourceRecordId__c = b.ssot__PartyId__c  
    LEFT OUTER JOIN UnifiedIndividual__dlm c /* ← Change to your Unified Individual DMO API name */  
        ON a.UnifiedRecordId__c = c.ssot__Id__c  
    WHERE a.UnifiedRecordId__c = '***' /* Unified Individual Id Filter */  
) t  
WHERE rn = 1  
ORDER BY Id  
LIMIT 10
```

### Unified Link Individual

- `UnifiedRecordId__c`: Unified Individual ID (32 digits)
- `SourceRecordId__c`: Individual ID (Salesforce ID or anonymous identifier)
- `ssot__DataSourceObjectId__c`: Data source name
- `CreatedDate__c`: Last update date of ID resolution

### Contact Point Email

- `ssot__EmailAddress__c`: Current email address

### Unified Individual

- `ssot__FirstName__c`: First name
- `ssot__LastName__c`: Last name

## Check Consent Status from Email Address

Check the current consent status from an email address.

```
SELECT ContactPointValue, Status, SubscriptionName, ChannelName, LastModifiedDate, SourceType, SourceName  
FROM (  
    SELECT  
        a.ssot__ContactPointValueText__c AS ContactPointValue,  
        a.ssot__ConsentStatus__c AS Status,  
        c.ssot__Name__c AS SubscriptionName,  
        d.ssot__Name__c AS ChannelName,  
        a.ssot__LastModifiedDate__c + interval '9 hour' AS LastModifiedDate,  
        a.ssot__ConsentCapturedSourceType__c AS SourceType,  
        a.ssot__ConsentCapturedSourceName__c AS SourceName,  
        ROW_NUMBER() OVER (  
            PARTITION BY a.ssot__ContactPointValueText__c, c.ssot__Name__c  
            ORDER BY a.ssot__LastModifiedDate__c DESC  
        ) AS rn  
    FROM ssot__CommunicationSubscriptionConsent__dlm a  
    JOIN ssot__CommunicationSubscriptionChannelType__dlm b   
        ON a.ssot__CommunicationSubscriptionChannelTypeId__c = b.ssot__Id__c  
    JOIN ssot__CommunicationSubscription__dlm c   
        ON b.ssot__CommunicationSubscriptionId__c = c.ssot__Id__c  
    JOIN ssot__EngagementChannelType__dlm d   
        ON b.ssot__EngagementChannelTypeId__c = d.ssot__Id__c  
    -- WHERE a.ssot__ContactPointValueText__c = '***' /*Email Filter*/  
) sub  
WHERE rn = 1  
ORDER BY LastModifiedDate DESC
```

### Communication Subscription Consent

- `ssot__ContactPointValueText__c`: Contact point (channel) value
- `ssot__ConsentStatus__c`: Consent status
- `ssot__LastModifiedDate__c`: Last modified date
- `ssot__ConsentCapturedSourceName__c`: Source type where consent was captured
- `ssot__ConsentCapturedSourceType__c`: Source name where consent was captured

### Communication Subscription

- `ssot__Name__c`: Subscription name

### Engagement Channel Type

- `ssot__Name__c`: Channel type

\*If data cannot be retrieved correctly with this query, the DLO mapping is not correct. It will work correctly by replacing the mapping below. The mapping cannot be deleted, but it can be replaced.

## Check Segment from Individual ID

Check the segments in which an individual (such as by name) is participating.

> *※ The API name of Unified Individual — Latest DMO must be modified.*

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
-- WHERE c.ssot__ExternalRecordId__c = '***' /* Individual ID Filter */  
-- WHERE c.ssot__FirstName__c = '***' AND c.ssot__LastName__c = '***' /* Full Name Filter */  
ORDER BY a.Timestamp__c DESC, a.Delta_Type__c DESC  
LIMIT 10
```

### Unified Individual — Latest

- `Id__c`: Unified Individual ID
- `Delta_Type__c`: “New” or “Existing”
- `Timestamp__c`: Segment publish date and time

### Market Segment

- `ssot__Name__c`: Segment name

### Unified Individual

- `ssot__ExternalRecordId__c`: Individual ID
- `ssot__FirstName__c`: First name
- `ssot__LastName__c`: Last name

### Contact Point Email

- `ssot__EmailAddress__c`: Current email address

### Communication Subscription Consent

- `ssot__ConsentStatus__c`: Consent status (opt-in status)

## Check Identity Match Integration Status

You can retrieve records to which Identity Match has been applied by the system.

```
SELECT  
    ssot__DataSourceObjectId__c AS DataSounceName,  
    ssot__RecordId__c AS RecordId,  
    ssot__MatchingRecordId__c AS MatchingRecordId,  
 ssot__IdentityMatchType__c AS IdentityMatchType,  
    ssot__CreatedDate__c + interval '9 hour' AS CreatedDate,  
    ssot__IdentityMatchWeight__c AS IdentityMatchWeight,  
    ssot__IsAMatch__c AS IdentityMatchFlag  
FROM  
    ssot__IdentityMatch__dlm  
ORDER BY  
    ssot__IdentityMatchWeight__c DESC,  
    ssot__CreatedDate__c DESC  
LIMIT 10
```

### Identity Match

- `ssot__DataSourceObjectId__c`: Source name of the previously obtained ID
- `ssot__RecordId__c`: Previously obtained ID
- `ssot__MatchingRecordId__c`: ID obtained later
- `ssot__IdentityMatchType__c`: ID match type
- `ssot__CreatedDate__c`: Record creation date and time
- `ssot__IdentityMatchWeight__c`: Match flag (numeric)
- `ssot__IsAMatch__c`: Match flag (boolean)

### **\*Reference: Match Types**

- ID match type: “prospect-to-lead”
- ID match type: “prospect-to-contact”
- ID match type: “lead-to-contact”
- ID match type: “device-to-known”

For Identity Match, please check the following.

[## SFMC Tips #155 : Marketing Cloud Next: Identity Resolution Using Identity Match DMO

### In Marketing Cloud Next Growth & Advanced Edition, the Summer ’25 release introduced the ability to add Identity Match…

medium.com](/@marketingcloudtips/marketing-cloud-next-identity-resolution-using-identity-match-dmo-d5c47b599d5e?source=post_page-----72d1675c06d8---------------------------------------)

## Check Ingestion Status into Individual DMO

Check whether records created or edited in Salesforce CRM have been ingested into the Individual DMO via a data stream.

```
SELECT   
    a.ssot__Id__c AS Id,  
    a.ssot__FirstName__c AS FirstName,  
    a.ssot__LastName__c AS LastName,  
 b.ssot__EmailAddress__c AS Email,  
    a.ssot__DataSourceObjectId__c AS DataSource,  
    /*a.ssot__IsAnonymous__c AS IsAnonymous,*/  
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
-- WHERE a.ssot__Id__c = '***'  
-- WHERE a.ssot__IsAnonymous__c = '1'  
ORDER BY a.ssot__LastModifiedDate__c DESC  
LIMIT 10
```

### Unified Individual — Latest

- `ssot__Id__c`: Individual ID (Salesforce ID or anonymous identifier)
- `ssot__FirstName__c`: First name
- `ssot__LastName__c`: Last name
- `ssot__DataSourceObjectId__c`: Data source name
- `ssot__IsAnonymous__c`: Confirmation whether it is an anonymous profile
- `ssot__LastModifiedDate__c`: Last modified date and time
- `ssot__CreatedDate__c`: Record creation date and time

### Contact Point Email

- `ssot__EmailAddress__c`: Current email address

That is all for this time.

Stay tuned for more Salesforce Marketing Cloud tips! 😎

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
