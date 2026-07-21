# SFMC Tips #218 : Marketing Cloud Next: Spring ’26 Release Highlights

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-next-spring-26-release-highlights-24c0c804b0cb

---

# SFMC Tips #218 : Marketing Cloud Next: Spring ’26 Release Highlights

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--24c0c804b0cb---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--24c0c804b0cb---------------------------------------)

25 min read

·

Dec 20, 2025

--

Photo by [Juliana Malta](https://unsplash.com/@julianamalta?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

The [Spring ’26 release](https://help.salesforce.com/s/articleView?id=release-notes.rn_marketing.htm&release=260&type=5) of **Marketing Cloud Next Growth & Advanced Edition** has been announced. In this article, I’ll walk you through the key highlights.

## Key New Features

The Spring ’26 release is, quite literally, the largest update to date. Among the many enhancements, the features that particularly stand out to me are as follows:

- Support for **dedicated IPs**
- **Business Unit** functionality officially released
- Ability to create **custom preference centers**
- **Marketing Cloud Engagement emails** can now be used from MCN
- Segment delivery using **Individual DMOs** and **Engagement DMOs**
- New functionality to **prevent duplicate message delivery** to recipients
- Ability to **trigger event-driven flows** based on CRM record changes
- **Progressive profiling** is now available (※ Postponed indefinitely)
- Addition of **Distributed Marketing** capabilities

Until now, Marketing Cloud Next only offered shared IPs, which imposed limitations on large-scale sends.  
With the introduction of dedicated IP support, we can finally see a future where **Marketing Cloud Next alone** — without relying on Marketing Cloud Engagement — can fully support serious B2C business operations.

In addition, long-awaited features such as **Business Units** and **custom preference centers**, which many users wanted but were previously unavailable, are now coming together all at once.

Another long-standing challenge — sending duplicate emails to recipients with multiple email addresses — also appears to be addressed in this update.  
Furthermore, while sending previously required starting from the **Unified Individual DMO**, it will now be possible to deliver segments based on **Individual DMOs** or **Engagement DMOs** as well.

There are so many new features in this release that catching up is honestly quite challenging.  
That said, my overall impression after reviewing everything is that these are all highly practical, genuinely “want-to-use” features. I’m really looking forward to the day when we can start applying them in real projects.

Now, let’s take a closer look at the **Spring ’26** new features one by one!

## Agentforce Updates

### ① Preview Campaigns Within the Campaign Creation Conversation

Within the Agentforce Campaign Creation conversation, you can now preview the campaign directly on the brief record. This allows you to review and refine the structure and content at any time before generating the final campaign.

To support these enhancements, the following updates have been implemented:

- Added a new **Refine Campaign Preview** agent topic and action
- Updated the **Save Campaign** and **Generate Campaign from Brief** flows
- Revised the **Draft Campaign from Brief** prompt template

In addition, related flows have been enhanced with improved error handling and the addition of a dedicated campaign preview step, enabling a more stable and streamlined end-to-end campaign creation process.

Campaign briefs with preview functionality are automatically displayed alongside the Agentforce chat panel, allowing you to review multi-channel steps — such as email and SMS — within the campaign flow.

[## SFMC Tips #259 : Marketing Cloud Next: Campaign Preview Refinement

### In the Spring ’26 feature release for Marketing Cloud Next Growth & Advanced Edition, a new update has been added to…

medium.com](/@marketingcloudtips/marketing-cloud-next-campaign-preview-refinement-1c4ef1bfda13?source=post_page-----24c0c804b0cb---------------------------------------)

### ② Engage Customers with Two-Way Conversational Email

**Conversational Email**, powered by Agentforce agents, engages customers through responsive, threaded conversations. It captures high-intent purchase responses, resolves customer inquiries, and delivers personalized support — without leaving the Salesforce platform.

With the **Campaign Agent**, you can easily create two-way conversational campaigns. By entering user utterances or selecting options in the campaign brief, the Campaign Agent generates a preview of a standard two-way email campaign. It also automatically includes the necessary flow elements to support two-way conversations using the Default Agent.

Enhancements in Flow Builder — such as **Wait Until Response** and conversation handoff — also make it possible to convert existing one-way campaigns into two-way campaigns.

[## SFMC Tips #281 : Marketing Cloud Next: How to Set Up Conversational Email

### Conversational Email has been introduced as a Spring ’26 new feature of Marketing Cloud Next Advanced Edition (\*this…

medium.com](/@marketingcloudtips/marketing-cloud-next-how-to-set-up-conversational-email-0ef29d7fd113?source=post_page-----24c0c804b0cb---------------------------------------)

### ③ Create Marketing Briefs from PDF and Word Files

To create campaign briefs grounded in existing content, upload documents such as PDF or Word files to **Salesforce Files** and reference them in your prompt.

The agent automatically performs grounding on the files, generates the brief, and adds links to the source documents to the new brief record.

![]()

[## SFMC Tips #261 : Marketing Cloud Next: Automatic Campaign Creation from PDF / Word

### With the Spring ’26 new feature release of Marketing Cloud Next Growth & Advanced Edition, it is now possible to create…

medium.com](/@marketingcloudtips/marketing-cloud-next-automatic-campaign-creation-from-pdf-word-136a30a73131?source=post_page-----24c0c804b0cb---------------------------------------)

### ④ Generate Campaigns Based on Brand Settings

When Agentforce Campaign Creation generates a campaign, it now uses the tone and brand identity associated with the brief. This enables you to obtain a more aligned and appropriate campaign draft with fewer manual adjustments.

> *Note: Previously, brand settings could be configured on the brief itself, but they were not reflected in the actual campaign content.*

[## SFMC Tips #117 : Marketing Cloud Next: Agentforce Campaign Creation

### The Marketing Cloud Next (Marketing Cloud Growth & Advanced Edition) includes an AI-powered feature for campaign…

medium.com](/@marketingcloudtips/marketing-cloud-on-core-agentforce-campaign-creation-697c992adbe6?source=post_page-----24c0c804b0cb---------------------------------------)

### ⑤ Add Campaign Context Through Brief Grounding

By using additional fields, you can provide critical context required for campaigns. With custom agents, you can include key campaign objectives, KPIs, priorities, CTAs, guardrails, and more. These additional grounding inputs enable agents to make more strategic and accurate decisions, reducing generic responses.

## Business Unit Updates

### ① Data and Content Segmentation and Alignment Using Business Units

Business Units enable compliance management, audience-specific messaging, and accurate measurement of marketing performance.

Business Units support the following capabilities:

- Create up to **50 Business Units per organization**
- Assign users to **one or more Business Units**
- Automatically add filters to Marketing DLOs and align Business Unit data with the corresponding Data Spaces
- Assign campaigns and marketing workspaces to Business Units
- Assign channels (Email, SMS, WhatsApp, Mobile App Messaging) and subscriptions to specific Business Units or to all Business Units
- View marketing performance by Business Unit or create Business Units to understand enterprise-wide performance
- Track visitor activity for campaigns on external web pages by Business Unit
- Use Einstein features — such as Send Time Optimization, engagement frequency, and engagement scoring — at the Business Unit level
- Specify which Business Unit the **Campaign Creation Agent** should operate in via Agentforce

**How to use:**  
After enabling Business Units in Setup, complete the steps to create the first two Business Units.   
Existing marketing settings (such as Data Spaces and default content workspaces) will be used as-is for the initial Business Unit setup.

[## SFMC Tips #266 : Marketing Cloud Next: Business Units Now Generally Available

### In Marketing Cloud Next Growth & Advanced Edition, Business Units were introduced as a new feature in the Spring ’26…

medium.com](/@marketingcloudtips/marketing-cloud-next-business-units-now-generally-available-b01e49c09a9a?source=post_page-----24c0c804b0cb---------------------------------------)

### Agentforce Scope Setting and Management

To define the scope of follow-up actions during campaign creation in the current Agentforce session, use the new **Identify Business Unit** agent action to determine the user’s Business Unit access.

To receive the latest updates for Business Unit support, redeploy the Campaign Creation Agent, topics, or actions.

From **Assistant Home** in Setup, you can monitor setup progress across all Business Units. You’ll see an overview of the required tasks for each Business Unit, along with a visual indicator of overall status.

## Content Updates

### ① Boost Productivity with Third-Party Extensions

By using extensions, you can add productivity tools — such as third-party generative AI tools, tone and grammar editors, and translation tools — directly into the content creation experience.

Extensions appear in a floating panel within the builder and can be used to draft, revise, and customize either the entire piece of content or individual components.

> *Note: Developers can also build extensions tailored to specific content types or builder components.*

### ② Templates for Fast and Easy Branding

You can access a library of preconfigured email and landing page templates designed for use across a wide range of industries.

Marketers can quickly and easily customize and style content to match campaign goals and brand guidelines.

**Examples of standard landing page templates**

![]()

- Free trial
- Gated content
- Offer pages, and more

**Examples of standard email templates**

- Appointment scheduling
- Coming soon / launch announcements
- Brand storytelling, and more

### ③ Addition of Distributed Marketing Capabilities

*Note: This feature is a* ***paid feature*** *(from $50 per user/month).*

To improve productivity without compromising brand consistency, you can now share approved email templates created in Marketing Cloud Next with non-marketing users such as sales representatives.

After marketers create an email template, they can add it to a Flow and lock or unlock specific components. Once the Flow is published, the template becomes available in a simplified email composition interface for immediate use.

To use this feature, administrators must enable Distributed Marketing and Alerts in Setup and add the required Lightning components to the record page.

[## SFMC Tips #260 : Marketing Cloud Next: Distributed Marketing & Alerts

### Distributed Marketing & Alerts has been released as a new feature in the Spring ’26 release of Marketing Cloud Next…

medium.com](/@marketingcloudtips/marketing-cloud-next-distributed-marketing-alerts-9182444afd2f?source=post_page-----24c0c804b0cb---------------------------------------)

### ④ Enforcing Brand Standards with Locked Email Templates

Marketing managers can lock specific elements within email templates to ensure brand consistency.

Critical content such as subject lines, headers, and legal disclaimers can be protected to prevent unintended changes, while unlocked areas remain flexible for creators to customize.

In the component tree (shown below), non-editable sections are clearly indicated with visual icons.

![]()

### ⑤ Advanced Email Personalization with Enhanced Data Sources

You can now achieve more flexible email personalization by leveraging extended data sources such as segment activation data, Apex classes, and lookup data graphs.

**Newly introduced data sources:**

1. **Activation Data Provider**
2. **Apex Class Data Provider**
3. **Lookup Data Graph Data Provider**

1. By referencing Data 360 segment activation data, data-driven email delivery is now possible.

[## SFMC Tips #243 : Marketing Cloud Next: Triggering Email Sends with Activation-Triggered Flows

### With Marketing Cloud Next Growth / Advanced Edition, it is now possible to send emails at the moment a segment is…

medium.com](/@marketingcloudtips/marketing-cloud-next-triggering-email-sends-with-activation-triggered-flows-6a2ad381713b?source=post_page-----24c0c804b0cb---------------------------------------)

2. Using the Apex Class Data Provider, complex and structured data — such as collections of order information — can be passed directly from flows into messages. This enables the creation of fast and highly personalized emails, such as order confirmation emails.

[## SFMC Tips #245 : Marketing Cloud Next: Run Event-Triggered Flows When CRM Records Change

### In the Spring ’26 new feature release of Marketing Cloud Next Growth & Advanced Edition, it is now possible to start an…

medium.com](/@marketingcloudtips/marketing-cloud-next-run-event-triggered-flows-when-crm-records-change-a3a05691b427?source=post_page-----24c0c804b0cb---------------------------------------)

3. You can now define dedicated lookup data graphs for using non-profile Data 360 data, such as product catalogs, allowing you to complement the default data graph.

[## SFMC Tips #296 : Marketing Cloud Next : Lookup Data Graph Data Provider

### In the Spring ’26 new feature release for Marketing Cloud Next Growth & Advanced Editions, a Lookup Data Graph became…

medium.com](/@marketingcloudtips/marketing-cloud-next-lookup-data-graph-data-provider-0054d3fcdd83?source=post_page-----24c0c804b0cb---------------------------------------)

### ⑥ Attach PDFs to Email Content

Marketers can now attach important business documents — such as terms and conditions, white papers, and invoices — to emails.

From the properties panel, you can select PDFs under 5 MB from Salesforce CMS and attach them to emails.

With the introduction of this feature, the ability to upload “Documents” within content has also been introduced.

[## SFMC Tips #258 : Marketing Cloud Next: Send Emails with PDF Attachments

### As a new feature released in Spring ’26 for Marketing Cloud Next Growth & Advanced Edition, it is now possible to send…

medium.com](/@marketingcloudtips/marketing-cloud-next-send-emails-with-pdf-attachments-78eee857af44?source=post_page-----24c0c804b0cb---------------------------------------)

### ⑦ Advanced Control of Email Content with Low-Code Scripts

For advanced content personalization and fine-grained control over messaging, you can use the industry-standard **Handlebars** templating language.

Existing emails can be converted into code, allowing you to write, review, and edit scripts with conditional logic and data references. During creation, Code View provides syntax validation, inline coding assistance, and search functionality.

> *Designers, developers, and advanced marketers can access this low-code scripting language directly from Code View when creating emails.*

[## Marketing Cloud Next - Handlebars low-code scripting - The Agentic Marketer

### Master Handlebars scripting in Salesforce Marketing Cloud Next. Learn to use low-code scripting for conditional logic…

the-agentic-marketer.com](https://the-agentic-marketer.com/marketing-cloud-next-deep-dives/marketing-cloud-next-handlebars-low-code-scripting/?source=post_page-----24c0c804b0cb---------------------------------------)

### ⑧ Enhanced Rich Text Editor for Email Styling

You now have more precise control over text styling and spacing within email layouts.

Key enhancements include:

- Emojis
- Font family, font size, and line height
- Text color and background color
- Quotes (blockquotes)
- Horizontal rules

Traditional Rich Text Editor

New Rich Text Editor

## Landing Page Updates

### ① Reusable Content Blocks for Landing Pages

To maintain consistency across landing pages, content administrators and managers can create reusable content blocks such as banners, footers, and other standard layouts.

With the new **Content Block: Landing Page**, you can create reusable blocks combining text, images, and buttons, which marketers can then add to landing pages.

> *※ The Form block cannot be used within content blocks.  
> ※ Reusable content blocks for email have already been released.*

### ② Landing Page Personalization with Dynamic Content

To personalize landing pages for different audiences, marketers can now create dynamic variations of components such as headers, sections, and images.

Rules that identify the target audience control which variation is shown to each visitor.

Enhanced preview capabilities allow marketers to test each variation by selecting segments and sample visitors.

Additionally, personalization points can be duplicated and reused to ensure consistent personalization across both emails and landing pages within a campaign.

*Note: This feature is available only in production orgs created in Spring ’25 or later. It is also not available in SDO, the partner-only demo org.*

[## SFMC Tips #174 : Marketing Cloud Next: How to Set Up Dynamic Content

### In Marketing Cloud Next (Marketing Cloud Growth & Advanced Edition), you can create dynamic content tailored to the…

medium.com](/@marketingcloudtips/marketing-cloud-next-how-to-set-up-dynamic-content-3c8ba2c53036?source=post_page-----24c0c804b0cb---------------------------------------)

### ③ Progressive Profiling Is (Not) Available

By applying progressive profiling rules to forms, you can speed up the submission process and increase lead capture.

> *Note: This feature release has been postponed indefinitely.*

[## SFMC Tips #256 : Marketing Cloud Next: Regarding the Progressive Profiling Feature (Article…

### Regarding the Marketing Cloud Next Progressive Profiling Feature (Important Notice — February 24, 2026)

medium.com](/@marketingcloudtips/marketing-cloud-next-progressive-profiling-fa159cc3e103?source=post_page-----24c0c804b0cb---------------------------------------)

Once a user responds to certain fields, subsequent interactions will prompt them for different information.

Progressive profiling optimizes the user experience by first collecting basics such as email address and name, and then requesting more detailed information — such as job title or phone number — in later interactions.

### ④ Customizing Brand-Aligned Preference Pages

By designing a custom preference page that reflects your brand, you can provide subscribers with a consistent and trustworthy experience.

![]()

By enabling the “Custom Preference Page” feature in the settings, you can create different pages for each channel.

[## SFMC Tips #277 : Marketing Cloud Next: Custom Preference Page Setup

### In the Spring ’26 release of Marketing Cloud Next Growth & Advanced Edition, in addition to the standard preference…

medium.com](/@marketingcloudtips/marketing-cloud-next-custom-preference-page-setup-311bc587f406?source=post_page-----24c0c804b0cb---------------------------------------)

## Flow Updates

### ① Marketing Cloud Engagement Emails Are Now Supported

You can now send **Marketing Cloud Engagement** emails through **segment-triggered flows**, **event-triggered flows**, **activation-triggered flows**, or **broadcast flows**.

By using the **Send Marketing Cloud Engagement Email** action, you can efficiently target **Data 360 segments** while reusing existing Marketing Cloud Engagement content and settings — without requiring activation or data duplication.

**How to use:**  
 To use this action, add the **Send Marketing Cloud Engagement Email** element to the Flow Builder canvas, then configure the following:

- Select the Business Unit
- Select the email content to use
- Select the publication list for consent management
- (Optional) Directly map personalization data from the flow to the triggered send data extension

This allows you to automate Marketing Cloud Engagement email sends directly from Flow in a flexible and efficient way.

### ② Preventing Duplicate Sends to Multiple Email Addresses

Previously in **Marketing Cloud Next**, when multiple contact points (email addresses) were associated with a single **Unified Individual**, messages were sent to **all associated email addresses**.

However, with this new feature, by using **Contact Point Selection Rules**, it is now possible to select the **appropriate individual record and a single messaging contact point** to send the message.

As a result, the **accuracy of message delivery is improved**.

[## SFMC Tips #166 : Marketing Cloud Next: Understanding Which Email Addresses Are Used for Sending

### In Marketing Cloud Next (Marketing Cloud Growth & Advanced Edition), it’s crucial to correctly identify which email…

medium.com](/@marketingcloudtips/marketing-cloud-next-understanding-which-email-addresses-are-used-for-sending-ca52aaace7d9?source=post_page-----24c0c804b0cb---------------------------------------)

> ***Important:*** *With this update, the flow can retrieve the email address* ***directly from the source system****, even if* ***identity resolution or the data graph has not yet been updated****.*

### Configuring Contact Point Selection Rules

1. First, configure contact point selection rules using **Data 360 activation templates**.
2. After defining the rules, open the flow and click **[Select Segment]** in the Start element to open the settings panel.
3. In the **Contact Point Configuration** section of the settings panel, select the activation template to use.

### For Engagement Signals

When configuring an **automation event-triggered flow**, specify where the contact point should be retrieved from:

- From event data, if included in engagement data
- From the source system, if required

The flow automatically retrieves the contact point based on the selected method. This ensures that messaging actions are executed reliably — even for newly created individual records or records still in data processing.

### ③ Sending Emails Using Activation Data

In activation-triggered flows, if you want to include activation-derived data in emails using the **Send Email Message** action, use the “**Activation Data Provider**” within the email.

[## SFMC Tips #243 : Marketing Cloud Next: Triggering Email Sends with Activation-Triggered Flows

### With Marketing Cloud Next Growth / Advanced Edition, it is now possible to send emails at the moment a segment is…

medium.com](/@marketingcloudtips/marketing-cloud-next-triggering-email-sends-with-activation-triggered-flows-6a2ad381713b?source=post_page-----24c0c804b0cb---------------------------------------)

### ④ More Flexible Scheduling for Segment-Triggered Flows

Segment-triggered flows can now run on customizable schedules, providing greater control and precision.

For example, you can run flows hourly to always use the latest data, or schedule them to run only on weekdays to avoid weekend sends.

Newly added scheduling options include:

- **Hourly**
- **Daily on weekdays**
- **Weekly on specific days**
- **Monthly on specific days**
- **Yearly**

Traditional Scheduling Screen

New Scheduling Screen

### ⑤ Sending Emails Based on Individual DMO or Engagement DMO

In addition to the Unified Individual DMO, you can now create segment-triggered flows using segments based on **Individual DMOs** or **Engagement DMOs**.

For example, you can create a segment such as “all contacts who converted yesterday”.

This update enables more precise targeting and provides access to engagement-specific data, such as order details and registration information.

[## SFMC Tips #270 : Marketing Cloud Next: Segment Triggered Flow Based on Individual

### In the Spring ’26 new features of Marketing Cloud Next Growth & Advanced Edition, in addition to the existing Unified…

medium.com](/@marketingcloudtips/marketing-cloud-next-segment-triggered-flow-based-on-individual-8964a8886f59?source=post_page-----24c0c804b0cb---------------------------------------)

### ⑥ Testing Multiple Records When Debugging Segment-Triggered Flows

You can now test up to **10 records simultaneously**.

> *※ Before Spring ’26, only one record could be selected using the radio button.*

Using the debug panel, you can immediately see how different customers move through a flow. This update helps you quickly identify issues across a variety of customer profiles before activating the flow.

**How to use:**  
When testing a segment-triggered flow, select up to 10 records from the segment member list using checkboxes.  
Then run the debugger to:

- Switch between individual test results
- Filter by error or success
- Highlight the path taken by the currently selected record directly on the flow canvas

[## SFMC Tips #157 : Marketing Cloud Next: Debugging Segment Trigger Flows

### In Marketing Cloud Next (Marketing Cloud Growth & Advanced Edition), the flow debugging feature is equivalent to the…

medium.com](/@marketingcloudtips/marketing-cloud-next-debugging-segment-trigger-flows-80efef3c4e7a?source=post_page-----24c0c804b0cb---------------------------------------)

### ⑦ Triggering Event-Triggered Flows Based on CRM Changes

You can now trigger **automation event-triggered flows** when Prospect, Lead, or Contact records — or related records — are updated.

For example, you can send a personalized email to a contact when a case is closed, or trigger a follow-up flow to notify a lead owner when an opportunity moves to a new stage.

This update allows you to engage customers immediately after key business events occur, using Prospect, Lead, and Contact data for message personalization.

**How to use:**

- Create an event-triggered flow
- Select **“Prospect, Lead, Contact or Related Record Change”** as the trigger type
- Choose the Prospect / Lead / Contact object or a related object
- Configure trigger conditions (when it runs) and entry conditions

[## SFMC Tips #245 : Marketing Cloud Next: Run Event-Triggered Flows When CRM Records Change

### In the Spring ’26 new feature release of Marketing Cloud Next Growth & Advanced Edition, it is now possible to start an…

medium.com](/@marketingcloudtips/marketing-cloud-next-run-event-triggered-flows-when-crm-records-change-a3a05691b427?source=post_page-----24c0c804b0cb---------------------------------------)

### ⑧ Automatically Receive Notifications for Path Experiment Results

Users who activate a flow will now receive **in-app notifications** when a Path Experiment is completed.

Notifications include:

- The selected winning path
- Fallback handling status
- Results when no conclusion is reached

This update allows flow creators to stay informed of experiment results without any additional setup.

> *Note: If the user who activated the flow is deactivated, notifications will not be sent.*

### ⑨ Control Path Selection During Path Experiment Debugging

In Path Experiment elements, you can now control how paths are assigned during debugging.

By default, paths are assigned randomly, but during debugging you can manually select the winning path.

Manual selection allows you to reliably test specific paths without relying on randomness, ensuring that intended branches and downstream logic behave as expected.

[## SFMC Tips #252 : Marketing Cloud Next: “Path Experiment” Enhancements — Spring ‘26

### In the Spring ’26 new feature release of Marketing Cloud Next, several important enhancements have been made to the…

medium.com](/@marketingcloudtips/marketing-cloud-next-path-experiment-enhancements-spring-26-424bc50ec961?source=post_page-----24c0c804b0cb---------------------------------------)

### ⑩ View Path Experiment History

A newly added **History** tab makes it possible to understand what happened during a Path Experiment.

![]()

You can review all changes made since activation, including:

- Timestamps (date and time of changes)
- The user who made the change
- Whether the change was automated or manual

The following events are also tracked:

- Experiment start
- Winning path selection
- Delayed group release
- Fallback processing

[## SFMC Tips #252 : Marketing Cloud Next: “Path Experiment” Enhancements — Spring ‘26

### In the Spring ’26 new feature release of Marketing Cloud Next, several important enhancements have been made to the…

medium.com](/@marketingcloudtips/marketing-cloud-next-path-experiment-enhancements-spring-26-424bc50ec961?source=post_page-----24c0c804b0cb---------------------------------------)

### ⑪ Track Individual Flow Paths

You can now troubleshoot individual customer issues by viewing the exact path a specific individual followed during flow execution.

This feature visualizes:

- Which branch path was selected
- Which elements were completed
- Where errors or delays may have occurred

This detailed view allows administrators to efficiently investigate and validate:

- Inquiries or complaints from specific customers
- Whether personalization logic is working correctly
- Bottlenecks affecting specific contacts within marketing automation flows

> *Element-level logging in Data 360 must be enabled.*

**How to use:**  
 To track a specific individual’s flow execution path:

- Open a completed flow in Flow Builder
- Click **[View Additional Analytics]**
- Select **[View Flow Run for Individual]**

[## SFMC Tips #309 : Marketing Cloud Next: View Flow Run for Individual Analytics

### The View Flow Run for Individual analytics feature, which was announced in the Spring ’26 release notes for Marketing…

medium.com](/@marketingcloudtips/marketing-cloud-next-view-flow-run-for-individual-analytics-70ebedf158bb?source=post_page-----24c0c804b0cb---------------------------------------)

### ⑫ Personalize On-Demand Flows Using Apex

You can now use Apex code to personalize on-demand flows and control processing priority when triggering flows via APIs.

This allows you to target specific individuals or contact points for message delivery.

You can also use built-in debugging tools to validate flows, test logic, and identify issues before activation. In addition, help documentation is directly accessible from the Start node, making it easy to review configuration options and best practices.

These updates provide greater flexibility in customizing flow behavior and enable faster troubleshooting during development.

[## SFMC Tips #244 : Marketing Cloud Next: Personalizing On-Demand Flows Using Apex

### With the Winter ’26 new feature release of Marketing Cloud Next Growth & Advanced Edition, a new flow type called…

medium.com](/@marketingcloudtips/marketing-cloud-next-personalizing-on-demand-flows-using-apex-366692c7ce6a?source=post_page-----24c0c804b0cb---------------------------------------)

### ⑬ Exclude Flow Participants (Individuals) via API

You can now exclude individuals from flows through API triggers from external systems.

For example, you can remove customers from a flow when an order is completed or when they reach a specific status.

This update enables flexible control over flow exit timing while integrating with external systems.

**How to use:**

- Configure exit rules that can be triggered via API
- Use the newly added REST API endpoint to programmatically remove flow participants

When the API call is received, the targeted individual is immediately removed from the flow.

API-driven exit rules are supported for all flow types:

- Segment-triggered flows
- Event-triggered flows
- On-demand flows

[## SFMC Tips #247 : Marketing Cloud Next: How to Forcefully Exit Contacts from a Flow

### In Marketing Cloud Next Growth & Advanced Edition, you can use various flows such as Segment-Triggered Flows…

medium.com](/@marketingcloudtips/marketing-cloud-next-how-to-forcefully-exit-contacts-from-a-flow-bfb9bd74e071?source=post_page-----24c0c804b0cb---------------------------------------)

### ⑭ Enhancements to Activation-Triggered Flows

The following new capabilities are now available in activation-triggered flows:

- Use of **Decision** elements
- Addition of **Exit** and **Re-entry** conditions
- Ability to pause active flows
- Mapping activation data up to **five levels deep** using the **Transform** element

[## SFMC Tips #243 : Marketing Cloud Next: Triggering Email Sends with Activation-Triggered Flows

### With Marketing Cloud Next Growth / Advanced Edition, it is now possible to send emails at the moment a segment is…

medium.com](/@marketingcloudtips/marketing-cloud-next-triggering-email-sends-with-activation-triggered-flows-6a2ad381713b?source=post_page-----24c0c804b0cb---------------------------------------)

## Analytics Updates

### ① View Path Comparison Results in the Path Experiment Element

You can now monitor Path Experiment results without leaving the Flow Builder canvas.

![]()

In the newly added **Analytics** tab within the Path Experiment element panel, you can review:

- Total participants
- Evaluation metrics
- Confidence level in the path comparison

This embedded summary provides a quick, at-a-glance view of experiment outcomes in a consistent format aligned with analytics available for other flow elements.  
 For deeper analysis, click **[View Analytics]**.

[## SFMC Tips #252 : Marketing Cloud Next: “Path Experiment” Enhancements — Spring ‘26

### In the Spring ’26 new feature release of Marketing Cloud Next, several important enhancements have been made to the…

medium.com](/@marketingcloudtips/marketing-cloud-next-path-experiment-enhancements-spring-26-424bc50ec961?source=post_page-----24c0c804b0cb---------------------------------------)

### ② Measure Campaign Impact with the Conversion Analytics Dashboard

A new **Conversion Analytics** dashboard provides detailed insights into marketing campaign outcomes.

You can track how Email and SMS sends contributed to tangible outcomes — such as order completion or form submission — within a **30-day conversion window**.

You can also filter using **First Touch** or **Last Touch** attribution models to understand which messages most effectively drove conversions.

![]()

[## SFMC Tips #286 : Marketing Cloud Next: Conversion Analytics Dashboard

### As a new feature introduced in Spring ’26 for Marketing Cloud Next Growth & Advanced Edition, the Conversion Analytics…

medium.com](/@marketingcloudtips/marketing-cloud-next-conversion-analytics-dashboard-ae03ba6cb890?source=post_page-----24c0c804b0cb---------------------------------------)

### ③ The **“Unified Engagement History Dashboard”** appears on the CRM record page.

A new dashboard, the **“Unified Engagement History” Dashboard**, powered by Tableau Next technology, has been introduced.

By enabling this feature and adding the component to the record pages of **Contacts, Leads, Person Accounts, and Accounts**, marketing and sales users can leverage customer engagement data in a more intuitive and effective way.

Because email opens, clicks, and various interaction histories can be visualized directly on the CRM screen, this helps improve the accuracy of customer understanding and supports better decision-making for appropriate actions.

> ***Important:*** *This feature retrieves engagement history based on the* ***Unified Individual ID****.*

[## SFMC Tips #257 : Marketing Cloud Next: Unified Engagement History Dashboard

### Marketing Cloud Next Growth & Advanced Edition introduces a new feature in the Spring ’26 release: the Unified…

medium.com](/@marketingcloudtips/marketing-cloud-next-unified-engagement-history-dashboard-ee97fd1d217f?source=post_page-----24c0c804b0cb---------------------------------------)

### ④ Gain Deeper Insights into Mobile App Metrics

You can monitor mobile app campaign performance via a unified dashboard covering **in-app messages** and **push notifications**.

If you want to review iOS- or Android-specific metrics, you can use platform filters.

By tracking delivery rate, dismissals, and CTA clicks, you can identify issues and improve your marketing strategy.

### ⑤ Visualize Delivery Status for SMS, WhatsApp, and Mobile Push

Using the **Low-Performing Campaign** view, you can identify underperforming campaigns across SMS, WhatsApp, and mobile push.

By applying delivery status filters and visualizing activity trends, you can uncover the causes of delivery failures.

### ⑥ Set Up External Web Tracking with Fewer Steps

The improved configuration process allows **external web tracking to be set up more quickly and efficiently**.

In addition, the following components — previously required to be **installed manually** —

**Data Streams**

- **Web Tracking — Identity (person data)**
- **Web Tracking — Behavioral Events (behavioral data)**
- **MarketingStreamingAppConfig\_Home (campaign association)**

are now **automatically installed when creating a Website Connector**.

Furthermore, the **same Website Connector can now be reused across multiple campaigns**, eliminating the need to create a **new connector for each campaign**.

[## SFMC Tips #130 : Marketing Cloud Next: Tracking External Websites with a Consent Banner

### In Marketing Cloud Next Growth & Advanced Edition, it is possible to track visitor activities and engagement on landing…

medium.com](/@marketingcloudtips/marketing-cloud-on-core-tracking-external-websites-with-a-consent-banner-2492904a799c?source=post_page-----24c0c804b0cb---------------------------------------)

## Setup Updates

### ① Safely Test Email Campaigns in Sandbox

To prevent test emails from being mistakenly sent to real customer email addresses, you can use a **black hole** feature in full or partial sandbox orgs.

When the black hole is enabled in a sandbox, emails are automatically discarded before sending.

You can also add exception (allowlist) settings for recipient domains that must receive test emails.

[## SFMC Tips #246 : Marketing Cloud Next: Email Sending Safeguard for Sandbox Environments

### To enable safer use even in environments that contain actual customer data, such as Full Sandbox and Partial Copy…

medium.com](/@marketingcloudtips/marketing-cloud-next-email-sending-safeguard-for-sandbox-environments-7f285435afe1?source=post_page-----24c0c804b0cb---------------------------------------)

### ② Maximize Deliverability with Dedicated IP Support

With support for **dynamic dedicated IP addresses**, you can improve inbox placement rates for high-volume email campaigns.

In Unified Messaging, high-volume senders (typically those sending around **5 million emails per month**) are automatically migrated from a shared IP pool to dedicated IPs. This enables you to build and maintain a strong sender reputation — without manual provisioning or additional licensing.

**What it Unlocks**

By dynamically scaling your sending infrastructure based on actual delivery volume, you can eliminate the operational overhead of manually managing individual IP SKUs.

In addition, data-driven isolation provides better protection for critical campaigns, helping maintain higher deliverability compared to traditional static configurations.

**How it Works**

In **Setup → Unified Messaging → Email → Settings**, a new screen called **“Sending IP Addresses”** allows you to view automatically provisioned and pooled IP resources.

Backend services dynamically add and recover IPs based on usage trends and bounce rates, enabling seamless infrastructure scaling.

**Considerations**

- After migrating to dedicated IPs, **IP warming is performed automatically** over a period of **0 to 35 days**.
- Any sending that exceeds the warming limits during this period will continue to be delivered via **shared IPs**.
- While **manual IP warming is no longer required**, **domain warming remains important**, and a gradual sending plan should be considered to maintain stable deliverability.
- Once IP warming is complete, you can send approximately **2 to 2.5 million emails per day**.
- The maximum number of available dedicated IPs is **32**.
- If the **average sending volume over the past 45 days** falls below the threshold (**5 million emails per month**), the allocated dedicated IPs will be **gradually reclaimed** and become unavailable (they may be reused after a cooldown period).
- If only **one dedicated IP remains**, and sending stays below **5 million emails per month for 90 consecutive days**, sending will **automatically revert to shared IPs**.
- Accounts with **high bounce rates** are temporarily moved to a dedicated IP pool called the **“gray pool”**, which is separate from both shared and dedicated IP pools.
- These accounts will continue sending from the gray pool until their bounce rates improve, helping maintain the overall health of both shared and dedicated IP environments.

[## SFMC Tips #291 : Marketing Cloud Next: d IP Addresses and Dedicated IP Addresses

### In the Spring ’26 new feature release for Marketing Cloud Next Growth & Advanced Editions, the long-awaited “Dedicated…

medium.com](/@marketingcloudtips/marketing-cloud-next-shared-ip-addresses-and-dedicated-ip-addresses-5237675268e2?source=post_page-----24c0c804b0cb---------------------------------------)

### ③ Forward RMM Replies in HTML Format

The forwarding capability of **Reply Mail Management (RMM)** has been enhanced so you can now view customer replies in **HTML format**.

In other words, by reviewing the HTML content included in the reply email, company representatives can identify which original HTML email the response came from.

## Mobile Updates

> *Availability of Mobile App features may vary by country.*

### ① Connect Directly with Mobile App Users via In-App Messages

You can engage customers in real time while they use your mobile app and deliver in-app messages aligned with business goals.

**Basic message types**

- Banner
- Modal
- Full Screen

**Advanced message types**

- **Push Primer**: A message type that prompts customers to enable push notifications

You can configure frequency caps for message display in the setup screen.  
 Marketers can create in-app message content and incorporate it as flow elements.

### ② Capture Attention Immediately with Flash Notifications

You can boost mobile engagement and strengthen brand loyalty by sending time-sensitive flash messages in near real time.

Once enabled, marketers can create flash messages and use them as elements within flows.

### ③ Configure and Monitor Customer Actions in the Mobile App

You can define and track customer behaviors — such as button clicks, screen views, and purchases — as custom events within the mobile app.

These events are streamed in real time from the mobile app through the integrated Marketing Cloud SDK.

Collected data can be used for:

- Segmentation and advanced analytics in Data 360
- Building personalized customer journeys in Flow Builder

### ④ Enhance SMS Tracking with UTM Links

By creating and using UTM links, you can track SMS campaign performance and understand which SMS messages drove the most traffic and conversions.

When creating SMS messages, you can build personalized URLs that include standard UTM parameters as well as custom parameters.

This enhancement reduces errors caused by manual configuration and helps you improve SMS strategy based on data-driven decision-making.

### ⑤  Business Contact Information on WhatsApp

You can use contact messages to quickly share personal or organizational details on WhatsApp, enabling smoother follow-ups.

You can include information such as name, phone number, email address, physical address, job title, and organization name.

### ⑥ Send Limited-Time Offers on WhatsApp

You can deliver limited-time promotions and coupons directly to customers via WhatsApp.

This new interactive message template includes expiration settings, encouraging immediate action and helping drive revenue.

### ⑦ Make Conversations More Engaging with WhatsApp Stickers

By adding stickers, you can make WhatsApp session messages more fun and visually appealing.

Marketers create stickers in **WEBP** format, then upload them to Marketing Cloud Next Content Builder or a public hosting service to obtain a secure URL.

After sending, customers can also download or forward the sticker.

### ⑧ Optimize Marketing Message Delivery with MM Lite

You can enable **Marketing Messages Lite (MM Lite)** setup to maximize the effectiveness of WhatsApp marketing initiatives.

This optimization, provided by Meta, may improve delivery by up to 5% and help increase return on ad spend (ROAS).

### ⑨ Send Payment Options on WhatsApp (Brazil Only)

You can now send payment options to customers using WhatsApp payment message templates.

You can configure up to two payment methods, such as Pix, Boleto, or payment links. This message template is currently available only in Brazil.

## Closing

How did you find these updates?

There’s a lot to unpack, so catching up may feel challenging — but personally, most of these features were exactly what I expected. Once they’re released, I’d like to review them as much as possible within realistic limits.

That’s all for this time.

Stay tuned for more Salesforce Marketing Cloud tips! 😎

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
