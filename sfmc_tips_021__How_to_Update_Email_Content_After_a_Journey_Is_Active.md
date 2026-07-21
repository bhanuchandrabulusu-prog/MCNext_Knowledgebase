# SFMC Tips #21 : How to Update Email Content After a Journey Is Active

**Source:** https://medium.com/@marketingcloudtips/how-to-modify-email-content-within-the-same-version-after-activating-a-journey-5dee6fced96c

---

# SFMC Tips #21 : How to Update Email Content After a Journey Is Active

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--5dee6fced96c---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--5dee6fced96c---------------------------------------)

5 min read

·

Feb 2, 2024

--

Photo by [Andhika Soreng](https://unsplash.com/@dhika88?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

After activating a journey in Journey Builder, there may be instances where you want to change part or all of the email content. This article outlines the method for making such changes.

Once a journey is activated, editing an email in Content Builder does not automatically update the email content within the journey.

For the person wanting to change the email content, **intentionally pressing the “Done” button on Journey Builder is the key step** to initiate the update.

Here are the steps to make the changes:

## Modification Steps

1. First, in Content Builder, prepare the updated email content. You can do this in two ways:

- Edit the running email content in overwrite.
- Copy the running email content to create new email content.

2. Once the updated email content is ready, click on the **“Email Activity”** in the relevant journey.

3. Switch to the **“Activity Summary”** in the Email Analytics screen.

4-1. **If you edited the running email content in overwrite (Step 1), simply press the “Done” button** shown in the image below. The “Done” button is equivalent to the “Publish” button. (Done = Publish)

4-2. On the other hand, **if you copied running email content to create a new one (Step 1), select Different Message**. After selecting another message, **the process of pressing the “Done” button is the same as in the previous step**.

With these steps, the modification is complete!!

However, to confirm that the email has been published as a new one, here are two methods:

## Method 1. Confirming in the Interaction Tab

1. Navigate to the **“Interaction” tab** in Email Studio, open the folder of the version of the relevant journey from the left menu.

2. As shown in the image, there is an item labeled **“Published”**. This indicates the “Last Publication Date” of the email. **This item will not display up to the “hour: minute: second” details**. This can make it challenging to identify if the update was published on the same day.

While this confirmation method is straightforward, those who want more detailed information can use Query Studio to create a query for investigation.

## Method 2. Confirming with Query Studio

**Pressing the “Done” button in Email Activity generates a new “Job ID” for the email**. By searching for this Job ID in Data View using SQL, you can determine if the email activity has been updated.

1. To do this, you need the Activity ID of the email activity. In a previous article, I explained how to easily obtain the Activity ID, so please check that article and retrieve the Activity ID.

![]()

[## SFMC Tips #10 : Playful Tricks to Snatch Journey Builder Activity IDs Easily

### In the enchanting realm of Salesforce Marketing Cloud, a nifty feature called “Data Views” diligently stores customer…

medium.com](/@marketingcloudtips/playful-tricks-to-snatch-journey-builder-activity-ids-easily-2c208c6a41b2?source=post_page-----5dee6fced96c---------------------------------------)

2. Once you have the Activity ID of the email activity, construct the following query in Query Studio:

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

As a result, the searched job ID will now be listed in two or more records. Among the displayed job IDs, **the one with the latest PickupTime should be considered as the one executed when the ‘Complete’ button was pressed**. Please verify if this is correct.

**If you want to confirm who made the changes, you can look at the AccountUserID column**. However, note that AccountUserID only displays numbers and not usernames. The list associating AccountUserID with usernames, as mentioned in the Excel file below, can be obtained from the audit log (Audit Trail Activity Log). However, since the audit log only reveals the AccountUserID for the listed subjects, it is recommended to proactively create a related list of ‘who is which user ID’ by searching for job IDs for each AccountUserID.

That’s it for this article.

## Conclusion

While these may have been common knowledge, **it is very useful to know how to check the revision history for troubleshooting after changes have been made**.

In this article, we’ve informed you about updating the content of emails within the same journey version. However, keep in mind that, of course, **by creating a journey as a ‘new version’, the email content will be updated to something new**. Feel free to adopt that approach as needed.

*Note: For LINE, SMS, and app push notifications, remember that content changes are only possible when you upgrade the journey version.*

Additionally, **please note that changes to the email subject or pre-header are not finalized using this method**. If you wish to edit the email subject or pre-header, please make the modifications in the designated section within the email activity and then press the ‘Done’ button.

Thank you for reading.

Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
