# SFMC Tips #265 : Marketing Cloud Next: Journey Decisioning Agent

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-next-journey-decisioning-agent-0226e5f82cd2

---

# SFMC Tips #265 : Marketing Cloud Next: Journey Decisioning Agent

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--0226e5f82cd2---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--0226e5f82cd2---------------------------------------)

11 min read

·

Mar 10, 2026

--

Photo by [Toni G](https://unsplash.com/@ton1_g?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

In the Winter ’26 new feature release of Marketing Cloud Next, a **Journey Decisioning Agent** has been introduced that leverages Agentforce capabilities to dynamically select the most appropriate journey for each customer.

In the traditional Journey Builder, customers are segmented based on predefined conditional branches. For example, it would be designed like the following:

- **① If the number of purchases is 3 or more → Journey A**
- **② Otherwise → Journey B**

However, in reality, each customer’s situation is more complex, such as:

- **Has not purchased recently but frequently opens emails**
- **Had a high purchase amount in the past but recent engagement is low**
- **Responds well to discount campaigns but not to brand messaging**
- **Even among dormant customers, the next best action differs from person to person**

In these situations, simple conditional branching cannot fully represent the differences.

By using the **Journey Decisioning Agent**, Agentforce can determine which journey is most appropriate based on real-time behavioral profiles and context.

In this article, I will explain the Journey Decisioning Agent.

## Capabilities of the Journey Decisioning Agent

There are mainly two things that can be done with the Journey Decisioning Agent.

### 1. Select the most appropriate journey

Based on customer attributes, behaviors, engagement trends, and context within Data 360, the agent selects the optimal journey from multiple candidates.

### 2. Generate content for that customer

For the selected journey, it can create custom content such as the subject line, preheader, and body copy.

> *Tips: The third action,* ***Get Context****, retrieves the customer context from the data graph.*

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

The overall structure when using the Journey Decisioning Agent is as follows.

### Step 1. Make customer information available in Data 360

First, ensure that customer attributes, behavioral history, and interests can be referenced in Data 360.  
 This is done using a **data graph**.

*In Journey Decisioning, this context is important.*

### Step 2. Enable the Journey Decisioning Agent

Enable Agentforce-related features in Marketing Cloud Next and activate the Journey Decisioning Agent.

> ***Tips:*** *First enable* ***Agentforce Employee Agent (AEA)****.  
> This allows the use of marketing-related agent templates.*

### Step 3. Register use cases

Register the journeys that the agent can select along with their **overview** and **expected results**.  
Up to **five journeys** can be configured.

> ***Important:*** *The journeys selectable here must be journeys that already have an* ***API Event Entry Source*** *configured as described in the previous* ***Send to Journey action*** *article.*

### Step 4. Call the agent from Flow

Execute the agent action in Flow Builder so the agent selects the most appropriate journey for each target customer.

### Step 5. Use the result in Journey Builder

The distribution results and generated content are stored in data extensions and can be used within journeys in Marketing Cloud Engagement.

## Using the Data Graph

In Journey Decisioning, decisions cannot be made appropriately without information about the customer.  
Therefore, a **data graph** containing relevant information must be prepared in Data 360.

For the example in this article, the following information may be used:

- **Last purchase date**
- **Total purchase amount**
- **Preferred categories**
- **Email open trends**
- **Click trends**
- **Membership tier**
- **Region**
- **Response to past campaigns**

Based on this information, Agentforce understands the context of each customer and selects the most appropriate journey.

## Configuration Method

In the Journey Decisioning Agent, the **Personalization: Get Context** action is used to retrieve context.

Within the **Marketing Cloud: Journey Decisioning** topic, the following instructions are included.  
The following two values must be replaced:

- **{DataGraph API Name}**
- **{Agent Version ID}**

To find the **DataGraph API reference name**, open Data 360, navigate to the **Data Graph** tab, locate the appropriate data graph, and use the exact name shown in the **Data Graph API Reference Name** field.

You can find the **Agent Version ID** in the URL.  
 It is the ID that appears immediately after **versionId=**.

https://xxxxx.lightning.force.com/AiCopilot/copilotStudio.app#/copilot/builder?copilotId=0XxHp000000e2F3KAI&versionId=0X9Hp000000ebw6KAA

![]()

## Creating Use Cases

In the Journey Decisioning Agent, the **overview and expected results of each journey are extremely important**.

This is because the agent reads these descriptions to understand:

- **What the journey is intended for**
- **Which customers it is suitable for**
- **What results are expected**

For example, the following description is not good.

### Poor Example

- **Overview**  
  Email for dormant customers
- **Expected Result**  
  Encourage repurchase

This description does not clearly convey the difference from other journeys.

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

It is important to **write the descriptions in a way that clearly communicates the role of each journey**.

## Configuration Steps

### 1. Install the Data Kit

Navigate to **Setup → Agentforce & Gen AI**, scroll to the **Journey Decisioning** section, and install the data kit.

- **Journey Decisioning Agent Decision Bundle (DSO, DLO, DMO)**

### 2. Define the Use Case

Enter the **use case name** and **overview**.

- **Use Case Name**Optimization of Repurchase Promotion Journeys for Dormant Customers
- **Description**This use case selects the most appropriate journey based on each customer’s engagement tendencies and level of interest rather than applying the same campaign to all dormant customers who have not purchased for a certain period. Customers who respond well to coupon campaigns receive price-focused messaging, customers with high product interest receive recommendations, loyal customers receive exclusive early access messages, and customers with declining engagement receive re-engagement campaigns. The goal is to improve repurchase rates and engagement.

### 3. Select the Marketing Environment

Select **Marketing Cloud Engagement** as the marketing environment and choose the **business unit**.

### 4. Configure Selectable Journeys

Add **3–5 journeys** that the agent can select.

For each journey, enter the **overview** and **expected results**, then save the configuration.

## Components Generated After Configuration

After completing the configuration, several components are automatically generated.

### ① Journey Decisioning Flow

This flow assigns subscribers to the most appropriate journey.

One flow is created for **each use case**.

![]()

### ② Content Creation Flow

This flow generates **personalized content** for each subscriber.

One flow is created for **each use case**.

![]()

Additionally, an **AF JourneyDecisioning** folder is automatically created in **Marketing Cloud Engagement**.

### ③ Journey Decisioning Data Extension

This data extension stores information about **which journey each subscriber is assigned to by Agentforce**.

### ④ Content Creation Data Extension

This data extension stores the **subject line, preheader, and message body** that can be used in **Journey Builder** for each subscriber.

Finally, confirm that **all four components above have been generated successfully**.

## Flow Configuration

In Flow Builder, start a **segment-triggered flow** or **event-triggered flow**, add a new element, and call the **Journey Decisioning Agent action**.

If the Journey Decisioning Agent is not enabled, it will not appear.

## Sample Input Value Text

When using the Journey Decisioning Agent action in Flow, a sentence-like input text must be provided.

The official help page provides the following examples.

### 1. Journey Selection Input Value Example

- **Action**  
  Journey Selection
- **Sample Input Value**  
  Using usecase {usecaseId}, select the best journey for the subscriber with unifiedIndividualId {unifiedIndividualId}. Use individualId {individualId} only for retrieving personalized context.

### 2. Journey Content Creation Input Value Example

- **Action**  
  Journey Content Creation
- **Sample Input Value**  
  Using usecase {usecaseId}, create journey email content on selectedJourneyId {selectedJourneyId} for the subscriber with unifiedIndividualId {unifiedIndividualId}. The email content should consider user preferences, given that they like [enter specifics here]. Use individualId {individualId} only for retrieving personalized context.

## About Replacing Placeholders

In the Journey Content Creation sample, the part **[enter specifics here]** should not be left as is.

It should be replaced with information that reflects the subscriber’s characteristics.

For example:

- Likes running
- Likes hiking
- Interested in outdoor activities
- Lives in the Northwest region
- Interested in sportswear

The key point is to include **specific information that represents the subscriber**.  
This helps generate content that is better aligned with that individual.

## Practical Points

In **Journey Selection**, you provide the information needed to determine **which journey should be selected**.

In contrast, **Journey Content Creation** specifies **what type of content should be generated for the selected journey**.

Therefore, adding more specific information such as subscriber preferences and interests improves the accuracy of personalization.

## Journey Builder Configuration

The routing results and generated content selected by the Journey Decisioning Agent are stored in the previously mentioned **Journey Decisioning Data Extension** and **Content Creation Data Extension**.

**Example of Journey Decisioning Data Extension**

**Example of Content Creation Data Extension**

These can then be used within journeys and emails in Marketing Cloud Engagement.

For example:

- **Route recipients based on the selected Journey ID**
- **Load subject lines and preheaders from the data extension**
- **Insert portions of the body text using AMPscript**

In other words, this feature does not replace Journey Builder.  
Rather, it is easier to understand it as **a mechanism where Agentforce generates the decision results that are then passed to Journey Builder**.

## Considerations

The Journey Decisioning Agent is a very interesting feature. However, making it too complex from the beginning can make it harder to understand.

Therefore, it is recommended to start with the following approach:

- **Limit candidate journeys to around 3–4**
- **Clearly differentiate the purpose of each journey**
- **Limit the customer data used for decisioning**
- **Start by testing only journey selection**
- **Expand to content generation once familiar**

Especially at the beginning, it is helpful to design the system so that it is easy to explain **why a particular customer was selected for a specific journey**.

## Conclusion

The Journey Decisioning Agent is a mechanism that allows Agentforce to select the most appropriate journey for each customer.

Its key feature is the ability to determine which journey a customer should enter based on **behavioral patterns, attributes, engagement levels, loyalty, and context within Data 360**, which cannot be fully expressed through simple conditional branching.

However, as with AI features such as STO, it is also important to consider **how much trust should be placed in AI decisions**. In other words, careful thought is required regarding how much operational decision-making should be delegated to AI.

As mentioned in the considerations above, it is important to design the system in a way that makes it easy to explain **why a particular customer was selected for a particular journey**. Then, while verifying that the actual results match expectations, it is best to expand its usage gradually.

> Note: Flex Credits are consumed when using the Journey Decisioning Agent, so cost considerations are necessary when using it for large-scale sends.

That is all for this time.

Stay tuned for more Salesforce Marketing Cloud tips! 😎

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
