# SFMC Tips #107 : Marketing Cloud Next: Understanding the “Preview and Test Send” Feature

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-on-core-understanding-the-preview-and-test-send-feature-a91b0f6a1ecf

---

# SFMC Tips #107 : Marketing Cloud Next: Understanding the “Preview and Test Send” Feature

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--a91b0f6a1ecf---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--a91b0f6a1ecf---------------------------------------)

4 min read

·

Apr 30, 2025

--

Photo by [Jake Colling](https://unsplash.com/@jakecolling?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

The “Preview and Test Send” feature is a crucial tool for ensuring email content is accurate and displays as intended.

This feature consists of two key phases:

### 1. Preview

In the preview phase, you select a single unified individual as the sample recipient. Using this individual’s data, you can view the email content on-screen to ensure personalization and dynamic content render correctly.

### 2. Test Send

Once previewing is complete, you can use the selected sample recipient’s data to send the email to up to 5 email addresses.

\*The “test send” functionality for “test data extensions” like those available in Marketing Cloud Engagement does not yet exist.

## Key Points to Note

### Preview is Mandatory for Test Send

To perform a test send, you must first complete the preview step by selecting a unified individual. Attempting a test send without previewing will result in an error.

### Segment Selection

When selecting a segment for the sample recipient, only **published segments** are eligible. Draft segments cannot be used.

- From the published segment, you can choose one unified individual from up to 10 contacts.
- If you need to preview a specific individual, consider creating a dedicated segment for that individual.

### Group Addresses in Test Send

You can include group email addresses among the 5 email addresses used in the test send. If a group address is associated with multiple recipients (e.g., 10 members), the email will be delivered to all members of the group.

### Ensuring Deliverability

To ensure deliverability, if the sending address is `abc@google.com`, it will be changed to either of the following formats for sending:

- `abc_at_google.com@XXX.salesforce.com`
- `abc_at_google.com@XXX.mx.salesforce.com`

## Tracking for Test Sends

When sending a test email to up to five email addresses, each send record is stored in:

- **“MessagingEventsEmail — EmailEngagement”** (DLO)
- **“Email Engagement”** (DMO)

Test send logs can be identified by the fact that the **IndividualId** field contains the value `"test-send-individual-id"`.

In addition, the **ContactPointEmailAddress** (email address field) recorded here is **not** the previewed unified individual’s email address, but rather the **actual email address** to which the test email was sent. In other words, the system clearly records exactly who received the test send.

### **Open and Click Tracking**

For test sends, the **“MessagingEventsEmail — EmailEngagement”** (DLO) and **“Email Engagement”** (DMO) will only contain history records for **“Sent”** and **“Unsubscribed”** events. History records for **“Open”** and **“Click”** events are not stored.

This is because **Track Clicks** and **Track Opens** are always “off” in test sends. There is no feature to turn them “on”.

![]()

### **Unsubscribe Links**

If you click an unsubscribe link in a preview or test send, the **“Communication Subscription Channel Type”** field in the **“Communication Subscription Consent”** DMO (which manages consent data) will be populated with a dummy value `"dummyCsctToken"`. This ensures that no one’s actual communication subscription is opted out.

### **Preference Center**

On the other hand, if you unsubscribe via the Preference Center, the **leftmost email address** among the test send recipients will actually be opted out.

![]()

**Note:** Previously, the system would opt out the email address of the customer being previewed. However, this has been improved so that the change now applies only to the **leftmost email address** in the test send recipient list. As shown below, the email address to be updated is displayed in advance, so please check it before confirming the update.

## Final Thoughts

Marketing Cloud Engagement also has a “Preview and Test Send” feature, but its specifications differ, so it’s important to understand those differences and be familiar with the specifications of each platform.

In addition, in Flows there is also a “Debug” function that allows you to test the entire flow, and this includes the ability to test email sends. I’ve explained that in the article below, so please check it out.

[## SFMC Tips #157 : Marketing Cloud Next: Debugging Segment Trigger Flows

### In Marketing Cloud Next (Marketing Cloud Growth & Advanced Edition), the flow debugging feature is equivalent to the…

medium.com](/@marketingcloudtips/marketing-cloud-next-debugging-segment-trigger-flows-80efef3c4e7a?source=post_page-----a91b0f6a1ecf---------------------------------------)

That’s all for now.

Stay tuned for more Salesforce Marketing Cloud tips! 😊

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
