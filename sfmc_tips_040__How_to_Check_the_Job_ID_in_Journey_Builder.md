# SFMC Tips #40 : How to Check the Job ID in Journey Builder

**Source:** https://medium.com/@marketingcloudtips/how-to-check-the-job-id-in-journey-builder-b75428447815

---

# SFMC Tips #40 : How to Check the Job ID in Journey Builder

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--b75428447815---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--b75428447815---------------------------------------)

5 min read

·

May 19, 2024

--

Photo by [David Pisnoy](https://unsplash.com/@davidpisnoy?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

**Have you ever wondered where to find the “Job ID” assigned to email sends in Salesforce Marketing Cloud?** For emails sent from Email Studio or Automation Studio, you can check the “Tracking” screen in the reports.

However, **for email sends in Journey Builder, there’s currently no straightforward way to check this from the Salesforce Marketing Cloud interface**. So, you need to use some method to find it.

In this article, **I’ll summarize the methods to check the “Job ID” in Journey Builder**. I’ll cover the following four methods:

## Table of Contents

1. Checking via “External Key” in Query Studio (👈️ Recommended by Salesforce)
2. Checking via “Journey Activity ID” in Query Studio (👈️ Recommended by me)
3. Checking via the “Account Send Summary” Report
4. Checking via Pivot Tables in “Intelligence Report”

## 1. Checking via “External Key” in Query Studio (👈 Recommended by Salesforce)

First, navigate to the “Tracking” section in Email Studio and select the “Journey Builder Sends” folder. From there, choose the version of the journey.

In this section, you can see the “**External Key**” for each email activity in the journey. **Use this “External Key” along with the following SQL query in Query Studio**. Replace the asterisks (\*\*\*) with the actual “External Key”.

```
SELECT j.JobId,  
       j.Category,  
       j.AccountUserID,  
       j.PickupTime  
FROM _job j  
WHERE j.TriggeredSendCustomerkey = '*****'  
AND j.Category LIKE 'version%'  
AND j.PickupTime IS NOT NULL
```

**If you don’t specify** `Category LIKE 'version%'` **in the WHERE clause, two "Job IDs" will be displayed**. This happens because a "Job ID" is created when the journey is in draft mode, and another one is created when it is activated.

**The “Job ID” associated with engagement data such as “Sent” is the one with** `Category` **labeled as "Version X (1, 2, 3…)"**. Please use this one.

Previously, in the article “**How to Modify Email Content within the Same Version After Activating a Journey**”, I mentioned that **updating the email content after activating the journey will change the “Job ID”**.

[## SFMC Tips #21 : How to Modify Email Content within the Same Version After Activating a Journey

### After activating a journey in Journey Builder, there may be instances where you want to change part or all of the email…

medium.com](/@marketingcloudtips/how-to-modify-email-content-within-the-same-version-after-activating-a-journey-5dee6fced96c?source=post_page-----b75428447815---------------------------------------)

**If multiple “Job IDs” labeled as “Version X (1, 2, 3…)” appear, the one with the latest** `PickupTime` **corresponds to the most recent content**. Choose the appropriate "Job ID" carefully.

*\*By the way,* ***even if the journey is changed to a new version*** *and the content remains exactly the same, the “Job ID” will change.*

## 2. Checking via “Journey Activity ID” in Query Studio (👈 Recommended by me)

Next, I’ll explain **how to check the “Job ID” using the Journey Activity ID**. If you’re not familiar with how to obtain the Journey Activity ID, please refer to the article below for instructions.

[## SFMC Tips #10 : Playful Tricks to Snatch Journey Builder Activity IDs Easily

### In the enchanting realm of Salesforce Marketing Cloud, a nifty feature called “Data Views” diligently stores customer…

medium.com](/@marketingcloudtips/playful-tricks-to-snatch-journey-builder-activity-ids-easily-2c208c6a41b2?source=post_page-----b75428447815---------------------------------------)

**The advantage of using the Journey Activity ID is that it makes it easier to visually identify the email activity within the journey**. In contrast, the first method relies on a text-based list.

Once you have the Journey Activity ID, replace the asterisks (\*\*\*) in the following SQL query and execute it in Query Studio.

```
SELECT j.JobId,  
       j.Category,  
       j.AccountUserID,  
       j.PickupTime  
FROM _job j  
JOIN _JourneyActivity ja  
ON j.TriggererSendDefinitionObjectId = ja.JourneyActivityObjectId  
WHERE ja.ActivityId = '*******************************'  
AND j.Category LIKE 'version%'  
AND j.PickupTime IS NOT NULL
```

*Similar to the first method,* ***you need to use*** `Category LIKE 'version%'` ***to filter the results as this method will also display two "Job IDs"****.*

## 3. Checking via the “Account Send Summary” Report

Next, let’s use the standard “Account Send Summary” report.

By exporting this report to Excel, you’ll get a list of “Job IDs” for each email activity.

To identify which email activity corresponds to which email, you’ll need to refer to the email names, which might be a bit cumbersome. However, **this method is useful when you need to find multiple “Job IDs” at once**.

**The “Job IDs” displayed here correspond to the ones labeled as** `Category` **"Version X (1, 2, 3…)" in methods 1 and 2**, so you can use them with confidence.

## 4. Checking via Pivot Tables in “Intelligence Report”

Finally, let’s use the pivot table in Intelligence Report. You can configure it to display items such as “Journey Activity Name,” “Journey Version,” and “Email Job ID” in the rows, and filter by “Journey Activity Name” to find the relevant “Job ID”.

**These pivot tables can be saved for future use, making it easier to reuse them later**. Previously, you could only rely on standard reports like in method 3, but now the Intelligence Report offers a more convenient alternative.

**The “Job IDs” obtained here also correspond to the ones labeled as** `Category` **"Version X (1, 2, 3…)" in methods 1 and 2**.

Personally, I almost always use method 2 with the Journey Activity ID in Query Studio. When I need to find a “Job ID,” I’m usually looking at the Journey Builder canvas, so I quickly get the Journey Activity ID from the canvas and start the search in Query Studio. This method also reduces the chances of getting the wrong “Job ID”.

Well, I’ve introduced various methods, so please choose the one you prefer.

Finally, as a bonus, **here is an SQL query to reverse lookup the Journey Name, Journey Activity ID, and Email Name from a “Job ID”**. Use this for reference.

```
SELECT j.JourneyName,  
       ja.JourneyActivityObjectId,  
       ja.VersionId,  
       job.EmailName  
FROM _Job job  
JOIN _JourneyActivity ja ON job.TriggererSendDefinitionObjectId = ja.JourneyActivityObjectId  
JOIN _Journey j ON j.VersionId = ja.VersionId  
WHERE job.JobId = 'XXXXX'
```

That’s all for today.

Thank you for reading.

Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
