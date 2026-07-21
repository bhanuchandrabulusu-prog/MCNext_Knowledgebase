# SFMC Tips #216 : Restoration of Records Cleared from a Data Extension

**Source:** https://medium.com/@marketingcloudtips/restoration-of-records-cleared-from-a-data-extension-44a14d558197

---

# SFMC Tips #216 : Restoration of Records Cleared from a Data Extension

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--44a14d558197---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--44a14d558197---------------------------------------)

2 min read

·

Dec 14, 2025

--

Photo by [Yana Hurska](https://unsplash.com/@yana_hurska?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

In the [Winter ’26 release](/@marketingcloudtips/marketing-cloud-engagement-winter-26-release-highlights-b32181d3e42a) of Marketing Cloud Engagement, a new feature was introduced that allows you to restore records that were cleared using **“Clear Data”** in a data extension.

With this feature, records that were removed by a full clear operation can be restored **within 30 days** after the clear is executed.

## **Notes on What Can Be Restored**

In Contact Builder, it has always been possible to delete records individually. However, records deleted in this way are **not** covered by this new restoration feature. Only records deleted using **Clear Data** can be restored.

In addition, records deleted by a **Data Retention Policy** are also excluded from restoration. Because records removed by a retention policy are treated as [**permanently deleted**](https://help.salesforce.com/s/articleView?id=000387245&type=1), they cannot be recovered, even by Salesforce Support.

## What’s Changed

Previously, there was already a way to restore an entire deleted data extension **with its records intact**.

With this new release, an additional safety net has been added for scenarios such as:

- Accidentally clicking the **“Clear Data”** button
- Unintentionally deleting all records in a data extension

In these cases, you can now recover the records, significantly improving operational safety when managing data extensions.

## Where Cleared Data Is Managed

“Cleared Data” eligible for restoration is managed under:

**Contact Builder Data Extensions > Recycle Bin > Cleared Data folder**

> ***Note:*** *If the Trash folder does not appear, it will be shown after you perform a* ***Clear Data*** *operation on any data extension once.*

## Important Considerations When Restoring

- Restored records **do not return to the original data extension**
- They are restored as a **new, separate data extension**

If you need to move the data back into the original data extension, use one of the following methods:

- SQL Query Activity
- Import Activity

to insert or migrate the data accordingly.

## Final Thoughts

For those who regularly handle data deletion and maintenance, this is a feature that can provide significant peace of mind just by knowing it exists.  
I recommend taking this opportunity to familiarize yourself with it.

Please note that when you use retention policies to delete all records based on a specific period or date, the deleted data is not retained as “cleared data” and cannot be restored.

That’s all for this time.

Stay tuned for more Salesforce Marketing Cloud tips! 😎

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
