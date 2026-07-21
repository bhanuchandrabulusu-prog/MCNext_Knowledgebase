# SFMC Tips #123 : Missing Data Reprocessing Feature for Intelligence Reports Released

**Source:** https://medium.com/@marketingcloudtips/missing-data-reprocessing-feature-for-intelligence-reports-released-4b77b77ed928

---

# SFMC Tips #123 : Missing Data Reprocessing Feature for Intelligence Reports Released

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--4b77b77ed928---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--4b77b77ed928---------------------------------------)

3 min read

·

May 28, 2025

--

Photo by [Brooke Cagle](https://unsplash.com/@brookecagle?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

As a new feature in Marketing Cloud Engagement, the functionality to “**reprocess missing report data in Intelligence Reports without creating a support case**”, announced during the **Spring ’25** release, has been officially launched. This article explains the details and usage of this new feature.

[## SFMC Tips #76 : Marketing Cloud Engagement: Spring ’25 Release Highlights

### Salesforce has announced the new features in the Spring ’25 Release for Marketing Cloud, and I would like to highlight…

medium.com](/@marketingcloudtips/marketing-cloud-spring-25-release-key-highlights-and-insights-51c43496c538?source=post_page-----4b77b77ed928---------------------------------------)

## Why This Feature Is Necessary

Since Intelligence Reports operates on AWS, data is transferred from Marketing Cloud Engagement through batch processing. As a result, real-time data verification is not possible (data is delayed by a day), and sometimes data transfers fail.

Previously, when data was missing or some anomaly occurred, users had to create a Salesforce support case and request assistance. With this new feature, users can now execute reprocessing directly from a dedicated interface, enabling more efficient operations.

## Setup Instructions

The reprocessing feature has been added to the **Data Management** tab within Intelligence Reports.

## Status Confirmation

Three types of statuses can be checked on the screen:

- **SUCCESSFUL** (Success)
- **PENDING** (Pending)
- **INVALID** (Invalid)

## Checking Execution History

1. Click **Execution History** to view all past execution logs (including both automatic and manual processes).

**Note:** Previously, under the specifications of Intelligence Reports, execution history exceeding 90 days was excluded from reprocessing via support cases. However, when I attempted to reprocess data older than 90 days, no processing errors occurred. That said, it is recommended to process within 90 days to ensure optimal results.

**2. Start Execution Time** indicates the execution date and time of the transfer.

**Note:** Even if you have not used SMS or WhatsApp in the past, you may still see some execution history.

## Executing Reprocessing

1. Click **Select a date** to choose the period for reprocessing. The maximum range for a single reprocessing session is 7 days.

2. If a range exceeding 7 days is selected, the error message **“Date range cannot be greater than 7 days”** will appear.

3. When a valid range is selected, the message **“Data stream processing has started”** will appear, indicating that reprocessing has begun.

**Note:** After performing a reprocessing operation, you cannot perform the same reprocessing operation again for 24 hours.

## Summary

With the introduction of this new feature, it has become possible to visualize data transfer errors and perform reprocessing promptly. This enables users to transition away from operations reliant on case submissions and manage data more efficiently. If you encounter missing data, be sure to take advantage of this functionality.

That’s all for this time.

Stay tuned for more Salesforce Marketing Cloud tips! 😊

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
