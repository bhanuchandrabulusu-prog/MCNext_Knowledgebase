# SFMC Tips #59 : How to Check the Update and Change History of Journey Emails

**Source:** https://medium.com/@marketingcloudtips/how-to-check-the-update-and-change-history-of-journey-emails-6802f45dc051

---

# SFMC Tips #59 : How to Check the Update and Change History of Journey Emails

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--6802f45dc051---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--6802f45dc051---------------------------------------)

3 min read

·

Oct 16, 2024

--

Photo by [Jason Leung](https://unsplash.com/@ninjason?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

This article is based on a previous piece I wrote, titled “How to Update Email Content After a Journey Is Active”. Despite the usefulness of this content, it has become harder to find through searches within Medium, so I decided to publish it as a standalone article.

[## SFMC Tips #21 : How to Update Email Content After a Journey Is Active

### After activating a journey in Journey Builder, there may be instances where you want to change part or all of the email…

medium.com](/@marketingcloudtips/how-to-modify-email-content-within-the-same-version-after-activating-a-journey-5dee6fced96c?source=post_page-----6802f45dc051---------------------------------------)

When you update or modify an email in a Journey’s Email Activity, clicking the “Done” button in that activity finalizes the changes and generates a new Job ID. By searching for this Job ID, **you can identify who updated or modified the email and when the update took place**.

### Step 1

First, you’ll need the Activity ID for the email activity. I’ve previously written an article on “How to Easily Retrieve the Activity ID”, so please refer to that article to obtain the Activity ID for the email activity.

[## SFMC Tips #10 : Playful Tricks to Snatch Journey Builder Activity IDs Easily

### In the enchanting realm of Salesforce Marketing Cloud, a nifty feature called “Data Views” diligently stores customer…

medium.com](/@marketingcloudtips/playful-tricks-to-snatch-journey-builder-activity-ids-easily-2c208c6a41b2?source=post_page-----6802f45dc051---------------------------------------)

### Step 2

Once you have the Activity ID, execute the following SQL query in Query Studio:

```
SELECT j.JobId,  
       j.Category,  
       j.AccountUserID,  
       DATEADD(hh, 15, j.PickupTime) AS PickupTime  
FROM _Job j  
JOIN _JourneyActivity ja  
ON j.TriggererSendDefinitionObjectId = ja.JourneyActivityObjectId  
WHERE ja.ActivityId = '*******************************'  
AND j.Category LIKE 'version%'  
AND j.PickupTime IS NOT NULL
```

*Note: “PrckupTime” is displayed in the CST time zone, so please adjust it to your time zone.*

### Verifying the Results

This query should return two or more records with Job IDs. Among these, the Job ID with the most recent PickupTime corresponds to the time when the “Done” button was last clicked — indicating the most recent update.

If you want to check who made the changes to the email activity, refer to the AccountUserID column. This column only displays a numerical ID, not the username itself.

You can retrieve a list linking these AccountUserIDs to usernames from the Audit Trail Activity Log, as shown in the Excel sheet below. However, note that the audit log only includes AccountUserIDs for specific users, so I recommend creating a reference list by searching for the Job IDs associated with each AccountUserID.

With the Winter ’25 release, you can now obtain both the AccountUserID (User ID) and the corresponding username directly from the Journey’s audit log, making it much faster to gather this information from there.

[## SFMC Tips #58 : Winter ’25 Release Highlights: Notable New Features in Marketing Cloud

### The release notes for Salesforce Marketing Cloud Winter ’25, focusing on new features, have been published. I would…

medium.com](/@marketingcloudtips/winter-24-release-highlights-notable-new-features-in-marketing-cloud-f9ab85aac8b1?source=post_page-----6802f45dc051---------------------------------------)

By the way, I’ve written another article on how to check the update and change history for Journey Builder itself. For up to 30 days, you can easily verify this via the Journey audit log screen. If you need to check beyond 30 days, you can retrieve the data using the API.

[## SFMC Tips #24 : How to Check the Change History of Journey Builder

### Do you ever experience not knowing who made changes to Journey Builder settings? It would be convenient to be able to…

medium.com](/@marketingcloudtips/how-to-check-the-change-history-of-journey-builder-1e4015bba67c?source=post_page-----6802f45dc051---------------------------------------)

Thank you for reading.

Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
