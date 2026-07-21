# SFMC Tips #120 : Marketing Cloud Engagement: Summer ’25 Release Highlights

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-engagement-summer-25-release-highlights-6af46f09309e

---

# SFMC Tips #120 : Marketing Cloud Engagement: Summer ’25 Release Highlights

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--6af46f09309e---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--6af46f09309e---------------------------------------)

8 min read

·

May 23, 2025

--

Photo by [Mel Elías](https://unsplash.com/@cuartodeiibra?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

Salesforce Marketing Cloud’s new features for the Summer ’25 release have been announced, so I’d like to share a highlight article.

[## Help And Training Community

### Edit description

help.salesforce.com](https://help.salesforce.com/s/articleView?id=release-notes.rn_marketing_engagement.htm&release=256&type=5&source=post_page-----6af46f09309e---------------------------------------)

This release will roll out between June 6 and June 27, 2025. Please note that as of the time of writing, these features are not yet live, so some details might change or be inaccurate!!

The most notable update in this release is that the **wait activity at the end of a Journey is no longer required!** This change is groundbreaking in that it makes building Journeys more intuitive.

…Okay, I may be exaggerating a bit here, but honestly, the fact that this is the *only* major highlight tells you that this release is pretty modest. It’s fair to say Summer ’25 has almost no standout new features.

On the other hand, **Marketing Cloud on Core** (Marketing Cloud Growth & Advanced Edition) introduces flashy new features like the **Repeater component** and **Agentforce Campaign Designer**. This clearly shows the ongoing shift from Marketing Cloud Engagement toward Marketing Cloud on Core.

Though Summer ’25 is quite understated, let’s take a look at what features are included, while looking forward to the next Winter ’26 release.

**You can also check out my article on the previous Spring ’25 release.**

[## SFMC Tips #76 : Marketing Cloud Spring ’25 Release: Key Highlights and Insights

### Salesforce has announced the new features in the Spring ’25 Release for Marketing Cloud, and I would like to highlight…

medium.com](/@marketingcloudtips/marketing-cloud-spring-25-release-key-highlights-and-insights-51c43496c538?source=post_page-----6af46f09309e---------------------------------------)

## Automation Studio

### 1. Improved Error Messages for File Transfer Activity

Error messages for File Transfer Activities have been improved to provide clearer explanations. While most users will not see an impact on their operations, if you have automated error handling, please review and adjust your configurations based on the new messages.

**Wrong path of file locations in Enhanced FTP**

- **Old Message**: Import failed due to system error.
- **New Message**: Invalid URI setup in File Transfer Location. Re-verify File Transfer Location configuration and try again.

**Invalid Amazon S3 credentials**

- **Old Message**: System error for invalid Amazon S3 credentials.
- **New Message**: File Transfer Location connection was unsuccessful. Access denied for the AmazonS3 location.

**File transfer activity timed out**

- **Old Message**: FTA failed due to FTPTimeoutException.
- **New Message**: An error has occurred when executing commands on the remote server. Ensure folders or files exist on the remote server before retrying this File Transfer Activity.

**Expired Azure Blob SAS token**

- **Old Message**: Blob SAS token has expired. Expiry(se).
- **New Message**: The Azure Blob SAS token has expired. Generate a new token and update the file location.

**Missing folder error**

- **Old Message**: System error for missing folder locations.
- **New Message**: We can’t find the path for this file. Validate the activity and file location parameters, then try again.

**Missing authentication key**

- **Old Message**: General system error.
- **New Message**: The key used to authenticate is missing. Verify that the Auth Key associated with the File Location is correct.

## Journey Builder

### 1. No More Mandatory Wait Activities at the End of Journeys

A standout feature of the Summer ’25 release is the elimination of the need to add a “Last Wait Activity” at the end of a journey. 😭

This change enables marketers to design journeys more efficiently. **In new journeys, the Last Wait Activity is no longer automatically included by default**.

Previously, I demonstrated in an article how the final wait activity was often ignored in execution:

[## SFMC Tips #68 : Understanding Wait Activity Behavior at the End of a Journey

### The help documentation on optimizing the performance of Journey Builder has undergone significant updates.

medium.com](/@marketingcloudtips/understanding-wait-activity-behavior-at-the-end-of-a-journey-ad08e68ff43d?source=post_page-----6af46f09309e---------------------------------------)

With this update, the “Last Wait Activity” itself will no longer be placed by default, making it easier for marketers to build smarter journeys.

### Situations Where Wait Activities Are Still Necessary

However, this doesn’t mean that wait activities are entirely obsolete. There are scenarios where they remain critical, such as:

- **Using “Re-entry only after exiting”**  
  The “Re-entry only after exiting” setting is a highly convenient feature. By placing a wait activity at the end of a journey, you can fine-tune the timing of re-entry. For precise control of re-entry timing, the final wait activity remains an essential component.
- **Using “Goal Activities”**  
  Goal activities are evaluated when exiting a wait activity. If you want to assess goals at the very end of a journey, a final wait activity becomes indispensable.

Thus, while wait activities are no longer a default element, they are still valuable in specific use cases and should be implemented thoughtfully as needed.

Thus, while wait activities are no longer a default element, they are still valuable in specific use cases and should be implemented thoughtfully as needed.

[## SFMC Tips #146 : No More Need for the Final Wait Activity in Journeys

### With the Summer ’25 release of Marketing Cloud Engagement, the requirement to add a “final wait activity” at the end of…

medium.com](/@marketingcloudtips/no-more-need-for-the-final-wait-activity-in-journeys-e4ade2176b2b?source=post_page-----6af46f09309e---------------------------------------)

### 2. Enhanced Status Reporting for Transactional Sends

A new “**data extension template”** has been introduced to ensure guaranteed message status reporting for SMS and transactional emails within a 72-hour timeframe.

![]()

This template supports send settings, recording final message statuses directly in a new dataview. **With a retention policy of 7 days**, marketers can easily maintain compliance without requiring complex reporting comparisons.

[## SFMC Tips #248 : Transactional Send Reconciliation: Guaranteed Delivery Status Reporting

### In the Summer ’25 new feature release of Marketing Cloud Engagement, a new “Sendable Reconcilable Data Extension” data…

medium.com](/@marketingcloudtips/transactional-send-reconciliation-guaranteed-delivery-status-reporting-a0877520c3e3?source=post_page-----6af46f09309e---------------------------------------)

## Report

### 1. Extended Retention Period for Engagement Data

I’ve previously covered this in another article, so this is more of a reminder than a new feature announcement. The deadline for this change has been updated to **June 16, 2025**, extending the data access period to **730 days** (2 years).

[## SFMC Tips #108 : Changes to Engagement Data Retention Policy: 730 Days

### Previously, I wrote an article stating that starting May 15, 2025, the retention period for engagement data in…

medium.com](/@marketingcloudtips/changes-to-engagement-data-retention-policy-730-days-1935685b18af?source=post_page-----6af46f09309e---------------------------------------)

### 2. Visual Analysis of Data Storage Usage

\*Initially announced in Spring ’25, the release of this feature was delayed but is now officially **available in Summer ‘25**.

Previously, the only way to check data storage usage was by exporting data in Excel format. Now, with the introduction of the “**Data Extension Usage**” dashboard, you can visually and intuitively analyze data storage usage within your account.

**How to Access:**  
 Go to **Settings > Data Management > Data Extension Usage** to access the dashboard.

**Release Timeline:** This feature will be progressively rolled out starting in June 2025.

[## SFMC Tips #147 : “Data Extension Usage” Dashboard Launches in Summer ‘25

### With the Summer ’25 release of Marketing Cloud Engagement, a brand-new feature called the “Data Extension Usage…

medium.com](/@marketingcloudtips/data-extension-usage-dashboard-launches-in-summer-25-402a06c3af77?source=post_page-----6af46f09309e---------------------------------------)

## Mobile

### 1. Testing Available for All Push Notification Types

As part of the Spring ’25 release, we covered the new functionality enabling test sends for push notifications. With Mobile Push test sends, you can now review the content, personalization, and design of push notifications, in-app messages, and inbox messages without interrupting the current workflow.

[## SFMC Tips #99 : Spring ’25 Spotlight: Revolutionizing MobilePush with Test Sends

### Salesforce Marketing Cloud Engagement has introduced a long-awaited feature in the Spring ’25 release: the ability to…

medium.com](/@marketingcloudtips/spring-25-spotlight-revolutionizing-mobilepush-with-test-sends-a2274920d18f?source=post_page-----6af46f09309e---------------------------------------)

This update further expands functionality by allowing test sends for all types of push notifications. You can now verify whether the notifications work as expected before sending them.

- **Carousel Push Notifications:** Ensure smooth operation before deployment to optimize the user experience.
- **Standard Push Notifications:** Test buttons, icons, and sounds in advance to ensure they behave as intended.

**Availability:** This feature will be rolled out gradually starting in June 2025.

### 2. Enhanced Experience with MobilePush SDK Version 9.0

The latest MobilePush SDK introduces rich media and event monitoring capabilities, offering more engaging and versatile notification experiences.

**Key Features:**

- Create visually compelling notifications using carousel templates, interactive buttons, custom icons, and notification sounds.
- Support multiple CTAs and personalize subject lines and message components.
- Leverage **Inbox 2.0** to send messages to users’ inboxes, even in case of delivery failures.
- Use the MobilePush event monitoring feature to track app usage, push notification interactions, and delivery success rates.

To take advantage of these features, please upgrade your MobilePush SDK for both Android and iOS to version 9.0 or later.

There was an interesting note in the help documentation:

![]()

Yes, I completely feel déjà vu.

This feature was included in the Spring ’25 release. According to Salesforce, MobilePush SDK version 9.0 started rolling out from Spring ’25 and will gradually become available throughout the Summer ’25 release. So this is essentially a re-announcement.

### 3. Compliance with TRAI Regulations Using DLT Templates (India)

To comply with the Telecom Regulatory Authority of India (TRAI) regulations, enable the Distributed Ledger Technology (DLT) template by contacting your account executive.

The DLT template integrates with MobileConnect and Journey Builder message templates, simplifying campaign processes and reducing spam messages.

### 4. TRAI-Compliant SMS Link Shortening (India)

Marketing Cloud Engagement’s URL shortening feature adheres to TRAI regulations, preventing SMS blocking. This ensures effective campaigns in the Indian market by supporting DLT-approved headers, custom or generic domains, and precise SMS CTAs.

### 5. Real-Time Monitoring for WhatsApp Templates and Phone Numbers

You can now monitor the approval status of WhatsApp message templates and the connection status of phone numbers in real time. This feature allows you to always stay updated with the latest status information, enabling you to run WhatsApp campaigns smoothly and efficiently.

Depending on the interface, this could be very convenient. With WhatsApp, when sending business messages, you need to create message templates in advance and get them approved by WhatsApp. This feature lets you check in real time whether a template is currently approved, still under review, or rejected. By doing so, you can avoid delays caused by waiting for template approvals during campaign preparation.

### 6. Interactive Messages for WhatsApp

Create highly customizable WhatsApp flows by incorporating dynamic variables, images, and engaging media types into interactive messages.

This feature allows customers to:

-  location information.
- Browse catalogs.
- Interact with carousel media cards.

## Package Manager

### 1. Support for Trigger Sends

Package Manager now supports trigger send definitions and user-initiated sends. This enables seamless creation and deployment of these definitions across business units, streamlining organizational processes and maintaining operational consistency.

## Final Thoughts

This Summer ’25 release, to be honest, wasn’t particularly appealing to me. This impression is quite similar to what I felt about the Spring ’25 release, though I believe many might even find Spring ’25 to have been slightly better.

This clearly reflects the focus on Marketing Cloud Growth & Advanced Edition. For users hoping for advancements in Marketing Cloud Engagement, the release might feel a bit underwhelming.

**Release Period:** The updates will be rolled out between **June 6 and June 27, 2025**. At the time of publishing, these features are not yet available.

That’s all for now.

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
