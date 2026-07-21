# SFMC Tips #48 : New Data Copy or Import Activity Arrives in Automation Studio

**Source:** https://medium.com/@marketingcloudtips/new-data-copy-or-import-activity-arrives-in-automation-studio-e941f123f7a5

---

# SFMC Tips #48 : New Data Copy or Import Activity Arrives in Automation Studio

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--e941f123f7a5---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--e941f123f7a5---------------------------------------)

3 min read

·

Jul 9, 2024

--

Photo by [David Lezcano](https://unsplash.com/@_thedl?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

The much-anticipated **Data Copy or Import activity**, which allows the copying of values in data extensions, has finally been released in Salesforce Marketing Cloud’s Summer ’24 update.

*The traditional Import File activity has been replaced by this new activity. However,* ***the original Import File activity itself remains unaffected****.*

So, what exactly has changed? Within the activity creation flow, there is a section called SOURCE. Previously, you could only select “File Location”, meaning you had to choose from SFTP, Amazon S3, or other file storage options. Now, **you can select data extensions as a source**.

When you proceed to the File Location side, you encounter the familiar “Import” screen, which remains largely unchanged.

On the other hand, when you proceed to the Data Extension side, you are directed to the “Data Copy” screen, where you can select the source data extension.

With this feature addition, moving values between data extensions will become much smoother.

**Unlike SQL activities, Import activities do not have an auto-kill function after 30 minutes and can handle extremely large volumes of records quickly**. Therefore, it is recommended to use this feature for record transfers.

Incidentally, while this is the first time this feature appears in Automation Studio’s Import Activity, it has been available in Contact Builder’s import function for some time. So, technically, it’s not entirely new.

My primary interest was whether, **like Contact Builder’s import function, “filtered data extensions” could be selected as the source or target data extension**.

So, I checked it out right away and, **unfortunately, only “standard data extensions” are available**.

What this means is that filtered data extensions cannot use SQL’s UNION feature under normal circumstances, limiting the conditions you can set.

If filtered data extensions could be used, it would be highly convenient for users who cannot use SQL, as it would perform operations similar to UNION. However, unfortunately, it is restricted to “standard data extensions” only.

***For more information on the UNION feature with filtered data extensions****, please refer to my previous article. It’s crucial information.*

[## SFMC Tips #31 : How to Add Records to a Filtered Data Extension

### Salesforce Marketing Cloud’s filtered data extensions allow you to set specific criteria and store records that meet…

medium.com](/@marketingcloudtips/how-to-add-records-to-a-filtered-data-extension-64857d3fc4ff?source=post_page-----e941f123f7a5---------------------------------------)

Although I am slightly disappointed personally, I believe this feature is quite useful. So, let’s make the most of it!

Thank you for reading.

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
