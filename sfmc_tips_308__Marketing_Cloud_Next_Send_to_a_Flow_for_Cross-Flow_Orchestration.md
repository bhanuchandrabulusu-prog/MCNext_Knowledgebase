# SFMC Tips #308 : Marketing Cloud Next: Send to a Flow for Cross-Flow Orchestration

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-next-send-to-a-flow-for-cross-flow-orchestration-859b7fcf84cc

---

# SFMC Tips #308 : Marketing Cloud Next: Send to a Flow for Cross-Flow Orchestration

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--859b7fcf84cc---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--859b7fcf84cc---------------------------------------)

3 min read

·

Jun 13, 2026

--

Photo by [Sasha Kaunas](https://unsplash.com/@akaunas?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

In the [Summer ’26 release](/@marketingcloudtips/marketing-cloud-next-summer-26-release-highlights-04f6c5abdee6) for Marketing Cloud Next Growth & Advanced Editions, a new **Send to a Flow** element has been introduced, enabling organizations to build more advanced and flexible customer journeys by connecting multiple flows together.

![]()

With this element, a customer identifier can be passed to a destination flow, while the source flow and destination flow run **asynchronously and in parallel**.

As a result:

- **The original flow continues running.**
- **A separate flow can execute processing at the same time.**

This enables more flexible flow orchestration scenarios.

Previously, implementing coordination across multiple flows often required complex custom logic or API integrations. With the introduction of this element, those architectures can now be implemented in a much simpler way.

This feature can be considered the Marketing Cloud Next equivalent of the **Send to Journey** element that was previously introduced in Marketing Cloud Engagement+ — essentially a “flow version” of that capability.

[## SFMC Tips #250 : Marketing Cloud Next: Send to Journey Action

### In environments using Marketing Cloud Engagement+, it is possible to send Marketing Cloud Next contacts from a…

medium.com](/@marketingcloudtips/marketing-cloud-next-send-to-journey-action-3a0c77cc2b63?source=post_page-----859b7fcf84cc---------------------------------------)

Typical use cases include:

- **Routing customers to different flows based on their loyalty program status.**
- **Following up only with customers who meet specific conditions in a separate flow.**
- **Modularizing common processes as reusable on-demand flows.**

### Flow Types That Can Contain the Element

- Segment Flow
- List Flow
- Campaign Flow
- Record Query Flow
- Event Trigger Flow
- Activation Trigger Flow
- On-Demand Flow

### Flow Types That Can Be Triggered

- On-Demand Flow

## Important Considerations for Implementation

The most important point when using this feature is that **users who execute the flow must be granted access to the target on-demand flow**.

If this configuration is overlooked, attempting to trigger an on-demand flow will result in a permission error on the email send element in the triggering flow. At the same time, nothing will happen in the target on-demand flow.

To grant access, open the **Details** page of the target on-demand flow and select **Manage Access** from the action menu.

Then grant access to the profile used by the users who will run the on-demand flow (for example, System Administrator).

*Because* ***this configuration must be performed for each on-demand flow individually****, be sure to apply the same setting whenever a new on-demand flow is created.*

## Summary

In this article, I introduced the **Send to a Flow** element added in the Summer ’26 release. While the concept itself is not particularly new, there are several important considerations when using it:

- **The original flow does not automatically exit and continues processing.**
- **The on-demand flow is executed immediately.**

In other words, sending a customer to another flow does **not** terminate the original flow. Depending on the design, this could unintentionally result in duplicate processing.

In addition, because on-demand flows execute in near real time, careful consideration should be given to timing and execution design.

That’s all for this article.

Stay tuned for more Salesforce Marketing Cloud tips! 😎

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
