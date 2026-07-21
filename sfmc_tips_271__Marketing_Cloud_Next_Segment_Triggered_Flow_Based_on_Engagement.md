# SFMC Tips #271 : Marketing Cloud Next: Segment Triggered Flow Based on Engagement

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-next-segment-triggered-flow-based-on-engagement-cf48dd0aa6c2

---

# SFMC Tips #271 : Marketing Cloud Next: Segment Triggered Flow Based on Engagement

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--cf48dd0aa6c2---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--cf48dd0aa6c2---------------------------------------)

6 min read

·

Mar 24, 2026

--

Photo by [Blake Cheek](https://unsplash.com/@blakecheekk?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

In the [Spring ’26 new features](/@marketingcloudtips/marketing-cloud-next-spring-26-release-highlights-24c0c804b0cb) of Marketing Cloud Next Growth & Advanced Edition, in addition to the existing Unified Individual-based segments,

- **Individual-based segments**
- **Standard engagement database segments**

can now also be used to create segment-triggered flows and send emails. This significantly improves the flexibility of communication design starting from segments.

> *This feature is enabled by utilizing the* ***“Activation Template”****, which is one of the Data 360 activation features.*

![]()

## What this new Activation Template feature enables

With this mechanism, the following three capabilities are now possible:

1. [**Single send in Unified Individual-based segment flows**](/@marketingcloudtips/marketing-cloud-next-understanding-which-email-addresses-are-used-for-sending-ca52aaace7d9)
2. [**Sending from Individual-based segment flows**](/@marketingcloudtips/marketing-cloud-next-segment-triggered-flow-based-on-individual-8964a8886f59)
3. [**Sending from Engagement-based segment flows**](/@marketingcloudtips/marketing-cloud-next-segment-triggered-flow-based-on-engagement-cf48dd0aa6c2)

## Supplement: Single send in Unified Individual-based segments

Previously, in Unified Individual-based segmentation, there was an issue where emails were sent to all email addresses associated with a single person.

With this new “single send” capability, it is now possible to control delivery as **1 person = 1 message**.

In this article, I focus specifically on **Engagement-based segments**.

## Evolution of Engagement-Based Segments

As mentioned in a previous article, with the update in June 2025, it became possible to activate engagement-based segments from Data Cloud into Marketing Cloud Engagement.

In that setup:

- Only records linked to contact points such as email addresses or phone numbers were targeted
- Data utilization was primarily intended for delivery from Marketing Cloud Engagement

[## SFMC Tips #202 : Data Cloud: Engagement-Based Segments and Activation Targets

### Until now, the “Segment On” option in Data Cloud segments was limited to data model objects (DMOs) in the Profile…

medium.com](/@marketingcloudtips/data-cloud-engagement-based-segments-and-activation-targets-dd63ebb540ed?source=post_page-----cf48dd0aa6c2---------------------------------------)

With the Spring ’26 update, **the key point is that these engagement-based segments can now also be used directly from Marketing Cloud Next for sending**.

In other words:

- Previously: Engagement data was treated as supplementary data to profiles

Now:

- **Engagement-level data can be directly used for sending in Marketing Cloud Next**

In this article, I validate whether use cases previously implemented in Engagement can now be achieved in the same way within Marketing Cloud Next.

## Setup Steps

In this validation, I prepared the following simple scenario:

- Prepare 3 Contacts

- Create purchase data using Data 360 file import

## Purchase Data Details

- Person 1: Purchased 3 products on the same day
- Person 2: Purchased 2 products on the same day
- Person 3: Purchased 1 product on the same day

In other words:

- **Laptop: purchased by 3 people**
- **Phone Charger: purchased by 2 people**
- **Wireless Headphones: purchased by 1 person**

Based on this data, I implement the following use case:

- Create an engagement-based segment
- Send messages on the day after purchase
- Send messages for each purchased product

The flow is designed as follows:

## Expected Outcome

- **Laptop path → 3 people (all)**
- **Phone Charger path → 2 people**
- **Wireless Headphones path → 1 person**

## Setup Steps

## Prerequisite: Data Graph Configuration

To use this Activation Template mechanism, a data graph based on Unified Individual is required.  
\**An engagement DMO-based data graph is not required.*

Connect the following path:

- Unified Individual → Unified Link Individual → Individual → Contact Point Email

Be sure to select the **Data Source** field for Contact Point Email.  
If this is not set, a warning will appear when saving the flow.

## 1. Create Activation Template

Go to the Activation tab and click **New**.

Then select the newly introduced **Template** option in Spring ’26.

## 2. Select Target Data Model

Configure as follows:

- Target Data Model Object: **Product Order Engagement**
- Platform: **Data Cloud**

> *Note:* ***Only standard engagement DMOs can be used****. Custom engagement DMOs are not supported.*

## 3. Select Channel

Select a channel.  
If SMS is not purchased, only Email is available, so select **Email**.

## 4. Configure Source Priority

Next is **Edit “Source Priority Order”**.

For Unified Individual-based activation templates, this setting is important, as explained in previous articles.

[## SFMC Tips #166 : Marketing Cloud Next: Send a Single Message per Unified Individual in Segments

### In Marketing Cloud Next Growth & Advanced Edition, when Unified Individual is used in a Segment-Triggered Flow, the…

medium.com](/@marketingcloudtips/marketing-cloud-next-understanding-which-email-addresses-are-used-for-sending-ca52aaace7d9?source=post_page-----cf48dd0aa6c2---------------------------------------)

Also, in the explanation of Individual-based segment-triggered flows, I covered the use of Email Type.

[## SFMC Tips #270 : Marketing Cloud Next: Segment Triggered Flow Based on Individual

### In the Spring ’26 new features of Marketing Cloud Next Growth & Advanced Edition, in addition to the existing Unified…

medium.com](/@marketingcloudtips/marketing-cloud-next-segment-triggered-flow-based-on-individual-8964a8886f59?source=post_page-----cf48dd0aa6c2---------------------------------------)

Here, I proceed with the default “**Any**” setting.

> *Note: This is an important point, so please refer to the respective articles.*

## 5. Next Screen (Attribute Selection)

In normal activation, this screen is used to add attributes, but for Activation Templates, there is no attribute selection.

Proceed as is.

## 6. Set Template Name

Finally, set the Activation Template name.

It is important to use a name that clearly indicates which source is prioritized.

Example:

- **Product Order Engagement — Email (Any Priority)** (= No email priority)

## 7. Use in Segment-Triggered Flow

Next, create a segment-triggered flow.

When selecting a segment created from standard engagement data, the Activation Template configuration screen will appear.

> *Note: If the segment is created from a custom engagement DMO, the Activation Template screen will not appear.*

Select the Activation Template created earlier.

## Result

After sending, the results are as expected:

- **Laptop path → 3 people (all)**
- **Phone Charger path → 2 people**
- **Wireless Headphones path → 1 person**

Success.

## Summary

Previously, flows using engagement-based segments were limited to sending at the person level (and specifically at the Unified Individual level), which restricted possible use cases.

However, with this new feature, **sending at the engagement level is now possible, enabling scenarios that were previously difficult to achieve**.

As a result, the range of design possibilities has significantly expanded.

If you are not aware of this feature, new ideas will not emerge.

I recommend trying it in an actual environment and exploring what kinds of use cases can be implemented.

That’s all for this article.

Stay tuned for more Salesforce Marketing Cloud tips! 😎

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
