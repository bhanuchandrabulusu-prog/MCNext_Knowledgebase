# SFMC Tips #305 : Marketing Cloud Next: Actionable List Flow

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-next-actionable-list-flows-42b6a0fcc277

---

# SFMC Tips #305 : Marketing Cloud Next: Actionable List Flow

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--42b6a0fcc277---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--42b6a0fcc277---------------------------------------)

6 min read

·

Jun 9, 2026

--

Photo by [Alvin Mahmudov](https://unsplash.com/@alvinmahmudov?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

With the [Summer ’26 release](/@marketingcloudtips/marketing-cloud-next-summer-26-release-highlights-04f6c5abdee6) for Marketing Cloud Next Growth & Advanced Editions, the entry point previously known as the **Segment Triggered Flow** has been renamed to **Audience Flow**.

Within this new **Audience Flow**, in addition to the traditional **Segment Flow**, you can now choose various data sources from the **Start** element based on your use case, including:

- Record Query Flow (Record)
- List Flow (List)
- Campaign Flow (Campaign)

As a result, audience-driven flows have been consolidated under the **Audience Flow** category, making flow creation and management simpler and easier to understand.

*For* ***Campaign Flows****, which send communications to campaign members, it was previously possible to segment campaign members and send communications through campaign flows. However, this update makes the process more intuitive and available with a single click.*

I explained **Record Query Flows** in the following article.

[## SFMC Tips #292 : Marketing Cloud Next: CRM Record Query Flow

### Marketing Cloud Next Growth & Advanced Editions Summer ’26 new feature release has renamed the entry point of the…

medium.com](/@marketingcloudtips/marketing-cloud-next-crm-record-query-conditional-search-flow-8bfb3e7c3d74?source=post_page-----42b6a0fcc277---------------------------------------)

In this article, I will focus on **List Flows**, one of the most noteworthy additions.

## What Is a List Flow?

A **List Flow** allows you to quickly reach a specific known audience (for example, people who signed up for marketing communications at a trade show) using a static list called an **Actionable List**.

Previously in Marketing Cloud Next, you had to wait for data to be synchronized to Data 360, then wait for Identity Resolution and Data Graph updates before sending communications. This often resulted in significant delays.

With **Actionable Lists**, however, once leads are imported from a CSV file, they can immediately be used for Marketing Cloud Next sends. While this feature can be used in an ad hoc (one-time) manner, it also supports ongoing management such as adding and removing list members.

## Creating an Actionable List

### 1. Open the Import Screen

The navigation path for configuring an **Actionable List** is somewhat difficult to find. Open either the **Contact** or **Lead** object page depending on your target audience. In this example, I will use **Leads**. Click the **Import** button.

**Note:** You cannot create a single Actionable List containing both Contacts and Leads.

### 2. Select Import from File

Choose **Import from File**.

### 3. Prepare a CSV File

Download the CSV template from the screen shown below. For example, create a list of 10 people who recently signed up for marketing communications at a trade show and enable the option to add them to an Actionable List.

### 4. Choose a List

Decide whether to create a new **Actionable List** or add the records to an existing list.

### 5. Enter a List Name

If creating a new list, provide a name and continue.

### 6. Run the Import

Execute the import process.

### 7. Import Completion Notification

After the import is completed, an email notification is automatically sent.

## Managing Actionable Lists

Navigate to the **Actionable Lists** tab to view created lists and list members.

- **Manually update lists:** Add or remove individual members as needed.
- **Automate list management:** Add or remove list members based on various criteria, such as field value changes. Only the creator of a list can remove list members.

You can also place a button on a standard list, allowing users to add records to the list one at a time directly from the standard list view.

## How Data Graphs Are Handled

One question many people have is how **Data Graphs** are handled within content and flows.

In a List Flow, even if an email contains merge fields derived from a Data Graph, those values are not referenced.

More specifically, Data Graph values are not retrieved. Instead, the configured **default values** are displayed. Even if the audience member has accessible values within the Data Graph, the system still uses the configured default values.

However, within Flow **Decision** elements, Data Graph values can be used for conditional evaluation.

In other words:

- Data Graph values are not used for content personalization.
- Data Graph values can be used in flow decision logic.

This results in somewhat unusual behavior.

## Use Content Variables for Personalization

If you need to personalize content, use **Content Variables**.

[## SFMC Tips #290 : Marketing Cloud Next: Personalization with Content Variables

### In the Summer ’26 new feature release for Marketing Cloud Next Growth & Advanced Editions, it became possible to add…

medium.com](/@marketingcloudtips/marketing-cloud-next-personalization-with-content-variables-18ebb6764911?source=post_page-----42b6a0fcc277---------------------------------------)

With this Summer ’26 feature, variables can now be passed directly from a flow into an email message.

Attributes from **Actionable List Member** are available through Quick Resources.

As shown below, the recipient’s name can be inserted using **Content Variables**.

## Summary

Even when using this mechanism, email sending still requires **Consent** records.

Therefore, if Consent record creation has not been automated, you must first import the Consent records, then create the Actionable List, and finally create and run the flow using that list.

If Consent records do not exist, emails will not be sent even if recipients are included in the list.

Keeping this requirement in mind will allow you to use Marketing Cloud Next to send emails to leads more efficiently and smoothly.

That’s all for this article.

Stay tuned for more Salesforce Marketing Cloud tips! 😎

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
