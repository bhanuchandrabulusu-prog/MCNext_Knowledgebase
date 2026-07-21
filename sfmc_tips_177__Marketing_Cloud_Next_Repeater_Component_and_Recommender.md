# SFMC Tips #177 : Marketing Cloud Next: Repeater Component and Recommender

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-next-repeater-component-and-recommender-fb41b9c72ad0

---

# SFMC Tips #177 : Marketing Cloud Next: Repeater Component and Recommender

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--fb41b9c72ad0---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--fb41b9c72ad0---------------------------------------)

9 min read

·

Sep 26, 2025

--

Photo by [Ferhat Deniz Fors](https://unsplash.com/@ferhat?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

In **Marketing Cloud Next (Marketing Cloud Growth & Advanced Edition)**, you can take advantage of the **Recommender** feature — part of **Salesforce Personalization** (formerly known as Einstein Personalization).

By combining **deep learning (AI)** with **business logic (mathematical calculations)**, it enables the automatic generation of personalized recommendations for each user.

### Personalization Features Covered in This Article

- ✖️ Unified Individual Data Model Object (Direct Attributes)
- ✖️ [Data Graph](/p/1af8d9aa9026) (Direct & Related Attributes)
- ✖️ [Event Data](/@marketingcloudtips/marketing-cloud-on-core-personalization-part-2-8d0efb6402af)
- ️⭕ **Personalization Recommender (Salesforce Personalization)**

For the basics of Personalization, please see the article below.

[## SFMC Tips #175 : Marketing Cloud Next: Understanding the Basics of Personalization

### With Salesforce Personalization (formerly Einstein Personalization), which was announced in Winter ’25 (2024) as…

medium.com](/@marketingcloudtips/marketing-cloud-next-understanding-the-basics-of-personalization-8bc5141ab807?source=post_page-----fb41b9c72ad0---------------------------------------)

[## SFMC Tips #176 : Marketing Cloud Next: First Steps in Personalization Setup

### Marketing Cloud Next’s Personalization is an application that integrates with Data Cloud to deliver optimized…

medium.com](/@marketingcloudtips/marketing-cloud-next-initial-setup-for-personalization-be47931cef01?source=post_page-----fb41b9c72ad0---------------------------------------)

### Using “Recommender” in Growth & Advanced Editions Emails

When embedding a recommender into an email, it can currently only be used **within a “Repeater” component**. For more details on the Repeater component, refer to the article below.

[## SFMC Tips #134 : Marketing Cloud Next: Introducing the “Repeater” Component

### In Marketing Cloud Next (Marketing Cloud Growth & Advanced Edition), the Summer ’25 release introduces a brand-new…

medium.com](/@marketingcloudtips/marketing-cloud-on-core-introducing-the-repeater-component-cc8017b01dc4?source=post_page-----fb41b9c72ad0---------------------------------------)

### Key Considerations When Using Recommender

- **Available Edition**: Only supported in **Marketing Cloud Advanced Edition**
- **Credits**: Requires purchasing credits for Personalization
- **Data Source**: You can only select trained recommenders that are based on the same data graph as the email default
- **Training**: When using a new recommender, allow for at least one training period
- **Configuration Constraints**: Data sources can be replaced, but cannot be deleted once configured

In this article, I’ll walk you through the steps of **sending emails that leverage the Recommender**.

## How to Configure a Recommender

In this example, I’ll use a relatively simple “**rule-based recommender”** to display items in order of **highest total sales value**.

Additionally, I’ll combine conditions such as **only targeting products available for online sales** and **displaying lists tailored to user preferences**.

### Data Graphs Required for Recommender Setup

To use a recommender, you’ll need the following two types of data graphs:

- **Profile Data Graph**
- **Item Data Graph**

### 1. Profile Data Graph

For the **Profile Data Graph**, you can use the “**default (basic) data graph**” that was registered during the initial setup of Marketing Cloud. For basic instructions on how to configure a data graph, please refer to the guide below.

[## Marketing Cloud on Core: Personalization

### Photo by Nathan Lee on Unsplash

medium.com](/@marketingcloudtips/marketing-cloud-on-core-personalization-1af8d9aa9026?source=post_page-----fb41b9c72ad0---------------------------------------)

In this example, I’ll include a preference field called “**Favorite Genre**”.

> ***Tips:*** *In general personalization use cases, you would use a* ***real-time profile data graph****. However, in cases like this where real-time responsiveness is not required, the* ***standard data graph*** *is sufficient. Of course, you can switch to a real-time data graph if needed, while considering cost implications. If you do so, don’t forget to update the default data graph settings as well.*

### 2. Item Data Graph

Next is the **Item Data Graph**.  
This graph stores the items that will be displayed in the content as a DMO (Data Model Object). Any fields you check here can be used within the **Repeater component**.

Examples of standard DMOs commonly set as the primary DMO include:

- **Goods Product DMO** (Product Information)
- **Knowledge Article Version DMO** (Knowledge Articles)

### Key Points When Setting Up Data Graphs

- The **primary DMO category** must be something other than “Engagement”.
- If a DMO is not mapped to a **data stream** or **data lake object**, you won’t be able to select it when creating a data graph. Therefore, make sure to **map it in advance**, even if data is not yet available.

For example, in a **retail setup**, you may need to update the Goods Product object. If the standard fields aren’t enough, add **custom fields** as needed. For instance, the “Image URL” field does not exist by default.

1. In **Data Cloud**, open the **Data Model** tab, search for the **Goods Product** object, and select it.

2. Click **Edit**, scroll to the bottom, add the following custom fields, and save:

- **Unit Price** (API Name: `UnitPrice`) — Data Type: Number
- **Image URL** (API Name: `ImageUrl`) — Data Type: Text

Once complete, the fields you select when creating the item data graph will all be available for use in emails. That’s why preparing the right fields in **Goods Product** is essential.

You’ll also notice a calculated insight called **Total Sales Value**. This is a custom calculated insight I created, and it’s required later when setting up the **rule-based recommender**.

### Example: Custom Calculated Insight “Total Sales Value”

Normally, this kind of calculated insight would be built using the **Visual Insight Builder**, but here’s the underlying query for clarity. It uses `SUM` to aggregate sales quantity and sales amount by product ID.

- Sales data is stored in the **Sales Order Product Engagement** standard DMO.
- To join two DMOs in the Visual Insight Builder, set up an **N:1 relationship** between `Sales Order Product Engagement.ProductId` and `Goods Product.Goods Product Id` beforehand.

```
SELECT   
    SUM(ssot__SalesOrderProductEngagement__dlm.ssot__OrderedQuantity__c) AS total_quantity__c,  
    SUM(ssot__SalesOrderProductEngagement__dlm.ssot__UnitPriceAmount__c) AS total_amount__c,  
    ssot__GoodsProduct__dlm.ssot__Id__c AS goods_product_id__c  
FROM   
    ssot__GoodsProduct__dlm  
JOIN   
    ssot__SalesOrderProductEngagement__dlm  
    ON (  
        ssot__GoodsProduct__dlm.ssot__Id__c = ssot__SalesOrderProductEngagement__dlm.ssot__ProductId__c  
        AND ssot__GoodsProduct__dlm.KQ_Id__c = ssot__SalesOrderProductEngagement__dlm.KQ_ProductId__c  
    )  
GROUP BY   
    goods_product_id__c
```

> ***Tips:*** *When defining the dimension, make sure to use* `ssot__GoodsProduct__dlm.ssot__Id__c AS goods_product_id__c`*.  
> Otherwise, you won’t be able to associate it under* ***Goods Product*** *when configuring the Data Graph.*
>
> *This requirement comes from the fact that Calculated Insights must have a relationship with the Segment On object, and the primary key attribute of the Segment On object must also exist as a dimension in the Calculated Insight.*

## Creating a New Recommender

1. Once both data graphs are prepared, go to the **Personalization** app, open the **Recommenders** tab, and click **New**.

2. Specify the data space, and for the **Profile Data Graph**, select Marketing Cloud’s **default data graph**.

3. Next, select the target **Item Data Graph**.

4. Enter the **Recommender Name** and **API Reference Name**, then save.

5. Choose **Rule-Based Recommender**.

6. Select the **calculated insight** linked to the Item Data Graph you configured earlier.

7. The calculated insight includes two measures: **total quantity per product** and **total amount per product**. For this example, select **Total Amount**.

8. Since I want to rank items by sales in descending order, specify **Descending** and continue.

9. Next, configure the filters — this is the critical step.  
You can apply static conditions to values in the Item Data Graph or compare attributes against the Profile Data Graph. In this example, set the following conditions:

- Display only items where **Is Sellable = “Y”**
- Display only items where the **Product Category** matches the **Profile Category’s Favortite Genre**

With this setup, only items that are **sellable**, **aligned with the user’s preferences**, and **sorted by highest sales amount** will be displayed — maximizing sales potential.

10. Save the configuration once complete.

11. After saving, make sure the status changes to **Complete**. Only then will the recommender be available for use in content.

> ***Note****: In this example, I used a relatively simple* ***rule-based recommender****. If you choose to use a* ***objective-based recommender (AI)****, the training process will begin at this stage, and the status must reach* ***Complete*** *before it can be used. As mentioned earlier in the considerations, you must allow sufficient time for training.*

## Configuring the Repeater Component

1. Once the recommender is complete, go to the **Content** tab in Marketing Cloud and open the **Data Sources** tab.

2. Click the **Add** button.

3. Enter a **Data Source Name**, and under **Type**, select **Personalization Recommendations Data Provider**.

4. Under **Goods Product**, you’ll see the recommender you just created. Select it and save.

> *⚠️* ***Important****: In SDO environments, you may be able to progress up to this point, but beyond here, you could encounter the following error that prevents further steps.*

5. Although it appears the data source is now registered, you must also configure the data source within the **Repeater Component** itself.  
This step ensures that multiple repeaters can be placed in a single email.

6. Drag and drop the **Repeater Component** into the email. On the right-hand side, you’ll see the **Repeater Data Source** settings panel.

7. From **Repeater Data Source**, select the recommender you created earlier.

8. Unlike when using a simple data graph with the repeater, you **cannot apply filters or sorting at this stage**. For recommenders, all conditions must be defined during recommender creation. Here, you only need to adjust the display layout.

9. The following steps are the same as for a regular repeater component. Continue building your email with reference to the related guide.

[## SFMC Tips #134 : Marketing Cloud Next: Introducing the “Repeater” Component

### In Marketing Cloud Next (Marketing Cloud Growth & Advanced Edition), the Summer ’25 release introduces a brand-new…

medium.com](/@marketingcloudtips/marketing-cloud-on-core-introducing-the-repeater-component-cc8017b01dc4?source=post_page-----fb41b9c72ad0---------------------------------------)

When configuring merge fields in your content, be sure to select them from **Recommendations**.

10. Once your email is complete, save and publish it. Then, send it via a **Segment Trigger Flow** to recipients who have a value in **Favorite Genre**.

## Verifying the Email

A recipient with **Favorite Genre = Rock** received the following email:

![]()

A recipient with **Favorite Genre = Jazz** received the following email:

![]()

## Conclusion

In the full **Salesforce Personalization** product, even after creating a recommender, you still need to configure **Response Templates**, **Personalization Points**, **Decision**, and **Targeting Rules**.

In contrast, when using it for email delivery in **Marketing Cloud Next (Growth & Advanced Editions)**, you only need to configure the recommender — making it a much simpler setup.

## Personalization Features by Edition

**Personalization using Unified Individual (direct attributes only)**= **Unified Individual Data Provider**✅ Available: Marketing Cloud Growth & Advanced Edition  
✅ Available: Salesforce Starter & Pro Suite

**Personalization using Data Graph (direct and related attributes)**= **Data Graph Data Provider**✅ Available: Marketing Cloud Growth & Advanced Edition  
❌ Not available: Salesforce Starter & Pro Suite

**Personalization using Event Data**= **Event Data Provider**✅ Available: Marketing Cloud Growth & Advanced Edition  
✅ Available: Salesforce Starter & Pro Suite

**Personalization using Personalization Recommenders**= **Personalization Recommendations Data Provider**✅ Available: Marketing Cloud Advanced Edition  
❌ Not available: Salesforce Starter & Pro Suite, Growth Edition

That’s it for this walkthrough!

Stay tuned for more Salesforce Marketing Cloud tips! 😊

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
