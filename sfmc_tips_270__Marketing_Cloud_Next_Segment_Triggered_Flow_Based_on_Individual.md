# SFMC Tips #270 : Marketing Cloud Next: Segment Triggered Flow Based on Individual

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-next-segment-triggered-flow-based-on-individual-8964a8886f59

---

# SFMC Tips #270 : Marketing Cloud Next: Segment Triggered Flow Based on Individual

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--8964a8886f59---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--8964a8886f59---------------------------------------)

4 min read

·

Mar 23, 2026

--

Photo by [Francis carcassi](https://unsplash.com/@fcarcassi?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

In the [Spring ’26 new features](/@marketingcloudtips/marketing-cloud-next-spring-26-release-highlights-24c0c804b0cb) of Marketing Cloud Next Growth & Advanced Edition, in addition to the existing Unified Individual–based segments, it is now possible to create segment-triggered flows and send emails from **Individual-based segments** and **Engagement Database segments**.

This enables more flexible segment-driven communication design.

For example, it is now possible to configure flows for segments targeting published Individuals, but in that case, it is necessary to newly configure an “**Activation Template**”.

![]()

## What this new Activation Template feature enables

With this mechanism, the following three capabilities are now possible:

1. [**Single send in Unified Individual-based segment flows**](/@marketingcloudtips/marketing-cloud-next-understanding-which-email-addresses-are-used-for-sending-ca52aaace7d9)
2. [**Sending from Individual-based segment flows**](/@marketingcloudtips/marketing-cloud-next-segment-triggered-flow-based-on-individual-8964a8886f59)
3. [**Sending from Engagement-based segment flows**](/@marketingcloudtips/marketing-cloud-next-segment-triggered-flow-based-on-engagement-cf48dd0aa6c2)

In this article, I will focus on Individual-based segments.

## Configuration Steps

## Prerequisite: Data Graph Setup

With the mechanism using this “Activation Template”, it is necessary to prepare a data graph based on Unified Individual.  
*Note: A data graph based on Individual is not required.*

Please connect the following path:

**Unified Individual > Unified Link Individual > Individual > Contact Point Email**

Be sure to select the “**Data Source”** field in Contact Point Email.  
If this field is not configured, a warning will be displayed when saving the flow.

## 1. Create an Activation Template

First, navigate to the Activation tab and click **New**.

Next, select **Template**, which was newly introduced in Spring ’26.

## 2. Select the Target Data Model

Configure the following:

- Target Data Model Object: **Individual**
- Platform: **Data Cloud**

## 3. Select the Channel

Select the channel. If SMS has not been purchased, only Email can be selected, so here we select **Email**.

## 4. Set Source Priority

Next is selecting **Edit “Source Priority Orders”**.  
In the case of Unified Individual–based Activation Templates, this source priority setting is important, as explained in a previous article.

[## SFMC Tips #166 : Marketing Cloud Next: Send a Single Message per Unified Individual in Segments

### In Marketing Cloud Next Growth & Advanced Edition, when Unified Individual is used in a Segment-Triggered Flow, the…

medium.com](/@marketingcloudtips/marketing-cloud-next-understanding-which-email-addresses-are-used-for-sending-ca52aaace7d9?source=post_page-----8964a8886f59---------------------------------------)

On the other hand, for the Individual-based case this time, it is generally not necessary to set priority (= keep it as **Any**).

However, as an exception, if Email Type is used in Data 360 operations, set the priority appropriately to control the correct destination.

## Supplement: Detailed Settings Using Email Type

Even for the same contact, in addition to the primary email address, there may be multiple email addresses such as:

- Secondary email address
- Personal email address

In such cases, by using the standard **Email Type** in Data 360, it becomes possible to perform more granular priority control.

After registering the priority, proceed to the next step.

## 5. Next Screen (Attribute Selection)

The next screen is normally used to add attributes in standard activation, but in Activation Templates there is no attribute selection.

Proceed to the next step as is.

## 6. Set the Template Name

Finally, set the Activation Template name.  
It is important to use a name that makes it clear which source is prioritized.

**Configuration examples:**

- **Individual — Primary Email Priority (prioritize primary email address)**
- **Individual — Primary Email Only (send only to primary email address)**
- **Individual — Personal Email Only (send only to personal email address)**

## 7. Use in a Segment-Triggered Flow

Next, create a segment-triggered flow.  
When selecting an Individual segment as the target, the Activation Template configuration screen will be displayed.

Here, select the Activation Template created earlier.

After that, simply activate the flow and send as usual.

## Summary

At first glance, you might feel that “maybe Unified Individual is no longer necessary going forward”, but in reality, since the data graph depends on Unified Individual, ID resolution is still required.

Because Data Cloud is designed based on the concept of “**data unification**”, understanding and utilizing this mechanism is most important.

And this feature is particularly effective for segment delivery using engagement data. I would like to explain this point in detail in another article.

That’s all for this time.

Stay tuned for more Salesforce Marketing Cloud tips! 😎

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
