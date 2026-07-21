# SFMC Tips #23 : Marketing Cloud Engagement: Spring ’24 Release Highlights

**Source:** https://medium.com/@marketingcloudtips/spring-24-release-highlights-notable-new-features-in-marketing-cloud-8c769e8402b6

---

# SFMC Tips #23 : Marketing Cloud Engagement: Spring ’24 Release Highlights

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--8c769e8402b6---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--8c769e8402b6---------------------------------------)

9 min read

·

Feb 7, 2024

--

Photo by [Silas Gregory](https://unsplash.com/@chalkpitcassetteclub?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

The release notes for **Salesforce Marketing Cloud Spring ’24**, focusing on new features, have been published. I would like to write an article highlighting these updates.

*\* Please note that this article is based on information available before the release of Spring ’24, so there may be inaccuracies in the content. Please be aware of this in advance.*

The release is scheduled **between February 16th and March 8th, 2024**. Among the features to be released this time, the one that personally excites me the most is the **ability to track individuals who have paused automation**. Until now, the record of who made changes was not logged until the ‘Save’ button was pressed. However, with the addition of recording the timing and the person who made changes when pausing, it has become more audit-friendly. It’s a feature I’ve been eagerly anticipating.

Now, as there are many releases this time as well, let’s take a look at the new features released in Spring ’24 one by one.

## ■ CloudPages — Related features

### 1. The name of the CloudPages Collection will be changed to a folder

The name, previously referred to as the CloudPages Collection, will now be changed to a folder. Similar to Content Builder, you can now move CloudPages from one folder to another and nest folders. This update aims to simplify the management of CloudPages assets.

### 2. Restore deleted content in CloudPages

You can now restore items sent to the CloudPages recycle bin without raising a case with support. To use the CloudPages recycle bin, deletion permissions are required, and only the user who owns the content can perform the restoration.

*Note: This feature was initially introduced in Winter ’24 but got postponed and is now set for release in Spring ‘24.*

## ■ Journey Builder — Related features

### 1. Send a large volume of emails with high throughput

To double the sending throughput, select “Journey Builder Email High Throughput Send” in the “**Journey Settings**”.

*Timing: This feature will be available after March 18, 2024.*

Is this feature unconstrained and unlimited? If it is indeed unlimited, one would always want to send at a high speed, wouldn’t they? 😅

The functionality has been released. One important point to note is that once activated, it cannot be deactivated, which seems to be a consideration. **It’s reassuring that it doesn’t affect features like Sendlog, Data View, or delivery windows**, but there seem to be some considerations, so caution is necessary.

▶ Journey Builder High-Throughput Sending Considerations

[## Help And Training Community

### Edit description

help.salesforce.com](https://help.salesforce.com/s/articleView?id=sf.mc_jb_high_throughput_sending.htm&type=5&source=post_page-----8c769e8402b6---------------------------------------)

### 2. Pause and Resume multiple journeys from the Journey Dashboard

Simplify the management of journeys from the Journey Dashboard. **You can now select up to 10 journeys at once and pause or resume either the current version or all versions**.

In the Winter ’24 release, the ability to “stop” multiple journeys from the Journey Dashboard was introduced, and now, following that, the functionality to pause and resume multiple journeys is available. This is excellent, for instance, in scenarios where there might be a disruption in the core system, and the latest data hasn’t been integrated. In such cases, having the ability to collectively pause journeys is fantastic. 🎉

*\*Some advanced pausing options aren’t available in this Dashboard view.*

### 3. Display Activity IDs in the Journey History Dashboard

By displaying Activity IDs on the Journey History Dashboard, it becomes easy to identify activities of the same type. For instance, if there are two “Wait by Duration” activities, each activity will be assigned a unique Activity ID for clear differentiation.

### 4. Enhance journey performance using recommendations

Journey Builder proactively offers recommendations for configurations that may impact performance **during journey validation**. The introduced recommendations in this release cover the following aspects:

- Number of activities on the canvas  
- Count of reused entry definitions  
- Usage of wait activities in conjunction with engagement splits  
- Consecutive decision split activities  
- Quantity of Salesforce data input objects

These recommendations aim to improve the performance of the journey without impeding the activation of the journey.

### 5. Extend URL tracking in Engagement Split activities

When using the Engagement Split activity to track clicks in an email, you can now input any URL for tracking purposes. Previously, you were only able to select URLs obtained from the content within the email.

## ■ Einstein Related — Related features

### 1. Segment creation using Einstein Segment Creation

Using Einstein Segment Creation and AI generation, you can now create segments targeting audiences in Data Cloud for Marketing. When describing your target users, Einstein Segment Creation automatically generates a segment within seconds using customer data available in Data Cloud. You can edit and fine-tune the segment as needed.

Target: This change applies to Developer Edition, Enterprise Edition, Performance Edition, and Unlimited Edition of Data Cloud. A Data Cloud Starter license is required for Einstein Segment Creation. Einstein-generated AI is available in Lightning Experience.

Procedure: When creating a segment in Data Cloud, select [Create with Einstein]. Use text in the Einstein panel to describe the segment. Review the draft and make necessary changes.

## ■ Intelligence Reports — Related features

### 1. WhatsApp in Intelligence Reports dashboard

View WhatsApp data to determine which messages were more successful, assess the performance of campaigns, and understand how customers engaged with WhatsApp messages.

Target: This change applies to the Engagement Intelligence reports in Pro, Corporate, and Enterprise Editions.

Procedure: On the [Dashboard] tab, expand the WhatsApp dashboard.

### 2. Analyze WhatsApp delivery data in Intelligence Reports

Analyze WhatsApp engagement and delivery data not only in the Intelligence Reports dashboard but also in pivot tables. **The new fields include Activity Name, Send Name, Deliveries, and more**.

Target: This change applies to Engagement Intelligence reports in Pro, Corporate, and Enterprise Editions.

## ■ Data Management — Related features

### 1. Performance improvement in Data Designer

To improve the performance of Data Designer in Contact Builder, if you choose “All records and data extensions” as the deletion target for the data extension retention policy, you can no longer link data extensions in Data Designer.

![]()

Linking a data extension in Data Designer that is intended to be deleted after a certain period is certainly not desirable.

### 2. Length restriction for items in sendable data extensions

To enhance performance when using a sendable data extension, **the length of items in the sendable data extension will be limited to 254 characters**.

*\* This limitation is set to take effect with the* ***Summer ’24 release****.*

The release notes regarding this limitation are highly ambiguous. Is the intention to restrict the length of all text-type fields in the sendable data extension to 254 characters, or is it specifically for the text-type fields associated with the subscriber relationship settings of the sendable data extension, linked to the subscriber key?

The wording of the release notes does not provide a clear indication. While it is likely to be the latter, if it turns out to be the former, it could pose a significant operational constraint. Therefore, let’s refrain from speculation and await official guidance from Salesforce for clarification.

## ■ Automation Studio — Related features

### 1. Configuration for importing blank files in Automation Studio

You can now choose how to handle blank files in each import activity. Specifically, **if an empty file is found during the import, you can choose to skip the import, overwrite existing data, or end the automation**.

The default value for a brand-new MC account is said to be “**Fail Import**”. Therefore, if there is a requirement to always proceed with processing even with an blank file, as before, **it is necessary to request a change in the default value to Support at the initial setup stage**.

### 2. General enhancements in Automation Studio

Automation Studio has undergone improvements to enhance automation performance, along with several other updates. The following points have been highlighted:

- Scheduled automations have increased by 62%. (It seems to refer to a 62% increase in performance or efficiency, based on the context.)
- In CSV files for Data Extension Storage Export function, external keys can now be displayed.
- Content types are recognized when transferring unencrypted files to Amazon Simple Storage Service (S3), Google Cloud Storage, and Microsoft Azure Blob Storage.
- The new File Drop API validation prevents the inadvertent creation of unmonitored folders.
- **On the summary screen of each automation, you can now identify the person who last paused that automation**. (Refer to the diagram below.)

![]()

Even in the official help documentation, it is quietly introduced in the last line, but finally, **it seems that the ability to track who paused an automation has been added**. Personally, I consider this feature to be the most fantastic addition in Spring ’24, but what do you all think?

Until now, it was not possible to confirm who paused the automation until you clicked “Save.” Sometimes, leaving an automation paused and unattended without the ability to audit and identify who stopped it could lead to problems. Now, with this feature, you can perfectly understand who did it. It’s wonderful that Salesforce recognized the high priority of adding this functionality. 🎊 Excellent!

## ■ Marketing Cloud Mobile App — Related features

### 1. Discontinuation of the Marketing Cloud Mobile App

It has been announced that the Marketing Cloud mobile app will be deprecated on May 5, 2024. (New downloads for the app were already disabled.)

Did you use the Marketing Cloud mobile app? Personally, I found it useful for monitoring Automation Studio processes, ensuring that automations ran smoothly when scheduled.

If the app is already installed on your mobile device, you can continue using it until the deprecation date. After May 5, 2024, access Marketing Cloud Engagement on your mobile device using a browser. The guidance suggests this transition. It would be interesting to know if there will be mobile optimization. Waiting for further updates from Salesforce on this matter.

## ■ Messaging — Related features

### 1. Send messages using WhatsApp Transactional API

Using the WhatsApp Transactional API, you can automatically send messages other than promotions. Additionally, with Marketing Cloud Events, you can provide customers with the latest information regarding deliveries through event-based messages such as order confirmations and shipping notifications.

Target: This feature applies to Marketing Cloud with WhatsApp Business Messaging in Corporate Edition and Enterprise Edition.

### 2. Upload the new authentication pattern for the Android app to the MobilePush management tab

The last piece of information is more of an announcement from Salesforce than release details.

On March 22, 2024, the authentication pattern for the Android app integrated with Marketing Cloud will be modified to comply with Google Firebase Cloud Messaging requirements. To continue sending push notifications to Android devices after this date, you will need to upload the google-services.json file for each active Android app by June 1, 2024.

Timing: After the completion of the Spring ’24 release, the authentication pattern will be changed on a rolling basis and will be updated for all customers by March 27, 2024.

Procedure: To upload the google-services.json file, navigate to the [Administration] tab of MobilePush after it becomes available and follow the instructions.

This release is scheduled to occur between February 16 and March 8, 2024. Please note that as of the current publication of this article, the features have not been released.

Additionally, I anticipate that Salesforce will host future feature release presentations. I plan to thoroughly catch up on those presentations and provide supplementary information once they take place.

Thank you for reading.

Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
