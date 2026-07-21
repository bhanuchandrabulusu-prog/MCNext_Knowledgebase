# SFMC Tips #297 : Marketing Cloud Next: How to Use the “Exit from a Flow” Element

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-next-how-to-use-the-exit-from-a-flow-element-6398bef93977

---

# SFMC Tips #297 : Marketing Cloud Next: How to Use the “Exit from a Flow” Element

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--6398bef93977---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--6398bef93977---------------------------------------)

3 min read

·

May 18, 2026

--

Photo by [John T](https://unsplash.com/@john_thng?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

In the [Summer ’26 new feature release](/@marketingcloudtips/marketing-cloud-next-summer-26-release-highlights-04f6c5abdee6) of Marketing Cloud Next Growth & Advanced Editions, it is now possible to automatically stop unnecessary communications for audiences that meet specific conditions or goals by using the newly added **“Exit from a Flow”** element.

![]()

- Only one flow can be selected per element at a time.

- You can also choose whether to exclude the audience from **all versions** of the selected target flow, or only from the **latest version**.

- When executed, the status of the element in the target flow becomes **Stopped**.

## Comparison with Traditional API-Based Exclusion

Previously, excluding audiences required handling through APIs, but this feature now allows the process to be controlled in a much simpler and more flexible way.

The method for **“excluding from a flow using APIs”** is explained below.

[## SFMC Tips #247 : Marketing Cloud Next: How to Forcefully Exit Audiences from a Flow

### In Marketing Cloud Next Growth & Advanced Edition, you can use various flows such as Segment-Triggered Flows…

medium.com](/@marketingcloudtips/marketing-cloud-next-how-to-forcefully-exit-contacts-from-a-flow-bfb9bd74e071?source=post_page-----6398bef93977---------------------------------------)

Even when comparing the supported flow coverage, the range is much broader.

### Flow Types Supported by Exit from a Flow

- Segment Flow
- List Flow
- Campaign Flow
- Record Query Flow
- Event Triggered Flow
- Activation Triggered Flow
- On-Demand Flow
- Broadcast Flow

### Flow Types Supported by Exit Individuals from a Flow (REST API)

- Segment Flow
- Event Triggered Flow
- On-Demand Flow

What did you think?

As a use case example, you could prepare a separate flow using something like an Event Triggered Flow, Data Cloud Triggered Flow, or On-Demand Flow, and execute this **“Exit from a Flow”** action at the moment a customer makes a purchase. This would allow another running Segment Flow to be terminated in an almost near real-time manner.

This could potentially be built much more simply compared to implementing a custom API-based solution.

In particular, for exit criteria and decision logic using data graphs, some fields may only be updated approximately once per day depending on the data source. In scenarios where you want to **immediately exclude someone from a flow**, this mechanism may work very effectively.

It can also be used for cases such as segmenting customers who encountered some kind of issue or exception condition and forcibly excluding them from the Segment Flow side.

Rather than viewing it as just a simple stop control mechanism, I personally felt this is a very interesting feature when viewed as a **control mechanism for supplementing real-time behavior**.

That’s all for this time.

Stay tuned for more Salesforce Marketing Cloud tips! 😎

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
