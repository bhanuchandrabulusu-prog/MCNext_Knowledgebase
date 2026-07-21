# SFMC Tips #213 : Data Cloud: Manual Full Refresh for CRM and SFMC Data Streams

**Source:** https://medium.com/@marketingcloudtips/data-cloud-full-refresh-for-crm-and-sfmc-data-streams-62b30ba01b10

---

# SFMC Tips #213 : Data Cloud: Manual Full Refresh for CRM and SFMC Data Streams

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--62b30ba01b10---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--62b30ba01b10---------------------------------------)

3 min read

·

Dec 10, 2025

--

Photo by [Erik Mclean](https://unsplash.com/@introspectivedsgn?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

In my view, this is the most impactful enhancement in the November release of Data Cloud — **you can now manually run a “Full Refresh”** on both CRM and Marketing Cloud Engagement data streams.

> *The feature was already available for Marketing Cloud Engagement in November, but* ***starting today, December 10th****, it’s now supported on the CRM side as well. 🎉*

## The struggle before…

Until now, running a full refresh required one of the following “workarounds”:

- Waiting for the standard refresh that happens once every two weeks
- Asking Salesforce Support (which sometimes took a week due to approval steps…)
- Forcing a refresh by connecting a new field
- Forcing a refresh by deleting a field

…none of these were ideal, and they often required time-consuming operations.

## Now, just one button

From the UI, you can now choose between:

- Full Refresh (complete reload)
- Incremental Refresh (standard)

## Why this matters

For example, if you change the logic of a formula field in CRM, that field value is technically updated, but the **Last Modified Date** doesn’t change.

As a result, Data Cloud doesn’t detect the update, and the revised values are **not** passed over.

💡 **Tip:** Data Cloud’s incremental refresh only updates records where the “Last Modified Date” changed, which corresponds to the date value below:

Previously, you had to trigger field updates manually via Developer Console or through other tricks. But with Full Refresh, **that problem is gone.**

## What the full refresh actually does

When you run a full refresh, existing data is removed and rebuilt from scratch using the latest values.  
 In other words — you always get the latest state.

And now, the refresh interval (previously fixed at two weeks) can be changed to any of the following:

- **No automatic refresh**
- **10 days (new default)**
- **25 days**
- **50 days**

![]()

## And it’s FREE

Until August 12, 2025, data processing from CRM incurred usage-based costs.  
But now, **you can refresh as many times as you want without charges.**

[## SFMC Tips #158 : Data Cloud: Data Pipeline Credit Charges Now Free

### Previously, I posted an article about the credit charges for Data Cloud Data Pipelines (ingestion into data streams)…

medium.com](/@marketingcloudtips/data-cloud-data-pipeline-credit-charges-now-free-891916c58c1f?source=post_page-----62b30ba01b10---------------------------------------)

Practically speaking, you now have “unlimited refresh”. 🚀

## Final thoughts

This new feature is truly a **game changer**.  
Development speed improves dramatically, and data sync testing, troubleshooting, and validation become much easier.

I’ve been waiting a long time for this update — so please give it a try!

*Note: This is a fantastic update, however, a full refresh of data streams has a significant impact on the cost of Identity Resolution.*

*In environments that utilize Unified Individual (such as Marketing Cloud Next), it may be acceptable during the development phase, but in production, it is important to avoid full refreshes as much as possible.* [*Please refer to this article for more details*](/@marketingcloudtips/marketing-cloud-next-key-points-to-be-careful-about-in-identity-resolution-ffa5f9484aed)*.*

That’s it for now.

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
