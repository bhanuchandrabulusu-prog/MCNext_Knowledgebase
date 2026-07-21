# SFMC Tips #156 : Marketing Cloud Next: Leveraging Website Engagement

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-next-leveraging-website-engagement-0536c8e0e110

---

# SFMC Tips #156 : Marketing Cloud Next: Leveraging Website Engagement

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--0536c8e0e110---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--0536c8e0e110---------------------------------------)

9 min read

·

Aug 8, 2025

--

Photo by [Jess Bailey](https://unsplash.com/@jessbaileydesigns?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

With **Marketing Cloud Next** (Marketing Cloud Growth & Advanced Edition), you can track visitor activity and engagement on both landing pages and external web pages.

## Categories of Web Tracking

Web tracking can be classified into the following four patterns. Each tracking method is explained in separate linked articles:

- [Tracking Marketing Cloud landing pages **with** a consent banner](/@marketingcloudtips/marketing-cloud-on-core-tracking-marketing-cloud-landing-pages-with-a-consent-banner-3672df5f9e73)
- [Tracking Marketing Cloud landing pages **without** a consent banner](/@marketingcloudtips/marketing-cloud-on-core-tracking-marketing-cloud-landing-pages-without-a-consent-banner-d23c0ba6da52)
- [Tracking external websites **with** a consent banner](/@marketingcloudtips/marketing-cloud-on-core-tracking-external-websites-with-a-consent-banner-2492904a799c)
- [Tracking external websites **without** a consent banner](/@marketingcloudtips/marketing-cloud-on-core-tracking-external-websites-without-a-consent-banner-467326874412)

**Tips:** To track external sites such as a corporate website and Marketing Cloud landing pages as the same individual, configure the domain of the Marketing Cloud landing page as a subdomain of the corporate site’s domain using a custom domain setup. This enables tracking with the same first-party cookie.

## Trackable Activities

By configuring web tracking, you can track activities such as:

- Page views
- Scrolling to the bottom of the page
- Link clicks
- Button clicks
- Form submissions

This data is stored in the **Website Engagement DMO (Data Model Object)** via the **Experience Cloud Event Connector**, which is a Web and Mobile App Connector.

In practice, the process flows as follows:

- **Data Stream**: Experience\_Cloud\_Event\_Connector — Behavioral Events
- **Data Lake Object**: Experience\_Cloud\_Event\_Connector

**Note:** Due to the specifications of the Web and Mobile App Connector, there may be a delay of up to about 15 minutes from when a web activity occurs until the data is stored. Please refer to [this help documentation](https://developer.salesforce.com/docs/data/data-cloud-int/guide/c360-a-mobile-web-app-connector.html).

**Tip:** The Experience Cloud Event Connector is automatically configured when you go to **Settings**, search for **All Sites**, select **Marketing Landing Page Builder**, and under **Integration** choose **Add Data Cloud to Site**.

![]()

## How to check the data

After tracking data is stored, you can visualize the contents of the **Website Engagement DMO** using **Data Explorer**.

Below are typical fields you can see in Data Explorer:

- Website Engagement Id
- Individual
- Engagement Date Time
- Page Public Title
- Engagement Channel Action
- Link URL
- Anchor Link Label
- OS Name
- OS Model Name
- Browser Name

Below is the SQL I use when checking this in the Query Editor with the above fields:

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

> *※ Fields with UTM parameters can be used when configuring an external website.*

## **How to Associate with a Unified Individual ID**

Website engagement data is stored in the **Website Engagement DMO**, but the Individual ID shown there is an anonymous ID, meaning it is not linked to any specific customer ID.

Tips: If you use a different computer or browser, a separate anonymous identifier (Anonymous ID) will be recorded. Similarly, if the browser cache is cleared, it will also be recorded as a different anonymous identifier (Anonymous ID).

There are two main ways to link this anonymous ID to a customer ID:

### **1. Using “Identity Resolution”**

When a user submits a form, the 36-character anonymous ID is stored in the **Website Engagement DMO** and is also created in the **Individual DMO**.  
 Although this record contains an anonymous ID, it also retains the form data, such as the name and email address submitted in the form.

Later, if a record such as a Lead is created through a form-triggered flow, it will also be registered in the **Individual DMO**. Since this record contains the same name and email address from the form, the two records will be merged as a result.

However, if the match rules are too strict, the records may fail to match. Care should be taken when setting these rules. For example, if the form does not collect a phone number, but the phone number is included as a match criteria in Identity Resolution rules, the match will fail and Website Engagement DMO data cannot be used.

That’s where the second method comes in.

### **2. Using the “Identity Match DMO”**

When a form submission creates a record such as a Lead, a relationship record is automatically created in the **Identity Match DMO**, as shown below:

- **Record** — Anonymous identifier (Anonymous ID)
- **Matching Record** — Customer ID (Salesforce CRM ID)

> *These capabilities are powered by a technology called* ***Identity Stitching****, which links an anonymous visitor’s web activity to a known customer once their identity has been established.*
>
> *For example, when a visitor browses a company’s website, their name and email address are not yet known. As a result, activities such as page views and clicks are recorded against an anonymous ID stored in a tracking cookie rather than being associated with a specific individual.*
>
> *Later, when the visitor submits a web form or clicks a tracked link in an email, their identity can be matched using information such as their email address or Salesforce CRM Lead or Contact record. At that point, the previously anonymous web activity is associated with the known customer.*
>
> *This enables sales and marketing teams to understand which product pages the customer viewed and what content they were interested in before they ever submitted an inquiry.*
>
> *When combined with* ***Marketing Cloud Next*** *and* ***Data Cloud****, Identity Stitching helps unify customer data across multiple channels — including email, web, and mobile — providing AI with richer context for customer analysis and more accurate next-best-action recommendations.*
>
> *Please note that it can take up to* ***24 hours*** *for anonymous web activity to be linked to a known customer. This is because identity resolution is typically processed on a 24-hour schedule.*

The following section explains how to leverage this functionality using the **Identity Match DMO**.

## Utilizing the Identity Match DMO

By using the relationship records stored in the Identity Match DMO, you can easily leverage the Website Engagement DMO data linked to anonymous IDs.

To effectively use the Website Engagement DMO for segmentation and other purposes, the key is to utilize the Identity Match DMO as an intermediate bridge.

### Steps to Configure Relationships

The relationship between the Identity Match DMO and the Individual DMO is preconfigured by default. However, the relationship between the Identity Match DMO and the Website Engagement DMO must be set manually.

1. Open the Website Engagement DMO and click the **Relationships** tab.

2. Click the **Edit** button and configure the relationship as follows:

**Website Engagement — Individual**  
(N : 1)  
**Data Cloud — Identity Match — Record**

By setting this relationship, data in the Website Engagement DMO — previously based on anonymous IDs — can now be used in segments and similar applications.

**Example segment:** Customers who have scrolled to the bottom of a landing page within the last 90 days.

### Other segmentation examples:

- **Customers who have accessed the website more than 5 times in the last 30 days**  
  *(Example: potential leads that may require follow-up)*
- **Customers who have viewed the URL of the product price list page updated this week**  
  *(Example: customers likely interested in pricing)*
- **Users from opportunities lost to competitors who have viewed the introduction page of a similar service in the last 30 days**  
  *(Example: customers with potential re-approach opportunities)*
- **Customers who have read a long-scroll page all the way to the end**  
  *(Example: customers interested in detailed information)*

When using the Website Engagement DMO in decision splits within a flow, be sure to configure the appropriate settings in the data graph.

## **Configuring Identity Resolution Using Identity Match DMO**

In the previous article, I introduced how the Identity Match DMO can also be leveraged during the conversion from prospect to lead.

[## SFMC Tips #155 : Marketing Cloud Next: Identity Resolution Using Identity Match DMO

### In Marketing Cloud Next (Marketing Cloud Growth & Advanced Edition), by adding Identity Match DMO as a “Match Rule” for…

medium.com](/@marketingcloudtips/marketing-cloud-next-identity-resolution-using-identity-match-dmo-d5c47b599d5e?source=post_page-----0536c8e0e110---------------------------------------)

This same mechanism can be applied to web tracking as well. By doing so, you can prevent situations where a change to an email address later on would otherwise exclude the record from Identity Resolution.

**Step 1:** In the “Rule Set”, configure the following Match Rule:

- **Data Model Object:** Identity Match
- **Field:** Identity Match Type
- **Matching Method:** Exact (Exact Match)

**Step 2:** Next, click **Settings** under Advanced Settings, enter **“device-to-known”** in Identity Match Type, and save the rule set.

## **Summary of Identity Match Settings**

Finally, based on [the previous article about prospect conversion](/@marketingcloudtips/marketing-cloud-next-identity-resolution-using-identity-match-dmo-d5c47b599d5e), here’s a summary of the settings you should configure for Identity Match:

**- Manual relation setup between Identity Match DMO and Website Engagement DMO**

**- Add the following four types to the ID resolution matching rules** (automatically applied as OR conditions):

- Identity Match Type: `prospect-to-lead`
- Identity Match Type: `prospect-to-contact`
- Identity Match Type: `lead-to-contact`
- Identity Match Type: `device-to-known`

Be sure to incorporate these into your campaign and scenario designs.

## Conclusion

By leveraging the **Identity Match DMO**, you can reliably link web behavior data with customer IDs, enabling more precise personalization and scenario design. As demonstrated in the segment examples introduced here, this should also significantly expand the range of marketing initiatives you can execute.

Additionally, when using **Website Engagement**, it’s helpful to keep a few precautions in mind:

- If a different computer or browser is used, each instance will be recorded under a separate anonymous ID.
- If the browser cache is cleared, it will also be recorded as a separate anonymous ID.
- It’s also important to understand the cookie expiration limits for each browser. By default, [Salesforce sets the expiration to 730 days](https://help.salesforce.com/s/articleView?id=sf.mktg_consent_tracking_cookies.htm&type=5), but some browsers may override this. The major browser limitations are as follows:

### **1. Google Chrome**

- **Maximum expiration:** 400 days
- **Note:** Since Chrome 104 (August 2022), the maximum expiration that can be set via the `Expires` or `Max-Age` attribute is limited to 400 days. Previously, it was possible to set cookies several years into the future, but this limit was introduced to protect user privacy.
- **Reference:** [Chrome Developers Blog](https://developer.chrome.com/blog/cookie-max-age-expires)

### **2. Mozilla Firefox**

- **Maximum expiration:** No strict limit (recommended ~400 days)
- **Note:** Technically unrestricted, but based on HTTP best practices, around 400 days is recommended. Future browser updates may change this behavior.

### **3. Apple Safari**

- **Maximum expiration:** Up to 7 days (for first-party cookies)
- **Note:** Safari’s **Intelligent Tracking Prevention (ITP)** feature limits cookies to 7 days unless the user revisits the site, in which case the expiration may be extended.

### **4. Microsoft Edge**

- **Maximum expiration:** 400 days
- **Note:** Chromium-based Edge follows the same specifications as Chrome, with a maximum cookie expiration of 400 days.

These details are accurate as of **August 2025**, so please refer to the latest information for updates.

That’s all for this time.

Stay tuned for more Marketing Cloud Growth & Advanced Edition tips! 😊

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
