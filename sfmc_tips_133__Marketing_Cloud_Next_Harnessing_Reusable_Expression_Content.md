# SFMC Tips #133 : Marketing Cloud Next: Harnessing Reusable “Expression” Content

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-on-core-harnessing-reusable-expression-content-c9c26098cb5a

---

# SFMC Tips #133 : Marketing Cloud Next: Harnessing Reusable “Expression” Content

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--c9c26098cb5a---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--c9c26098cb5a---------------------------------------)

4 min read

·

Jun 9, 2025

--

Photo by [Annie Spratt](https://unsplash.com/@anniespratt?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

In Marketing Cloud Next (Marketing Cloud Growth & Advanced Edition), reusable “Expression” content enables you to save sorting and filtering conditions for attributes, making them easy to use as merge fields.

![]()

This article provides a detailed guide to the features of “Expression” content and specific steps based on practical use cases.

## Benefits of Using “Expression” Content

- **Improved Efficiency**: Conditions created once can be easily reused in emails and landing pages.
- **Consistency**: Managing reusable content reduces errors in data display and logic.
- **Enhanced Flexibility**: Even complex logic can be applied across various content types after being set up once.

## Use Cases for “Expressions”

### Scenario

Providing information related to recently viewed products.

### Application

Using browsing history data collected from an e-commerce site, follow these steps to leverage the information:

1. Sort “Browsing History” records in descending order and extract the name of the last viewed product.
2. Insert the extracted product name into an email, along with links to detailed product information and customer success stories.

This approach helps deliver personalized content aligned with customer interests, increasing engagement.

## Example Email Text

*“Discover the detailed specifications and success stories of the product you recently viewed, ‘[Last Viewed Product Name],’ through the links below”.*

## **How to Configure an “Expression”**

### 1. Create New Content

From the content menu, select “**Add Content**” and choose **“Expression”**.

![]()

### 2. Select Attributes

Set a title for the expression (e.g., “Last Viewed Product Name”), then select **“ProductName”** from the attributes panel on the right.

**Prerequisite:**  
 A custom DMO (Data Model Object) called **“View History”**, which contains the **ProductName** field, must already be related to the **Individual** object and configured in the data graph.

### 3. Configure Sorting Conditions

Set **“ViewDateTime”** to **Descending Order** to prioritize the most recently viewed product.

### 4. Save and Publish

After saving the expression, click the **“Publish”** button to make it available for use.

## How to Configure Content with an Expression

### 1. Insert a Merge Field

Select the desired location in the email body and click the **“Merge Field”** button.

### 2. Choose Merge Field Type

From the merge field type options, select **“Saved Expression”**.

### 3. Select a Predefined Expression

Choose **“Last Viewed Product Name”** from the displayed list.

If no further edits are needed, simply click **“Next”**.

### 4. Configure the API Reference Name

If required, enter an API reference name and click the **“Done”** button.

### 5. Preview the Results

Once the setup is complete, verify the functionality in the preview screen.

Ensure that the product name is correctly inserted.

### Reference: Verifying Data in Data Cloud

Using the **Data Cloud Data Explorer**, you can verify the data for the corresponding user:

Filter the data for the target user and sort “ViewDateTime” in descending order to identify the “Last Viewed Product”.

The product displayed in the email (Product\_9) matches the identified data. Success!

## Conclusion

If you’ve used Marketing Cloud Engagement before, you might find it helpful to compare this to using AMPscript’s **LookupOrderedRows** to prioritize and display the top product.

With the **Data Graph**, you can leverage “indirect attributes”, enabling functionality similar to Lookup without the need to write complex code.

By utilizing reusable **“Expression”** content, you can expect the following benefits:

- **Efficient Management of Merge Fields**
- **Consistent Application of Marketing Logic**
- **Reduction in Work Time**

Take full advantage of this feature to enhance your strategies in **Marketing Cloud Growth & Advanced Edition**!

That’s all for now.

Stay tuned for more Salesforce Marketing Cloud tips! 😊

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
