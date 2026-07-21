# SFMC Tips #175 : Marketing Cloud Next: Understanding the Basics of Personalization

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-next-understanding-the-basics-of-personalization-8bc5141ab807

---

# SFMC Tips #175 : Marketing Cloud Next: Understanding the Basics of Personalization

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--8bc5141ab807---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--8bc5141ab807---------------------------------------)

6 min read

·

Sep 24, 2025

--

Photo by [ManSan Lu](https://unsplash.com/@lums?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

With **Salesforce Personalization** (formerly Einstein Personalization), which was announced in Winter ’25 (2024) as natively integrated with Marketing Cloud Next, you can leverage deep learning and business logic to generate optimized recommendations for each individual user.

> *In Spring ’25, the product name officially changed from Einstein Personalization to Salesforce Personalization.*

A key strength of this solution is its ability to incorporate both user behavior data and business context, enabling optimized, personalized recommendations across multiple channels — such as email (Growth & Advanced Editions) and websites (via [Web Personalization Manager](https://mcp.hubs.vidyard.com/watch/KX7UUeodqjdSFmddjG2ayF)).

> ***Note:*** *Salesforce Personalization requires implementation of the* ***Salesforce Interactions SDK****. For setup details, please refer to the* [*developer documentation*](https://developer.salesforce.com/docs/marketing/einstein-personalization/guide/overview.html)*.*

### **Example Use Cases**

- **E-commerce:** Optimize cross-sell and upsell opportunities to increase average order value.
- **Media sites:** Suggest related content based on browsing history to improve engagement and session depth.
- **Financial services:** Recommend products aligned with user profiles to strengthen conversion rates.

The following sections will provide a structured overview of the fundamental mechanisms of Personalization.

## How Recommenders Work

### **① Objective-Based Recommendations**

This type of recommender leverages **deep learning** to automatically generate personalized recommendations for each user. The optimization is aligned with business objectives — such as maximizing revenue or improving click-through rates — making it particularly effective when aiming to drive measurable results.

- You can use **pre-defined objectives**
- Or configure your own **custom objectives**

👉 [[Learn more about Objective-Based Recommenders (Salesforce Help)](https://help.salesforce.com/s/articleView?id=mktg.persnl_recommender_configure_objective_based.htm&type=5)]

> ***Important:*** *To use objective-based recommendations, you must first complete a* ***training period****. During training, the recommender needs to reference data across engagement objects and must have at least three types of engagement activities recorded (e.g., page views, add-to-cart actions, purchases).*

### **② Rule-Based Recommendations**

This type of recommender relies on **mathematical calculations**, such as pre-computed insights or ranking logic, to display recommendations based on defined rules. Examples include **“Top-selling products”** or **“Most viewed articles”**, which provide recommendations grounded in clear, easy-to-understand criteria.

👉 [[Learn more about Rule-Based Recommenders (Salesforce Help)](https://help.salesforce.com/s/articleView?id=mktg.persnl_recommender_configure_rule_based.htm&type=5)]

**Additional Resources**  
For a deeper understanding, I recommend watching the following videos:

### Using Pre-defined Objectives

Salesforce Personalization comes with two default objectives out of the box: **Maximize Revenue** and **Maximize Clicks**.

> *To use these, you’ll need to complete the setup described in the* [*Help documentation*](https://help.salesforce.com/s/articleView?id=mktg.persnl_setup_obj_based_recommender_data_graphs.htm&type=5)*.*

### Defining Custom Objectives

With the **Spring ’25 release**, you can now define **custom objectives** tailored to your own business requirements.

### **Steps to Define a Custom Objective**

**1. Create engagement signals** (the user behaviors you want to track)

- Examples: product detail views, add-to-cart actions, purchases

**2. Specify maximize/minimize parameters**

- Examples: maximize purchase actions, minimize churn behaviors

**3. Aggregate signals into metrics and feed into model training**

- The tracked behaviors are consolidated into metrics and used by the machine learning model for optimization

Through this mechanism, you can achieve optimization aligned with your unique KPIs — such as **increasing first-time purchase rates** for new customers or **driving repeat purchases** from existing ones.

## Recommender Filters

Within recommender settings, you can configure **filters** to more precisely control the content that is displayed. By flexibly adjusting what to include and what to exclude, you can further enhance the user experience. This is an **optional** configuration.

### **Types of Filters (3 categories)**

**1. Static**  
 Narrow results using fixed attributes.

- Example: include products priced above ¥1,500, exclude articles published before a specific date

**2. Decision Context**  
 Filter based on the user’s current browsing context.

- Example: display products in the same color as the one currently being viewed, include articles by the same author

**3. Profile Data Graph**  
 Leverage the user’s profile data and historical activity.

- Example: exclude products purchased within the past 30 days

👉 [[Learn more about Recommender Filters (Salesforce Help)](https://help.salesforce.com/s/articleView?id=mktg.persnl_recommender_filters_configure.htm&type=5)]

## Leveraging Personalization Points

### **Role of Personalization Points**

A **Personalization Point** acts as a framework — a container that brings together the key elements of personalization. It includes the following components:

- **Data Space**
- **Profile Data Graph**
- **Personalization Type**
- **Response Template**

👉 [[Learn more about Personalization Points (Salesforce Help)](https://help.salesforce.com/s/articleView?id=mktg.persnl_personalization_point.htm&type=5)]

### **Personalization Type & Response Template**

- **Personalization Type:** Defines the type of content to be displayed (Recommendations or Manual Content).
- **Response Template** (formerly known as Personalization Schema): Determines the fields returned as personalized data. For recommendations, only the DMO (Decision Model Object) used as the root object of the Item Data Graph can be selected.

### **Decisions & Targeting Rules**

- **Decision:** A label for each targeting rule.
- **Targeting Rule:** Defines under which conditions specific content will be displayed.

### **Multiple Decisions and Prioritization**

You can add multiple decisions to a single Personalization Point.

- Priority is assigned in the order of creation (the first one created is top priority).
- The order can be rearranged at any time, allowing you to adjust priority dynamically.

**Additional Resources**  
For a deeper understanding, I recommend watching the following videos:

**Tip: Using Manual Content**  
Personalization Points and Decisions can also be leveraged to deliver **manual content** (such as background images, links, or call-to-action text). By combining automated and manual approaches, you can achieve even more effective personalization.

### Monitoring Credit Consumption

With **Digital Wallet**, you can now monitor Salesforce Personalization credit consumption in near real time. Detailed usage breakdowns are displayed by type and time period, allowing you to easily track trends over a given timeframe.

## Wrapping Up

Some of the features introduced here are also leveraged within **Dynamic Content** in Marketing Cloud Growth & Advanced Editions, as well as in **Path Experiments** within Segment-Triggered Flows — showing how these capabilities are interconnected. For a deeper dive, I’ve covered this in the following article:

[## SFMC Tips #174 : Marketing Cloud Next: How to Set Up Dynamic Content

### In Marketing Cloud Next (Marketing Cloud Growth & Advanced Edition), you can create dynamic content tailored to the…

medium.com](/@marketingcloudtips/marketing-cloud-next-how-to-set-up-dynamic-content-3c8ba2c53036?source=post_page-----8bc5141ab807---------------------------------------)

### Want to Learn More?

To further deepen your understanding, I recommend exploring both the official Salesforce Help documentation and the following **Trailhead module**:

[## Salesforce Personalization in Marketing Cloud Next: Quick Look

### Discover how Salesforce Personalization leverages AI and Data Cloud to create tailored customer experiences. Boost…

trailhead.salesforce.com](https://trailhead.salesforce.com/content/learn/modules/einstein-personalization-quick-look?source=post_page-----8bc5141ab807---------------------------------------)

Additionally, the curated video collection in **“Personalization — Partner Enablement”** (introduced earlier in this article) is an extremely valuable resource worth checking out:

[## Personalization - Partner Enablement

### Join our Salesforce Product Managers as they give a complete overview of the Salesforce Personalization platform…

mcp.hubs.vidyard.com](https://mcp.hubs.vidyard.com/?source=post_page-----8bc5141ab807---------------------------------------)

That’s all for this time.

Stay tuned for more Salesforce Marketing Cloud tips! 😊

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
