# SFMC Tips #90 : Marketing Cloud Next: A Guide to Consent Management

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-on-core-a-guide-to-consent-management-5ca95a1602a0

---

# SFMC Tips #90 : Marketing Cloud Next: A Guide to Consent Management

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--5ca95a1602a0---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--5ca95a1602a0---------------------------------------)

7 min read

·

Mar 21, 2025

--

Photo by [Matheus Frade](https://unsplash.com/@matheusfrade?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

## The Importance of Consent Management

One of the key aspects of using Marketing Cloud Next (Marketing Cloud Growth & Advanced Edition) is managing consent.

### How Marketing Cloud Growth & Advanced Edition Differs from Marketing Cloud Engagement

- **Marketing Cloud Engagement:**  
  All subscribers are treated as Opt-In by default. Unsubscribes are often handled using custom flags set up by individual companies.
- **Marketing Cloud Growth & Advanced Edition:**  
  Registered contacts and leads are considered Opt-Out by default. Pre-registration as Opt-In is required, and emails cannot be sent without this registration.

### Disabling Consent Management

Consent Management can also be disabled in Setup.   
For more details, see the article below.

[## SFMC Tips #168 : Marketing Cloud Next: Disabling Consent Management

### In Marketing Cloud Next (Marketing Cloud Growth & Advanced Edition), there is a Consent Management feature that ensures…

medium.com](/@marketingcloudtips/marketing-cloud-next-disabling-consent-management-41d58a4acbef?source=post_page-----5ca95a1602a0---------------------------------------)

## **Consent Management System**

The consent management tool utilizes “**Communication Subscriptions**” for tracking consent data. Below are its key features:

### Supported Channels

- **Email** is included by default.
- **SMS** and **WhatsApp** require paid add-ons.

### Multiple Subscriptions

You can manage different communication subscriptions separately, such as **“Product Update Notifications”** and **“Weekly Newsletter.”** This is similar to the **Publication List** feature in Marketing Cloud Engagement.

### Management on the Data Cloud Platform

Consent management is handled via Data Cloud’s **DMOs (Data Model Objects)**, which include:

- **Communication Subscription**
- **Communication Subscription Channel Type**
- **Communication Subscription Consent**

Changes to consent data can be tracked in the **ConsentAuditTrail-ConsentAuditTrail** Data Lake Object (DLO), allowing you to monitor opt-in/opt-out timestamps down to the **year, month, day, hour, and minute**.

### Consent Management Considerations

**Location of Consent Records**  
Consent records are managed within **Data Cloud**. They are separate from the opt-in information stored in Salesforce CRM.

**Management Unit**  
Consent is managed at the **email address** or **phone number** level, not by individual ID. Therefore, if an email address changes, a new consent record must be created for the updated email.

**Reflection Time Lag**  
After updating a consent record, it takes approximately **2–3 minutes** for the change to be reflected in Data Cloud’s DMOs. It’s recommended to keep the Data Cloud data accurate.

**Impact of Deletion**  
Deleting a communication subscription will **also delete all related consent data**. Deletions should be avoided whenever possible.

**Limitations**  
“**Privacy Consent Status**” was not supported for Person Accounts or Accounts. However, **support for “Person Accounts” began in Spring ’26**.

## **How to Set Up Communication Subscriptions**

**1. Accessing Marketing Cloud Growth & Advanced Edition**  
Search for “Marketing” in the App Launcher to access the Marketing Cloud Growth & Advanced Edition.

**2. Navigating to the Settings Screen**  
From the “**Consent**” tab in Marketing Cloud Growth & Advanced Edition.

Select “**Preferences Page and Subscriptions**”.

This will take you to the following page:

**3. Managing the Preference Center**

- **Preview and Edit**: You can preview the page by selecting “View Page” and choose which communication subscription to publish by selecting “Edit Form”. This functionality is similar to the “Publication Lists” in MCE.
- **Subscription Settings**: The section labeled “Subscription” corresponds to “Communication Subscriptions”.

*In addition, with the Spring ’26 new feature release, a custom preference center was introduced, making it possible to include any text you like and reflect your brand.*

[## SFMC Tips #277 : Marketing Cloud Next: Custom Preference Page Setup

### In the Spring ’26 release of Marketing Cloud Next Growth & Advanced Edition, in addition to the standard preference…

medium.com](/@marketingcloudtips/marketing-cloud-next-custom-preference-page-setup-311bc587f406?source=post_page-----5ca95a1602a0---------------------------------------)

## **Data Processing**

Marketing Cloud Growth & Advanced Edition’s Opt-In and Opt-Out information is managed through the following Data Model Objects (DMO) in Data Cloud:

- **Communication Subscription Consent**  
   This acts similarly to the “All Subscribers” in MCE.

### Important Notes

There seems to be a time lag before updated information is reflected in this DMO. Based on my experience, it takes around 2 to 3 minutes for synchronization.

### Managing Consent Outside of Data Model Objects (DMOs)

**Managing via CRM Record Pages**  
By adding the **“Privacy Consent Status”** component to the record pages of **Contacts, Leads, and Prospects**, you can view and freely update each individual’s consent status.

*As of Spring ’26 and later, it is now supported for* ***Person Accounts*** *as well.*

*Note: When a new person record is created, it is* ***registered as “Opt-Out”*** *by default.*

From the dropdown marked in red in the image above, you can navigate to a screen where you can **manually change** the consent status to **Opt-In** or **Opt-Out**.

For instructions on how to configure this feature, please refer to the article linked below.

[## SFMC Tips #110 : Marketing Cloud Next: A Practical Guide to Enhanced CRM Record Pages

### Using Marketing Cloud Next (Marketing Cloud Growth & Advanced Edition) requires integration with Sales Cloud and…

medium.com](/@marketingcloudtips/marketing-cloud-on-core-a-practical-guide-to-enhanced-crm-record-pages-34650d05475b?source=post_page-----5ca95a1602a0---------------------------------------)

### Test Send Considerations

These are things that Marketing Cloud Engagement operators would likely be curious about, so please keep them in mind.

- When sending a test email, the current customer opt-out information is **not** taken into account. This means that even if you preview a recipient who is opted out, the test email can still be sent.
- If you unsubscribe via the Preference Center link in a test email, the email address positioned furthest to the left in the list of test recipients will actually be opted out.

![]()

However, clicking the unsubscribe link in the test email will **not** opt anyone out. This is because the Communication Subscription Channel Type is recorded as `dummyCsctToken`, so there is no impact on actual customers.

### Difference from Marketing Cloud Connect

When opting out in Marketing Cloud Growth & Advanced Edition:

- The CRM’s **Email Opt-Out** field will not be updated. This is because the “consent” in Marketing Cloud Growth & Advanced Edition manages Opt-In and Opt-Out for each communication subscription.

![]()

## **How to Import Consent Data**

You can import consent data by uploading a **CSV file** from the “**Consent**” tab.

### CSV Requirements

**Management Format**: Email address-based  
This is similar to MCE’s “Auto-Suppression List” design.

**Required Fields**: Email Address, Date Data  
The date should be written in one of the following formats:

- yyyy-MM-dd HH:mm:ss.SSSZ
- MM/dd/yyyy HH:mm:ss
- MM/DD/YYYY
- yyyy-MM-dd
- M/DD/YYYY

### Important Notes

- **Channel Separation**: Different channels (Email and SMS) cannot be imported simultaneously.
- **Information Separation**: Opt-in and Opt-Out information cannot be imported at the same time.
- **Import Limitation:** If a record with the same **Communication Subscription** and **Email Address** already exists in the DMO, it is updated only when the imported record has a later date than the existing record. Otherwise, the imported record is ignored.

## About Automating Consent Creation

With the Summer ’25 new feature release, it became possible to create consent records using **Data Cloud Triggered Flows**, allowing consent creation to be triggered by changes to DMO records.

In addition, the Spring ’26 new feature release introduced the ability to execute **Event-Triggered Flows** based on CRM record changes, making it possible to create consent records within this type of flow as well.

***Note:*** *Record-Triggered Flows do not include a “Create Consent” element.*

I explain this in the following article.

[## SFMC Tips #142 : Marketing Cloud Next : Automating Consent Creation

### In the Summer ’25 new feature release for Marketing Cloud Next Growth & Advanced Editions, the “Create Consent”…

medium.com](/@marketingcloudtips/marketing-cloud-next-leveraging-custom-unsubscribe-links-78649b12da0e?source=post_page-----5ca95a1602a0---------------------------------------)

What did you think?

In this article, I broadly organized the topic of **consent management in Marketing Cloud Next Growth & Advanced Editions**, including the differences from Marketing Cloud Engagement, the mechanism of communication subscriptions, how consent data is managed on the Data Cloud side, how to configure a preference center, precautions for test sends, and methods for manually importing and automating consent data.

One particularly important point is that, in **Marketing Cloud Growth & Advanced Editions**, consent is managed separately from Salesforce CRM’s **“Email Opt Out”** as **consent data on Data Cloud**. In addition, consent is managed based on **email addresses and phone numbers rather than Individual IDs**, so care must be taken when email addresses change or when communication subscriptions are deleted.

**Consent management is an extremely important area because it directly affects whether emails can be sent.** During the initial implementation phase, I believe it is important to design in advance:

- **Which communication subscriptions will be created**
- **At what timing opt-ins will be generated**
- **How existing consent information on the CRM side will be organized**

That’s all for this time.

Stay tuned for more Marketing Cloud Growth & Advanced Edition tips! 😊

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
