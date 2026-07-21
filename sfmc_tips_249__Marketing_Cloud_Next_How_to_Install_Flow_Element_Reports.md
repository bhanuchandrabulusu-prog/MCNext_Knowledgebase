# SFMC Tips #249 : Marketing Cloud Next: How to Install Flow Element Reports

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-next-create-consent-records-with-a-subflow-dc81903fe488

---

# SFMC Tips #249 : Marketing Cloud Next: How to Install Flow Element Reports

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--dc81903fe488---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--dc81903fe488---------------------------------------)

3 min read

·

Feb 15, 2026

--

Photo by [Jordon Conner](https://unsplash.com/@jordonsconner?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

For organizations that had been using Marketing Cloud Next Growth & Advanced Editions before Spring ’26, there were previously **two standard CRM reports related to flows** available before the transition to the current **Flow Performance** feature (part of Marketing Performance).

These were the following reports.

## ① Flow Element Analytics

**Custom Report Type:** Flow Run Details by Individual  
**Stored Folder:** Flow Element

- This report allows you to review the execution status of each element, including **which element an individual is currently waiting on** and **which elements have already been completed**.
- It is also possible to identify **the causes of errors occurring within Decision elements**.

## ② Email Engagement Outcomes

**Custom Report Type:** Flow Element Run to Email Outcomes  
**Stored Folder:** Flow Email Engagement

- This report allows you to review **engagement history (opens, clicks, etc.) for each individual “Send Email” element**.
- By searching with each email element ID, it is also possible to **extract and export engagement data** related to the corresponding element.

***Note:*** *For both reports, if an Individual leaves the Data Space, that Individual will no longer appear in these reports. Please be careful when using this data to calculate engagement statistics.*

## Sudden End of New Install Availability

These were actually **very important standard reports for marketers**.

However, after Salesforce transitioned to **Flow Performance powered by Tableau Next**, these standard CRM reports **suddenly became unavailable for new installation from Setup after Spring ’26**, without any particular announcement.

As a result:

- For users who recently started using Marketing Cloud Next, these are reports they may not even know ever existed.
- For users who had been using the platform previously, these are reports that continue to function, but **suddenly became impossible to newly install**.

## Installation Method

However, at this moment, they are still installable from the following URL.

**https://[xxxxxxxxxx].lightning.force.com/packagingSetupUI/ipLanding.app?apvId=04tWs000000RrUr**

*Please replace [xxxxxxxxxx] with your own “My Domain”.*

They are probably already outside Salesforce official support coverage, but based on the actual component contents, the package only creates:

- **2 reports**
- **2 report folders**
- **3 custom report types**

Therefore, it does not appear to have a major impact on the organization itself.

If you are interested, this would be at your own responsibility, but it may still be worth installing once and reviewing the reports.

That is all for this time.

Stay tuned for more Salesforce Marketing Cloud tips! 😎

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
