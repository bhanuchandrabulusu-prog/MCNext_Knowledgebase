# SFMC Tips #294 : Marketing Cloud Next: Flow Save History Can Now Be Reviewed and Restored

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-next-flow-save-history-can-now-be-reviewed-and-restored-109e00034ac9

---

# SFMC Tips #294 : Marketing Cloud Next: Flow Save History Can Now Be Reviewed and Restored

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--109e00034ac9---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--109e00034ac9---------------------------------------)

3 min read

·

May 15, 2026

--

Photo by [Anna Tukhfatullina Food Photographer/Stylist](https://unsplash.com/@anna_tukhfatullina?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

In the [Summer ’26 new feature release](/@marketingcloudtips/marketing-cloud-next-summer-26-release-highlights-04f6c5abdee6) for Marketing Cloud Next Growth & Advanced Editions, a new feature was added that allows you to **review the save history of flows and easily restore them to a previous state**.

Every time a flow is saved, the history is automatically recorded, and you can review information such as:

- **Saved date and time**
- **Editing user**
- **Summary of added, modified, and deleted elements**
- **Detailed flow canvas information at the time of the save**

As a result, it is now possible to **roll back to a previous state without creating a new flow or a new version**, helping improve audit readiness, compliance, and safer improvement cycles.

## How to Use

- Each time a flow is saved, the state at that point is recorded as history.
- To access this feature, click the **“Edit History”** button.

- When you open the **“Flow Version Edit History”** panel, a list of save histories is displayed.
- By clicking **“Details”** for any saved point, you can review a brief summary of what edits were made.
- It also records **who performed the edit and save**.

- By clicking the link for the **“Saved Date and Time”,** the contents from that point in time are previewed on the canvas.
- You can review the exact state in detail, including **the configuration of each element**.

- If you ultimately want to restore that version, click **“Restore”** from the action button for the corresponding save point.

*Note: Simply executing* ***“Restore”*** *does not immediately apply the changes to the flow. After restoring, you must explicitly save the flow again.*

What did you think?

I felt this was a very useful improvement for addressing audit-related questions that are also commonly seen in Marketing Cloud Engagement, such as:

> *“Who was the last person that edited this automation or journey?”*

With this new capability in Marketing Cloud Next, it is now much easier to review edit history and trace changes safely.

In addition, even after making major temporary changes for debugging purposes, it is now **very easy to revert back to the production configuration**.

Previously, many organizations managed this by creating separate flows or separate versions, so this should also help **reduce operational overhead**.

On the other hand, as the number of save histories increases, it may become difficult to identify which version was the official production version.

For that reason, it may also become important operationally to keep a simple memo of the **“final approved save date and time”.**

That’s all for this time.

Stay tuned for more Salesforce Marketing Cloud tips! 😎

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
