# SFMC Tips #134 : Marketing Cloud Next: Introducing the “Repeater” Component

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-on-core-introducing-the-repeater-component-cc8017b01dc4

---

# SFMC Tips #134 : Marketing Cloud Next: Introducing the “Repeater” Component

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--cc8017b01dc4---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--cc8017b01dc4---------------------------------------)

7 min read

·

Jun 9, 2025

--

Photo by [Mohammad Faruque](https://unsplash.com/@primitivestudios?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

In **Marketing Cloud Next (Marketing Cloud Growth & Advanced Edition)**, the **Summer ’25 release** introduces a brand-new **“Repeater” component**. In this article, I’ll review this exciting new feature.

[## SFMC Tips #106 : Marketing Cloud on Core: Summer ’25 Release Highlights

### Exciting updates for Marketing Cloud on Core (Marketing Cloud Growth & Advanced Edition) have been unveiled. For the…

medium.com](/@marketingcloudtips/marketing-cloud-on-core-summer-25-release-highlights-4ad6f39c5d6d?source=post_page-----cc8017b01dc4---------------------------------------)

This component brings the dynamic display functionality of **AMPscript’s** `LookupOrderedRows` **in Marketing Cloud Engagement** into a more intuitive **UI-based experience**.

Previously, in another article, I introduced the **Expression component**, which also resembled `LookupOrderedRows`. However, that functionality was limited to displaying only the **first-priority element**.

While that feature is valuable for working with unified data, the newly released **Repeater component** goes further by allowing you to display **not just the first element, but subsequent elements in sequence**. This evolution enables **more flexible and richer expressions**, making it truly a **major functional enhancement**.

[## SFMC Tips #133 : Marketing Cloud on Core: Harnessing Reusable “Expression” Content

### In Marketing Cloud on Core (Marketing Cloud Growth & Advanced Edition), reusable “Expression” content enables you to…

medium.com](/@marketingcloudtips/marketing-cloud-on-core-harnessing-reusable-expression-content-c9c26098cb5a?source=post_page-----cc8017b01dc4---------------------------------------)

## The Repeater Component Setup Steps

Let’s jump straight into the steps! A new “Repeater” component is now available in the components menu. You can start using it by simply dragging and dropping it onto the canvas.

### Layout Configuration

This feature allows you to automatically arrange layouts combining images, headers, paragraphs, and buttons. When dragged and dropped onto the canvas, the default setup displays two horizontal cards side by side.

The layout is fully customizable. You can set up to 6 columns horizontally, and in my tests, more than 5,000 cards (lists) vertically were possible. However, for practical use — considering display limitations in email clients — keeping the number of rows to just a few dozen is advisable.

*A sample layout with three columns horizontally and two rows vertically*

Additionally, you can switch from “**Card View**” to “**List View**”. In the list layout, images are displayed on the left side of the text, as shown below:

If you prefer, you can also skip templates entirely and build fully customized layouts from scratch.

## Sample Scenario Overview

In this sample scenario, I’ll demonstrate how to create a ranking based on sales data from the previous day and display this ranking in an email. Ranking-based scenarios like this are a common use case in promotional campaigns.

![]()

Typically, in **Marketing Cloud Engagement**, achieving this would require leveraging **AMPscript** and **HTML**. However, with **Marketing Cloud Growth & Advanced Edition**, this process can be configured effortlessly through on-screen interactions, highlighting a significant advantage.

### Setting Up the Data Model Object

First, I’ll create a Data Model Object (DMO) called **Ranking** to store the ranking data.

Next, this data is prepared for use in the **Data Graph**.

**Prerequisite:**  
To link the **Individual** object with the newly created **Ranking** DMO in the Data Graph, a relationship setup is required beforehand. In this example, I added a **Favorite Genre** field to the Individual object and linked it to the **Genre** field in the Ranking DMO as a one-to-many relationship.

With this preparation, the ranking data is now ready for use.

## Content Builder Configuration Steps

### 1. Placing the Repeater Component

Start by creating the other necessary elements in your content. Then, drag and drop the **Repeater** component into the desired section of the canvas.

### 2. Configuring the Data Layout

In the data layout section, adjust the settings as follows:

- **Columns:** 3
- **Rows:** 2
- **Disable mobile column stacking** (optional)

### 3. Selecting the Repeater Source

Choose the **Repeater Source** and select **Ranking** from the Data Graph.

### 4. Setting the Sorting Order

Click on **Edit Expression** to configure the sorting order of the displayed data.

Select **Ranking** as the repeater source.

*Note:* Although the source isn’t labeled explicitly as “Ranking”, it’s clearly displayed in a position that makes its role as the repeater source understandable.

Choose **Rank** as the sorting field and set the order to **Ascending**.

### 5. Configuring Merge Fields

Set up the merge fields for the top-left element.

![]()

Merge fields should be selected from the **Ranking** repeater source.

![]()

### 6. Button Configuration

For buttons, use the “**Link to Dynamic URL**“ feature introduced in the Summer ’25 release. Select merge fields from the **Ranking** repeater source.

### 7. Configuring Image Merge Fields

For images, select the “**Merge Field**“ radio button and choose fields from the **Ranking** repeater source.

### 8. Verifying the Settings

Once all merge fields are configured, confirm that the content entered for the top-left element is automatically reflected across other combinations.

![]()

## Email Preview and Verification

### 1. Sending the Email to Verify Functionality

After completing the setup, send the email via the flow to test its functionality. The personalized ranking is displayed as follows:

- If the recipient’s **Favorite Genre** is **Rock**, the email displays the ranking for **Rock**.

![]()

- If the recipient’s **Favorite Genre** is **Jazz**, the email displays the ranking for **Jazz**.

![]()

### 2. Results

As expected, the rankings were displayed correctly. Success! The final email appears as shown below:

![]()

**Note:** Due to the length of text within the **Repeater** component, the button positions may shift slightly. Currently, this is a limitation that cannot be adjusted.

## Known Issues

### [Email rendering issues on Outlook](https://help.salesforce.com/s/issue?id=a028c00000zLYzgAAG&title=email-rendering-issues-on-outlook)

In older versions of Outlook, rendering issues may occur. Specifically, images might display at their original pixel dimensions or appear broken.

![]()

**Example of an email received with rendering errors**

We can’t address the issue of broken images, but for image sizing, since the email width is 600 px, you can resolve the problem by explicitly setting widths — for example, 186 px for a 3-column layout or 284 px for a 2-column layout. However, this may affect the appearance of other components, so make sure to test thoroughly.

### **Issues with Merge Fields Not Displaying Properly**

Occasionally, when setting up “Images” or “URLs,” the values may not properly reflect in the designated fields and fail to display.

In such cases, directly entering strings like `{!$Expression.URL_2}` or `{!$Expression.Image_5}` ensures proper rendering. `URL_2` and `Image_5` refer to the Merge Field API names defined during setup.

Please rewrite and use the format below as needed:

```
{!$Expression.●●●●●}
```

## Closing Thoughts

How did you find this feature?

With the introduction of the **Repeater** component in **Marketing Cloud Growth & Advanced Edition**, users can now transition from traditional AMPscript-based advanced personalization to a more intuitive **no-code** approach.

While many users may hope for a similar component in **Marketing Cloud Engagement**, it’s unlikely to be developed.

To bridge this gap, I plan to publish a follow-up article demonstrating how to implement a functionality equivalent to the **Repeater** component using **HTML** and **AMPscript**. Stay tuned for that!

That concludes this overview.

Stay tuned for more Salesforce Marketing Cloud tips! 😊

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
