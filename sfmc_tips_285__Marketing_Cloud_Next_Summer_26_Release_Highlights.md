# SFMC Tips #285 : Marketing Cloud Next: Summer ’26 Release Highlights

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-next-summer-26-release-highlights-04f6c5abdee6

---

# SFMC Tips #285 : Marketing Cloud Next: Summer ’26 Release Highlights

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--04f6c5abdee6---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--04f6c5abdee6---------------------------------------)

25 min read

·

Apr 30, 2026

--

Photo by [Damian Barczak](https://unsplash.com/@barczakshoots?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

The new features release for **Marketing Cloud Next Growth & Advanced Edition Summer ’26** has been published.

- [Marketing Cloud Next related](https://help.salesforce.com/s/articleView?id=release-notes.rn_marketing.htm&release=262&type=5)
- [Marketing Flow related](https://help.salesforce.com/s/articleView?id=release-notes.rn_automate_flow_marketing_cloud.htm&language=en_US&type=5&release=262)

In this article, I will deliver the highlights.

## Notable New Features

This Summer ’26 release follows the previous Spring ’26 release and represents one of the largest update volumes. Many new features have been added, and among them, the introduction of **AMPscript** is particularly noteworthy.

In the Spring ’26 release, **Handlebars** was introduced, but for Marketing Cloud Engagement users, it had some aspects that were somewhat difficult to use. In that sense, this support for AMPscript feels like a very significant step forward for existing users.

In addition, the newly introduced **Marketing Objects** have the potential to be used as a data source for AMPscript as an alternative to data graphs, and there are high expectations for future developments.

Furthermore, the fact that these scripting capabilities can now be used not only in the code editor but also within the visual editor is an extremely valuable improvement in practical operations.

In the Spring ’26 release, foundational features such as business units and dedicated IP addresses were also established, and considering this release, it gives the impression that the reasons for choosing Marketing Cloud Next over Marketing Cloud Engagement are gradually becoming clearer. The range of what can be done has expanded significantly.

Now, let’s go through the contents of this release step by step.

For the highlights of the previous Spring ’26 release notes, please refer to the following.

[## SFMC Tips #218 : Marketing Cloud Next: Spring ’26 Release Highlights

### The Spring ’26 release of Marketing Cloud Next Growth & Advanced Edition has been announced. In this article, I’ll walk…

medium.com](/@marketingcloudtips/marketing-cloud-next-spring-26-release-highlights-24c0c804b0cb?source=post_page-----04f6c5abdee6---------------------------------------)

## Content & Landing Page

### ① Customize messages flexibly with AMPscript

You can now use **AMPscript code within messages in Marketing Cloud Next**. By utilizing AMPscript, you can retrieve recipient data from Marketing Objects and programmatically incorporate reusable content.

This feature also reduces the effort required when recreating content built in Marketing Cloud Engagement within Marketing Cloud Next.

*You can check the AMPscript functions available in Marketing Cloud Next on* [*this site*](https://developer.salesforce.com/docs/marketing/marketing-cloud-ampscript/references/mc-ampscript-references/mc-ampscript-references-index.html)*.*

[## SFMC Tips #280 : Marketing Cloud Next: Customize messages flexibly with AMPscript

### One of the biggest topics in the Summer ’26 new feature release for Marketing Cloud Next Growth & Advanced Editions is…

medium.com](/@marketingcloudtips/marketing-cloud-next-summer-26-ampscript-support-has-arrived-18272b5f6a1e?source=post_page-----04f6c5abdee6---------------------------------------)

### ② Store marketing data in Marketing Objects

Marketing Objects is a data store that enables handling marketing data with **high throughput and low latency**. By importing CSV files, data from external systems can be brought into Marketing Objects. Marketers can read and process data within Marketing Objects using Handlebars or AMPscript and utilize it for personalization.

[## SFMC Tips #313 : Marketing Cloud Next: How to Configure Marketing Objects

### Marketing Objects, introduced in the Marketing Cloud Next Growth & Advanced Editions Summer ’26 release, are containers…

medium.com](/@marketingcloudtips/marketing-cloud-next-how-to-configure-marketing-objects-ec7213fda266?source=post_page-----04f6c5abdee6---------------------------------------)

### ③ Improve script development efficiency within the visual editor

Without switching to the code editor, AMPscript and Handlebars can now be used within the traditional visual editor. In addition, syntax validation functionality has been added, allowing HTML, Handlebars, and AMPscript to be freely combined.

If there are errors in the code, the relevant sections are automatically highlighted, and hints for correction are provided, enabling efficient content creation while maintaining quality.

### ④ Prepare a plain text version of emails

We can now create and add a plain-text version of email messages to help increase engagement and ensure delivery across all viewing formats, including secure email clients and screen readers.

- Secure email clients  
   → Block HTML → Display text version
- Screen readers  
   → Text may be easier to read aloud
- All display formats  
   → The optimal format (HTML or text) is selected depending on the environment

To edit the message body, open the email in the editor and select the **“Plain Text” view**.

*For existing published HTML emails, the plain-text version is automatically populated with text content and link URLs extracted from the HTML email.*

### ⑤ Dynamic From Addresses and Reply-To Addresses

To increase customer engagement and strengthen customer relationships, send marketing emails from trusted senders. Salesforce contact and account data can now be dynamically added to the From Address and Reply-To Address, allowing emails to appear as if they were sent directly from the account owner or sales representative, instead of from a generic address such as do-not-reply@. When customers reply, those responses are delivered directly to the appropriate representative.

Procedure: In the setup screen, select “**Authorized Email Domains**” under “**Unified Messaging**”. Then, add and verify the email domain that will be used for dynamic addresses.

Once domain verification is complete, marketers can use “**merge fields**” to dynamically configure the From Address and Reply-To Address when creating campaigns.

![]()

[## SFMC Tips #304 : Marketing Cloud Next: Dynamic From Address and Reply Address

### In Marketing Cloud Next Growth & Advanced Editions, it is mandatory to use email addresses from DKIM-authenticated…

medium.com](/@marketingcloudtips/marketing-cloud-next-dynamic-from-address-and-reply-address-ca084748f1e2?source=post_page-----04f6c5abdee6---------------------------------------)

### ⑥ Personalize emails with a new data provider

To personalize emails using the latest business data, merge fields based on two new data sources — **“Salesforce objects”** and **“Content variables”** — can be added to messages.

[## SFMC Tips #306 : Marketing Cloud Next: Salesforce Record Data Provider

### The Summer ’26 release for Marketing Cloud Next Growth & Advanced Editions introduced merge fields that can use a new…

medium.com](/@marketingcloudtips/marketing-cloud-next-salesforce-record-data-provider-df07d9206206?source=post_page-----04f6c5abdee6---------------------------------------)

[## SFMC Tips #290 : Marketing Cloud Next: Personalization with Content Variables

### In the Summer ’26 new feature release for Marketing Cloud Next Growth & Advanced Editions, it became possible to add…

medium.com](/@marketingcloudtips/marketing-cloud-next-personalization-with-content-variables-18ebb6764911?source=post_page-----04f6c5abdee6---------------------------------------)

### ⑦ Embed personalized offers into emails

By embedding offers (such as coupon codes) directly into email content, promotional distribution can be streamlined and manual errors reduced.

In the email builder, offers can be added as a data source, and information such as offer name, description, and coupon code can be automatically inserted using merge fields.

Furthermore, by setting dynamic content rules based on attributes such as loyalty rank, it becomes possible to deliver the most suitable offer to each recipient, enabling more personalized communication.

### ⑧ Expand multilingual campaigns with content variations

With new language support for content variants, various content blocks such as emails, images, headers, footers, and promotional sections can now be flexibly localized.

Since translations can be centrally managed within a single email or content block, global campaign operations are greatly simplified.

Additionally, without duplicating campaigns, optimal content based on each recipient’s language settings can be delivered, enabling a more personalized customer experience while reducing operational burden.

[## SFMC Tips #307 : Marketing Cloud Next: Multilingual Support with Content Variations

### The Summer ’26 release for Marketing Cloud Next Growth & Advanced Editions introduced language support through Content…

medium.com](/@marketingcloudtips/marketing-cloud-next-multilingual-support-with-content-variations-175963c1fb97?source=post_page-----04f6c5abdee6---------------------------------------)

### ⑨ Enable CC in marketing emails

To allow business communications to be shared among all relevant parties, email addresses both inside and outside the organization can now be added as CC (carbon copy).

To use the CC feature, enable the CC field in the **Unified Messaging settings page**.

Up to **10 email addresses** can be added per email send.

[## SFMC Tips #303 : Marketing Cloud Next: How to Configure the CC Email Feature

### The Summer ’26 release for Marketing Cloud Next Growth & Advanced Editions introduced the CC (Carbon Copy) feature for…

medium.com](/@marketingcloudtips/marketing-cloud-next-how-to-configure-the-cc-email-feature-7f9fb279aa97?source=post_page-----04f6c5abdee6---------------------------------------)

### ⑩ Preserve Sent Emails with the New Email Archiving Feature

To support regulatory compliance, auditing requirements, and corporate governance policies, Salesforce has introduced **Email Archiving**, a feature that automatically stores copies of sent emails.

With this capability, organizations can now retain an audit trail of emails sent through Marketing Cloud Next directly within Salesforce. This makes the platform more suitable for industries with strict compliance requirements, such as financial services and healthcare.

Archived emails are stored in Salesforce’s standard **Email Message** object.

However, retaining large volumes of emails over an extended period can consume Salesforce storage. To export and manage archived email data efficiently, organizations should use the **Salesforce Archive App**.

If you are interested in using the Archive App, please contact your Salesforce Account Executive for more information.

**Important Considerations for Custom Fields**

If you have added custom fields to the **Email Message** object, special attention is required.

The Email Archiving feature does not function correctly if a custom field has the setting **“Always require a value in this field in order to save a record”** enabled.

Before enabling Email Archiving, verify that no custom fields on the Email Message object are configured as required fields.

**How to Enable Email Archiving**

1. Open **Setup** → **Email Archiving**.
2. Enable **Email Archiving**.
3. Configure whether individual users can control archiving settings for their own email sends.

Once Email Archiving is enabled, the **Archive Email** option in the **Send Email Message** flow element is enabled by default.

If administrators allow users to control archiving behavior, marketers can disable archiving for specific email sends. However, any email sent with archiving disabled cannot be archived retroactively.

**Limitations and Considerations**

Before using Email Archiving, be aware of the following limitations:

- Up to **100,000 emails per day** can be archived.
- Emails larger than **131 KB** are truncated before being stored.
- Email attachments are not supported.
- The HTML email body is archived, but attachment information is not stored in the Email Message object.

In particular, because attachments themselves are not retained, organizations that must preserve documents such as contracts, invoices, or other files for audit purposes should implement a separate attachment retention strategy.

[## Salesforce Help

### Edit description

help.salesforce.com](https://help.salesforce.com/s/articleView?language=en_US&id=mktg.um_channel_email_set_up_archiving.htm&type=5&source=post_page-----04f6c5abdee6---------------------------------------)

### ⑪ Achieve a consistent brand experience with custom fonts

By adding custom web fonts to the content builder, marketers can select fonts best suited to their brand when creating emails, landing pages, forms, and templates. Additionally, by defining fallback fonts in advance, readability can be ensured even in environments where custom fonts cannot be loaded.

![]()

Furthermore, by assigning web-hosted fonts to each business unit, brand consistency can be maintained across all content, providing a recognizable experience for users.

### ⑫ Personalization of landing page templates

For landing page templates, it is now possible to preconfigure rule-based dynamic content and merge fields across objects, significantly improving the reusability and scalability of web content.

In addition, new personalization settings in the content editor enable variations to be synchronized across multiple components, including locked components.

With this update, campaign-ready pages with built-in brand data logic can be published quickly, and incorrect edits to personalization rules can also be prevented.

***Note:*** *This may not be available in organizations created before Spring ’25 or in partner demo organizations (SDO). This will be verified after release.*

### ⑬ Customize consent banners for web tracking

It is now possible to create custom banners in Content Builder for obtaining consent related to web tracking (permission to collect and use users’ behavioral data).

![]()

This allows you to flexibly control the design and text based on your use case. In addition, button text — which previously could not be changed — can now also be customized.

[## SFMC Tips #295 : Marketing Cloud Next: Create Custom Web Tracking Consent Banners

### In the Summer ’26 new feature release for Marketing Cloud Next Growth & Advanced Editions, it is now possible to create…

medium.com](/@marketingcloudtips/marketing-cloud-next-create-custom-web-tracking-consent-banners-27de46f86e0b?source=post_page-----04f6c5abdee6---------------------------------------)

## Campaign

### ① The default for campaign flows has changed

When creating a new campaign or creating a flow for an existing campaign, the process has changed so that you start from the **“Build Your Own”** tab.

![]()

From here, you can configure campaign flow triggers and refer to flow templates, allowing you to build more flexibly.

Also, by using the **“Quick Start”** tab, you can still start campaigns immediately based on preconfigured flows as before, enabling efficient launches according to the use case.

### ② Create campaigns faster with flow templates

To help marketers build flows more quickly, it is now possible to directly access the flow template library from campaigns.

※ It can be selected from the **“Build Your Own”** tab.

Each template includes prebuilt flow elements that correspond to typical marketing use cases, reducing the effort of designing from scratch and allowing you to start building smoothly.

In addition, newly created flows are automatically associated with the campaign, reducing setup effort while enabling consistent campaign management.

### ③ Strengthen campaign collaboration with Slack channels

By using Slack channels, you can smoothly advance collaboration in campaign management while improving team productivity.

When a campaign is added from the campaign tab, the corresponding Slack channel is automatically created or linked to an existing channel, functioning as a hub that aggregates discussions and the latest information.

Important campaign-related information is organized and displayed in this dedicated channel, making it easier for all stakeholders to understand the situation. Furthermore, AI-based task automation reduces communication effort and enables more efficient campaign operations.

[## SFMC Tips #317 : Marketing Cloud Next: How to Integrate Campaigns with Slack

### The Summer ’26 release for Marketing Cloud Next Growth & Advanced Editions introduces integration with Slack channels…

medium.com](/@marketingcloudtips/marketing-cloud-next-how-to-integrate-campaigns-with-slack-082b5b628342?source=post_page-----04f6c5abdee6---------------------------------------)

## Flow

### ① Sending to audiences is unified into Audience Flows

Flows based on audience data can now be created from a simplified and unified **“Audience Flow”.** Depending on the use case, you can select data sources such as lists, segments, records, and campaigns.

Marketers create audience-based flows using various data sources, but by consolidating them into a dedicated category called **“Audience Flow”,** creating and managing flows becomes simpler.

### ② Extend personalization with low-code, without Apex

Without writing Apex, you can now extend personalization options for email messages by mapping Content Builder content variables to flow merge fields.

When email content is created using custom resources such as manually configured variables or record data providers, those fields appear as dynamic input fields within the flow’s message action.

This low-code approach allows marketers to control personalization using customer data more flexibly and independently.

[## SFMC Tips #290 : Marketing Cloud Next: Personalization with Content Variables

### In the Summer ’26 new feature release for Marketing Cloud Next Growth & Advanced Editions, it became possible to add…

medium.com](/@marketingcloudtips/marketing-cloud-next-personalization-with-content-variables-18ebb6764911?source=post_page-----04f6c5abdee6---------------------------------------)

### ③ Enhance flow personalization using source data

Data retrieved from data sources can now be narrowed down by **sorting** and **filtering** from the Resource Manager or resource selection fields and used as a **selected record resource**.

![]()

By using this resource, you can access nested information from various data sources, including data graphs, greatly expanding the range of flow personalization.

This allows marketers and administrators to directly use detailed, nested data within data sources without relying on activation or custom code.

[## SFMC Tips #293 : Marketing Cloud Next : Retrieving a Specific Record from a Data Graph in…

### With the Summer ’26 new feature release for Marketing Cloud Next Growth & Advanced Editions, source data such as Data…

medium.com](/@marketingcloudtips/marketing-cloud-next-retrieving-a-specific-record-from-a-data-graph-in-marketing-flows-e03c87cea117?source=post_page-----04f6c5abdee6---------------------------------------)

### ④ Enhance condition settings and re-entry control in event-triggered flows

In Event Triggered Flows, it is now possible to use fields from the primary DMO to configure more detailed trigger conditions. To configure trigger conditions, select **“Add Condition”** in the **“Additional Criteria”** section of the Start element.

In addition, by defining re-entry conditions, it is now possible to flexibly control whether the same user can re-enter the flow.

The following types of control are available:

- **Always**: Allow re-entry every time the event occurs
- **After completion**: Allow re-entry only after the flow is completed
- **Never**: Execute only once (re-entry not allowed)

### ⑤ Expanded Use Cases for Event Triggered Flows

In Event Triggered Flows, it is now possible to specify contact points such as SMS and WhatsApp.

In addition, when creating Engagement Signals, Profile DMOs can now also be selected in addition to traditional Engagement DMOs, allowing customer data to be configured in signal definitions and conditions with up to 10 fields.

As a result, it is now possible to implement advanced controls such as triggering a flow when a brochure request PDF is downloaded, then referencing the customer’s Title and triggering emails only for people with specific job titles.

[## SFMC Tips #150 : Marketing Cloud Next: Custom Event-Triggered Flow

### In Marketing Cloud Next (Marketing Cloud Growth & Advanced Edition), with the Summer ’25 new feature release, you can…

medium.com](/@marketingcloudtips/marketing-cloud-next-custom-event-triggered-flow-7ae54b7798b5?source=post_page-----04f6c5abdee6---------------------------------------)

### ⑥ Automate Engagement with Behavioral Triggers

New marketing triggers designed around key customer behaviors and events now make it possible to approach customers at the optimal timing. By easily configuring these triggers, personalized messages can be automatically delivered across multiple channels according to important touchpoints in the customer journey.

*This feature is considered to be the Marketing Cloud Next version of* ***Behavioral Triggers*** *in Marketing Cloud Engagement.*

Available triggers include the following order lifecycle events:

- 1️⃣ Abandoned Shopping Cart
- 2️⃣ Abandoned Product Browse
- 3️⃣ Abandoned Page
- 4️⃣ Product Price Drop
- 5️⃣ Product Low Inventory
- 6️⃣ Product Back In Stock

These order lifecycle-related triggers enable timely communication aligned with customer behavior.

For details on how to configure each trigger, please refer to the help documentation.

[## Salesforce Help

### Edit description

help.salesforce.com](https://help.salesforce.com/s/articleView?id=mktg.mktg_admin_set_up_retail_triggers.htm&type=5&source=post_page-----04f6c5abdee6---------------------------------------)

### ⑦ Build More Sophisticated Logic with Decision Elements and Exit Rules

**Decision Elements** and **Exit Rules** now support aggregate functions for numeric data contained in Related Attributes, such as data retrieved from Data Graphs.

The following aggregate functions are now available:

- Average
- Sum
- Max
- Min

Previously, only simple conditions such as “record count is greater than or equal to 1 (Count >= 1)” could be configured.

In addition, date-based conditions have been significantly enhanced. Twenty new operators are now available for Date fields, including options such as “Is Anniversary of Today”, “Is Today”, and “Last Number of Days”.

New Date Operators:

- Is Anniversary of Today
- Is Not Anniversary of Today
- Is Today
- Is Tomorrow
- Is Yesterday
- Is This Month
- Is Next Month
- Is Last Month
- This Year
- Next Year
- Last Year
- Is On
- Is Before
- Is After
- Greater Than Last Number of Days
- Last Number of Days
- Next Number of Days
- Last Number of Months
- Next Number of Months
- Last Number of Years

*Note: Datetime fields continue to support the same eight operators that were previously available.*

*Previously, it was difficult to create flexible conditions based on numeric or date values contained in Related Attributes. As a result, implementing complex decision logic often required data preparation or segment creation in advance.*

*With this enhancement, you can now evaluate conditions directly within a flow, such as:*

- *Customers whose* ***average purchase amount is greater than or equal to $100 and who have not made a purchase in the last 14 days***
- *Customers whose* ***last purchase date falls on the same anniversary date as today***

*This enables more advanced and precise audience orchestration than ever before.*

### ⑧ Use Standard Events and Custom Events as Exit Rules

Previously, audiences could only exit a flow through Exit Rules based on Data Graph or Calculated Insight data conditions. With this enhancement, **standard events** and **custom events** can now be used as exit criteria.

![]()

![]()

For example, you can now configure:

- A **standard event**, such as exiting the flow when a customer opens a specific email
- A **custom event**, such as exiting the flow when an engagement signal is received

This allows audiences to leave a flow based on customer behavior and real-time events, providing greater flexibility and more accurate timing for audience management.

[## SFMC Tips #287 : Marketing Cloud Next: Behavior of Exit Rules

### In this article, I summarize the behavior of Exit Rules in Marketing Cloud Next Growth & Advanced Edition.

medium.com](/@marketingcloudtips/marketing-cloud-next-behavior-of-exit-criteria-7f55f708ecea?source=post_page-----04f6c5abdee6---------------------------------------)

### ⑨ Automatically exclude audiences from active flows

By using the newly added **“Exit from a Flow”** element, you can now automatically stop unnecessary communications for audiences who meet specific conditions or goals.

![]()

Until now, excluding audiences required manual handling or complex custom logic, but it can now be controlled more simply and flexibly. In addition, you can choose whether to exclude them from all versions of the target flow or only from the latest version.

[## SFMC Tips #297 : Marketing Cloud Next : How to Use the “Exit from a Flow” Element

### In the Summer ’26 new feature release of Marketing Cloud Next Growth & Advanced Editions, it is now possible to…

medium.com](/@marketingcloudtips/marketing-cloud-next-how-to-use-the-exit-from-a-flow-element-6398bef93977?source=post_page-----04f6c5abdee6---------------------------------------)

### ⑩ Enable advanced journey design across multiple flows

It is now possible to seamlessly guide customers to another flow while maintaining their progress. By using the newly added **“Send to a Flow”** element, you can build more advanced and flexible customer journeys that connect multiple flows.

This element passes customer identifiers to the destination flow, and the original flow and destination flow run asynchronously in parallel. Therefore, while continuing the original flow, processing can also proceed simultaneously in another flow. Until now, linking multiple flows required complex custom logic or API integration, but it can now be achieved more simply.

*It is available to users with the* ***“Send to a Flow”*** *permission. This permission is enabled by default.*

### ⑪ Unify elements and functionality across all marketing-related flows

Regardless of the type of marketing flow, the available elements and functionality have been unified. This allows key flow elements such as **Wait** and **Decision** to be used consistently across all marketing flow types.

With this unification, migrating between flows and making design changes becomes smoother, and flows can be built and operated flexibly without needing to be aware of element compatibility or functional limitations.

### ⑫ Review and restore flow version edit history

You can now review the save history of flow versions and easily return to a previous state. Each time a flow is saved, a history is recorded, and you can view a list of the save date and time, the executing user, and a summary of elements that were added, changed, or deleted.

By using edit history, you can roll back to a previous state without creating a new version, helping support audits and compliance, and enabling a safe improvement cycle.

- When a flow is saved, the state at that point is recorded as history. If there are unsaved changes, save them before opening the history.
- When you open the **“Flow Edit History”** panel, a list of save history is displayed, and you can select any save point to preview its contents. To restore, select the target and click **“Restore”.**

[## SFMC Tips #294 : Marketing Cloud Next : Flow Save History Can Now Be Reviewed and Restored

### In the Summer ’26 new feature release for Marketing Cloud Next Growth & Advanced Editions, a new feature was added that…

medium.com](/@marketingcloudtips/marketing-cloud-next-flow-save-history-can-now-be-reviewed-and-restored-109e00034ac9?source=post_page-----04f6c5abdee6---------------------------------------)

### ⑬ Automate LinkedIn operations in connection with Campaign

It is now possible to publish posts to a specific LinkedIn account either immediately or on a scheduled basis. This allows marketers to publish content directly from Marketing Cloud Next to a connected LinkedIn account.

By incorporating LinkedIn posts as part of a campaign, it becomes possible to manage activities consistently across the entire initiative.

As a result, engagement for individual posts and overall campaign performance can be monitored in a centralized manner, making it easier to drive data-driven improvements and optimization.

[## SFMC Tips #310 : Marketing Cloud Next: LinkedIn Posting from Campaigns

### With the Summer ’26 new feature release for Marketing Cloud Next Growth & Advanced Editions, it is now possible to…

medium.com](/@marketingcloudtips/marketing-cloud-next-linkedin-posting-from-campaigns-61e043fe8a88?source=post_page-----04f6c5abdee6---------------------------------------)

### ⑭ General users can now check flow dependencies

In the Automation app, users without administrator permissions can now check the dependencies of their own marketing flows.

Until now, only users with the **“Manage Flow”** permission could view them, but more users can now understand flow structures and related elements, improving operational visibility and efficiency.

## Audience

### ① Create lead acquisition campaigns from flow templates

Until now, when creating lead acquisition campaigns that include signup forms, it was necessary to select **“Signup Form”** from the **“Quick Start”** tab of the campaign flow, and configure each step individually in the order of signup form → flow → landing page.

This time, by becoming able to start from flow templates, the effort and complexity of building this series of settings one by one has been eliminated, making it possible to create lead acquisition campaigns more simply and smoothly.

[## SFMC Tips #298 : Marketing Cloud Next: Creating a Signup Form (Simplified Version)

### In the Summer ’26 feature release for Marketing Cloud Next Growth & Advanced Editions, several improvements were added…

medium.com](/@marketingcloudtips/marketing-cloud-next-creating-a-signup-form-simplified-version-43e797302478?source=post_page-----04f6c5abdee6---------------------------------------)

### ② Create actionable lists that can be easily sent to

When **“who you want to send to”** is clear, complex condition settings using Data 360 segments are unnecessary. By using actionable lists, you can deliver campaigns precisely to specific leads or contacts.

Lists can be easily created by importing CSV files or manually adding members. For example, you can create a list of leads based on signup information acquired at a trade show and send welcome emails or promotions to that list.

[## SFMC Tips #305 : Marketing Cloud Next: Actionable List Flow

### With the Summer ’26 release for Marketing Cloud Next Growth & Advanced Editions, the entry point previously known as…

medium.com](/@marketingcloudtips/marketing-cloud-next-actionable-list-flows-42b6a0fcc277?source=post_page-----04f6c5abdee6---------------------------------------)

## Agentforce

### ① Redeploy agents with the new Agentforce Builder

The templates for the **Campaign Creation Agent** and **Journey Decision Agent** are now available in the **new Agentforce Builder**, where agents can be built using Agent Script. This makes it possible to design and build agents more flexibly and efficiently.

Existing agents are not automatically migrated to the new Agent Builder, so administrators must redeploy them. Until migration is complete, existing agents can continue to be used, but considering future extensibility and operability, migration to the new Agentforce Builder is recommended.

[## SFMC Tips #117 : Marketing Cloud Next: Campaign Creation Agent

### In Marketing Cloud Next Growth & Advanced Editions, you can use the Campaign Creation Agent, which leverages generative…

medium.com](/@marketingcloudtips/marketing-cloud-on-core-agentforce-campaign-creation-697c992adbe6?source=post_page-----04f6c5abdee6---------------------------------------)

### ② Optimize customer experiences with Agentforce Journey Decisioning

By providing contextual information to the Journey Decision Agent, it can now make decisions based on real-time behavioral data and profile data, and dynamically select the optimal campaign flow.

This enables flexible communication based on the customer’s status and timing, rather than a uniform scenario, leading to maximized results.

### **③ Identify Buying Groups with the Account Discovery Agent**

The Account Discovery Agent helps marketing and sales teams focus on opportunities with the highest purchase intent. It identifies buying groups within existing accounts, provides insights into the engagement of key contacts, and summarizes the overall status and trends of the account.

![]()

To make the Account Discovery Agent available to your team, deploy it using the new agent template provided in Agentforce Builder.

[## SFMC Tips #320 : Marketing Cloud Next: Account Discovery Agent

### The Summer ’26 release for Marketing Cloud Next Growth & Advanced Editions introduces a new Agentforce template: the…

medium.com](/@marketingcloudtips/marketing-cloud-next-account-discovery-agent-78150805119d?source=post_page-----04f6c5abdee6---------------------------------------)

## Distributed Marketing

### ① Visualize engagement while maintaining compliance

When operating Distributed Marketing & Alerts, images and phrases that can be used in email templates can now be approved and managed in advance, enabling operations while maintaining brand guidelines and compliance.

By configuring send-on-behalf-of permissions for specific users, controlled communication across the organization can also be achieved. In addition, sales users can preview default merge field values in advance, and through the new **“Distributed Sends”** dashboard, they can centrally understand the results of 1-to-1 emails and mass sends.

### ② Enhance insights for Distributed Marketing messages

With the newly added Distributed Marketing Agent, sales users can gain insights based on engagement data while using email templates approved by the marketing department.

Furthermore, by using prebuilt flows and campaigns, messages can be delivered efficiently while flexibly personalizing templates.

## Mobile

### ① Strengthen brand recognition with virtual contact cards

By creating and sending **Virtual Contact Cards** as MMS messages on the spot, subscribers can easily save contact information to their mobile devices. This enables smooth establishment of customer touchpoints.

Once the contact card is saved, the brand name and logo are displayed in all subsequent communications, promoting continuous brand recall and improving recognition.

*Sending MMS messages is supported only in the United States and Canada.*

### ② Strengthen expression with personalized MMS messages

By combining not only text, but also images, GIFs, videos, personalized contact cards, and more, you can create more visual and compelling messages. This can attract recipients’ attention and improve engagement.

*Sending MMS messages is supported only in the United States and Canada.*

### ③ Visualize conversions from Meta Click-to-WhatsApp ads

WhatsApp conversations generated through Meta’s **“Click-to-WhatsApp”** ads can now be automatically tracked and linked, allowing conversions to be accurately understood. Referral data is connected to Data 360, making it possible to visualize the effectiveness of ad investment and optimize marketing based on data.

### ④ Send payment options on WhatsApp, for India

By sending payment options directly within WhatsApp chats, you can shorten the path to purchase and improve conversion rates. As payment methods, **UPI Intent** or payment links can be configured.

*This message template is currently available only in India.*

### ⑤ Strengthen messaging with Rich Communication Services

By incorporating **Rich Communication Services (RCS)** into multichannel marketing, you can provide interactive mobile experiences that reflect the brand’s worldview. Once RCS setup and sender ID authentication are complete, marketers can use the RCS message content type in Salesforce CMS to create highly engaging messages that combine text with media such as images and videos, rich cards, and interactive suggestions.

*※ RCS messages can be delivered to customers in the United States, United Kingdom, Mexico, Brazil, Germany, and France.*

RCS (Rich Communication Services) is a messaging standard that extends traditional SMS and enables experiences close to LINE or WhatsApp within the “standard messaging app”, such as:

- Sending images and videos
- Messages with buttons, such as reservations or purchases
- Carousels, or horizontally scrollable cards
- Read receipts
- Brand authentication, such as company name and logo display

## Analytics

### ① Retain Send Log Data in Marketing Flows

The **Send Marketing Cloud Engagement Email** element now supports Send Logging and includes the **Retain Send Log Data** option.

This enhancement allows organizations to retain send log data even when emails are sent from Marketing Cloud Next flows, making it easier to use send logs for reporting, auditing, and troubleshooting purposes.

![]()

[## SFMC Tips #268 : Marketing Cloud Next: Send Marketing Cloud Engagement Emails from a Flow

### With the Spring ’26 new feature release of Marketing Cloud Next Growth & Advanced Edition, accounts using Marketing…

medium.com](/@marketingcloudtips/marketing-cloud-next-send-marketing-cloud-engagement-emails-from-a-flow-450b1173ace2?source=post_page-----04f6c5abdee6---------------------------------------)

### ② Filter flow element analytics by date range

Flow element analytics data can now be filtered by a specified date range. Metrics for each element are updated according to the selected period, making it easier to analyze recent performance, compare periods, and evaluate according to campaign periods.

The introduction of date filters reduces the effort required to open detailed screens for each element or export data, enabling more efficient analysis.

### ③ Visualize outcome metrics for path experiments

You can now check outcome metrics for each path experiment element on the analytics dashboard. By comparing the performance of each path, you can select the optimal path, or winning pattern, with more appropriate judgment.

By visualizing outcomes for each path, it becomes easier to understand experiment results, enabling data-based decision-making both during and after execution.

Steps: Open a flow that contains a path experiment element, either already run or active. Display the analytics dashboard from the **“Analytics”** tab and click **“Open Details”.** In the displayed **“Outcome”** column, you can check the outcome for each path.

### ④ Visualize marketing engagement on opportunity records

You can now directly check from the opportunity record how contacts related to an opportunity are responding to marketing initiatives such as emails, forms, and web pages. Sales representatives can use the **“Unified Engagement History”** dashboard to visually understand various engagement data and connect it to more effective approaches.

## Business Unit

### ① Manage marketing operations scalably

With the Summer ’26 update, marketing administrators can operate flexibly according to business growth and efficiently share content across business units.

The main enhancements are as follows:

- Create up to 150 business units
- Support deactivation of business units that are no longer needed
- Assign web custom fonts by business unit
- **Publish content to a shared asset library, allowing other business units to copy it into their own workspace**

This makes it possible to greatly improve content utilization and operational efficiency across the organization while maintaining brand consistency.

*※ Business unit functionality is available only in Marketing Cloud Advanced Edition.*

## Setup

### ① Simplify discovery and setup of next-generation features

From the centralized Salesforce Go screen, you can now easily discover, set up, and configure Marketing Cloud Next features. First, by using the **“Initial Setup”** card, you can smoothly proceed with foundational setup such as installing Marketing Cloud Next and configuring data streams.

In addition, feature cards prepared for each marketing channel allow you to proceed with setup while checking guided setup steps, and progress is also visualized.

### ② Easily configure Slack and RCS from Assistant Home

From **Setup > “Assistant Home”,** you can now directly access Slack and Rich Communication Services (RCS) settings.

- Connect Slack with marketing campaigns and centralize collaboration within the team
- Configure RCS to provide rich messaging to mobile-first users

This enables faster and more efficient setup and use of key channels.

## Marketing Cloud Engagement+

### ① Use SMS codes from the Engagement side in Next

US and Canadian SMS short codes and long codes from Marketing Cloud Engagement can now be used in Marketing Cloud Next.

Because there is no longer a need to reacquire codes, you can unify your messaging strategy and manage outbound and inbound traffic for both Journey Builder and Flow Builder from a single code.

Configuration Method: From the Marketing Cloud Next setup, navigate to Marketing Cloud Engagement > **Connect Data**, and share the code from the following management screen.

### ② Map consent between MCE and MCN

Consent information from Marketing Cloud Engagement subscriber lists and publication lists can now be mapped to **Communication Subscriptions** in Marketing Cloud Next. When lists are mapped, the status is automatically synchronized each time subscribers update their consent.

This change helps maintain compliance whether messages are sent from either app.

Availability: Email consent mapping will be gradually available by **July 13, 2026**. SMS and WhatsApp consent mapping will be gradually available by **August 17, 2026**.

How was it?

Since there was quite a lot of content, it may be difficult to catch up, but personally, most of the features were as expected. Once they are released, I would like to review them as much as possible.

That’s all for this article.

Stay tuned for more Salesforce Marketing Cloud tips! 😎

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
