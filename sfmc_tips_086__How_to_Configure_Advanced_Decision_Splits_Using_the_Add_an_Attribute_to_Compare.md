# SFMC Tips #86 : How to Configure Advanced Decision Splits Using the “Add an Attribute to Compare”…

**Source:** https://medium.com/@marketingcloudtips/how-to-configure-advanced-decision-splits-using-the-add-an-attribute-to-compare-feature-238ad29abb2b

---

# SFMC Tips #86 : How to Configure Advanced Decision Splits Using the “Add an Attribute to Compare” Feature

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--238ad29abb2b---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--238ad29abb2b---------------------------------------)

6 min read

·

Mar 4, 2025

--

Photo by [Severin Höin](https://unsplash.com/@sevhoein?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

In Salesforce Marketing Cloud’s Journey Builder, the “Decision Split” feature includes a handy option called “Add an Attribute to Compare”, which allows you to compare one attribute with another. While some users may not be familiar with this feature, it can be incredibly useful. In this article, I’ll introduce practical use cases to illustrate its potential.

## Use Case 1: Accurately Retrieving Values Corresponding to the Same Attribute

### Scenario

A gaming company executes customer nurturing scenarios after selling game apps. Once a game app is purchased, the app name is stored in the entry source, and the following journey begins:

1. Send a welcome email.
2. Send an email introducing similar game apps.
3. 30 days after purchase, send specific content via email to customers who have opened the purchased game app fewer than three times.

This journey can be represented as follows:

In this article, I’ll focus on the decision split for the third email step:  
**“Send specific content via email to customers who have opened the purchased game app fewer than three times 30 days after purchase”.**

### Entry Source Data Extension Fields

The data extension in the entry source includes the following fields:

- **Id** (Primary Key)
- **GameAppName** (Primary Key)
- **Email**

Since a single customer may purchase multiple game apps, the records are structured to allow multiple rows per customer:

### Game App Open Counts Data Extension Fields

To manage the number of times game apps are opened, another data extension contains the following fields. This is linked in Contact Builder’s Data Designer and utilized as “Contact Data”:

- **Id** (Primary Key)
- **GameAppName** (Primary Key)
- **Open**

This data extension tracks open counts for multiple game apps, with the open count updated dynamically as customers open the app:

### The Problem

When linking **Id** and **GameAppName** in Contact Builder and configuring the decision split with conditions like these:

The following incorrect results may occur:

1. **GAME A** is entered → Open count of **2** is retrieved, and the email is sent.
2. **GAME B** is entered → Open count of **2** is retrieved, and the email is sent.

This happens because the decision split evaluates the **first matching record** (the top record in the data extension), leading to incorrect results where emails are sent for both **GAME A** and **GAME B**.

Regardless of whether the entry is for **GAME A** or **GAME B**, the system adopts the top record’s open count (e.g., **2**) from the data extension managing app open counts.

\*Salesforce considers this behavior as **“working as designed”.**

## Solution: Configure the “Add an Attribute to Compare” Feature

To address this issue, use the “Add an Attribute to Compare” feature and configure the decision split as follows:

### Steps

1. Drag **GameApp** from “Contact Data” to the left side.
2. Check the box for **“Add an Attribute to Compare”.**
3. Drag **GameApp** from “Journey Data” to the right side.
4. Leave the operator as **“equal” (default).**
5. Combine this condition with the open count condition using an **“AND”** operator.

### Result

With this configuration, the correct open count value is retrieved for each entered game app:

1. **GAME A** is entered → Open count of **2** is retrieved, and the email is sent.
2. **GAME B** is entered → Open count of **15** is retrieved, and the email is not sent.

## Important Considerations

When setting this up, think of it as adding a “subkey” to the subscriber key for evaluating contact data. However, there are some **prerequisites** to keep in mind:

- Encrypted fields are not supported.
- Only attributes with the same data type can be compared. If the data types differ, drag-and-drop actions will be blocked.
- While attributes allowing null values are officially unsupported, they appear to work without issues. However, to avoid potential future problems, these attributes should ideally be configured as **required fields**.

## Use Case 2: Sending Emails to Customers with Decreased Scores

### Scenario

The entry source of the journey includes a “Customer Score” recorded at the start of the scenario. This “Customer Score” is used as fixed **Journey Data** during the journey.

**Fields in the Entry Source Data Extension**:

- **Id** (Primary Key)
- **Email**
- **Score** (Recommended as a Required Field)

![]()

On the other hand, the current “Customer Score” is managed and calculated in real time in **Contact Data**.

**Fields in the Contact Data Extension**:

- **Id** (Primary Key)
- **Latest\_Score** (Recommended as a Required Field)

![]()

Now, let’s consider a scenario where, 30 days after the journey starts, an email is sent if the latest “Customer Score” in the **Contact Data** is lower than the initial “Customer Score” recorded in the journey’s entry source. In this case, the **“Add an Attribute to Compare”** feature can be configured as follows:

### Steps

1. Drag **Score** (number type) from “Journey Data” to the left side.
2. Check the box for **“Add an Attribute to Compare”.**
3. Drag **Latest\_Score** (number type) from “Contact Data” to the right side.
4. Change the operator to **“greater than”.**

**Note:**  
Ensure that you click “Done” to confirm the operator selection. If you click “Summary” instead, the operator will revert to the default value of **“Equal”.**

### Results

- **Contact BOR501** → The “Customer Score” exceeds the latest score by **5**, so the email is **not sent.**
- **Contact BOR502** → The “Customer Score” is lower by **3**, so the email is **sent.**

## Known Issues and Recommendations

While the “Add an Attribute to Compare” feature provides flexibility, there are known issues associated with it. Always test your journeys to ensure conditions are applied correctly.

### Combining Conditions in Use Case 1

As shown in **Use Case 1**, when combining “Attribute Comparison” with additional conditions, the following arrangement is recommended:

- **Left side:** Drag attributes from **Contact Data.**
- **Right side:** Drag attributes from **Journey Data.**

Although improvements were made in 2023, some bugs persist. Exercise caution when using combined conditions.

[## Attribute to Attribute Comparison does | Known Issues

### Attribute to Attribute Comparison does not always work when Contact Data is on the Right Side and there is more than…

issues.salesforce.com](https://issues.salesforce.com/issue/a028c00000gAw1pAAC/attribute-to-attribute-comparison-does-not-always-work-when-contact-data-is-on-the-right-side?source=post_page-----238ad29abb2b---------------------------------------)

### Numeric Comparison in Use Case 2

When comparing numeric attributes, using the following arrangement may result in validation errors during the journey:

- **Left side:** Drag attributes from **Contact Data.**
- **Right side:** Drag attributes from **Journey Data.**

To resolve these errors, reverse the arrangement:

- **Left side:** Drag attributes from **Journey Data.**
- **Right side:** Drag attributes from **Contact Data.**

In **Use Case 2**, since no combined conditions are involved, placing “Journey Data” on the left works as expected. Adjust the arrangement based on the condition type and attribute type to ensure smooth configuration.

## Final Thoughts

The **“Add an Attribute to Compare”** feature may require a bit of “ingenuity” 💡, but it enables surprisingly flexible branching within decision splits.

That said, known issues abound, so remember to thoroughly test your journeys to verify that they branch correctly.

Thank you for reading!!

Stay tuned for more Salesforce Marketing Cloud tips! 😊

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
