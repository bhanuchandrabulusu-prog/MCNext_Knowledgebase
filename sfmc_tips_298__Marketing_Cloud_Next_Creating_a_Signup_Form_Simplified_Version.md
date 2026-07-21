# SFMC Tips #298 : Marketing Cloud Next: Creating a Signup Form (Simplified Version)

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-next-creating-a-signup-form-simplified-version-43e797302478

---

# SFMC Tips #298 : Marketing Cloud Next: Creating a Signup Form (Simplified Version)

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--43e797302478---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--43e797302478---------------------------------------)

7 min read

·

May 19, 2026

--

Photo by [kiryl](https://unsplash.com/@kshar2?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

In the [**Summer ’26** feature release](/@marketingcloudtips/marketing-cloud-next-summer-26-release-highlights-04f6c5abdee6) for **Marketing Cloud Next Growth & Advanced Editions**, several improvements were added to the **campaign flow creation experience** and **flow template functionality**.

This article explains the following points:

- ① The default start tab changed from **“Quick Start”** to **“Build Your Own”**
- ② Direct access to “flow templates” is now available from **“Build Your Own”**
- ③ Easy setup is now possible with the new **“Signup Form”** flow template

## ① The Default Start Tab Changed from “Quick Start” to “Build Your Own”

When creating a flow from a campaign record, the default entry point has changed from the previously displayed **“Quick Start”** tab to the **“Build Your Own”** tab.

![]()

From this **“Build Your Own”** tab, it is now possible to configure campaign flow starting settings and browse flow templates, making it easier to build flows more flexibly.

Of course, it is still possible to use the **“Quick Start”** tab to quickly launch campaigns based on preconfigured flows, just like before.

## ② Direct Access to Flow Templates from “Build Your Own”

With this improvement, marketers can now directly access the **Flow Template Library** from the **“Build Your Own”** tab.

Flow templates already include flow elements for common marketing use cases, reducing the effort required to design flows from scratch and enabling smoother implementation.

As of **Summer ’26**, the following four flow templates are available.

## Flow Templates

## 1. Event Email Automation Template

This template is designed to encourage customers to attend webinars, conferences, product launches, and other events.

A series of event communications, such as registration confirmations, reminders, and post-event follow-ups, are preconfigured.

Included content:

- Email 1: Event One Week Reminder
- Email 2: Event Registration Confirmation
- Email 3: Event One Day Reminder
- Email 4: Event Attended Follow-Up
- Email 5: Event Didn’t Attend Follow-Up

## 2. Lead Capture Follow-Up Email Automation Template

This template is designed for follow-up communications that help convert leads into customers.

Emails such as welcome messages, brand introductions, and product/service highlights are preconfigured.

Included content:

- Email 1: Lead Capture Welcome Email
- Email 2: Lead Capture Product Highlights
- Email 3: Lead Capture Brand Value Proposition

![]()

## 3. Upsert a Record for a Person Template

If a matching **Contact** or **Lead** record exists, this template updates the person’s record.  
If no matching record exists, it creates or updates a **Prospect** record.

This flow helps maintain **data consistency** across related records.

*\*Because this template is intended for use as a subflow, it is created as an* ***Autolaunched Flow (No Trigger)****.*

This template is explained in detail in the following article.

[## SFMC Tips #186 : Marketing Cloud Next: Upsert a Record for a Person Flow Template

### In the Winter ’26 release of Marketing Cloud Next Growth & Advanced Edition, a new flow template called “Upsert a…

medium.com](/@marketingcloudtips/marketing-cloud-next-upsert-a-record-for-a-person-flow-template-76fe6855686e?source=post_page-----43e797302478---------------------------------------)

## 4. Newly Added: “Signup Form” Template

This template uses signup forms to generate leads and collect consent for any messaging channel.

*\*This template is explained in the next section.*

## Deprecation of Flow Templates

Previously, there were six marketing-related flow templates available, but currently only the following four remain.

**Marketing Flow Template Library After Summer ’26**

The following three templates may have been removed in **Summer ’26**.  
(*This will be confirmed when the official production release becomes available.*)

- Birthday Promotional Email Automation Template
- Nurture Campaign Email Automation Template
- Reengagement Email Automation Template

**Marketing Flow Template Library Before Summer ’26**

## ③ Easy Setup with the New “Signup Form” Flow Template

Previously, when using **“Signup Form”** from **Quick Start**,

it was necessary to configure each step individually, such as:

1. Forms
2. Flows
3. Landing Pages

With the new ability to start directly from a flow template, these configuration tasks can now be completed together in a unified setup process, greatly reducing the complexity that was often difficult for beginners.

As a result, lead generation campaigns can now be built much more simply and smoothly.

## Setup Procedure

## 1. Select the Flow Template

Select **“Signup Form”** from the Flow Template Library.

Click **“Next”.**

## 2. Configure the Flow Name

Enter the flow name.

## 3. Configure the Processing Object and Communication Subscription

Configure the target object and communication subscription settings.

## 4. Configure Branding

Configure the branding settings.

*In some cases, branding settings may not be reflected on the landing page side.  
If this occurs, configure branding separately on the landing page afterward.*

## 5. Configure the Form Content

Configure the form field labels.

Also configure the header, footer, button text, and related settings.

***Important:*** *Some fields are treated as required and cannot be removed.* ⚠️

## 6. Decide Whether to Use a Landing Page

A landing page is not required for signup forms.

Choose whether to add a landing page, then click **“Create”.**

## 7. Change the URL Alias

It is strongly recommended to change the URL alias beforehand.

*An important point to note is that* ***once the landing page is published even once, the URL alias can no longer be changed afterward.*** ⚠️

Click the action button on the landing page.

Click **“Edit URL Details”.**

Rewrite the URL alias and save it.

## 8. Publish the Form

The item displayed under the **Start** section at the top represents the form settings.

Click **“Edit”.**

The form screen opens. Review the content, and if there are no issues, publish it as-is.

*It may take several minutes for publishing to complete.  
The status may remain as* ***“Draft”*** *temporarily, but this is normal.  
Once publishing is complete, a notification email will be sent.*

## 9. Verify the Flow

Next, open the flow.

When the form was published earlier, the flow was automatically activated.

After confirming that everything is configured correctly, close the flow.

![]()

***Note:*** *In the default configuration, the* ***Email*** *field may not be mapped in the* ***Create Records*** *element.   
If the mapping is missing, create a new version and add the Email mapping manually.* ⚠️

## 10. Publish the Landing Page

Finally, publish the landing page.

This process also takes several minutes to complete.  
 Once finished, a notification email will be sent.

## 11. Retrieve the Landing Page URL

The setup is now complete.

To retrieve the landing page URL, click **“View Record”.**

Open the **“URL”** tab to confirm the landing page URL.

How was it?

To be honest, regarding this new **“Signup Form”** mechanism, I personally felt that the previous method provided a stronger sense of being able to carefully review and configure each screen step by step.

Additionally, at the current stage, there are still many rough edges (such as Email not being mapped, or fields incorrectly treated as required and impossible to remove). In practice, it feels like some manual adjustments and edits are still necessary to make everything behave as expected. Hopefully these issues will be improved in future minor updates.

On the other hand, the previous setup process was quite complicated for beginners, and there were probably many cases where users became confused midway through the configuration process.

This new flow may also feel confusing at first, but once users become familiar with it, it may actually become a very efficient way to launch campaigns.

I plan to continue testing it in real use cases and evaluate its usability and operational behavior over time.

For reference, the setup flow of the previous **“Signup Form”** method is explained in the following article.

[## SFMC Tips #104 : Marketing Cloud Next: Creating a Signup Form

### Marketing Cloud Next (Marketing Cloud Growth & Advanced Editions) provides an efficient way to capture new leads by…

medium.com](/@marketingcloudtips/marketing-cloud-on-core-creating-a-signup-form-dcb43bbe9fea?source=post_page-----43e797302478---------------------------------------)

That’s all for this time.

Stay tuned for more Salesforce Marketing Cloud tips! 😎

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
