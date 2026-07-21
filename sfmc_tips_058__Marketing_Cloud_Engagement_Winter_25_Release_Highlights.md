# SFMC Tips #58 : Marketing Cloud Engagement: Winter ’25 Release Highlights

**Source:** https://medium.com/@marketingcloudtips/winter-24-release-highlights-notable-new-features-in-marketing-cloud-f9ab85aac8b1

---

# SFMC Tips #58 : Marketing Cloud Engagement: Winter ’25 Release Highlights

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--f9ab85aac8b1---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--f9ab85aac8b1---------------------------------------)

8 min read

·

Oct 1, 2024

--

Photo by [Joseph Pearson](https://unsplash.com/@josephtpearson?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

The release notes for **Salesforce Marketing Cloud Winter ’25**, focusing on new features, have been published. I would like to write an article highlighting these updates.

- Please note that as the release is not yet live, the information shared here may contain errors.
- This article focuses on key highlights and does not cover all new features.
- Additional updates will be made if further release information is shared.

**The Winter ’25 release is scheduled between October 4 and October 25, 2024**. One feature that caught my eye 👀 is the ability to access real-time data from Automation Studio-related data views.

This is a groundbreaking update, as previously, only data from over 24 hours ago could be retrieved. **With this change, troubleshooting on the same day becomes much easier**. In fact, the technique I introduced in a previous note article on how to retrieve automation activity execution times can now be applied to visualize automations happening on the same day. 🛠️ You can refer to the article linked below.

[## SFMC Tips #45 : How to Bulk Retrieve Execution Times of Automation Activities in Each Step of…

### Have you ever wanted to find out:

medium.com](/@marketingcloudtips/how-to-bulk-retrieve-execution-times-of-automation-activities-in-each-step-of-automation-studio-16903798fc9a?source=post_page-----f9ab85aac8b1---------------------------------------)

■ Please also check out the article on the previous Summer ’24 release.

[## SFMC Tips #42 : Summer ’24 Release Highlights: Notable New Features in Marketing Cloud

### The release notes for Salesforce Marketing Cloud Summer ’24, focusing on new features, have been published. I would…

medium.com](/@marketingcloudtips/summer-24-release-highlights-notable-new-features-in-marketing-cloud-0d9ba139c988?source=post_page-----f9ab85aac8b1---------------------------------------)

Now, let’s dive into the exciting new features released in Winter ‘25!

## ■ Automation Studio — Related features

### ① Real-time Access to Automation Data Views

As mentioned earlier, it is now possible to query the Automation Studio data view in real-time. Previously, you could only retrieve data for automations executed from 24 hours ago to up to 31 days.

I tried it right away, and I was able to retrieve the data for the current day without any issues. In line with this update, **I’ve rewritten the code in my article below to also retrieve data for the current day**. This update will make troubleshooting automations on the same day significantly easier!

[## SFMC Tips #45 : How to Bulk Retrieve Execution Times of Automation Activities in Each Step of…

### Have you ever wanted to find out:

medium.com](/@marketingcloudtips/how-to-bulk-retrieve-execution-times-of-automation-activities-in-each-step-of-automation-studio-16903798fc9a?source=post_page-----f9ab85aac8b1---------------------------------------)

```
SELECT TOP 10000   
    AutomationName,  
    ActivityName,  
    ActivityInstanceStep,  
    CONVERT(VARCHAR(19), DATEADD(HH, 9, ActivityInstanceStartTime_UTC), 120) AS [ActivityInstanceStartTime],  
    CONVERT(VARCHAR(19), DATEADD(HH, 9, ActivityInstanceEndTime_UTC), 120) AS [ActivityInstanceEndTime],  
    FORMAT(DATEDIFF(S, ActivityInstanceStartTime_UTC, ActivityInstanceEndTime_UTC) / 60, '00') + ':' +   
    FORMAT(DATEDIFF(S, ActivityInstanceStartTime_UTC, ActivityInstanceEndTime_UTC) % 60, '00') AS [Duration]  
FROM   
    _automationactivityinstance  
WHERE   
    AutomationName = 'XXXXXXXXXXXXXXX'  
    AND DATEADD(HH, 9, ActivityInstanceStartTime_UTC) >= CONVERT(DATE, DATEADD(HH, 15, GETDATE()), 111)  
ORDER BY   
    CONVERT(DECIMAL, ActivityInstanceStep) ASC,   
    DATEDIFF(S, ActivityInstanceStartTime_UTC, ActivityInstanceEndTime_UTC) DESC
```

### ② Job ID Added to the Automation Activity Instance Data View

If there’s an email send activity within an automation, **the Job ID will now be included in the Automation Activity Instance data view**, making it easier to join with other data views like Sent, Open, and Click.

### ③ Error Returns for Failed Decryption in File Transfer Activities

In the event of a decryption failure due to incorrect GPG or PGP key settings, the system will now return an error to the user, instead of simply logging it internally.

### ④ New S3 Path Requirements for File Locations

When you create or modify an S3 File Location, the AWS Bucket Name field can no longer contain a relative path. You can only specify a bucket name in the AWS Bucket Name field, and a relative path in the AWS Relative Path field.

[## SFMC Tips #69 : How to Transfer Files from Amazon S3 to Marketing Cloud

### Salesforce Marketing Cloud supports file transfers not only with SFTP but also with Amazon S3, Google Cloud Storage…

medium.com](/@marketingcloudtips/how-to-transfer-files-from-amazon-s3-to-marketing-cloud-85f9af08b16f?source=post_page-----f9ab85aac8b1---------------------------------------)

## ■ Journey Builder — Related features

### ① Journey Builder Auditing: Dedicated Audit Logs

Visualize changes made to journeys **within the past 30 days**, allowing you to monitor journey modifications and maintain accountability within your team. Information about when and by whom journeys were created, modified, activated, deactivated, paused, and deleted is displayed. You can access this from the History screen shown below.

*\*The Time is localized to your time-zone, not CST.*

You can filter the displayed information by date and activity. The filter options you select will be retained even after closing the filter panel.

Additionally, you can add or remove columns from the table and download the results as a CSV file. You can also copy the data to the clipboard and paste it into Excel.

By the way, the REST API for auditing Journey Builder has existed for some time. In my article below, I explain how to retrieve it. Using this method, **you can retrieve data beyond 30 days**. If you want to access older history, I recommend using the REST API.

[## SFMC Tips #24 : How to Check the Change History of Journey Builder

### Do you ever experience not knowing who made changes to Journey Builder settings? It would be convenient to be able to…

medium.com](/@marketingcloudtips/how-to-check-the-change-history-of-journey-builder-1e4015bba67c?source=post_page-----f9ab85aac8b1---------------------------------------)

```
--- Method  
GET  
  
--- Endpoint  
https://[REST Base URL].rest.marketingcloudapis.com/interaction/v1/interactions/[Journey ID]/audit/all?versionNumber=[Version Number]  
  
--- Headers  
Content-Type: application/json  
Authorization: Bearer [Access Token]
```

### ② Journey Builder Auditing: Slack Notifications

A **Slack notification** feature for auditing purposes has been released in Journey Builder. You can find the **Slack Notification Settings** button to the left of the “Back” button on the journey canvas, where you can configure the settings.

When you open the settings screen, various notification settings are available, as shown below.

I attempted to set it up myself, but so far, I have not been successful.

There is no official help document available for this feature yet. Details, especially about how to connect to a Slack channel and what exactly needs to be entered, are still unclear.

By the way, I tried the following in my environment, but simply entering them in the Slack channel field did not establish a connection:

- nacmarketingcloud
- nacmarketingcloud.slack
- nacmarketingcloud.slack.com

I plan to revisit this setup once more detailed official help documents are released.

*\*When trying to activate a journey, you may encounter an error stating that Slack Notification Settings have not been configured, preventing activation. In such cases, opening the Slack Notification Settings, pretending to configure them, and then clicking the “Done” button without making any actual settings will resolve the error during validation.*

It seems that Salesforce provided the following comment regarding this feature. It appears to be part of a future release. Thanks Saketh for the info.

*“The feature you are referencing is not in the current release (nor the official release notes) and was incorrectly enabled in accounts and we are taking steps to revert this. We apologize for any inconvenience this has caused.”*

### ③ High-Throughput Sending Recommendations During Journey Validation

During journey validation, Journey Builder identifies configurations that could affect performance. If there are any draft or active journeys where High-Throughput sending is not enabled for email activities, Journey Builder will recommend enabling High-Throughput sending to improve email performance.

Journey Builder can process up to 2 million emails per hour per tenant. By using this High-Throughput sending feature, **it is generally possible to achieve more than double the normal throughput**.

💡 **High-Throughput Sending Considerations**

[## Help And Training Community

### Edit description

help.salesforce.com](https://help.salesforce.com/s/articleView?id=sf.mc_jb_high_throughput_sending.htm&type=5&source=post_page-----f9ab85aac8b1---------------------------------------)

### ④ UI Improvements for Default Email Address in Contact Data

It has become easier to more accurately select data when retrieving email attributes from contact data.

Previously, for example, when selecting the email addresses of all subscribers, the process was to first select “Email Addresses” and then choose “Email Address”.

Now, you start from “Contact Data,” and if you want to use the email addresses of all subscribers, you select “System Data,” then choose “Email Addresses” and “Email Address”.

![]()

This UI, which may have seemed a bit confusing for beginners, has now been improved to align with other features. A home button has also been added.

### ⑤ Removal of Unnecessary Rows in the Journey ‘History’ Tab

In the Journey ‘History’ tab, unnecessary rows, such as those with blank activity names or completed statuses, will no longer appear.

## ■ Einstein — Related features

### ① Multilingual Support for Einstein-Generated Subject Lines and Body

With Einstein generative AI, you can now create subject lines and body content in French, German, Italian, Japanese, Portuguese, and Spanish. This allows you to quickly generate localized content and deliver messages to a broader audience. When the culture code is set to match one of these languages, the language is automatically configured.

[## SFMC Tips #60 : Multilingual Support for Einstein AI Generated Subject Lines and Body

### One year ago, with the Winter ’24 release, Salesforce introduced a feature that automatically generates “email subject…

medium.com](/@marketingcloudtips/multilingual-support-for-einstein-ai-generated-subject-lines-and-body-83fff13c7092?source=post_page-----f9ab85aac8b1---------------------------------------)

### ② New Audit Export Feature for AI Content

A comprehensive audit of AI-generated content over the past 90 days can now be exported, helping ensure compliance with safety guidelines and brand consistency.

You can export it from the Einstein Copy Insights setup screen.

## ■ App — Related features

### ① Farewell to Social Studio 👋

Social Studio will be fully retired on November 18, 2024. After that date, access will be removed, and customer data will be deleted 90 days later.

How did these highlights resonate with you?

Once again, **the Winter ’25 release will take place between October 4 and October 25, 2024**. As of this article’s publication, these features have not yet been rolled out, so stay tuned for more updates.

I’ll also keep an eye on any upcoming Salesforce-hosted webinars for further clarification and updates on these features.

Thank you for reading.

Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
