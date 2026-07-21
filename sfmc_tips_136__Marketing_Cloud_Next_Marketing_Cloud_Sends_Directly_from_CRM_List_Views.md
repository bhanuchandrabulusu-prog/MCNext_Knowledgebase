# SFMC Tips #136 : Marketing Cloud Next: Marketing Cloud Sends Directly from CRM List Views

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-on-core-marketing-cloud-sends-directly-from-crm-list-views-106cd7c2c465

---

# SFMC Tips #136 : Marketing Cloud Next: Marketing Cloud Sends Directly from CRM List Views

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--106cd7c2c465---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--106cd7c2c465---------------------------------------)

5 min read

·

Jun 11, 2025

--

Photo by [Ryoji Iwata](https://unsplash.com/@ryoji__iwata?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

## Overview of the New Feature

With the Summer ’25 release for **Marketing Cloud Next (Marketing Cloud Growth & Advanced Edition)**, users can now send Marketing Cloud emails directly from CRM list view screens.

[## SFMC Tips #106 : Marketing Cloud on Core: Summer ’25 Release Highlights

### Exciting updates for Marketing Cloud on Core (Marketing Cloud Growth & Advanced Edition) have been unveiled. For the…

medium.com](/@marketingcloudtips/marketing-cloud-on-core-summer-25-release-highlights-4ad6f39c5d6d?source=post_page-----106cd7c2c465---------------------------------------)

Previously, users of **Marketing Cloud Engagement** could leverage **Marketing Cloud Connect** to send emails directly from the CRM interface. This new feature brings a similar, seamless experience to Marketing Cloud Growth & Advanced Edition.

## Why This Matters

For those less familiar with **creating Data Cloud segments** or **building flows**, this enhancement provides a straightforward way to send emails designed in Marketing Cloud Growth & Advanced Edition.

This simplicity makes the feature especially appealing for teams looking to maximize efficiency without delving into complex configurations.

## **Prerequisites and Key Considerations**

### 1. Be Mindful of Filter Criteria When Creating Segments

When setting up filters in the list view, conditions based on specific relationships — such as “My Leads (Contacts)” or “Recently Viewed” — cannot be applied. If these conditions are used, you won’t be able to proceed with the setup, requiring you to revise your filter criteria.

**Pro Tip:** Start by switching from “My Leads (Contacts)” to “All Leads (Contacts)” before applying filters. This ensures broader compatibility with the available criteria.

### 2. Integration with Data Cloud

The filter criteria available in the list view must be mapped to Data Cloud’s **Data Model Objects (DMO)**. If they aren’t mapped, you’ll encounter an error during the process, such as the one shown below:

This requirement exists because the process automatically generates a **Data Cloud Segment** as part of the workflow. At a minimum, your criteria need to be segment-ready for the system to function as expected.

## **Step-by-Step Guide: Sending Emails from List Views**

Follow these steps to set up email sending from list views using Marketing Cloud Growth & Advanced Edition.

### 1. Create a List View for Your Target Segment

In the CRM interface, create a list view to define your target audience.

### 2. Click the “Send List Email” Button

Locate the “**Send List Email**” button at the top-right corner of the list view and click it.

### 3. Select “Marketing List Email”

Choose **Marketing List Email** and click **Next** to proceed.

### 4. Review List View Filters

On the next screen, the filter criteria for your list view will be displayed.

**Note:** Filters cannot be edited on this screen. Ensure your list view filters are configured beforehand.

### 5. Be Cautious About Draft Segment Creation

Clicking **Next** at this stage creates a draft segment.

**Note:** If you repeatedly click **Next** during testing, multiple draft segments will be created in Data Cloud. Proceed with caution to avoid unnecessary drafts.

### 6. Transition to Content Builder

Click the link for “**draft a new email**” to move to Content Builder.

In Content Builder, you can create new email content.

### 7. Create Email Content

Once your email content is ready, click **Next** to continue.

### 8. Select Existing Email Content

Alternatively, select a pre-existing email content template.

### 9. Final Settings and Sending

Choose “**Communication Subscription**” and “**From**” **Email Address**.

In the final screen, click **Send Email**.

**Note:** There is “no confirmation screen” at this stage, and emails will be sent immediately. Exercise caution when proceeding.

### 10. Completion and Campaign Confirmation

After sending, a pop-up banner will confirm the process and provide a link to the associated campaign record.

Navigating to the link will show the newly generated campaign record and confirm the email is being sent. Note that the process may take some time due to segment publishing.

### 11. Check Sending Results

After a short wait, you can verify the email has been sent. The process supports the latest email components, including the new **Repeater Component** introduced in Summer ’25. Success!

![]()

## Important Notes on Permissions

To perform the steps outlined above, you must have at least one of the following **permission sets**:

- **Marketing Cloud Admin**
- **Marketing Cloud Manager**

If these permissions are not assigned, clicking the “**Send List Email**” button will instead display the “**Sales List Email”** screen (below), preventing access to this feature.

## Final Thoughts

Since campaign records are automatically generated, users with strict naming conventions for campaigns should exercise caution. Additionally, when setting filter criteria, ensure you fully understand the mapping status of **Data Cloud**. Misunderstanding which fields are usable or restricted could lead to confusion. Verifying these aspects beforehand is strongly recommended.

I hope this guide helps you better understand the process of sending Marketing Cloud emails using list views.

That’s all for this time.

Stay tuned for more Salesforce Marketing Cloud tips! 😊

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
