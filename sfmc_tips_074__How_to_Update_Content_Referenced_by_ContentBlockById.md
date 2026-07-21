# SFMC Tips #74 : How to Update Content Referenced by ContentBlockById

**Source:** https://medium.com/@marketingcloudtips/how-to-update-content-referenced-by-contentblockbyid-c56741e90aa5

---

# SFMC Tips #74 : How to Update Content Referenced by ContentBlockById

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--c56741e90aa5---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--c56741e90aa5---------------------------------------)

8 min read

·

Jan 23, 2025

--

Photo by [Jason Leung](https://unsplash.com/@ninjason?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

In Salesforce Marketing Cloud email creation, reusable content blocks are often called using AMPscript functions such as `ContentBlockById`, `ContentBlockByKey`, or `ContentBlockByName`.

These functions are especially useful for dynamically referencing shared components like "headers" or "footers" that are included in all emails, or custom recommendation blocks, ensuring they are always rendered with their latest content.

However, one important limitation to be aware of is that once a journey is activated and emails are sent, a **cache is created**. Even if the referenced content in Content Builder is updated, the emails already running within the journey will not reflect these changes.

To update the content after activation, you need to “**republish**” the email. Republishing essentially means **creating a new “Job ID”** for the email activity. In this article, I will explore methods to change the Job ID and ensure the latest version of your content is reflected.

**Note**: Strictly speaking, the cache is not created when the Job ID changes but when the first email is sent after the Job ID has changed.

## How to Change the Job ID

Here are four ways to update the Job ID:

1. **Republishing from the Journey Email Activity**
2. **Republishing from Email Studio Interactions**
3. **Republishing by Creating a New Journey Version**
4. **Republishing Using the “Known Issue” of Auto Suppression List**

> Important: Currently, there has been an internal behavior change, and Method 4 is no longer available. However, it may become available again in the future, so please make sure to check the behavior of the Job ID each time you execute it.

I’ll also introduce a fifth method to **dynamically update the content without changing the Job ID using AMPscript**. While this requires some setup, it is highly effective and can resolve many issues.

Let’s dive into each approach.

### 1. Republishing from the Journey Email Activity

The simplest method to address this is to open the email activity within the journey and republish it.

1. After making changes to the email content in **Content Builder**, click on the relevant email activity, then click **Activity Summary**.

2. Next, if the content has already been updated in **Content Builder**, simply click the **Done** button. This will update the Job ID.

As previously mentioned, updating the Job ID does not create a new cache. Cache creation occurs only when the initial email is sent. Therefore, if the journey is already active and the first email is scheduled to send a month later, you are free to make changes during that one-month period.

One important note when using this method: avoid closing the screen during the saving process. Failing to adhere to this may cause the job to stop, as per the system’s specifications. For more details, refer to another article where I’ve covered this in depth.

[## SFMC Tips #6 : The Impact of Closing the Window During Email Content Saving in Journey Builder

### Efficiently managing email content in Journey Builder is crucial for successful marketing campaigns. When making…

medium.com](/@marketingcloudtips/the-impact-of-closing-the-window-during-email-content-saving-in-journey-builder-07015caccc16?source=post_page-----c56741e90aa5---------------------------------------)

### 2. Republishing from Email Studio Interactions

If you need to republish blocks used across multiple emails, such as headers or footers, it’s more efficient to handle the process via **Email Studio Interactions** rather than opening and updating each email activity individually.

1. In **Email Studio**, select the **Interactions** tab, choose the relevant journey, and select all the associated emails.

2. Click on **Pause**.

3. Then, select all the emails again and click **Publish Changes**.

4. Finally, select all the emails once more and click **Start/Resume**. At this point, the Job ID is updated. Note that the Job ID does not change when clicking **Publish Changes** — it updates when **Start/Restart** is clicked.

Be careful not to forget the **Start/Restart** step. If you skip this, the email activity will not send and will remain in the “queue”.

### 3. Republishing by Creating a New Journey Version

The method of creating a new version of a journey depends on the situation and may not always be possible. As you know, contacts currently in progress within a journey cannot be moved to a new version. Therefore, you must choose between:

1. Stopping the journey entirely and creating a new version.

2. Leaving contacts in the old version while creating a separate new version.

In the new version, the latest content will be reflected. Once the new version is created, activating it will ensure that the latest content is used. However, if you choose to leave contacts in the old version, be aware that those contacts will continue to receive emails with the old content.

### 4. Republishing Using the “Known Issue” of Auto Suppression List

The method of using the Auto Suppression List is somewhat of a workaround. Are you aware of the following “known issue”?

[## Creating an Auto Suppression list will | Known Issues

### When an Auto Suppression list is added, it will automatically republish associated triggered send definitions to…

issues.salesforce.com](https://issues.salesforce.com/issue/a028c00000tJMj5AAG/?source=post_page-----c56741e90aa5---------------------------------------)

Currently, creating an Auto Suppression List causes the Job ID to be automatically changed, which is the “known issue”. By taking advantage of this, simply creating the Auto Suppression List will change the Job ID for all email activities in the account at once.

When creating the Auto Suppression List, no configuration is necessary. Just decide on the name and click “Save”.

To explain this method in more detail, simply creating the Auto Suppression List does not immediately change the Job ID. After the list is created, the first email sent from the email activity will trigger an evaluation that the Auto Suppression List has increased, causing the Job ID to be newly generated.

Additionally, if the Auto Suppression List is “deleted”, the Job ID will also be issued in the same way. This means that after the last send, if the Auto Suppression List is created or deleted, the Job ID will be generated at the first send after that change. Therefore, even if you create and immediately delete the Auto Suppression List, the Job ID will still be generated.

**Notes**

- **Job ID Change Timing**  
  The Job ID will not be changed at the time the Auto Suppression List is created. The Job ID is issued when the first email is sent from each email activity. For example, if the first send is scheduled to occur one month later, you will need to wait one month for the Job ID to change.
- **No Need to Add Records**  
  There is no need to add records to the Auto Suppression List. Simply creating the list is sufficient.
- **Risk of Resolving the Known Issue**  
  Since this method leverages the current “known issue”, if Salesforce resolves this issue, this workaround may no longer work.

> Important: Currently, there has been an internal behavior change, and Method 4 is no longer available. However, it may become available again in the future, so please make sure to check the behavior of the Job ID each time you execute it.

## **Changing the Content Without Changing the Job ID**

### 5. **Switching Content Using AMPscript Lookup**

The last method I will introduce allows you to change content without altering the Job ID. Personally, I recommend this method.

The approach is to integrate the `Lookup` function within `ContentBlockById` as shown below. The data extension that should be used for the lookup is typically one that includes all the target recipients, such as the send master data extension.

In this send master data extension, you would store the content block IDs for elements like the “Header” and “Footer”.

```
%%=ContentBlockById(Lookup("Master_DE", "Footer", "Id", _SubscriberKey))=%%
```

To explain a bit more specifically, you create fields like “Id” for the Subscriber Key, “Header”, and “Footer” in the “Master\_DE” data extension.

This type of send master data extension is usually created via SQL. You would insert the content block IDs for the header and footer into the fields “Header” and “Footer”.

\*If you have a Footer block, the content ID for it will be listed in the corresponding red box as shown in the image.

As an example, here’s an SQL query that will assign the content block ID for the header and footer:

```
SELECT Id,  
       Email,  
       '30159098' AS [Header],  
       '30159099' AS [Footer]  
FROM DataExtension
```

With this setup, the “Footer” field will always have the value “30159099” fixed.

Once the setup is complete, you just need to include the `ContentBlockById` with the `Lookup` in your email and send it.

```
%%=ContentBlockById(Lookup("Master_DE", "Footer", "Id", _SubscriberKey))=%%
```

If you want to change the footer, rather than editing the content of “30159099”, you should create a new content block (e.g., “Footer2”) using the duplication function and then edit that.

For instance, if the content ID for the duplicated “Footer2” is “30159100”, you would modify the SQL query as follows:

```
SELECT Id,  
       Email,  
       '30159098' AS [Header],  
       '30159100' AS [Footer]  
FROM DataExtension
```

Once this SQL is executed and the values are reflected in the send master data extension, the footer in the subsequent emails will be updated to the new content ID “30159100”.

The key here is using `Lookup` to change the target. Even if you modify the content of “30159099”, the cache will remain, and the old content will still be displayed, so be careful.

It is also assumed that the Subscriber Key for the recipient is included in the Master Send Data Extension being referenced by the `Lookup` function. If it is not included and the email is sent, it will not simply send without the header or footer being displayed; instead, an internal error will occur, and the email will not be sent at all.

## **Conclusion**

If you only need to change content blocks used in a single email, I believe method 1 would be the best approach. However, if you need to make changes to 100 or 1,000 emails, it can be quite cumbersome. In such cases, I suggest exploring methods 4 and 5.

By the way, regarding method 4, I think it could be considered a “forbidden” practice in formal operations, and you might receive a reprimand from Salesforce itself. However, personally, I view it as a clever hack (in a positive sense), so if it’s acceptable within your company, feel free to give it a try.

That’s it for now — thank you for reading!

Stay tuned for more Salesforce Marketing Cloud tips! 😊

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
