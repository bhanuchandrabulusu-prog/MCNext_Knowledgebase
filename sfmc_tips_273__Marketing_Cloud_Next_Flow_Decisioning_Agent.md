# SFMC Tips #273 : Marketing Cloud Next: Flow Decisioning Agent

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-next-flow-decisioning-agent-0d0ace1b85e9

---

# SFMC Tips #273 : Marketing Cloud Next: Flow Decisioning Agent

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--0d0ace1b85e9---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--0d0ace1b85e9---------------------------------------)

11 min read

·

Apr 2, 2026

--

Photo by [Ameer Basheer](https://unsplash.com/@24ameer?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

First, to clarify from the beginning, there is no official feature called a “Flow Decisioning Agent”. What is explained in this article is a Marketing Cloud Next-oriented mechanism of the “[Journey Decisioning Agent](/@marketingcloudtips/marketing-cloud-next-journey-decisioning-agent-0226e5f82cd2)” that was introduced in a previous article.

In this article, I will review the previous article while explaining the setup method. To summarize again, as a new feature in Winter ’26, the “Journey Decisioning Agent” was introduced, which uses Agentforce to allow AI to select the optimal journey for each customer.

In traditional segment-triggered flows and Journey Builder in Marketing Cloud Engagement, the design is based on predefined conditional branching to segment customers.

For example:

- **① If the number of purchases is 3 or more, then Journey A**
- **② Otherwise, Journey B**

However, in reality, each customer’s situation is complex as follows:

- **Has not purchased recently but frequently opens emails**
- **Had a high purchase amount in the past but recent engagement is low**
- **Responds well to discount campaigns but not to brand messaging**
- **Even among dormant customers, the next best action differs from person to person**

In such situations, there are cases where simple branching alone cannot fully represent the scenario.

By using the Journey Decisioning Agent, **Agentforce can determine which journey is optimal based on real-time behavioral profiles and context**.

The same concept applies to the flow version explained this time. The Journey Decisioning Agent selects the optimal flow and **uses engagement signals as triggers to activate the flow**.

Now, in the main section, I will explain this “**Flow version of the Journey Decisioning Agent**” in detail.

## Features of the Journey Decisioning Agent

The Journey Decisioning Agent mainly provides the following two capabilities:

### 1. Select the optimal flow/journey

Based on customer attributes, behavior, engagement tendencies, and context on Data 360, it selects the optimal flow/journey from multiple candidates. This is the most fundamental function.

### 2. Generate content for that customer

In addition, it can create custom content such as subject lines, preheaders, and body copy for the selected journey.

> *The third item, Personalization: Get Context, is an action used to retrieve customer context from the data graph.*

In this flow version, unlike the Marketing Cloud Engagement version, please note that the focus is on “selecting the optimal flow”.

## Use Case

This time, I will consider a use case involving dormant customers for an e-commerce site.

For example, suppose you want to encourage repurchases from customers who have not purchased for more than 90 days. However, applying the same campaign to all dormant customers is not always optimal.

For instance, there may be differences such as:

- **Customers who previously responded well to coupon campaigns**
- **Customers who recently opened emails but did not purchase**
- **High-spending loyal customers**
- **Customers with very low engagement who first need their relationship with the brand warmed up again**

In this case, the following journey candidates can be prepared.

### ① Coupon Repurchase Journey

- Send a limited coupon to customers who are highly responsive to discount campaigns.

### ② New Product Recommendation Journey

- Recommend products that match their interests based on recent browsing and email engagement trends.

### ③ Early Access Journey for Loyal Customers

- Encourage revisits through exclusivity and early access rather than discounts.

### ④ Re-engagement Journey

- Instead of immediate promotion, first rebuild interest in the brand.

The **Journey Decisioning Agent** determines which journey is most suitable for each customer from among these candidates.

This represents the concept of selecting the **“next best action”**, rather than simply extending traditional IF conditions.

## Overall Architecture

The overall structure when using the Journey Decisioning Agent is as follows:

### Step 1. Make customer information available in Data 360

First, make customer attributes, behavioral history, and interests available on the Data 360 side. This uses data graphs.

*In Journey Decisioning, this context is very important.*

### Step 2. Enable the Journey Decisioning Agent

Enable Agentforce-related features on the Marketing Cloud Next side and activate the Journey Decisioning Agent.

*Tips: First enable Agentforce Employee Agent (AEA).  
This allows you to use marketing-related agent templates.*

### Step 3. Register use cases

Here, register both the “summary” and “expected outcome” of the flows that the agent will select from. Up to 5 can be configured.

### Step 4. Call the agent from Flow

Execute the Journey\_Decisioning\_Agent action in Flow Builder to select the optimal flow for each target customer.

### Step 5. Use the result in Flow

The results of the routing are stored in Data 360 DLO/DMO, and based on that, engagement signals are triggered, which then activate event-triggered flows.

## Use of Data Graph

First, in Journey Decisioning, appropriate decisions cannot be made without information about the customer. Therefore, it is necessary to prepare a **data graph** on the Data 360 side that contains the information to be evaluated.

In this example, the following types of information can be considered:

- **Last purchase date**
- **Total purchase amount**
- **Preferred categories**
- **Open behavior**
- **Click behavior**
- **Membership tier**
- **Region**
- **Response to past campaigns**

Based on this information, Agentforce understands the context of each customer and selects the optimal journey.

## Configuration

In the Journey Decisioning Agent, the **Personalization: Get Context action** is used to retrieve context.

The **Marketing Cloud: Journey Decisioning topic** includes the following instructions. Replace the following two:

- **{DataGraph API Name}**
- **{Agent Version ID}**

To find the **DataGraph API reference name**, open Data 360, navigate to the **Data Graph** tab, locate the appropriate data graph, and use the exact name shown in the **Data Graph API Reference Name** field.

Find the agent version ID in the URL. It is the ID immediately following “versionId=” in the URL.

https://xxxxx.lightning.force.com/AiCopilot/copilotStudio.app#/copilot/builder?copilotId=0XxHp000000e2F3KAI&versionId=0X9Hp000000ebw6KAA

![]()

## Creating Use Cases

In the Journey Decisioning Agent, the summary of each flow and the expected results are extremely important.

This is because the agent looks at these descriptions to understand:

- **What this flow is for**
- **What kind of customers it is suitable for**
- **What kind of outcomes are expected**

For example, the following description is not good.

### Poor Example

- **Overview**  
  Email for dormant customers
- **Expected Result**  
  Encourage repurchase

With this, the difference from other flows is hardly conveyed.

On the other hand, the following example is clearer.

### ① Coupon Repurchase Journey

- **Overview**  
  This journey sends an email with a limited coupon to dormant customers who have not made a purchase for more than 90 days but have historically responded well to coupons or sales campaigns. Rather than simply announcing a discount, it presents a clear reason to repurchase by highlighting that a special benefit is currently available.
- **Expected Result**  
  Increase the repurchase rate among dormant customers who respond well to price incentives and restore contact with customers who are beginning to disengage.

### ② New Product Recommendation Journey

- **Overview**  
  This journey targets customers who have recently opened emails or browsed products but have not yet made a purchase. It promotes new products that align with their interests and browsing behavior. Instead of focusing on discounts, it aims to naturally lead to purchasing behavior by recommending products or categories currently relevant to the customer.
- **Expected Result**  
  Convert highly interested customers into buyers and encourage customers who are currently only browsing to move to the next action.

### ③ Early Access Journey for Loyal Customers

- **Overview**  
  This journey targets customers with high cumulative purchase amounts and strong brand loyalty. Instead of offering general discount campaigns, it sends exclusive early access information with a sense of exclusivity or privilege. Examples include early access to new products, member-exclusive offers, and invitations to special events.
- **Expected Result**  
  Promote continued purchasing while maintaining brand value and further strengthen long-term relationships with loyal customers.

### ④ Re-engagement Journey

- **Overview**  
  This journey targets customers whose email opens, clicks, and purchases have all declined. Rather than immediately applying strong promotional messaging, it focuses on reintroducing the appeal of the brand and products. Through popular products, curated content, usage scenarios, and editorial content, it gradually rebuilds customer interest.
- **Expected Result**  
  Restore contact with low-engagement customers and improve engagement metrics such as open and click rates while preparing them to respond to future promotional campaigns.

In this way, it is important to write so that the differences in the role of each flow are clearly conveyed.

## Setup Method

1. Go to **Settings > Agentforce & Gen AI**, scroll to the Journey Decisioning section, and **install the data kit**.

- **Journey Decisioning Agent Decision Bundle (DSO, DLO, DMO)**

2. Enter the **use case name** and **description**.

- **Use Case Name**Optimization of Repurchase Promotion Journeys for Dormant Customers
- **Description**This use case selects the most appropriate journey based on each customer’s engagement tendencies and level of interest rather than applying the same campaign to all dormant customers who have not purchased for a certain period. Customers who respond well to coupon campaigns receive price-focused messaging, customers with high product interest receive recommendations, loyal customers receive exclusive early access messages, and customers with declining engagement receive re-engagement campaigns. The goal is to improve repurchase rates and engagement.

3. Select **Marketing Cloud (Next)** as the marketing environment to be used.

4. Add 3 to 5 flows that the agent can select, along with summaries and expected results, and save.

5. Once the setup is complete, two types of flows are automatically generated. There is basically no need to modify the contents of these flows.

6. In addition, **engagement signals** corresponding to the flows that the agent can select are created. They are created starting with “**[AF] JourneyDecisioning …**”, so they are easy to identify.

## Flow Setup

1. First, create a new event-triggered flow that the AI will select. For the start element, select each engagement signal and create the scenario.

2. In the email used in this event-triggered flow, it is better to set the same engagement signal as the start element in the data source using the event data provider.

3. Next, create a segment-triggered flow, place a new action element, and configure the Journey\_Decisioning\_Agent action.

*It will not be displayed unless the Journey Decisioning Agent is enabled.*

Set the following text as input values.

- Sample input value  
  **Use case: 1WoHp0000008OIFKA2** (← this is the use case ID)  
  **Select the best journey for the subscriber with unifiedIndividualId {!$Record.ssot\_\_Id\_\_c}.  
  Use individualId only to retrieve personalized context.**

4. This completes the setup. Execute the segment-triggered flow.

5. Then, the agent reads the use case and sends each individual to the most optimal flow. Success.

![]()

In the Marketing Cloud Engagement version, the information determined by the Journey Decisioning Agent was stored in Data Extensions. On the other hand, in the Marketing Cloud Next version, the results are stored in the following:

- **“Journey Decisioning Agent-JourneyDecisio” DLO**
- **“Journey Decisioning Agent Decision” DMO**

It can be understood that engagement signals are ultimately triggered based on the data in this DMO.

At this point, those who are familiar may consider placing a decision element in the latter part of the segment-triggered flow and branching there.

However, for branching using decision elements to function correctly, **the data graph must be updated in real time**. This is because decision elements use values from the data graph.

Therefore, in this architecture, it is considered that **this constraint is avoided by using engagement signals to immediately trigger the next event and pass processing to the event-triggered flow**.

It is theoretically possible to complete everything within a single flow by providing sufficient wait time (for example, about 24 hours).

However, at present, there is an issue that the “Journey Decisioning Agent Decision” DMO cannot be connected in the data graph (Recency Field cannot be set), and I am also struggling to address this point.

## Considerations

The Journey Decisioning Agent is a very interesting feature, but making it too complex from the beginning can make it difficult to understand.

Therefore, it is recommended to start as follows:

- **Limit candidate journeys to around 3–4**
- **Clearly differentiate the purpose of each journey**
- **Limit the customer data used for decisioning**
- **Start by testing only journey selection**
- **Expand to content generation once familiar**

Especially at the beginning,  
it is easier to understand if the design allows you to explain:

“Why this customer was selected for this journey”

## Conclusion

The Journey Decisioning Agent is a mechanism that allows Agentforce to select the optimal flow/journey for each customer.

Its major feature is that it can determine which flow/journey to proceed with by considering behavior patterns, attributes, engagement, loyalty, and context on Data 360, which cannot be fully expressed by simple conditional branching.

On the other hand, like AI features such as STO, it is essential to consider how much to trust AI decisions. In other words, it is necessary to carefully consider, at the same level of granularity, how much of the AI-selected branching should be entrusted to operations.

As mentioned in the considerations above, it is important to first design in a way that makes it easy to explain “why this customer was selected for this flow/journey”. Then, while sufficiently verifying whether the actual selection results are as expected, it is better to gradually expand its use.

*Note: The use of the Journey Decisioning Agent consumes Flex Credits, so cost considerations are necessary when using it for large-scale sending.*

That’s all for now.

Stay tuned for more Salesforce Marketing Cloud tips! 😎

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
