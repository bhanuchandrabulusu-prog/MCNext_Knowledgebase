# SFMC Tips #65 : Changes to Engagement Data Retention Policy: 180 Days

**Source:** https://medium.com/@marketingcloudtips/changes-to-engagement-data-retention-policy-180-days-d7d31cc837c5

---

# SFMC Tips #65 : Changes to Engagement Data Retention Policy: 180 Days

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--d7d31cc837c5---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--d7d31cc837c5---------------------------------------)

4 min read

·

Nov 20, 2024

--

Photo by [Joshua Hoehne](https://unsplash.com/@joshua_hoehne?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

## About the Changes

As announced on April 28, 2025, the latest update extends the data access period to **730 days (2 years)**. This change will take effect starting **June 16, 2025**.

For more details, please refer to the article below.

[## SFMC Tips #108 : Changes to Engagement Data Retention Policy: 730 Days

### Previously, I wrote an article stating that starting May 15, 2025, the retention period for engagement data in…

medium.com](/@marketingcloudtips/changes-to-engagement-data-retention-policy-730-days-1935685b18af?source=post_page-----d7d31cc837c5---------------------------------------)

Starting May 15, 2025, the period during which engagement data in Salesforce Marketing Cloud Engagement will remain accessible will be reduced to 180 days. Think of this change as aligning the retention period for engagement data with “Data Views”, making it easier to understand.

⚠️ ***The change was initially scheduled for January 15, 2025, but on January 3, 2025, the deadline was revised and has now been postponed to May 15, 2025****.*

## Impacted Reports

The term “engagement data” is broad, but here are the reports that will be affected by this change:

**■ Engagement data from Email Studio Tracking**

**■ Standard Reports in Analytics Builder**, including:

- Journey Builder Email Send Summary
- Journey Builder Email Send Summary by Day
- Unengaged Subscribers for a List
- Single Email Performance by Device
- Region Performance for Triggered Sends Over Time
- Subscriber Most Recent Activity
- Subscriber Engagement

When it comes to whether metrics like “Open Rate” or “Click Rate” on the tracking screen in Email Studio are recalculated in an incomplete manner after six months, or if they remain unaffected, it seems that the metrics themselves are not impacted. Instead, only access to detailed engagement data at the subscriber level is lost. Therefore, the “Open Rate” and “Click Rate” will not display abnormal values even after six months have passed.

💡 **Note:** Data Views and Intelligence Reports will not be impacted by this change.

## Exporting Data

### 🔶 [**Marketing Cloud Engagement Data Retention Help**](https://help.salesforce.com).

[## Help And Training Community

### Edit description

help.salesforce.com](https://help.salesforce.com/s/articleView?id=002231187&type=1&utm_source=techcomms&utm_medium=email&utm_campaign=FY25_Marketing_Cloud&source=post_page-----d7d31cc837c5---------------------------------------)

If you wish to store data beyond 180 days, Salesforce recommends automating the process of exporting and compressing the data to an external location, such as Amazon S3 (a paid service). The Help document outlines how to set this up, so be sure to check it out.

Although storing the data in a data extension is another option, this may not be feasible for organizations with large-scale sends involving millions of records. For such cases, exporting to an external location is likely necessary.

For smaller to mid-sized senders, storing data in a data extension should suffice. If you need more information on managing data extensions, check out my related article for reference.

[## SFMC Tips #20 : Extracting Subscribers Who Haven’t Opened Emails in the Last 180 Days Using…

### In your organization, is there a possibility that subscribers who have not opened any emails in the past 180 days might…

medium.com](/@marketingcloudtips/extracting-subscribers-who-havent-opened-emails-in-the-last-180-days-using-automation-studio-27c0d1c9bb80?source=post_page-----d7d31cc837c5---------------------------------------)

## Additional Notes

If your Marketing Cloud Engagement contract date is before April 10, 2024, here’s what you need to know:

***My Marketing Cloud Engagement contract is dated before April 10, 2024. How much data can I access?***

- *Beginning on May 15, 2025, the most recent 180 days of subscriber engagement data will be accessible in your reports, but Salesforce will retain the data indefinitely. After your next contract renewal, your data retention period changes to 180 days.*

This means that if your organization signed a “**New Contract**” or “**Renewed its agreement**” on or after April 10, 2024, you will lose access to data older than 180 days starting May 15, 2025.

**\*Please note that the contract date includes not only the initial contract date but also the contract renewal date**.

## About Intelligence Reports

Here’s some supplementary information about Intelligence Reports, which you’ll likely rely on more going forward:

- Intelligence Reports retains two years of data based on **EventDate**.
- When installed, Intelligence Reports retrieves data from the past 90 days. Older data will not be imported.
- Data is managed outside Marketing Cloud (on AWS), with daily data transfers from Marketing Cloud to Intelligence Reports. These transfers occur at varying times depending on the account, and you cannot modify the timing.

If a day’s data appears missing in the dashboard, it might be due to a failed transfer. Although retries are attempted, some data may still be lost. If this happens, submit a case within 90 days to reprocess the missing data.

### What Happens to Engagement Data After Contact Deletion?

If a contact is deleted, numerical engagement data (e.g., opens, clicks) is not deleted since it doesn’t contain personally identifiable information. This ensures metrics like open and click rates remain unaffected.

However, if you’re using the **paid version of Intelligence Reports Advanced**, which integrates personally identifiable information from data extensions, deleted contacts will no longer be linked. This process typically takes 1–3 days, although Salesforce guarantees it will be completed within 90 days.

### Timezone Settings

Even in child business units, the same timezone as the parent business unit will be applied.

### Using Intelligence Reports on Hyperforce

When Intelligence Reports operates on Hyperforce, engagement data is stored and processed in **Data Cloud**, which may affect your Data Cloud billing.

That’s all for now. Let’s keep an eye on these changes and adapt our processes accordingly!

Thank you for reading.

Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
