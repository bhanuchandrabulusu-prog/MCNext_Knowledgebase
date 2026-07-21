# SFMC Tips #159 : Marketing Cloud Next: Tracked Links for Website Traffic Sources

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-next-tracked-links-for-website-traffic-sources-81593fde6581

---

# SFMC Tips #159 : Marketing Cloud Next: Tracked Links for Website Traffic Sources

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--81593fde6581---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--81593fde6581---------------------------------------)

4 min read

·

Aug 13, 2025

--

Photo by [Arno Smit](https://unsplash.com/@_entreprenerd?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

In **Marketing Cloud Next** (Marketing Cloud Growth & Advanced Edition), the **Tracked Links** feature allows you to track visitor behavior on external websites and identify which content led them to those external sites.

![]()

These tracked links are created in **CMS Content**.

> *This feature was released as part of the* ***Summer ’25*** *updates.*

[## SFMC Tips #106 : Marketing Cloud Next: Summer ’25 Release Highlights

### Exciting updates for Marketing Cloud Next (Marketing Cloud Growth & Advanced Edition) have been unveiled. For the first…

medium.com](/@marketingcloudtips/marketing-cloud-on-core-summer-25-release-highlights-4ad6f39c5d6d?source=post_page-----81593fde6581---------------------------------------)

## Notes on Using Tracked Links

- To protect the privacy of site visitors, obtain tracking consent via a **consent banner** on the external website.
- You can set up to **50 tracked links**.
- **Marketing Cloud Landing Pages are NOT supported**.
- The validity period of an issued tracked link URL is **5 years**.
- Linking the tracked link to a campaign is **mandatory**.
- If you make a tracked link private and then republish it, the **tracked link URL will change**.

## Steps to Create a Tracked Link

1. Make sure that the external website has the web tracking feature configured. For setup instructions, refer to the article below.

[## SFMC Tips #130 : Marketing Cloud Next: Tracking External Websites with a Consent Banner

### With Marketing Cloud Next (Marketing Cloud Growth & Advanced Editions), you can track visitor activity and engagement…

medium.com](/@marketingcloudtips/marketing-cloud-on-core-tracking-external-websites-with-a-consent-banner-2492904a799c?source=post_page-----81593fde6581---------------------------------------)

[## SFMC Tips #131 : Marketing Cloud Next: Tracking External Websites without a Consent Banner

### With Marketing Cloud Next (Marketing Cloud Growth & Advanced Editions), you can track visitor activity and engagement…

medium.com](/@marketingcloudtips/marketing-cloud-on-core-tracking-external-websites-without-a-consent-banner-467326874412?source=post_page-----81593fde6581---------------------------------------)

\*In particular, confirm that the standard URL parameters are mapped to Website Engagement as shown below.

2. In Marketing Cloud, go to the **Content** tab, click **Add**, select **Tracked Link** from the content type options, and then click **Create**.

3. Specify the name and API name for the tracked link, and select the Marketing Cloud campaign to associate with the click activity.

> *Currently, there is a* [*known issue*](https://help.salesforce.com/s/issue?id=a02Ka00000fuCarIAE) *where you can only choose from the top 10 items in alphabetical order.*

![]()

4. Enter the URL of the landing page (LP) you want to track.  
The website must already be registered in Marketing Cloud as an external website that allows activity tracking.  
 (In other words, it must be a site where the JavaScript beacon has already been embedded.)

![]()

5. Enter the UTM parameters. The example shown in the diagram assumes a tracked link to be placed on **Instagram**.

![]()

6. Save your changes and **publish** the tracked link.

7. After publishing, copy the **Tracked Link URL** from the content details page, and use it in any desired content such as Instagram, LINE, or flyer advertisements.

![]()

## Checking the Data

After clicking the Tracked Link URL above, you can check the **Website Engagement DMO** to see results like the following returned as UTM-related data.

This allows you to track the behavior of visitors who accessed your site via Instagram.

Below is a sample query text for use in **Query Editor**:

```
SELECT  
    ssot__IndividualId__c AS Id,   
    ssot__EngagementDateTm__c + interval '9 hour' AS EngagementDateTime,  
    ssot__PagePublicTitleName__c AS PageTitle,   
    ssot__EngagementChannelActionId__c AS ActionName,   
    ssot__LinkURL__c AS ClickLinkURL,  
    ssot__AnchorLinkLabelText__c AS ClinkLinkText,  
    ssot__UtmMediumName__c AS Medium,  
    ssot__UtmTermDescription__c AS Term,  
    ssot__UtmContentDescription__c AS Content,  
    ssot__UtmCampaignName__c AS Campaign,  
    ssot__UtmId__c AS CampaignId,  
    ssot__UtmSourcePlatformName__c AS SourcePlatform,  
    ssot__ReferrerURL__c AS ReferrerURL,  
    ssot__OSName__c AS OSName,  
    ssot__OSModelName__c AS OSVersion,   
    ssot__BrowserName__c AS BrowserName  
FROM ssot__WebsiteEngagement__dlm   
-- WHERE ssot__IndividualId__c = '***' /*Individual Id Filter*/  
ORDER BY ssot__EngagementDateTm__c DESC   
LIMIT 10
```

**Website Engagement**

- **ssot\_\_IndividualId\_\_c**: Individual ID (anonymous identifier)
- **ssot\_\_EngagementDateTm\_\_c**: Engagement date and time
- **ssot\_\_PagePublicTitleName\_\_c**: Web page name
- **ssot\_\_EngagementChannelActionId\_\_c**: Type of action
- **ssot\_\_LinkURL\_\_c**: Clicked link URL
- **ssot\_\_AnchorLinkLabelText\_\_c**: Link text
- **ssot\_\_UtmMediumName\_\_c**: UTM medium
- **ssot\_\_UtmTermDescription\_\_c**: UTM keyword
- **ssot\_\_UtmContentDescription\_\_c**: UTM content
- **ssot\_\_UtmCampaignName\_\_c**: UTM campaign name
- **ssot\_\_UtmId\_\_c**: UTM campaign ID
- **ssot\_\_UtmSourcePlatformName\_\_c**: Referring platform
- **ssot\_\_ReferrerURL\_\_c**: Referrer URL
- **ssot\_\_OSName\_\_c**: OS name
- **ssot\_\_OSModelName\_\_c**: OS version number

> *A new anonymous identifier is assigned if the device, browser, or cache changes.*

By following this process, you can accurately measure clicks on external websites and use the results to analyze your marketing effectiveness.

That’s all for now.

Stay tuned for more Salesforce Marketing Cloud tips! 😊

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
