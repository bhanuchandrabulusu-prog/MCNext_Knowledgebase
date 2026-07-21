# SFMC Tips #108 : Changes to Engagement Data Retention Policy: 730 Days

**Source:** https://medium.com/@marketingcloudtips/changes-to-engagement-data-retention-policy-730-days-1935685b18af

---

# SFMC Tips #108 : Changes to Engagement Data Retention Policy: 730 Days

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--1935685b18af---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--1935685b18af---------------------------------------)

2 min read

·

May 1, 2025

--

Photo by [Hannes Richter](https://unsplash.com/@harimedia?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

Previously, I wrote an article stating that starting **May 15, 2025**, the retention period for engagement data in Marketing Cloud Engagement would be reduced to 180 days.

[## SFMC Tips #65 : Changes to Engagement Data Retention Policy: 180 Days

### Starting May 15, 2025, the period during which engagement data in Salesforce Marketing Cloud Engagement will remain…

medium.com](/@marketingcloudtips/changes-to-engagement-data-retention-policy-180-days-d7d31cc837c5?source=post_page-----1935685b18af---------------------------------------)

However, there has been an important update announced on **April 28, 2025**.

### Key Updates:

1. **New Effective Date**: The change has been postponed to **June 16, 2025**.
2. **Retention Period Extended**: The data retention period has been extended to **730 days (2 years)**.

**Reference**: [Help Document (help.salesforce.com)](https://help.salesforce.com/s/articleView?id=002231187&type=1)

### Reports Affected by the Policy Change:

As highlighted in my previous article, the following reports will be impacted by this change in data retention policy:

**■ Engagement data from Email Studio Tracking**

**■ Standard Reports in Analytics Builder**, including:

- Journey Builder Email Send Summary
- Journey Builder Email Send Summary by Day
- Unengaged Subscribers for a List
- Single Email Performance by Device
- Region Performance for Triggered Sends Over Time
- Subscriber Most Recent Activity
- Subscriber Engagement

**Note**: The retention period for engagement data in Data Views remains **6 months**.

## FAQs:

**If my Marketing Cloud Engagement contract started on or after April 10, 2024, how much data can I access?**  
You will have access to the most recent **730 days** of data only.

**If my Marketing Cloud Engagement contract started before April 10, 2024, how much data can I access?**  
For contracts initiated before this date, copies of sending and engagement data older than 730 days will be retained. However, this data will no longer be accessible via the UI, reports, or API. It will be deleted upon contract renewal, after which only the most recent 730 days of data will be accessible.

**Does this change apply to Hyperforce organizations?**  
 Yes, the 730-day data retention limit applies to both first-party and Hyperforce Marketing Cloud Engagement organizations.

## Final Thoughts

While the exact reasons for these changes remain unclear, it’s likely that some challenges arose with the initial plan to limit access to 180 days of data. This is the **second date revision** (January 15 → May 15 → June 16), but this is the **first time the retention period has been extended to 730 days (2 years)**.

For many users, a two-year data retention period should be sufficient, even if older data becomes inaccessible. With this update, it seems the policy is now finalized, and further changes are unlikely.

That’s all for now.

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
