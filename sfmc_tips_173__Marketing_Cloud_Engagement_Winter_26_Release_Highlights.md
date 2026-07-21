# SFMC Tips #173 : Marketing Cloud Engagement: Winter ’26 Release Highlights

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-engagement-winter-26-release-highlights-b32181d3e42a

---

# SFMC Tips #173 : Marketing Cloud Engagement: Winter ’26 Release Highlights

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--b32181d3e42a---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--b32181d3e42a---------------------------------------)

12 min read

·

Sep 13, 2025

--

Photo by [Rombo](https://unsplash.com/@rombo_guitar_picks?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

Release notes about the new features in Marketing Cloud Engagement Winter ’26 have just been published, so I’d like to share an article highlighting the key points.

[## Salesforce Help

### Edit description

help.salesforce.com](https://help.salesforce.com/s/articleView?id=release-notes.rn_marketing_engagement.htm&release=258&type=5&source=post_page-----b32181d3e42a---------------------------------------)

> *This release will roll out between October 3, 2025, and November 1, 2025.*

The highlight this time is the integration feature called **Marketing Cloud Next for Engagement**, which connects Marketing Cloud Next with Marketing Cloud Engagement.

However, the announcement itself does not go beyond what was presented in the Connections 2025 session, *“*The Future of Marketing Cloud Engagement”; it simply confirms that the features introduced there will be officially released starting November 2025.

[## SFMC Tips #138 : The Future of Marketing Cloud Engagement Session Overview

### The highly anticipated session, “The Future of Marketing Cloud Engagement”, which was also a personal highlight of mine…

medium.com](/@marketingcloudtips/the-future-of-marketing-cloud-engagement-session-overview-2794b9b3e83e?source=post_page-----b32181d3e42a---------------------------------------)

In addition, the ability to download **ALL** journey history directly from the Journey History dashboard is undoubtedly a **game-changer**. Until now, only the data displayed on the screen could be downloaded as a CSV, and retrieving the complete history required using the Journey History Download API. Going forward, however, it will be possible to obtain all the data as a CSV directly from the dashboard.

In terms of practical use, you can extract contacts who went through a specific path and import them into a Data Extension, making them immediately available as a delivery list for other scenarios. This is also useful if you want to restart a journey in another scenario after stopping it.

Furthermore, if you are using Marketing Cloud Next, you can import journey history into **Data Cloud** and use it as a filter for segments. In this case, you can analyze and apply the data directly without needing to download it first, further enhancing convenience.

Lastly, this release also includes numerous updates related to **WhatsApp**. While LINE remains more popular in my country, Japan, and use cases may be limited, these improvements are certainly noteworthy for companies leveraging WhatsApp.

So, let’s go ahead and review the new features in the order they’ll be released.

## **Marketing Cloud Next for Engagement Updates**

Marketing Cloud Engagement administrators can restrict access to these features for individual users by toggling navigation buttons **on** or **off**.

> ***Timing:*** *These features will be rolled out gradually starting in* ***November 2025****.*

### **① Creating Dynamic Customer Experiences with Agentforce**

In **Agent Builder**, you can now configure “**Journey Decisioning Agents**” for specific tasks or use cases related to existing journeys in **Journey Builder**.

These agents can create personalized message content tailored to each individual and determine which journey is most relevant. The selected content and journeys are stored in a data extension and can be used by marketers in Journey Builder.

Specifically, the following actions are provided:

**Evaluation Journey**  
The agent analyzes the customer’s current journey status and guides whether adjustments or optimizations are needed to improve engagement and conversion rates.

**Trigger Journey Entry Event**  
Based on customer behavioral data and campaign logic, the agent triggers entry into the appropriate journey.

**Create Content**  
Using GenAI, customized email or SMS content is created based on brand tone, customer data, and campaign goals.

**Send Copy to Data Extension**  
 The created content is sent to the appropriate Data Extension, enabling personalization and delivery through the selected channels.

**Scope:** This change applies only to **Marketing Cloud Next for Engagement**. Only users with the **MC Agent Actions User** permission can leverage Agentforce capabilities within journeys.

### **②** ing to Journey Builder Events in Flows

Journey events such as when a contact meets a goal, enters a journey, or exits a journey can now be used in **Flows**.

**Types of Journey Event Triggers**

**Entry Journey**  
Triggers a flow when a contact enters a journey.

**Exit Journey**  
Triggers a flow when a contact exits a journey.

**Goal Met**  
Triggers a flow when a contact meets a goal.

With journey events, you can add customers to a flow or release them from a **Wait Until Event** activity inside the flow.

### **③ Injecting Contacts into Journeys from Flows**

A new **“Send to Journey”** **action** in Flow allows you to inject contacts from a flow directly into a journey. A single flow can manage insertions into multiple journeys.

Marketers can link journeys through clicks instead of code, all within a single flow canvas view. This enhancement enables prioritization of journeys based on customer attributes and behaviors, delivering an end-to-end customer experience.

[## SFMC Tips #250 : Marketing Cloud Next: Send to Journey Action

### If you are using Marketing Cloud Engagement+, you can send contacts from a Marketing Cloud Next flow to Marketing Cloud…

medium.com](/@marketingcloudtips/marketing-cloud-next-send-to-journey-action-3a0c77cc2b63?source=post_page-----b32181d3e42a---------------------------------------)

### **④ Enhanced Reporting by Linking Journeys with Campaigns**

You can now add existing journeys in **Marketing Cloud Engagement** to campaigns for improved organization and analytics.

Marketing Cloud Next campaigns provide a connected workspace for activities and data, serving as the single source of truth for marketing activities across the Salesforce Platform.

When a journey is linked to a campaign, Marketing Cloud Next automatically aggregates its metrics into the overall campaign data. In Journey Builder, linked journeys display an icon indicating they are part of a campaign. Marketing users can also connect journeys to campaigns directly from the campaign page in Marketing Cloud Next.

[## SFMC Tips #210 : Marketing Cloud Next: Engagement+ Integration Setup

### As of November 2025, both new and existing Marketing Cloud Engagement customers can use Marketing Cloud Next by…

medium.com](/@marketingcloudtips/marketing-cloud-next-engagement-integration-setup-6fae8c535337?source=post_page-----b32181d3e42a---------------------------------------)

### ⑤ Reporting and Segmentation with Journey History Data

By adding journey history data to **Data Cloud**, you can gain deeper insights into customer journeys.

In the **Analytics** tab of **Marketing Cloud Next**, this data can be used to create custom reports on journey entries, journey exits, goal achievements, and messaging activities.

Additionally, in **Data Cloud**, journey history can be leveraged to create segments, perform data transformations, and run high-performance zero-copy exports.

[## SFMC Tips #201 : Data Cloud: Journey Activity Run Added to Starter Data Bundle

### With the Winter ’26 release, the integration between Data Cloud and Marketing Cloud Engagement has been further…

medium.com](/@marketingcloudtips/data-cloud-journey-activity-run-added-to-starter-data-bundle-bbbe73434dd0?source=post_page-----b32181d3e42a---------------------------------------)

### **⑥ On-Screen Visibility into Message Usage**

**Marketing Cloud Next for Engagement** now includes a **Digital Wallet**, giving you visibility into message usage by day, by channel, and by Marketing Cloud Engagement business unit.

To simplify billing, every message sent consumes Salesforce message credits.

> ***Availability:*** *This feature was released on* ***July 15, 2025****.*

[## SFMC Tips #152 : Message Usage Visibility Now Available in Marketing Cloud Engagement+

### If you’re currently using Marketing Cloud Engagement+, as of July 28, 2025, you can now view the message usage data…

medium.com](/@marketingcloudtips/message-usage-visibility-now-available-in-marketing-cloud-engagement-dcb477d08c66?source=post_page-----b32181d3e42a---------------------------------------)

## **Automation Studio Updates**

### **① Introduction of the Query Activity Optimizer Dashboard**

You can now improve SQL query performance in Automation Studio by leveraging insights from the **SQL Query Activity Optimizer Dashboard**. Each query is assigned a performance risk score along with a list of actionable recommendations, helping optimize efficiency and reduce execution time.

The recommendations are likely based on the general best practices for SQL query execution outlined in the help documentation:  
Help: [Optimizing SQL Query Activities](https://help.salesforce.com/s/articleView?language=ja&id=mktg.mc_as_optimize_the_query_activity.htm&type=5)

### **② Extended Data Retention for Automation Data Views**

The data retention period for automation-related data views has been extended from **31 days (including the current day)** to **6 months**. This enhancement allows for deeper insights, more effective performance monitoring, and more efficient troubleshooting.

Reference: How to Bulk Retrieve Automation Activity Execution Times

[## SFMC Tips #45 : How to Bulk Retrieve Execution Times of Automation Activities in Each Step of…

### Have you ever wanted to find out:

medium.com](/@marketingcloudtips/how-to-bulk-retrieve-execution-times-of-automation-activities-in-each-step-of-automation-studio-16903798fc9a?source=post_page-----b32181d3e42a---------------------------------------)

### **③ Improved Recommendations for Automation Start Times**

The recommendation feature for suggesting optimal automation start times has been enhanced. Based on statistical data, it now helps ensure that automations run at the most efficient times, enabling smoother execution.

Once this feature is released, I plan to review and update the content of the following article accordingly.

[## SFMC Tips #49 : Introducing the New Feature: Recommended Automation Start Times

### The Salesforce Marketing Cloud Summer ’24 release is nearing its conclusion. A new feature that recommends automation…

medium.com](/@marketingcloudtips/introducing-the-new-feature-recommended-automation-start-times-259b17962f37?source=post_page-----b32181d3e42a---------------------------------------)

### **④ Force-Stop Automation Triggers**

The **Stop** button can now clear all automations queued for execution. This prevents new automations from starting before the previous ones have fully stopped, improving system stability and data consistency. It seems this change may reflect an update in the underlying system behavior.

## **Journey Builder Updates**

### **① Download Results from the Journey History Dashboard**

You can now download **all history events** that match your filter criteria directly from the Journey History dashboard. Additionally, it is now possible to search by specifying an **Activity ID**.

Until now, only the data displayed on the dashboard could be downloaded as a CSV, making it cumbersome to scroll through large datasets. To retrieve the complete history, you previously had to use the **Journey History Download API**, as explained in the article linked below. Going forward, marketers will be able to download all relevant data directly from the dashboard with ease.

[## Extracting Contacts Passing Through Wait activities Using Journey Builder REST API

### In the ever-evolving landscape of Salesforce Marketing Cloud, developers often grapple with the challenge of…

medium.com](/@marketingcloudtips/extracting-contacts-passing-through-wait-activities-using-journey-builder-rest-api-8d22ff0048a0?source=post_page-----b32181d3e42a---------------------------------------)

This feature is extremely convenient. Previously, in order to extract contacts who passed through a specific path, you had to place a **“Update Contact” activity** in advance and record the contacts in a Data Extension. From now on, you can download the contacts who passed through the target path **directly**, without any prior setup. Once downloaded, this data can be imported into a Data Extension, making further analysis with SQL queries or additional processing straightforward.

However, please note that the data available for download is limited to the **past 30 days**.

### **② Filter Journey Information at a Glance**

The Journey Dashboard now includes new icons, making it easier to see key information at a glance.

- A **connected campaign icon** indicates which journeys are part of a campaign.
- An **HTS icon** indicates that High Throughput Sending is enabled on a journey.

Additionally, the **Last Activity Date** column shows when a contact was last processed in the journey. When you apply multiple filters, the journey count automatically updates to display the number of journeys matching the selected filters.

### **③ Personalize Journeys with MMS Messages**

Journey Builder’s messaging capabilities have been expanded with support for **MMS (Multimedia Messaging Service)**. In addition to text, you can now send images, GIFs, audio, and video to personalize messages and drive stronger engagement.

### **④ Removal of Default Selection for Pausing Journeys**

To confirm whether you truly intend to pause a journey, the default selection has been removed from the pause modal. You must now explicitly select the pause action before saving changes.

### **⑤ Default Enablement of High Throughput Sending (HTS)**

High-Throughput Sending (HTS) can now be reliably enabled for all journeys. Administrators can turn on HTS by default for all new journeys within a business unit. To enable this feature, go to **Email Options Features** in Setup and switch it on.

> *Previously, enabling HTS by default required submitting a support case.*

By the way, once HTS is enabled for a journey, it cannot be disabled for that specific journey. HTS does not affect commonly used features such as data views, delivery time window settings, or send logs, but it may impact certain tracking or sending functionalities.

- Journey Builder email send summary reports and daily reports do not track HTS sends. However, metrics are available in Journey Builder Analytics and Intelligence Reports.
- When HTS is enabled, Email Studio’s journey tracking folders are not created. Metrics remain available in Analytics and Intelligence Reports.
- If errors or suppressions occur in email activities, subscribers remain in the journey, but the email is not delivered.
- HTS email send errors are not shown in journey history. To check them, open the activity in the journey canvas and go to **View Details → Not Sent**. You can also use the **NotSent Extract** in Automation Studio to see undelivered subscribers.
- HTS cannot be used if **Field-Level Encryption** is enabled.
- Message priority is not recognized under HTS.
- Subscriber error thresholds in triggered sends are not recognized when HTS is enabled.

### **⑥ Improved Accuracy for Salesforce Data Entry Sources**

This update is part of the **Spring ’26 Release**. To enable this feature early for testing purposes, please contact Salesforce Customer Support.

The accuracy of **Salesforce Data Entry Sources** in Journey Builder will be improved in Spring ’26. The **“Is Updated”** condition in entry criteria will now compare before-and-after field values, allowing CRM object changes to be detected more precisely.

This ensures that more contacts can enter journeys at the right time. For example, when the **Status** field changes from In Progress to Completed, the contact becomes eligible to enter a journey, enabling automation triggered by specific customer lifecycle changes.

## **Contact Builder Updates**

### **① Restore Data Cleared from a Data Extension**

A new **“Cleared Data”** folder has been added to the **Recycle Bin** in Contact Builder. When you use the **[Clear Records]** button to remove all records from a data extension, the data is moved to this **Cleared Data** folder and retained for **30 days**.

If you accidentally clear data from a data extension, you can now **restore it into a new data extension**.

**How to Restore:**

1. In **Contact Builder**, go to the **[Data Extensions]** tab.
2. Select **[Recycle Bin] > [Cleared Data]**.
3. Choose the data you want to restore and click **[Restore]**.

> ***Availability:*** *Rolling out gradually starting* ***November 2025****.*

## **WhatsApp Updates**

### **① Ensure Compliance with Blockout Windows**

Set up blockout windows to restrict message delivery during certain times of day. This helps reduce unnecessary communications, minimize potential complaints, and ensure that your messaging practices comply with regional regulations and customer preferences.

### **② Send Time-Limited Offers**

You can now deliver time-limited promotions and coupons directly to customers through WhatsApp. This new **interactive message template** includes an expiration feature for offers, encouraging timely action and driving sales.

### **③ Enhance Conversations with WhatsApp Stickers**

WhatsApp session messages can now be enriched with curated stickers, making replies more engaging and visually expressive.

Stickers must be created in **.webp format** and uploaded to **Content Builder** or a public hosting service to obtain a secure URL. Sent stickers can be downloaded and forwarded by customers.

### **④  Business Locations with Customers**

Provide accessible business information by sending location details. Both **session messages** and **template messages** in WhatsApp can now include location sharing. Add details such as location name, latitude, and longitude to guide customers directly to your business.

### **⑤ Access the New Meta APIs**

Users of **WhatsApp Direct** can now take advantage of Meta’s latest set of APIs, specifically designed for marketing use cases. These APIs help streamline campaign execution and improve deliverability rates.

## **Einstein Updates**

### **① Greater Flexibility in Einstein Engagement Scoring**

Einstein Engagement Scoring is now more flexible, allowing you to enable or disable the feature at the **business unit level**.

You can also control **web engagement tracking** by toggling web conversions on or off within Einstein Engagement Scoring.

> *This feature was released on July 31, 2025.*

## **Audit Trail Updates**

### **① Gain Insights into Automation Activities with** Advanced Audit Trail

The Advanced Audit Trail update makes it possible to track which users created, updated, or deleted **Automation Studio activities**.

You now have access to detailed action logs for file transfers, queries, data copy or import activities, scripts, extracts, reports, waits, data validations, and journey events.

\*Advanced Audit Trail is a paid feature.

### **② Track Package Changes with Basic Audit Trail**

Basic Audit Trail now includes tracking for **changes to installed packages**. This allows you to monitor when users modify package components, permissions, client secrets, and other package-related elements.

## Closing Notes

The release of **Marketing Cloud Next for Engagement** is certainly the most interesting part. Although **Marketing Cloud Engagement+** is now available for purchase, it’s unclear whether you can use it immediately in your existing environment simply by buying a license. Since the functionality is quite different, if a data migration to the replacement Marketing Cloud Engagement+ environment is required, it could involve a bit of work. 🤔

> *This Winter ’26 release will be rolled out gradually between* ***October 3, 2025, and November 1, 2025****. Please note that as of the time this article is published, the new features are not yet available.*

That’s all for this update.

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
