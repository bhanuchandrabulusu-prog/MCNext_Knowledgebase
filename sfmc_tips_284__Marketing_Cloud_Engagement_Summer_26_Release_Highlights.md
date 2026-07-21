# SFMC Tips #284 : Marketing Cloud Engagement: Summer ’26 Release Highlights

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-engagement-summer-26-release-highlights-d51f444d3402

---

# SFMC Tips #284 : Marketing Cloud Engagement: Summer ’26 Release Highlights

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--d51f444d3402---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--d51f444d3402---------------------------------------)

4 min read

·

Apr 28, 2026

--

Photo by [Ha Pham](https://unsplash.com/@virmise?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

The information for the [**Summer ’26 new feature release**](https://help.salesforce.com/s/articleView?id=release-notes.rn_marketing_engagement.htm&release=262&type=5) **of Marketing Cloud Engagement** has been published, so this time I would like to summarize the highlights.

While **Journey Builder** has received several enhancements, there are no major updates for **Automation Studio** or **Email Studio**, making this a relatively compact release overall.

Among the most notable updates is the introduction of **MCP server** support. This could mark the beginning of a new era where **Marketing Cloud Engagement** can be operated through direct conversations with AI.

In particular, areas where Marketing Cloud Engagement has traditionally been lacking — such as:

- **Natural language operations**
- Assistance with **SQL**
- Automation of administrative tasks
- Faster analysis

may increasingly be complemented by tools like **Claude** and **Gemini**.

It may even be the start of an era where AI works “side by side” with **Marketing Cloud Engagement administrators and operators**.

In terms of integration with **Marketing Cloud Next**, another important update is the addition of the long-awaited **consent mapping** functionality for **Marketing Cloud Engagement**, which had previously been a challenge. This is a significant enhancement that addresses a critical point for real-world operations and could be considered one of the key highlights of this release.

Now then, let’s take a look at these new features in release order.

## **Journey Builder**

### ① Improve performance with on-canvas automated recommendations

A **“recommendations” feature** has been added for marketers, allowing them to directly select the most suitable tools on the Journey Builder canvas.

These prompts help marketers leverage advanced features such as **Flow Builder** to perform tasks beyond messaging, and to strengthen journey connectivity and prioritization by utilizing **Marketing Cloud Next campaigns**.

*The UI is not yet available, but once the actual screens are released, it will become clearer what kind of recommendations will be displayed and where.*

### ② Filter and organize journeys more efficiently

On the journey dashboard, it is now possible to **select multiple journeys and move them simultaneously** to a folder or subfolder.

Additionally, with the introduction of a **campaign filter**, users can quickly find journeys associated with specific campaigns.

## **Contact Builder**

### ① Contact Builder import size limited to 6 MB

To improve performance, the file import wizard in Contact Builder has been updated to support a **maximum file size of up to 6 MB** when uploading via a browser.

## **Einstein**

### ① Einstein retired in some Hyperforce regions

Einstein functionality was retired on **March 16, 2026**, in Hyperforce regions in **Australia, Japan, and Canada**.

To maintain continuity, data can be processed in the **United States or the European Union**, or you can **migrate to Marketing Cloud Next** and keep data within the region.

## **WhatsApp**

### ① Track conversions from “Click-to-WhatsApp” ads

By using Meta Ads’ **“Click-to-WhatsApp” feature**, conversations initiated by users on WhatsApp can be automatically tracked and linked to ads.

By ingesting the acquired **referral data into Data 360**, marketers can more accurately visualize the effectiveness of their ad spend and optimize **data-driven marketing strategies**.

### ② India: Send payment options via WhatsApp

By sending **payment options directly within WhatsApp chats**, the purchasing process becomes seamless, enabling faster decision-making and improved conversion rates.

As payment methods, either **UPI intent or payment links** can be configured.

*This message template is currently available only for messages sent to India.*

## **Marketing Cloud Engagement+**

### ① Use Engagement-side SMS codes in Next

SMS **short codes and long codes (US and Canada)** from Marketing Cloud Engagement can now be used in Marketing Cloud Next.

Since there is no need to reacquire codes, messaging strategies can be **unified**, and both outbound and inbound traffic in Journey Builder and Flow Builder can be managed from a **single code**.

Configuration Method: From the Marketing Cloud Next setup, navigate to Marketing Cloud Engagement > **Connect Data**, and share the code from the following management screen.

### ② Consent mapping between MCE and MCN

Consent information from **subscriber lists and publication lists** in Marketing Cloud Engagement can now be mapped to **“Communication Subscriptions” in Marketing Cloud Next**.

Once mapped, the status is **automatically synchronized whenever a subscriber updates their consent**.

With this change, **compliance can be maintained regardless of which application is used to send messages**.

Availability:

- Email consent mapping: rolling out until **July 13, 2026**
- SMS and WhatsApp consent mapping: rolling out until **August 17, 2026**

## **AI**

### ① AI Integration Using the MCP Server

**MCP (Model Context Protocol)** is a common standard proposed by **Anthropic** that enables AI to safely interact with external systems. Put simply, it acts as a “bridge” that allows AI to directly operate external tools.

With this new capability, we are moving toward an era where users can directly instruct **Claude** or **Gemini**, and have them operate **Marketing Cloud Engagement** on their behalf.

For example, operations such as:

- Creating a new **Data Extension**
- Identifying the journey with the highest unsubscribe rate over the past week
- Investigating journeys or email assets

will become possible through direct AI interaction.

Unlike **Marketing Cloud Next**, **Marketing Cloud Engagement** did not previously have something like **Agentforce** operating on the core platform.

However, if you think of it as “Claude or Gemini directly taking on the role of Agentforce,” it becomes much easier to understand the significance of this new feature.

*Scheduled for gradual rollout to environments starting from July 2026.*

[## SFMC Tips #300 : The Future of Marketing Cloud Engagement Changed by MCP Servers

### In the Summer ’26 new feature release for Marketing Cloud Engagement, MCP Servers will finally become available.

medium.com](/@marketingcloudtips/the-future-of-marketing-cloud-engagement-changed-by-mcp-servers-e2f7f29ecd90?source=post_page-----d51f444d3402---------------------------------------)

That’s all for this time.

Stay tuned for more Salesforce Marketing Cloud tips! 😊

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
