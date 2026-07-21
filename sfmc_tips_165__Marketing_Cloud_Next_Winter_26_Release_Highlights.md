# SFMC Tips #165 : Marketing Cloud Next: Winter ’26 Release Highlights

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-next-winter-26-release-highlights-81240775f843

---

# SFMC Tips #165 : Marketing Cloud Next: Winter ’26 Release Highlights

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--81240775f843---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--81240775f843---------------------------------------)

22 min read

·

Aug 27, 2025

--

Photo by [Else-Marie de Leeuw](https://unsplash.com/@elsemariedeleeuw?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

The Winter ’26 new feature release for **Marketing Cloud Next (Marketing Cloud Growth & Advanced Edition)** has been announced.  
 In this article, I’ll walk you through the highlights of these new features.

[## Salesforce Help

### Edit description

help.salesforce.com](https://help.salesforce.com/s/articleView?id=release-notes.salesforce_release_notes.htm&release=258&type=5&source=post_page-----81240775f843---------------------------------------)

The Winter ’26 release date varies depending on your Salesforce instance:

- September 20, 2025
- October 4, 2025
- October 11, 2025

To check the exact upgrade date for your production instance, go to [Salesforce Trust](https://status.salesforce.com/products/Salesforce_Services), search by your instance name or domain, and click “**Maintenance Tab**”. There, you can see when the Winter ’26 release is scheduled to be applied to your instance and plan accordingly.

If you’re unsure which instance your org is on, the easiest way to check is by going to Setup > **Company Information** in your Salesforce org.

## Key Highlights

One of the most exciting updates in the Winter ’26 release is the ability to send **push notifications directly to mobile apps**. By extending the **Marketing Cloud Engagement SDK**, implementation and ongoing operations have become much simpler and more accessible. However, at this time, it’s only available for Marketing Cloud Next instances hosted in **Germany** and the **United States**.

The **landing page functionality** has also received a major upgrade. In addition to **form handlers**, **merge fields**, and **hidden fields**, the new **honeypot feature** provides built-in spam protection. It feels like we’re getting much closer to a point where a **full transition from Marketing Cloud Account Engagement** is finally within reach.

On the **Flow** side, the long-awaited **automation of the “path experiment” component** has finally arrived — transforming what used to be a manual process into an automated one, greatly improving efficiency. There’s also a new capability equivalent to **“Wait by Attribute”** activity in Marketing Cloud Engagement, along with a powerful “**on-demand flow” trigger via REST API**, which deserves special attention.

Let’s take a closer look at what’s new in **Winter ’26**!!

## Mobile Updates

### ① Send Push Notifications Using the Unified Marketing Cloud SDK

With the **Unified Marketing Cloud SDK**, you can now send push notifications directly to app users.  
 Previously, the SDK only supported push notifications via Marketing Cloud Engagement, but with this update, **Marketing Cloud Next** is now supported as well. This means developers who are already familiar with the Engagement SDK can send notifications with the same experience.

> *Currently, this feature is only available for Marketing Cloud Next instances hosted in* ***Germany*** *and the* ***United States****, and is limited to the* ***Advanced Edition****.*

### ② Create Interactive Push Notifications

You can now send **interactive push notifications** to authenticated mobile devices to boost customer engagement.

**Basic Push Type**

- Option to attach one media file
- Content customization
- Tap action configuration
- Add Android-specific icons and interactive buttons

**Carousel Push Type**

- Supports up to six swipeable cards
- Each card can include media, text, and its own tap action

> *Currently, this feature is only available for Marketing Cloud Next instances hosted in* ***Germany*** *and the* ***United States****, and is limited to the* ***Advanced Edition****.*

### ③ Gain Deeper Insights with Mobile App Messaging Analytics

When you add mobile app messaging channels to your campaigns, you’ll be able to view **aggregate metrics** for all messages sent.  
 You can track detailed insights such as **sent, delivered, viewed, and interaction counts**, both for individual messages and for the overall campaign. These analytics can then be leveraged to **optimize engagement strategies and improve performance**.

> *Currently, this feature is only available for Marketing Cloud Next instances hosted in* ***Germany*** *and the* ***United States****, and is limited to the* ***Advanced Edition****.*

### ④ Expanded SMS Marketing to More Countries

**Hong Kong, Honduras, Peru, and Singapore** have been added to the supported SMS marketing regions.

To send messages in these countries, you must request a **sender code**, and note that compliance and sending regulations vary by country. Be sure to review the requirements in advance.

### ⑤ Make WhatsApp Messaging More Engaging

New **interactive capabilities** such as WhatsApp Flows, location sharing, and CTA buttons enable you to boost customer satisfaction and conversion rates.

- Use **carousel messages** to showcase multiple products
- Integrate with real-time product catalogs to display **up-to-date pricing and inventory**
- Trigger flows based on customer responses to build **dynamic and personalized marketing strategies**

## Agentforce Updates

### ① Flexible Campaign Creation with Agentforce and Flows

Actions such as creating briefs and building or saving multi-channel campaigns can now be executed through customizable flows.

> *This is less of a “new feature” and more of an announcement that flows can now be customized. For more details about Agentforce in Marketing Cloud, please refer to the article below.*

[## SFMC Tips #117 : Marketing Cloud Next: Agentforce Campaign Creation

### The Marketing Cloud Next (Marketing Cloud Growth & Advanced Edition) includes an AI-powered feature for campaign…

medium.com](/@marketingcloudtips/marketing-cloud-on-core-agentforce-campaign-creation-697c992adbe6?source=post_page-----81240775f843---------------------------------------)

Administrators can modify flows in Flow Builder to execute campaign actions according to business needs.

For example, the following customizations are possible:

- Integration with other systems
- Automatic assignment of campaign owners
- Sending notifications to other teams
- Adding approval steps or specific business logic

This allows marketers to request Agentforce to create briefs or campaigns, make adjustments as needed, and save them — enabling efficient campaign management.

### ② Simplified Campaign Analytics with Agentforce

Marketers can easily gain insights into past campaign performance by leveraging Agentforce.

This action is added by default to the **“Campaign Planning”** topic, so users can start using it without any special configuration.

![]()

**“Generate Campaign Insights” Action**

- Automatically retrieves key performance data such as open rates, click rates, and unsubscribe rates
- Automatically generates a summary of major insights

Administrators can customize this action in Flow Builder to focus on metrics most relevant to the business.

Additionally, marketers can compare high-performing and low-performing initiatives to derive specific improvement recommendations, such as optimizing subject lines or adjusting email send intervals.

### ③ Automate Content Creation with the Content Builder Agent

The new **autonomous Content Builder Agent** collaborates with users to draft, revise, and optimize content from Salesforce CMS.

- Quickly create marketing assets such as subject lines, SMS messages, and body content
- Define company information and agent speaking rules to maintain brand consistency
- To get started, simply select the new **Content Builder Agent template** from Agent Builder

[## SFMC Tips #192 : Marketing Cloud Next: Content Builder Agent

### In the Summer ’25 release, Salesforce announced the retirement of Agentforce (Default). While it continues to function…

medium.com](/@marketingcloudtips/marketing-cloud-next-content-builder-agent-4c426d6dec3a?source=post_page-----81240775f843---------------------------------------)

## Content Updates

### ① Reusable “Content Block” Components

You can now speed up email creation, ensure consistency, and strengthen personalization by reusing **standardized content** such as banners, footers, and terms of service as **content blocks**.

**How it works**:

- Content managers can build blocks combining text, images, links, and buttons, then save them in the Marketing workspace.
- Different blocks can be created for different audiences.
- Marketers can quickly build emails using these blocks and apply variation rules to deliver **personalized content** to each recipient.

[## SFMC Tips #180 : Marketing Cloud Next: Introduction of Reusable Content Blocks

### With the Winter ’26 release of Marketing Cloud Next Growth & Advanced Edition, content reusability has been…

medium.com](/@marketingcloudtips/marketing-cloud-next-introduction-of-reusable-content-blocks-2b50a771fd8c?source=post_page-----81240775f843---------------------------------------)

### ② Save Time with New Email Templates

By using **Email Templates**, you can reduce work time while maintaining brand consistency across your campaigns.

Admins and campaign managers can create and manage standardized brand templates, while creators can simply select one to quickly build their own marketing emails. This streamlines the email creation process and establishes a consistent workflow across the team.

![]()

> *Note: Only published templates are available for use.*

### ③ Manage Data Sources to Enhance Personalization

Marketers now have greater flexibility in managing the data sources used for **merge fields**, **repeatable content**, and **dynamic content** within emails.

**For Data Graph data sources:**

- You can now **replace** the default Data Graph directly from the **Data Source** tab while editing an email.
- Before performing a replacement, you must delete all fields that were previously configured using the old Data Graph; otherwise, the email cannot be saved.
- While the **Remove** option for Data Graphs is still disabled (grayed out), at least one Data Graph must always be present.
- With this update, the previous limitation that required marketers to always use the **default Data Graph** has been lifted.

![]()

*Previous view*

![]()

*Updated view*

**For Event data sources:**

If the content is still in **draft** (before publication):

- The “Event” data source can be **replaced**.
- Starting with **Winter ’26**, it can now also be **removed**.

![]()

> ***Note:*** *Once the content has been* ***published*** *even once with an “Event” data source configured, the* ***Replace*** *and* ***Remove*** *buttons will no longer appear. The limitation that “Event” data sources cannot be modified after publication remains unchanged.*

### ④ Easier Email Detail Management

The **title, API name, and description fields** have been moved out of the settings panel and are now accessible via the **details icon** in the header of the canvas.

- Titles are auto-generated when an email is created
- Marketers can edit them directly from the header if needed

## Flows Updates

### ① Build Flows Optimized for Each Brand or Region by Data Space

When creating a new marketing flow or using an existing marketing flow template, you can now associate a data space with the flow.

By linking a data space, you can achieve more precise marketing automation and, by restricting access to specific data spaces, also enhance data security.

For example, if multiple business units are mapped to different data spaces, you can create customized flows tailored to the goals and requirements of each unit.

> *In Winter ’26, there was also discussion about Marketing Cloud Next business units, but this is not yet documented in the official help materials.*

[## #mcnext #marketingchampions #salesforcemarketingcloud | Mounir Nejjai | 22 comments

### When I first saw 𝗕𝘂𝘀𝗶𝗻𝗲𝘀𝘀 𝗨𝗻𝗶𝘁𝘀 in the Salesforce Marketing Cloud Next Winter 26 release, I thought: "Ok…

www.linkedin.com](https://www.linkedin.com/posts/mounirnejjai_mcnext-marketingchampions-salesforcemarketingcloud-activity-7373712904396881920-Jhha/?source=post_page-----81240775f843---------------------------------------)

### ② Run A/B Tests with Automatic Path Selection in “Path Experiment”

With the **automatic path selection** feature of the **Path Experiment** element, you can conduct A/B tests to guide customers toward the most effective path. This eliminates the need for manual intervention, allowing the system to automatically determine the optimal path for your audience — resulting in more efficient optimization.

Here’s an overview of the setup process:

1. Open the **Path Experiment** configuration screen and set the **label name** and **API name**. Then, under Configure Path Selection, click **Automated**, and select which metric will be used to determine the winning path.

2. Available metrics include standard options such as:

- **Higher email click rate**
- **Higher email open rate**
- **Lower email opt out rate**

In addition to these, you can also select **custom metrics** using **Engagement Signals**.

3. Set the **test group percentage** and **test duration**. After the test period ends, if you select **“Select the Best Performer”,** the remaining recipients will automatically be sent down the **winning path**.

4. You can add up to **10 paths** and freely adjust the percentage allocation for each.

[## SFMC Tips #188 : Marketing Cloud Next: A/B Testing with the “Path Experiment” Element

### The “Path Experiment” element in Marketing Cloud Next Growth & Advanced Edition combines the capabilities of “Random…

medium.com](/@marketingcloudtips/marketing-cloud-next-a-b-testing-with-the-path-experiment-element-5e39af4e0210?source=post_page-----81240775f843---------------------------------------)

### ③ Trigger On-Demand Flows via REST API

You can now launch new **on-demand flows** using API calls.  
For instance, you might set up an automation to send a promotional SMS after a user registers for a membership program or clicks a button on your website.

**How to create and trigger an on-demand flow:**

1. In the **Automation app**, click **[New]**, select the **Auto-Start** category, then choose **On-Demand Flow**.
2. To trigger it, use a REST call to the callable action endpoint and define the flow path:

```
POST /services/data/v65.0/actions/custom/flow/FLOW_NAME_HERE
```

[## Marketing Cloud Next: On-Demand Flows with REST API

### Photo by hesam Link on Unsplash

medium.com](/@marketingcloudtips/marketing-cloud-next-on-demand-flows-with-rest-api-fbef5c58804e?source=post_page-----81240775f843---------------------------------------)

### ④ Ensure Consistent Customer Data with New Flow Templates

The new “**Upsert a Record for a Person” flow template** allows you to look up and update an existing contact or lead record — or automatically create a new one if none is found.

This is particularly useful when IDs are not provided during form submissions (e.g., form-triggered flows). With this capability, you can reliably identify or create the appropriate record, ensuring faster responses and consistent customer data.

**Key Benefits:**

- **Faster response:** Instantly handle new leads right after a form submission
- **Data consistency:** Prevent duplicates by checking for existing records before creating new ones
- **Flexible scalability:** Use as a subflow element within other automations for easy reuse

**How it works:**

1. If a triggered flow does not provide a user ID, create a flow using the **“Upsert a Record for a Person” flow template**.
2. Reference this flow as a subflow from the main automation.
3. After execution, the Upsert flow returns the **record ID** of the created or updated record.
4. The main automation can then use this ID to execute subsequent customer data–based actions.

With this template, marketers can act on the **most current and consistent customer data** without relying on delayed identity resolution — strengthening marketing automation strategies.

[## SFMC Tips #186 : Marketing Cloud Next: Upsert a Record for a Person Flow Template

### In the Winter ’26 release of Marketing Cloud Next Growth & Advanced Edition, a new flow template called “Upsert a…

medium.com](/@marketingcloudtips/marketing-cloud-next-upsert-a-record-for-a-person-flow-template-76fe6855686e?source=post_page-----81240775f843---------------------------------------)

### ⑤ Easy Access to Individual DMO Data Within Flows

Although **this is exclusive to “segment-triggered flows”**, you can now directly reference Individual DMO fields from the resource picker based on the contents of the flow’s associated **data graph**. You can select from the available **attributes**.

Previously, retrieving this data required a separate **Get Records** element, but this enhancement reduces that extra step.

### ⑥ Determine the Corresponding CRM Record for an Individual

The newly added **“Determine CRM Record for Individual”** action allows a “**segment-triggered flow**” to automatically identify whether the incoming unified individual corresponds to a **Contact**, **Lead**, or **Prospect** in CRM.

![]()

Additionally, in Winter ’26, record referencing within flows has become even simpler. By placing elements such as **“Update Records”** on the paths of the **Determine CRM Record for Individual** action, you can now directly access the target object records on that path without first setting up a **Get Records** element.

Example: On a lead path, all fields within the Lead object can now be accessed directly.

[## SFMC Tips #185 : Marketing Cloud Next: Determine CRM Record for Individual

### In the Winter ’26 release of Marketing Cloud Next Growth & Advanced Edition, a new feature called “Determine CRM Record…

medium.com](/@marketingcloudtips/marketing-cloud-next-determining-the-corresponding-crm-record-for-each-individual-3ad8b0d5a805?source=post_page-----81240775f843---------------------------------------)

### ⑦ Custom Events Now Supported in “Wait Until Event”

Previously, the **“Wait Until Event”** element only supported **standard events** such as email clicks or SMS replies.

With this update, you can now use **custom events** — such as webinar registration or purchase completion — powered by “**Engagement Signals**” as wait conditions.

This enhancement enables more **timely and relevant interactions** based on actual customer behavior, while also offering greater flexibility to accommodate **business-specific scenarios**.

![]()

**Considerations:**

- The wait will be released either when the signal occurs or when the waiting period expires.
- Signals that are in use by active flows cannot be edited or deleted.

### ⑧ **“Wait Until Date” Now Supports Date and DateTime Fields**

Previously, **“Wait Until Date”** only supported fixed date and time values.  
With this enhancement, flows can now resume **based on date or datetime attributes** stored in records, eliminating the need to build complex workarounds.

![]()

- You can specify either a **fixed calendar date/time** or an **attribute-based date/datetime value** — similar to **“Wait by Attribute”** in Marketing Cloud Engagement.
- This improvement enables flexible flow control based on **user-specific attributes**, such as contract start dates or birthdays.

## Landing Pages Updates

### ① Integrate External Forms with Form Handlers

With the new **form handler**, data from external web forms can be sent directly into Salesforce.

- Map any web form fields to Salesforce objects **without code**
- Trigger flows to send follow-up emails or create tasks
- Add **honeypot fields** for spam prevention
- Specify custom **redirect URLs** for success/failure outcomes
- Monitor user engagement and form performance via **web tracking**

This allows you to deliver an excellent user experience while ensuring data quality. The setup steps are explained below.

[## SFMC Tips #184 : Marketing Cloud Next: How to Configure Form Handlers

### In the Winter ’26 release of Marketing Cloud Next Growth & Advanced Edition, a new Form Handler feature has been…

medium.com](/@marketingcloudtips/marketing-cloud-next-how-to-configure-form-handlers-ed3e045adfad?source=post_page-----81240775f843---------------------------------------)

### ② Simplify User Input with Hidden Fields and Default Values

Collecting key information efficiently on forms helps **maximize conversions** and provides insights into customer engagement with campaigns.

- **Hidden Fields:** Capture data such as campaign name or lead source page via URL parameters
- **Default Values:** Pre-populate values that users don’t need to enter

Hidden fields and default values can be applied across various input components, including **checkboxes, dropdowns, numbers, plain text, and text areas**.

[## SFMC Tips #189 : Marketing Cloud Next: Hidden Fields and Default Values in Forms

### In the Winter ’26 release, the Marketing Cloud Next Growth & Advanced Edition introduced new form features: Hidden…

medium.com](/@marketingcloudtips/marketing-cloud-next-hidden-fields-and-default-values-in-forms-a817f76c4b2e?source=post_page-----81240775f843---------------------------------------)

### ③ Personalize Landing Pages with Merge Fields

Using **merge fields** on landing pages helps capture visitor attention and **maximize lead generation**:

- Display visitor’s name or organization
- Highlight products or services relevant to each visitor
- Leverage **real-time Data Cloud data graphs** for optimized personalization

Select data graphs directly from the data source panel during editing for immediate reflection on the page

> *Note: This feature is available only for orgs created after Spring ’25. It’s not available in SDO environments. The button in the red box above will not be displayed.*

[## SFMC Tips #190 : Marketing Cloud Next: Merge Fields for Landing Pages

### With the Winter ’26 release of Marketing Cloud Next Growth & Advanced Edition, you can now use merge fields on landing…

medium.com](/@marketingcloudtips/marketing-cloud-next-merge-fields-for-landing-pages-e07985ecc67f?source=post_page-----81240775f843---------------------------------------)

### ④ Creating Landing Pages with Templates

You can now create and manage **Landing Page Templates**. This allows you to quickly launch effective landing pages and maximize campaign performance.

![]()

> *Note: Only published templates are available for use.*

### ⑤ Web Tracking Connector Update

To leverage the latest connector features and accurately track visitor activity on your website, administrators need to perform the following updates:

- Obtain the latest **External Tracking Data Kit** and **Marketing Website Connector**, and redeploy the data stream.
- Copy the new **web tracking script** from the connector and replace the existing script.

> *Note: If you have external tracking configured before Winter ’26, please redo your settings from scratch. External tracking configurations created prior to Winter ’26 are not compatible with the latest feature updates and will no longer function properly.*
>
> *Additionally, if connectors do not appear on the Web Tracking setup page, and your connector was created before March 2025, please contact Salesforce Customer Support to request an update.*

No new article was created for this update; instead, the previous article has been refreshed. Please refer to the updated article below.

[## SFMC Tips #130 : Marketing Cloud Next: Tracking External Websites with a Consent Banner

### With Marketing Cloud Next (Marketing Cloud Growth & Advanced Editions), you can track visitor activity and engagement…

medium.com](/@marketingcloudtips/marketing-cloud-on-core-tracking-external-websites-with-a-consent-banner-2492904a799c?source=post_page-----81240775f843---------------------------------------)

## Identity Resolution Updates

### ① Smarter Identity Resolution Match Rules

The contents of the “**default identity resolution rule set**” for unified individuals have been updated, improving the accuracy of tracking web visitors and preventing duplicate records.

[## SFMC Tips #183 : Marketing Cloud Next: Smarter Identity Resolution Match Rules

### With the Winter ’26 release of Marketing Cloud Next Growth & Advanced Edition, the contents of the “default identity…

medium.com](/@marketingcloudtips/marketing-cloud-next-smarter-identity-resolution-match-rules-ea432cbb5cc5?source=post_page-----81240775f843---------------------------------------)

When the default identity resolution rule set is generated at initial setup, two new match rules are automatically included:

- **Lead to Contact (lead-to-contact)**: Prevents duplication when a lead is converted to a contact.
- **Device to Known (device-to-known)**: Matches web visitors to known profiles.

Previously, the default identity resolution rule set only used **email address** matching.

### Considerations

- The newly added Identity Match-type rules, such as Device to Known and Lead to Contact, cannot be combined with other conditions. As a result, the “⚠️ Warning” message displayed in the interface cannot be removed.
- If you are already using an existing rule set, it is recommended to manually add these new match rules. The steps for adding them are explained below.

[## SFMC Tips #155 : Marketing Cloud Next: Identity Resolution Using Identity Match DMO

### In Marketing Cloud Next Growth & Advanced Edition, the Summer ’25 release introduced the ability to add Identity Match…

medium.com](/@marketingcloudtips/marketing-cloud-next-identity-resolution-using-identity-match-dmo-d5c47b599d5e?source=post_page-----81240775f843---------------------------------------)

**Tips**: If you are working with Prospects, we also recommend adding the following match types manually at this stage:

- **Prospect to Lead (prospect-to-lead)**
- **Prospect to Contact (prospect-to-contact)**

## **Consent Updates**

### **① Preserve the Latest Consent Date During Import**

A new validation check has been introduced to ensure that the consent date is only updated if the imported consent date is **newer than the existing one**.

This enhancement prevents older consent dates from accidentally overwriting more recent ones when importing marketing consent files. During the import process, if the consent date provided is **earlier than the existing consent date**, it will be **ignored**.

## Scoring Updates

### ① **Improved Evaluation Accuracy with Multi-Scoring Models**

Previously, only a single fixed scoring model could be used. With this update, you can now **combine multiple scoring models**, enabling **more flexible and accurate evaluations**.

- Segment scoring by **needs, product, region, or channel**
- Use **sub-scoring** in a test environment to reduce the cost of transitioning to new scoring rules

![]()

Additionally, when a **draft** is created, **four pre-calculated insights** are automatically generated. These insights are **automatically scheduled** as soon as the scoring model is **published**.

[## SFMC Tips #191 : Marketing Cloud Next: Multiple Scoring Models Now Available

### Previously, in Marketing Cloud Next Growth & Advanced Edition, only a single scoring model could be used. However…

medium.com](/@marketingcloudtips/marketing-cloud-next-multiple-scoring-models-now-available-b697017c6fd8?source=post_page-----81240775f843---------------------------------------)

## Analytics Updates

### ① Optimize Your Strategy with the Advanced “Insights” Dashboard

The enhanced Insights Dashboard introduces new features that allow you to visually analyze marketing performance.

- **New Chart:** Easily identify high-performing audience segments
- **Line Graph:** Track activity trends across multiple channels over time

️ These updates enable even more precise, data-driven decision-making.

### ② Refine Your Email Strategy with the Latest “Deliverability” Dashboard

The redesigned **“Deliverability”** tab in Marketing Performance now offers deeper analysis of email campaigns.

- Using the new **domain filter**, you can visualize delivery failure reasons by recipient domains such as Gmail and Hotmail.

- Additionally, the **message type filter** lets you analyze and compare performance between promotional and transactional emails.

### ③ View Detailed Performance Analytics in Flow Builder

Within **Flow Builder**, you can now view **detailed performance analytics** for segment-triggered flows and automation event-triggered flows.

By integrating with **Tableau Next**, you gain deeper visibility into the execution of each flow element and its downstream impact — helping teams make more **data-driven decisions**.

### ④ New WhatsApp Metrics for Stronger Analytics

In the **Insights Dashboard**, you can now view new metrics for **WhatsApp open rates and click-through rates**.

By filtering on **Sender Display Name**, you can focus your analysis on results tied specifically to authenticated sender names.

## Setup Updates

### ① Test Marketing Cloud Next in Sandbox Orgs

You can safely explore **Marketing Cloud Next features and content** in a sandbox environment without affecting production.

For example:

- Build and test complex **multi-channel campaigns** in your sandbox org
- Verify that campaigns work as expected before deploying to production

[## SFMC Tips #196 : Marketing Cloud Next: Testing with Sandbox

### With the Winter ’26 release of Marketing Cloud Next Growth & Advanced Edition, Salesforce introduced Sandbox…

medium.com](/@marketingcloudtips/marketing-cloud-next-testing-with-sandbox-22f23d92eef0?source=post_page-----81240775f843---------------------------------------)

### ② Migrate Form-Triggered Flows with Sandbox Change Sets

Change sets from **sandbox orgs** now support both:

- **Flow Definition components (for flows)**
- **Digital Experience components (for forms)**

Previously, form data was cleared during deployment. With this update, you can **safely migrate form-triggered flows** — including customizations — between orgs using change sets.

This strengthens governance and ensures that marketing teams can build, test, and deploy customer-facing automations with confidence.

### ③ Enhanced Guidance for Email Domain Setup

Several improvements have been made to streamline the email setup process and enhance the overall user experience:

- Simplified domain configuration
- Downloadable sample file for DNS entries
- Improved brand link management
- Expanded support for multiple subdomains and display names

In addition, multiple bug fixes have been implemented to improve overall system stability.

## Marketing Cloud Next for Engagement Updates

Marketing Cloud Engagement administrators can restrict access to these features for individual users by toggling navigation buttons **on** or **off**.

> ***Timing:*** *These features will be rolled out gradually starting in* ***November 2025****.*

### ① Creating Dynamic Customer Experiences with Agentforce

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

### ② ing to Journey Builder Events in Flows

Journey events such as when a contact meets a goal, enters a journey, or exits a journey can now be used in **Flows**.

**Types of Journey Event Triggers**

**Entry Journey**  
Triggers a flow when a contact enters a journey.

**Exit Journey**  
Triggers a flow when a contact exits a journey.

**Goal Met**  
Triggers a flow when a contact meets a goal.

With journey events, you can add customers to a flow or release them from a **Wait Until Event** activity inside the flow.

### ③ Injecting Contacts into Journeys from Flows

A new **“Send to Journey”** **action** in Flow allows you to inject contacts from a flow directly into a journey. A single flow can manage insertions into multiple journeys.

Marketers can link journeys through clicks instead of code, all within a single flow canvas view. This enhancement enables prioritization of journeys based on customer attributes and behaviors, delivering an end-to-end customer experience.

[## SFMC Tips #250 : Marketing Cloud Next: Send to Journey Action

### If you are using Marketing Cloud Engagement+, you can send contacts from a Marketing Cloud Next flow to Marketing Cloud…

medium.com](/@marketingcloudtips/marketing-cloud-next-send-to-journey-action-3a0c77cc2b63?source=post_page-----81240775f843---------------------------------------)

### ④ Enhanced Reporting by Linking Journeys with Campaigns

You can now add existing journeys in **Marketing Cloud Engagement** to campaigns for improved organization and analytics.

Marketing Cloud Next campaigns provide a connected workspace for activities and data, serving as the single source of truth for marketing activities across the Salesforce Platform.

When a journey is linked to a campaign, Marketing Cloud Next automatically aggregates its metrics into the overall campaign data. In Journey Builder, linked journeys display an icon indicating they are part of a campaign. Marketing users can also connect journeys to campaigns directly from the campaign page in Marketing Cloud Next.

[## SFMC Tips #210 : Marketing Cloud Next: Engagement+ Integration Setup

### As of November 2025, both new and existing Marketing Cloud Engagement customers can use Marketing Cloud Next by…

medium.com](/@marketingcloudtips/marketing-cloud-next-engagement-integration-setup-6fae8c535337?source=post_page-----81240775f843---------------------------------------)

### ⑤ Reporting and Segmentation with Journey History Data

By adding journey history data to **Data Cloud**, you can gain deeper insights into customer journeys.

In the **Analytics** tab of **Marketing Cloud Next**, this data can be used to create custom reports on journey entries, journey exits, goal achievements, and messaging activities.

Additionally, in **Data Cloud**, journey history can be leveraged to create segments, perform data transformations, and run high-performance zero-copy exports.

[## SFMC Tips #201 : Data Cloud: Journey Activity Run Added to Starter Data Bundle

### With the Winter ’26 release, the integration between Data Cloud and Marketing Cloud Engagement has been further…

medium.com](/@marketingcloudtips/data-cloud-journey-activity-run-added-to-starter-data-bundle-bbbe73434dd0?source=post_page-----81240775f843---------------------------------------)

### ⑥ On-Screen Visibility into Message Usage

**Marketing Cloud Next for Engagement** now includes a **Digital Wallet**, giving you visibility into message usage by day, by channel, and by Marketing Cloud Engagement business unit.

To simplify billing, every message sent consumes Salesforce message credits.

> ***Availability:*** *This feature was released on* ***July 15, 2025****.*

[## SFMC Tips #152 : Message Usage Visibility Now Available in Marketing Cloud Engagement+

### If you’re currently using Marketing Cloud Engagement+, as of July 28, 2025, you can now view the message usage data…

medium.com](/@marketingcloudtips/message-usage-visibility-now-available-in-marketing-cloud-engagement-dcb477d08c66?source=post_page-----81240775f843---------------------------------------)

## Final thoughts

It was quite a lot of information, so catching up might be challenging. Personally, most of the updates were **as expected**. I plan to review the released features as much as possible once they become available.

Finally, the Winter ’26 release notes for Marketing Cloud Engagement should include details about this integration with Marketing Cloud Next. Since those release notes are scheduled to be announced in mid-September, let’s look forward to them!

That’s all for this summary of Winter ’26 highlights.

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
