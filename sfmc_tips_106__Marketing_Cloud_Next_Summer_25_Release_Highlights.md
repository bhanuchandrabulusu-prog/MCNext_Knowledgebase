# SFMC Tips #106 : Marketing Cloud Next: Summer ’25 Release Highlights

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-on-core-summer-25-release-highlights-4ad6f39c5d6d

---

# SFMC Tips #106 : Marketing Cloud Next: Summer ’25 Release Highlights

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--4ad6f39c5d6d---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--4ad6f39c5d6d---------------------------------------)

17 min read

·

Apr 25, 2025

--

Photo by [Spencer Everett](https://unsplash.com/@sp3v?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

Exciting updates for **Marketing Cloud Next** (Marketing Cloud Growth & Advanced Edition) have been unveiled. For the first time, I’m bringing you a release highlights article focused exclusively on Marketing Cloud Growth & Advanced Edition.

[## Help And Training Community

### Edit description

help.salesforce.com](https://help.salesforce.com/s/articleView?id=release-notes.rn_marketing.htm&release=256&type=5&source=post_page-----4ad6f39c5d6d---------------------------------------)

### About the Summer ’25 Release

The Summer ’25 release is scheduled to roll out to production environments in **mid-June 2025**. However, as of this article’s publication, the features have not been officially released yet. Please note that the information provided here is subject to change.

## Key Features to Watch

One of the most exciting features in the Summer ’25 release is Salesforce’s **Agentforce Campaign Designer**.

[## SFMC Tips #118 : Marketing Cloud on Core: Agentforce Campaign Designer

### Marketing Cloud on Core (Marketing Cloud Growth & Advanced Edition) includes the AI-powered campaign creation feature…

medium.com](/@marketingcloudtips/marketing-cloud-on-core-agentforce-campaign-designer-708c127992b1?source=post_page-----4ad6f39c5d6d---------------------------------------)

### Agentforce Campaign Designer

Previously, the **Agentforce Campaign Creation** tool utilized a conversational format for building campaigns. The new **Campaign Designer** introduces a dedicated wizard-style interface, enabling seamless progress from campaign briefing to content creation.

![]()

### The Potential of Repeater Components

The functionality of the Repeater Component is also noteworthy. It enables dynamic content display, similar to using AMPscript’s `LookupOrderedRows` in Marketing Cloud Engagement, but with a more intuitive UI.

[## SFMC Tips #134 : Marketing Cloud Next : Introducing the “Repeater” Component

### With the Summer ’25 release of Marketing Cloud Next (Marketing Cloud Growth & Advanced Edition), the Content Builder’s…

medium.com](/@marketingcloudtips/marketing-cloud-on-core-introducing-the-repeater-component-cc8017b01dc4?source=post_page-----4ad6f39c5d6d---------------------------------------)

Marketing Cloud Growth & Advanced Edition seems to be steering towards minimizing the need for advanced coding, and this new feature can be seen as part of that initiative.

Now, let’s take a closer look at the features that are part of the Summer ’25 release!

## Campaign

### ① Campaign Creation with Agentforce Campaign Designer

Previously, AI-powered campaign creation was limited to **Campaign Creation**, but with the introduction of the beta version of **Campaign Designer**, AI-driven campaign design has reached a new level of sophistication.

**Key Features of Campaign Designer:**

- **Improved User Experience with a Dedicated Wizard Interface**  
   Unlike the conversational approach of the traditional **Campaign Creation**, the new **Campaign Designer** offers a dedicated wizard-style interface. This enables users to smoothly navigate from campaign briefing to content creation in a streamlined flow.

![]()

- **Automated Campaign Design with AI**  
   Using minimal input, AI suggests campaign flows optimized for multi-channel use, including email, SMS, and WhatsApp. While these AI-generated flows and messages can be customized freely, providing flexibility to adapt to unique campaign needs.

![]()

**Steps to Finalize the Campaign:**

- Manually set up the schedule and add target segments.
- By default, there is a one-day wait time between message sends, which can be adjusted.

Note: This feature is exclusive to Marketing Cloud Advanced Edition.

[## SFMC Tips #118 : Marketing Cloud on Core: Agentforce Campaign Designer

### Marketing Cloud on Core (Marketing Cloud Growth & Advanced Edition) includes the AI-powered campaign creation feature…

medium.com](/@marketingcloudtips/marketing-cloud-on-core-agentforce-campaign-designer-708c127992b1?source=post_page-----4ad6f39c5d6d---------------------------------------)

### ② Build Campaign Flows from Scratch

Previously, campaign records were limited to pre-configured, template-based flows. However, with the introduction of the new **“Build Your Own”** tab, you can now create custom flows from scratch. This tab allows you to select a flow type — either **Segment Trigger** or **Event Trigger** — and design campaigns tailored to your ideas.

### ③ Enhanced Campaign Flow Management

Managing campaign flows has become even simpler, enabling you to continue building flows without transitioning to Flow Builder. If the flow contains five or fewer elements, you can directly add message elements or wait elements from the campaign screen. Additionally, settings like **Einstein Send Time Optimization (STO)** and tracking options (e.g., whether to track opens and clicks) can now be completed entirely within the campaign flow.

In practice, the supported features currently include sending messages and basic wait time elements. More complex features like branching logic or decision elements are not yet available. However, for simple scenarios, the process feels much more intuitive and straightforward compared to using Flow Builder. Looking forward to further enhancements in the future!

## Einstein

### ① Einstein Decision Element for Path Branching

A new AI-powered decision element, **Einstein Decision**, has been added to Flow Builder. This feature allows you to easily create branches utilizing two AI analytics: **Einstein Engagement Scoring** and **Einstein Engagement Frequency**.

For example, selecting **Persona Splits** in Einstein Engagement Scoring would look like this:

Unnecessary paths can be easily removed, so you don’t have to worry about irrelevant options.

Note: This feature is exclusive to Marketing Cloud Advanced Edition.

### ② Einstein STO Score Graph Enhancements

The **Einstein Send Time Optimization (STO)** data model has been updated to allow the creation of **data graphs**. By temporarily disabling and re-enabling STO in the setup, users can generate and leverage data graphs to collect, automate, and personalize email send time data effectively.

### ③ Retrieve Marketing Scores in Agentforce

A new action, **“Marketing Cloud: Get Score for Record ID,”** has been added to Agentforce.

With this feature, you can now interact with Agentforce to effortlessly retrieve **Overall Score**, **Engagement Score**, and **Fit Score** for Leads, Contacts, and Prospects whenever needed.

![]()

Check out the article below to see the step-by-step process for retrieving Marketing Scores.

[## Marketing Cloud Next : Retrieving Marketing Scores in Agentforce

### With the Summer ’25 new feature release for Marketing Cloud Next (Marketing Cloud Growth & Advanced Edition), a new…

medium.com](/@marketingcloudtips/marketing-cloud-next-retrieving-marketing-scores-in-agentforce-9eeb7acf3dfc?source=post_page-----4ad6f39c5d6d---------------------------------------)

### ④ Expanded Character Limit for Brand Identity

The character limit for the **Brand Identity** field has been expanded to **1,000 characters** (up from the previous 250). This allows organizations to detail their brand story, nuances, and unique qualities more effectively, providing richer and more comprehensive branding opportunities.

## Content

### ① Create Emails Using Custom HTML

You can now convert existing emails into HTML format and create highly customized responsive designs by fine-tuning the structure and stylesheets.

### Steps to Convert to HTML Format

**1. Click the “Code View” Toggle**  
At the top of the builder, click the **“Code View” toggle**. This will switch to the “Code View” tab, where the HTML code is displayed.

**2. Click “Convert to HTML”**  
Within the “**Code View**” tab, click the **“Convert to HTML” button**.

**3. Review Important Notes**  
When converting to HTML, keep the following points in mind:

- **Drag-and-drop functionality disabled**: Adding or editing components will no longer be possible.
- **Style adjustments disabled**: Design changes using the “Style” tab in the builder will no longer be available.
- **Dynamic content removed**: The following features will be disabled and removed from the email: Repeaters, Conditional Logic, and Content Variants.

[## SFMC Tips #119 : Marketing Cloud Next: Freedom in Design with HTML Code View

### In Marketing Cloud Next (Marketing Cloud Growth & Advanced Edition), email creation was previously limited to…

medium.com](/@marketingcloudtips/marketing-cloud-on-core-freedom-in-design-with-html-code-view-3673788cee5a?source=post_page-----4ad6f39c5d6d---------------------------------------)

### ② Enhanced “Data Source” Tab and Updated “Event Data”

The improved **Data Source** tab now allows marketers to easily view and manage the data sources used for personalization and merge fields at a glance.

Previously, updating an event source could break the email content, rendering it unusable. With this update, event data sources can now be seamlessly refreshed directly within the email.

However, as with the previous behavior, **once an email has been published, its data source can no longer be updated**.

**Pro Tips:**

1. Only one event data source can be used per piece of content.
2. If you select event data on the content, the same event must be used as the “Start” source in the event-triggered flow. If they do not match, you will encounter an error like the one below.

### ③ Consistent Layouts Using the Repeater Component

The new **“Repeat”** component allows you to dynamically display items with consistent designs using cards, lists, or custom layouts. By connecting the “Repeat” component to an available data source and utilizing merge fields, you can easily display details for each item, such as product names, descriptions, and images.

This new feature provides a more intuitive UI for dynamic displays, similar to what could previously be achieved with AMPscript’s `LookupOrderedRows`. It seems that Marketing Cloud Growth & Advanced Edition is steering towards a direction that reduces the need for advanced coding like AMPscript.

![]()

### Considerations

- If a repeater source doesn’t have data applicable to an email recipient, the repeater appears empty when that recipient opens the email in their inbox.
- There’s no limit to the number of items shown in a repeater, but too many items can increase the size of your entire email.

[## Help And Training Community

### Edit description

help.salesforce.com](https://help.salesforce.com/s/articleView?id=mktg.mktg_content_personalization_repeater.htm&type=5&source=post_page-----4ad6f39c5d6d---------------------------------------)

I have outlined the setup steps in the following article. Please use it as a reference.

[## SFMC Tips #134 : Marketing Cloud on Core: Introducing the “Repeater” Component

### With the Summer ’25 release of Marketing Cloud on Core (Marketing Cloud Growth & Advanced Edition), the Content…

medium.com](/@marketingcloudtips/marketing-cloud-on-core-introducing-the-repeater-component-cc8017b01dc4?source=post_page-----4ad6f39c5d6d---------------------------------------)

### ④ Static to Dynamic URLs for Image and Button Components

Previously, image component sources and button component actions could only accept static URLs. Now, you can input dynamic URLs, enabling greater flexibility and customization.

### ⑤ New Field Types for Forms

Additional field types have been introduced for form data source objects, enabling more flexible and accurate data collection tailored to specific data types.

By utilizing field types like “Date”, “Date/Time”, and “Number”, you can streamline the management of schedules and numerical data. Furthermore, the “Text Area” field includes an expanded input area, allowing you to adjust the field size through drag-and-drop operations.

## FLOW

### ① Addition of “Never” Option for Recurring Flows

The rejoin mode for Recurring Flows previously did not include the “Never” option, requiring custom adjustments for scenarios where you wanted contacts to enter the flow only once. However, the “Never” option has now been added alongside “Always” and “After Completion.” This brings it to the same level as Marketing Cloud Engagement.

![]()

[## SFMC Tips #139 : Marketing Cloud Next: Addition of “Never” Option for Recurring Flows

### As part of the Summer ’25 new feature release for Marketing Cloud Next (Marketing Cloud Growth & Advanced Edition), a…

medium.com](/@marketingcloudtips/marketing-cloud-next-addition-of-never-option-for-recurring-flows-54a38c91c733?source=post_page-----4ad6f39c5d6d---------------------------------------)

### **② Ability to Identify Flows Created Before Summer ‘25**

Flow types created prior to Summer ’25 are now marked with a `v0` suffix. This makes it possible to distinguish older flows.

### ③ Utilizing Segment Membership in Data Graph Triggers

Segment Membership (Unified Individual — Latest) is now available in Real-Time Data Graph Trigger Flows.

> ***Note:*** *Only* ***real-time segments*** *can be selected as event trigger conditions.  
> Standard segments are not displayed.*

With this update, you can now execute **triggered sends** to members who have joined **real-time segments** created from a real-time data graph.

[## SFMC Tips #179 : Marketing Cloud Next: Leveraging Real-Time Segments

### In Marketing Cloud Next (Marketing Cloud Growth & Advanced Edition), the Summer ’25 release introduces a new feature…

medium.com](/@marketingcloudtips/marketing-cloud-next-leveraging-real-time-segments-868c0f591205?source=post_page-----4ad6f39c5d6d---------------------------------------)

### **④ Triggering Flows Using Engagement Signals**

You can now create **custom event-triggered flows** by defining **Engagement Signals**. These flows are triggered when the conditions specified in your Engagement Signal are met.

Examples of Engagement Signals include **web clicks**, **email opens or replies**, and **PDF downloads**. These signals are built on DMO (Data Model Object) records within the **Engagement** category in **Data Cloud**, allowing for a wide range of event-triggering ideas.

**Considerations:**

- Under normal circumstances, you can define conditions using both fields from the selected Engagement DMO (primary DMO) and fields from related DMOs (secondary DMOs).  
   However, if you check the **“Use in Flow”** option, you’re limited to using only fields from the **primary DMO**.
- For event conditions, the only supported operator is **“equals”**, regardless of whether the field is of type **text** or **date**.

[## SFMC Tips #150 : Marketing Cloud Next: Custom Event-Triggered Flow

### In Marketing Cloud Next (Marketing Cloud Growth & Advanced Edition), you can now create custom event-triggered flows by…

medium.com](/@marketingcloudtips/marketing-cloud-next-custom-event-triggered-flow-7ae54b7798b5?source=post_page-----4ad6f39c5d6d---------------------------------------)

### **⑤ Access to the Toolbox in Flow Builder**

Marketing Cloud users can now access and create resources from the toolbox within Flow Builder.

![]()

### **⑥ Reference Records Created by the “Create Records” Element**

You can now directly reference records created by the “Create Records” element. For example, when a lead record is created upon form submission, you can reference the Salesforce ID of the created lead in the subsequent elements. This feature is available only for Salesforce object records.

### **⑦ Using the “Wait Until Event” Element in Event-Triggered Flows**

By adding the “Wait Until Event” element, you can pause an event-triggered automation flow until the customer performs a specified action. For example, you might have a flow that sends a thank-you email each time a customer submits a form. After that, you can use this element to pause the flow until the customer opens the email.

![]()

[## SFMC Tips #167 : Marketing Cloud Next: Wait Until Event in Form-Triggered Flows

### Starting with the Summer ’25 release, Marketing Cloud Next (Marketing Cloud Growth & Advanced Edition) allows you to…

medium.com](/@marketingcloudtips/marketing-cloud-next-waiting-for-events-in-form-triggered-flows-db08c98630cd?source=post_page-----4ad6f39c5d6d---------------------------------------)

### **⑧ Quickly Build Flows with Flow Scenario Templates**

As of Summer ’25, five flow scenario templates are available, enabling you to quickly build flows:

- Birthday promotion scenario
- Event registration scenario
- Lead nurturing campaign scenario
- Re-engagement scenario
- Form submission and follow-up scenario

To access the templates, create a new flow, and enter “marketing” in the search bar.

Below is an example of the “Re-engagement Scenario”.

**Note:** The generated emails are created in English.

## CRM Record Page

### ① Send Emails to Lead and Contact List Views

From the lead or contact list view, click **“Send List Email”**. Then, select the marketing email option and follow the on-screen instructions to create and send your content.

Previously, with Marketing Cloud Engagement, it was possible to send Marketing Cloud Engagement emails directly from the CRM using Marketing Cloud Connect. This new feature offers a similar user experience.

For those who are less familiar with **“Data Cloud segment creation”** or **“flow creation”**, this feature provides a simple way to send emails created in Marketing Cloud Growth & Advanced Edition with an easy-to-follow process.

Please refer to the setup steps below for more details.

[## SFMC Tips #136 : Marketing Cloud on Core: Marketing Cloud Sends Directly from CRM List Views

### Overview of the New Feature

medium.com](/@marketingcloudtips/marketing-cloud-on-core-marketing-cloud-sends-directly-from-crm-list-views-106cd7c2c465?source=post_page-----4ad6f39c5d6d---------------------------------------)

## Personalization

### ① Salesforce Personalization Recommendation Functionality

Salesforce Personalization is part of Marketing Cloud Next and is a Data Cloud–driven personalization tool, distinct from Marketing Cloud Personalization.

By connecting the Personalization Recommender — one of the features of Salesforce Personalization — to a repeater component, you can display a customized set of recommended products for each email recipient.

It allows you to recommend products or services tailored to your target audience.

By connecting recommendation data to a repeater component, you can display personalized product lists in emails for each recipient.

**Note:**

- This feature is available only in the **Advanced Edition**.
- To use Salesforce Personalization, **Personalization Decision Credits** are required.

[## Marketing Cloud Next: Repeater Component and Recommender

### In Marketing Cloud Next (Marketing Cloud Growth & Advanced Edition), you can take advantage of the Recommender feature…

medium.com](/@marketingcloudtips/marketing-cloud-next-repeater-component-and-recommender-fb41b9c72ad0?source=post_page-----4ad6f39c5d6d---------------------------------------)

## Consent Management

### ① Expanded Scope for Consent Request Elements

Previously, the “Consent Request” action was only available for event-triggered flows that included form submissions. However, it is now also supported in **Data Cloud-triggered flows** in addition to **other Event-triggered flows**.

This makes it possible to automate “Consent Creation” triggered by the creation or update of records.

[## SFMC Tips #142 : Marketing Cloud Next : Automating Consent Creation

### In the Summer ’25 new feature release for Marketing Cloud Next Growth & Advanced Editions, the “Create Consent”…

medium.com](/@marketingcloudtips/marketing-cloud-next-leveraging-custom-unsubscribe-links-78649b12da0e?source=post_page-----4ad6f39c5d6d---------------------------------------)

### ② Support for Country Codes in Consent Import Files

When importing consent data for SMS or WhatsApp, you can now include a column for the corresponding country code. This data type was not supported in import files previously.

*Note: This feature does not apply to email import templates.*

## Analytics

### ① Introduction of the “Deliverability” Tab

The newly added “Deliverability” tab in Marketing Performance is a powerful tool for marketers to analyze the factors driving campaign success or identifying challenges. With this dashboard, you can compare high-performing and low-performing campaigns, and dive deeper into specific metrics to uncover reasons for email delivery failures.

Additionally, by leveraging the integrated “Deliverability Dashboard” within each campaign record, you can gain a clear view of the delivery performance specific to each campaign, helping you plan more effective improvement strategies.

Navigate to the screen using the tab below:

Marketing Performance is a next-generation analytics tool powered by Tableau Next, as explained in the guide below:

[## SFMC Tips #115 : Marketing Cloud on Core: Transforming Campaign Insights with Marketing Performance

### With Marketing Cloud on Core (Marketing Cloud Growth & Advanced Editions), you can unlock two powerful analytics tools…

medium.com](/@marketingcloudtips/marketing-cloud-on-core-transforming-campaign-insights-with-marketing-performance-7c3f91f77304?source=post_page-----4ad6f39c5d6d---------------------------------------)

Since this feature leverages Tableau Next-based functionalities, only users with the following permission set can view the tab and access the screen:

- **“Tableau Next Included App Business User”** Permission Set

### ② Maximizing Content Effectiveness with the Performance Dashboard

You can now directly track the performance of emails, SMS, WhatsApp messages, tracking links, and landing pages from content records. This feature provides valuable insights into audience engagement and enables you to evaluate the effectiveness of “dynamic content” variations. Access this functionality via the tabs within the content record:

Since this feature leverages Tableau Next, the next-generation analytics tool powering Marketing Performance, only users with the following permission set can view the tab and access the screen:

- **“Tableau Next Included App Business User”** Permission Set

### ③ Creating Links to Track Traffic Sources to External Websites

The **Tracked Links** feature allows you to monitor visitor activity on external websites and identify which content led them to those sites. These tracked links are created in **CMS Content**.

![]()

### Notes on Using Tracked Links

- To protect the privacy of site visitors, obtain tracking consent via a **consent banner** on the external website.
- You can set up to **50 tracked links**.
- Marketing Cloud Landing Pages are **not** supported.
- The validity period of an issued tracked link URL is **5 years**.
- Linking the tracked link to a campaign is **mandatory**.
- If you make a tracked link private and then republish it, the **tracked link URL will change**.

[## SFMC Tips #159 : Marketing Cloud Next: Tracked Links for Website Traffic Sources

### In Marketing Cloud Next (Marketing Cloud Growth & Advanced Edition), the Tracked Links feature allows you to track…

medium.com](/@marketingcloudtips/marketing-cloud-next-tracked-links-for-website-traffic-sources-81593fde6581?source=post_page-----4ad6f39c5d6d---------------------------------------)

## Identity Resolution

### ① Add Salesforce Recommended Rules to the Identity Resolution Rule Set

To make the most of Identity Resolution, it is recommended to add the following two types of custom rules to your Unified Individual rule set:

**Type 1. Rule for Matching Records When a Lead Is Converted to a Contact**  
When a lead is converted to a contact, matching the original lead information with the resulting contact record using exact values can significantly improve the accuracy of identity resolution. A similar rule setup is also effective when converting a prospect.

[## SFMC Tips #155 : Marketing Cloud Next: Identity Resolution Using Identity Match DMO

### In Marketing Cloud Next (Marketing Cloud Growth & Advanced Edition), by adding Identity Match DMO as a “Match Rule” for…

medium.com](/@marketingcloudtips/marketing-cloud-next-identity-resolution-using-identity-match-dmo-d5c47b599d5e?source=post_page-----4ad6f39c5d6d---------------------------------------)

**Type 2. Rule for Accurately Associating Web Tracking Data with the Unified Individual**  
When using web tracking on Marketing Cloud landing pages or external connected sites, add a rule that ensures the collected activity data is properly linked to the correct Unified Individual. This enables consistent profile management that includes behavioral data from the web.

[## SFMC Tips #156 : Marketing Cloud Next: Leveraging Website Engagement

### With Marketing Cloud Next (Marketing Cloud Growth & Advanced Edition), you can track visitor activity and engagement on…

medium.com](/@marketingcloudtips/marketing-cloud-next-leveraging-website-engagement-0536c8e0e110?source=post_page-----4ad6f39c5d6d---------------------------------------)

## Setup

### ① Introduction of Dedicated Data Spaces for Marketing Cloud

With the Marketing Cloud Growth & Advanced Editions, you can now take advantage of dedicated data spaces to better isolate and manage your marketing data within Data Cloud. This enhancement improves data security, shortens data ingestion and processing times, and helps maintain higher data quality.

Previously, all marketing data was stored in a single, default data space. Starting with the Summer ’25 release, however, more flexible data management options are available through custom data spaces.

That said, the number of data spaces remains limited to one per Marketing Cloud Growth or Advanced Edition environment — just as before. Please note that a data space is not equivalent to a Business Unit.

If your Marketing Cloud Growth or Advanced Edition environment was provisioned before the Summer ’25 release, it will continue to use the default data space unless otherwise configured.

**Note:** Custom data spaces are a paid option and are not included with environments like SDO (demo-environments).

### ② Support for Identity Licenses

Marketing Cloud Growth & Advanced Edition now supports **Identity licenses**, allowing users without a full Salesforce license to access Marketing Cloud **at no additional cost** by assigning them a custom Identity profile for Marketing Cloud.

With this setup, users can access Marketing Cloud with **permissions equivalent to a Marketing Cloud Manager**. They will have full access to key features such as Campaigns, Segments, Flows, and shared Analytics Reports.

**Note:** You can create up to **100 Identity license users**, each assigned with an **Identity profile**, the **Marketing Cloud Manager** permission set, and the **Tableau Next Included App Business User** permission set.

[## SFMC Tips #162 : Marketing Cloud Next: Identity License Support Begins

### Starting with the Summer ’25 new release, Marketing Cloud Next (Marketing Cloud Growth & Advanced Edition) now allows…

medium.com](/@marketingcloudtips/marketing-cloud-next-identity-license-support-begins-3a1762e0d87b?source=post_page-----4ad6f39c5d6d---------------------------------------)

### ③ Attribute Library Navigation Enhancements

The Attribute Library used for segment building has been redesigned. This update introduces a more intuitive hierarchical structure with the target DMO at the top, smoother navigation back to the original DMO via breadcrumbs, and clearer distinctions between DMOs, Calculated Insights, and Attributes — along with other subtle improvements.

![]()

**Previous Attribute Navigation**

![]()

**Improved Attribute Navigation**

[## SFMC Tips #160 : Marketing Cloud Next: Attribute Library Navigation Enhancements

### In the Summer ’25 new feature release for Marketing Cloud Next (Data Cloud, Marketing Cloud Growth & Advanced Edition)…

medium.com](/@marketingcloudtips/marketing-cloud-next-attribute-library-navigation-enhancements-ed3235976679?source=post_page-----4ad6f39c5d6d---------------------------------------)

## Final Thoughts

This article marks my first attempt at writing about the new feature releases for Marketing Cloud Growth & Advanced Edition. Clearly, the highlight of this release is the **Campaign Designer**. With **Connections 2025** set to take place in Chicago on **June 11–12, 2025**, it’s highly likely that this feature will be prominently showcased during the event.

Personally, I’m particularly intrigued by the **Repeater Component**. Its user-friendliness and marketer-oriented design will be key points to watch.

Lastly, please note that this release is scheduled to be made available in **mid-June 2025**. At the time of publishing this article, these features have not yet been officially released.

That’s all for now.

Stay tuned for more Salesforce Marketing Cloud tips! 😊

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
