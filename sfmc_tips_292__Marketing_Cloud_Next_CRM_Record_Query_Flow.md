# SFMC Tips #292 : Marketing Cloud Next: CRM Record Query Flow

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-next-crm-record-query-conditional-search-flow-8bfb3e7c3d74

---

# SFMC Tips #292 : Marketing Cloud Next: CRM Record Query Flow

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--8bfb3e7c3d74---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--8bfb3e7c3d74---------------------------------------)

5 min read

·

May 13, 2026

--

Photo by [Evgeni Tcherkasski](https://unsplash.com/@evgenit?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

Marketing Cloud Next Growth & Advanced Editions [Summer ’26 new feature release](/@marketingcloudtips/marketing-cloud-next-summer-26-release-highlights-04f6c5abdee6) has renamed the entry point of the traditional “Segment Triggered Flow” to **“Audience Flow”.**

Within this **Audience Flow**, when creating a flow, users can now select various data sources from the **Start** element depending on the use case, in addition to the traditional **Segment Flow**, including:

- **Record Query Flow (Record)**
- **List Triggered Flow (List)**
- **Campaign Member Flow (Campaign)**

As a result, audience-based flows have now been unified under the **Audience Flow** category, making flow creation and management simpler and easier to understand.

*Regarding the* ***Campaign Flow*** *used for sending messages to* ***campaign members****, it was previously possible to segment and send to campaign members through campaign flows. However, with this update, the functionality has become more intuitive and can now be used with a single click.*

In this article, I would like to focus specifically on the particularly noteworthy **Record Query Flow (Record)** and explain it in detail.

## What is a Record Query Flow?

The **Record Query Flow**, newly introduced in the Summer ’26 release, is a new flow type that directly sets conditions on CRM records in the “Start” element and retrieves the target audience from CRM records **in real time immediately before execution** for sending.

In this Record Query Flow, instead of sending based on **“Unified Individuals”** like traditional segment-based delivery, it becomes possible to perform scheduled sends using the **latest records stored on the CRM side** as the data source.

For search conditions, in addition to **AND** and **OR**, **custom logic** can also be used, making it possible to define complex conditions such as:

**“(1 AND 2 AND 3) OR 4”**

*Note: Since the search conditions are evaluated for the first time immediately before the flow starts, the send count and retrieved audience cannot be confirmed in advance. Therefore,* ***it is recommended to initially configure only a “Wait” element and perform a dry run to verify the actual send count before enabling the flow****.*

![]()

## Latest CRM Records Can Be Used Immediately

The **biggest feature** of this Record Query Flow is that **there is no need to wait for synchronization to Data 360.**

For example, even a contact record created just **one minute ago** can immediately be used for delivery execution. The email address used at this time is the contact’s **standard email field.**

This mechanism is a **very impactful sending method** that significantly changes the traditional concept of Marketing Cloud Next, where delivery was based on data ingested into Data 360 and unified as a **Unified Individual.**

## How Data Graphs Are Handled

What many people are probably wondering here is how **“Data Graphs”** used in content and flows are handled.

In this Record Query Flow, even if merge fields derived from **Data Graphs** are included in the email content, **those values are not referenced.**

More precisely, **Data Graph values are not retrieved, and the configured “default values” are displayed instead.** Even if the audience actually has accessible values in the Data Graph, the **“default values”** will still be displayed.

On the other hand, in the **“Decision”** element within the flow, **condition evaluation using Data Graph values is possible.**

In other words:

- **Data Graphs are not used for content merge fields**
- **However, Data Graphs can be used for flow conditional branching**

This results in somewhat unusual behavior.

## Use “Content Variables” for Personalization

However, if you absolutely need to personalize content, please use personalization through **“Content Variables”.**

[## SFMC Tips #290 : Marketing Cloud Next: Personalization with Content Variables

### In the Summer ’26 new feature release for Marketing Cloud Next Growth & Advanced Editions, it became possible to add…

medium.com](/@marketingcloudtips/marketing-cloud-next-personalization-with-content-variables-18ebb6764911?source=post_page-----8bfb3e7c3d74---------------------------------------)

With this new feature released in Summer ’26, it becomes possible to **pass variables directly from the flow to the email message.**

**Triggered Record** attributes are available from the **Triggered Record** resource in Quick Resources.

Note that the **Attributes** resource in the Flow Profile corresponds to the values of the **Individual** in the Data Graph. Any fields that you want to use in the flow must be made available beforehand in the Data Graph configuration.

As shown below, the name is inserted using the **“Content Variable”** feature.

What did you think?

With the traditional **Marketing List Email** functionality, customers extracted through list views were synchronized to Marketing Cloud Next segments for use, but it felt heavily dependent on the **Data Cloud** and **Marketing Cloud Next** environment.

![]()

On the other hand, by using this **Record Query** feature, **CRM records can be searched directly**, enabling more flexible audience creation.

That’s all for this time.

Stay tuned for more Salesforce Marketing Cloud tips! 😎

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
