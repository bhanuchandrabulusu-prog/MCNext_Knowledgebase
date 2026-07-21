# SFMC Tips #293 : Marketing Cloud Next: Retrieving a Specific Record from a Data Graph in Marketing…

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-next-retrieving-a-specific-record-from-a-data-graph-in-marketing-flows-e03c87cea117

---

# SFMC Tips #293 : Marketing Cloud Next: Retrieving a Specific Record from a Data Graph in Marketing Flows

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--e03c87cea117---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--e03c87cea117---------------------------------------)

5 min read

·

May 14, 2026

--

Photo by [Jon Tyson](https://unsplash.com/@jontyson?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

With the [Summer ’26 new feature release](/@marketingcloudtips/marketing-cloud-next-summer-26-release-highlights-04f6c5abdee6) for **Marketing Cloud Next Growth & Advanced Editions**, source data such as **Data Graphs** can now be narrowed down in advance using **“sorting”** and **“search conditions (filtering)”** within the Flow **“Resource Manager”** and **“Resource Selection Fields”.**

This makes it possible to retrieve and utilize **“one specific record that you want to use in the flow”** from sources that contain multiple records, such as Data Graphs.

For example:

- **“Most recently purchased product”**
- **“Latest login history”**
- **“Highest-value order information”**

It is now possible to select and handle **“one representative record”** from array data, which improves the flexibility of personalization and conditional branching within flows.

### **Important**

This mechanism is only available in the following flow types:

- **Segment Triggered Flow**
- **Activation Triggered Flow**

## Previous Limitation

For example, consider the case where a Data Graph is used in a **“Decision”** element.

With the previous mechanism, related attributes in the Data Graph were treated as **arrays (multiple records).**

Therefore, even if multiple purchase histories existed in **“Sales Order Product Engagement”,** the only thing that could be evaluated was:

***“Whether at least one record among multiple records matches the condition.”***

In other words, it was not possible to perform detailed condition evaluations targeting **“one specific record”,** such as:

- **“I only want to look at the latest purchase history”**
- **“I want to branch based on the newest order record”**
- **“I only want to target the highest-value order”**

When directly selecting the Data Graph, it looked like the following.

So, with this new feature, it has now become possible to:

***“Extract one representative record from multiple records for use within the flow.”***

In fact, this concept itself had already been introduced earlier on the **Content Builder** side.

For example, when creating a content **“Expression”** or configuring personalization fields, you have probably already configured:

- **Sorting**
- **Search Conditions (Filtering)**

The same mechanism has finally been introduced into flows as well.

[## SFMC Tips #133 : Marketing Cloud Next: Harnessing Reusable “Expression” Content

### In Marketing Cloud Next (Marketing Cloud Growth & Advanced Edition), reusable “Expression” content enables you to save…

medium.com](/@marketingcloudtips/marketing-cloud-on-core-harnessing-reusable-expression-content-c9c26098cb5a?source=post_page-----e03c87cea117---------------------------------------)

## Configuration Steps

### 1. Open Resource Manager and click “New Resource”.

### 2. As a resource type, a new option called “Collection Filter Criteria” has been added.

In Salesforce Help, this is introduced under the name **“Selected Record”.**

![]()

### 3. Here, you can select “related attributes in a Data Graph” as the data source.

Needless to say, direct attributes are unrelated to today’s topic.

![]()

### 4. This time, since we want to retrieve the “most recently purchased product”

(API Name: **latestPurchasedProductName**), select **“Sales Order Product Engagement”.**

Select **“Entire Resource”** and complete the setup.

![]()

### 5. After selecting the DMO, the following areas will appear at the bottom of the screen:

- **Top section: Sort Conditions — required**
- **Bottom section: Filter Conditions — optional**

### 6. The important points here are as follows.

### Important Notes for “Sort Conditions”

- You can only select fields from the **exact same DMO** as the data source.  
  Although the UI allows you to select fields from other DMOs, doing so will actually result in an error.

### Important Notes for “Filter Conditions”

- You can use fields from **all DMOs that were traversed while selecting the data source.**However, fields from DMOs that were not traversed will result in errors.

Please configure the settings with this in mind.

### 7. This time, we simply configure “Record Created Date” in descending order.

In other words, the configuration is:

***“Retrieve the newest purchase history as the representative record”***

![]()

### 8. This creates “latestPurchasedProductName” as a “Collection Filter Criteria” resource generated from Data Graph data.

### 9. This time, we will use this resource in a “Decision” element.

Other use cases, such as using it in an **“Assignment”** element, are also possible.

### 10. From the one representative record retrieved in “latestPurchasedProductName”, select the “Product” field.

### 11. Then specify the product name that should match the “most recently purchased product”.

### 12. This now makes it possible to branch only when:

***“The latest purchased product is ○○.”***

What did you think?

I believe this is one of those **“small but extremely useful”** types of features.

It is not a flashy feature with immediate impact, but when you think:

- **“Can’t I perform this kind of conditional evaluation?”**
- **“I only want to use the latest record”.**
- **“I want to select only one record from multiple records”.**

it is important to remember:

***“Oh right, there was such a mechanism in Resource Manager 🤔”***

Conversely, if you never become aware of the feature called **“Collection Filter Criteria (Selected Record)”,** it may very well become a feature you never use for your entire life.

Especially if you want to implement **advanced personalization** or **conditional branching using Data Graphs**, I believe this will become a very important mechanism going forward.

That is all for this time.

Stay tuned for more Salesforce Marketing Cloud tips! 😎

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
