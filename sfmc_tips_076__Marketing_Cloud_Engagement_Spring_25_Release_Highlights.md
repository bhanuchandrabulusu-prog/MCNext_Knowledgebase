# SFMC Tips #76 : Marketing Cloud Engagement: Spring ’25 Release Highlights

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-spring-25-release-key-highlights-and-insights-51c43496c538

---

# SFMC Tips #76 : Marketing Cloud Engagement: Spring ’25 Release Highlights

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--51c43496c538---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--51c43496c538---------------------------------------)

9 min read

·

Feb 4, 2025

--

Photo by [Tatiana Rodriguez](https://unsplash.com/@tata186?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

Salesforce has announced the new features in the **Spring ’25 Release for Marketing Cloud**, and I would like to highlight some of them in this article.

[## Help And Training Community

### Edit description

help.salesforce.com](https://help.salesforce.com/s/articleView?id=release-notes.rn_marketing_engagement.htm&release=254&type=5&source=post_page-----51c43496c538---------------------------------------)

- Please note that as the release is not yet live, the information shared here may contain errors.
- This article focuses on key highlights and does not cover all new features.
- Additional updates will be made if further release information is shared.

\*The Spring ’25 Release is scheduled to roll out between February 21 and March 14, 2025.

## Key Takeaway

Now, regarding the new features in Spring ’25, to cut to the chase, there are no significant updates or feature improvements related to Journey Builder, Automation Studio, Email Studio, or Content Builder.

At the very least, I had expected the “Journey Builder Audit Enhancements: Slack Notification Feature”, which I wrote about prematurely during the Winter ’25 new features release, to finally be launched this time. However, it seems that it will not be released this time either.

Among the new features, if I were to highlight something noteworthy, it would be the **“Test Send” feature for App Push notifications**. Whether this “Test Send” feature is available directly in Mobile Push or can be sent from Content Builder could greatly affect its usability. **If it can be used from Content Builder, it would likely be quite practical**. I’ll check and verify the functionality once this feature is released.

Now, let’s go through what features have been introduced in the Spring ’25 release.

■ If you haven’t already, please check out my article on Winter ’25 as well.

[## SFMC Tips #58 : Marketing Cloud Winter ’25 Release: Key Highlights and Insights

### The release notes for Salesforce Marketing Cloud Winter ’25, focusing on new features, have been published. I would…

medium.com](/@marketingcloudtips/winter-24-release-highlights-notable-new-features-in-marketing-cloud-f9ab85aac8b1?source=post_page-----51c43496c538---------------------------------------)

## Automation Studio

### 1. New Limitation on Data Extract Activities

This isn’t so much a new feature as it is an announcement from Salesforce.

Starting February 10, 2025, a new usage limit will be imposed on Data Extract Activities in Marketing Cloud Engagement accounts to safeguard performance. The maximum number of processes that can be executed at one time will be capped at 250.

This might be related to the incident that occurred in the Stack 12 environment on December 24, 2024. Hopefully, this limitation will help prevent such incidents from happening again in the future.

[## Trust Status

### Edit description

status.salesforce.com](https://status.salesforce.com/incidents/13580?source=post_page-----51c43496c538---------------------------------------)

## Journey Builder

### 1. Enable High-Throughput Sends by Default

In Winter ’25, Journey Builder was enhanced to identify configurations that might impact performance during journey validation. If there were draft or active journeys where High-Throughput Sends (HTS) were not enabled for email activities, the system would recommend enabling the setting.

Now, with Spring ’25, you can finally enable High-Throughput Sends as the default setting.

**How to enable it:**  
Contact Salesforce Support to request the default setting for HTS to be enabled.

**Notes:**

- This does not apply to journeys created by duplicating existing journeys.
- Journey Builder can process up to 2 million email sends per hour per tenant. By using High-Throughput Sends, it is generally possible to achieve more than double the throughput as a baseline.

**■ Considerations for High-Throughput Sends**

[## Help And Training Community

### Edit description

help.salesforce.com](https://help.salesforce.com/s/articleView?language=en_US&id=sf.mc_jb_high_throughput_sending.htm&type=5&source=post_page-----51c43496c538---------------------------------------)

## Reports

### 1. Engagement Data Retention Policy Schedule Change

I’ve covered this topic in detail in a previous article. Please refer to the article below for more information.

[## SFMC Tips #65 : Changes to Engagement Data Retention Policy: 180 Days

### Starting May 15, 2025, the period during which engagement data in Salesforce Marketing Cloud Engagement will remain…

medium.com](/@marketingcloudtips/changes-to-engagement-data-retention-policy-180-days-d7d31cc837c5?source=post_page-----51c43496c538---------------------------------------)

The implementation date has been postponed from January 15, 2025, to **May 15, 2025**. This announcement was made on January 3.

### 2. Intelligence Reports Are Not Accessible on Hyperforce

In Marketing Cloud Engagement on Hyperforce, Intelligence Reports are no longer accessible. Instead, you’ll need to use Data Cloud Reports to create Intelligence Reports. This seems like a reasonable adjustment in terms of both operations and costs, given that both operate within the AWS environment.

I wonder how the previous issue of data delays (a one-day lag) will be handled in Hyperforce. Since I haven’t yet experienced Marketing Cloud Engagement on Hyperforce, I’m curious to know. If you have any insights, please share them in the comments. 🙏

**Notes:**

- This change does not affect Marketing Cloud Engagement instances that are not on Hyperforce.
- This change was fully implemented in January 2025.

### 3. Reprocess Missing Report Data Without Creating a Case

Since Intelligence Reports operates on AWS, data transfer is performed in batch processing from Marketing Cloud Engagement. Due to this mechanism, real-time data verification is not possible (data is delayed by one day), and data transfer may fail at times.

Previously, when there was a lack of data or any kind of anomaly, it was necessary to create a case with Salesforce Support and request assistance for resolution. With this new feature, users can now reprocess data directly from a dedicated screen, enabling more efficient operations.

The screen has been released, and the details are explained below.

[## SFMC Tips #123 : Missing Data Reprocessing Feature for Intelligence Reports Released

### As a new feature in Marketing Cloud Engagement, the functionality to “reprocess missing report data in Intelligence…

medium.com](/@marketingcloudtips/missing-data-reprocessing-feature-for-intelligence-reports-released-4b77b77ed928?source=post_page-----51c43496c538---------------------------------------)

## Einstein

### 1. New Fields Added to AI Content Audit Export Functionality

In Winter ’25, the ability to export a comprehensive audit of generative AI content from the past 90 days (including inputs, outputs, and user feedback) was introduced to support safety and compliance efforts.

The goal is to review and analyze content to ensure it adheres to brand guidelines. By using the exported data, brands can refine their identity and personality, ensuring consistency across all AI-generated content.

With Spring ’25, new fields have been added, and column formatting has been improved to enhance review and analysis capabilities.

\*This export can be accessed from the Einstein Copy Insights setup screen.

## Mobile

### 1. Test and Verify Push Messages Before Sending

With the simplified test send feature, you can review the content, personalization, and design of push notifications, in-app messages, and inbox messages without disrupting your current workflow.

Before publishing, you can test messages directly on a device to ensure they’re ready to capture your customers’ attention.

**Availability:** This feature will be rolled out gradually starting in March 2025.

As mentioned earlier, the usability of this “test send” feature will depend on whether it is part of Mobile Push or accessible via Content Builder. If it can be used from Content Builder, it could be significantly more convenient. Once this feature is released, I will confirm its functionality.

### 2. Apply Custom Domains for SMS Link Shortening

By using a custom domain for shortened links in MobileConnect, subscriber user experience and brand awareness are improved. Previously, the only domain used for shortened links was Bitly.

In short, the appearance of the shortened URL now allows subscribers to easily identify the source, making them feel more comfortable clicking the link.

**Availability:** This feature will be rolled out gradually starting in February 2025. For details on timing and eligibility, please contact your account executive.

### 3. Ability to Disable SMS Fallback Option

Previously, when a phone number was invalid, the system would search for other phone numbers associated with the contact and attempt to send the message. However, an option has been added to prevent the system from searching for alternative phone numbers. This allows messages to be sent only to the phone number from the entry source, even if other valid phone numbers exist.

### 4. Interactive Messages on WhatsApp

By including lists or reply buttons in WhatsApp messages, you can simplify customer interactions and reduce response time. For example, customers can quickly respond by selecting options from a predefined menu.

This enables you to design structured flows that guide customer decision-making and seamlessly move the conversation to the next step without interruptions.

![]()

## Developer

### **1. Import Encrypted Files Directly via REST API**

You can now import encrypted files directly using the `/data/v1/async/import` REST endpoint. This eliminates the need to transfer and decrypt files before importing them into a data extension.

**Note:** Only “**asymmetric**” private keys are supported.

### 2. Bulk Import API for Large-Scale Data

The Bulk Import API is now available for asynchronous processing of large datasets. It enables you to insert, upsert, or update extensive data sets within a data extension seamlessly.

## Setup

### 1. Additional AWS S3 File Transfer Destinations

To enhance data management across geographic regions, additional AWS S3 file transfer destinations have been added, including:

- Asia Pacific (Hyderabad, Jakarta, Melbourne)
- Canada West (Calgary)
- Europe (Spain, Zurich)
- Israel (Tel Aviv)
- Middle East (UAE)
- AWS GovCloud (US-East, US-West)

### 2. Analyze Data Storage Usage On-Screen

Previously, data storage usage could only be exported to Excel for analysis. Now, the new “Data Extension Storage” dashboard enables visual analysis of Marketing Cloud Engagement data storage usage directly on the screen.

**How to Access:** Navigate to **[Setup] > [Data Management] > [Data Extension Storage]** to access the dashboard.

**Timing:** It will be released in a rolling manner starting from April 2025.

### 3. Self-Provisioning for SAP and Private Domain Requests

Previously, configuring SAP and private domains required submitting a request to Support. The process took up to 5 days for first-party data centers (legacy) and over 2 weeks for Hyperforce environments.

With the new UI improvements released in Spring ’25, customer administrators (primarily implementation vendors) can now self-configure within the MC Engagement Setup UI, reducing the configuration time to just 3 days.

**■ Applicability:**  
This change applies to all Marketing Cloud Engagement editions but is not yet available for Hyperforce (planned for future release as per the roadmap).

**■ Process:**  
The flow begins by clicking the “**New Domain**” button under **Setup > Security > Domain SSL Certificates**.

**■ Unsupported Features — Cases that still require Support intervention:**

- Reusing dedicated IPs
- Switching between private domains and SAP, or vice versa
- Changing subdomains (e.g., from `mail.example.com` to `mail2.example.com`)

## Package Manager

### 1. Retrieve Deployment Details and Summary

When deploying a package via the Package Manager, you can now view the object IDs and customer keys of the original and deployed items within the package on the deployment summary screen. Additionally, you can view the details of past deployments or download the summary as a shareable CSV or XLSX file.

Effective Date: Packages created on or **after March 17, 2025**

Note: Packages created before the effective date will not include this additional information.

### 2. Package Manager Folder Added

Journey Builder, Automation Studio, Content Builder, CloudPages, and Data Extension folders will be available within the Package Manager. This makes it easier to find and select the packages.

## Personal Reflections

To be honest, I found the Spring ’25 updates underwhelming. Perhaps many of you feel the same way?

As a reminder, this release will roll out between **February 21, 2025, and March 14, 2025**. Please note that at the time of writing this article, the features have not yet been released.

Additionally, Salesforce will likely host a release webinar for these new features. Once it’s held, I’ll make sure to catch up and provide supplementary information.

[## Marketing Cloud Spring '25 Release Panel

### Paul Cordasco, Product Marketing Director, Salesforce Sara Fefferman, Senior Product Marketing Manager, Salesforce…

www.salesforce.com](https://www.salesforce.com/form/events/webinars/form-rss/4842657?source=post_page-----51c43496c538---------------------------------------)

That’s all for this update!

Stay tuned for more Salesforce Marketing Cloud tips! 😊

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
