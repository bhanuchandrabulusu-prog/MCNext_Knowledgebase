# SFMC Tips #125 : Marketing Cloud Next: Waterfall Segment

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-on-core-waterfall-segment-fbe99d4af303

---

# SFMC Tips #125 : Marketing Cloud Next: Waterfall Segment

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--fbe99d4af303---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--fbe99d4af303---------------------------------------)

5 min read

·

Jun 3, 2025

--

Photo by [Clem Onojeghuo](https://unsplash.com/@clemono?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

In a previous article, I explained the basics of segment within Marketing Cloud Next (Marketing Cloud Growth & Advanced Edition).

[## SFMC Tips #92 : Marketing Cloud on Core: Basics of Segment

### When leveraging Marketing Cloud on Core (Marketing Cloud Growth & Advanced Edition), designing effective segment is…

medium.com](/@marketingcloudtips/marketing-cloud-on-core-basics-of-segmentation-d240bb357d3d?source=post_page-----fbe99d4af303---------------------------------------)

This time, I’ll dive into **Waterfall Segment**, a feature within the Data Cloud segment capabilities of Marketing Cloud Growth & Advanced Edition. I’ll explore its functionality, benefits, and key considerations.

### Data Cloud Segment Features Covered in This Article

1. ✖️ [Standard Segment](/p/d240bb357d3d)
2. ⭕ [**Waterfall Segment**](/@marketingcloudtips/marketing-cloud-on-core-waterfall-segment-fbe99d4af303)
3. ✖️ [Real-Time Segment](/@marketingcloudtips/marketing-cloud-next-leveraging-real-time-segments-868c0f591205)
4. ✖️ [Dynamic Segment](/@marketingcloudtips/marketing-cloud-next-how-to-use-dynamic-segments-06ee41977c2a)
5. ✖️ Einstein Segment Creation (AI-Driven Segment)

## What is Waterfall Segment?

Waterfall Segment is a feature that allows you to prioritize and hierarchically arrange multiple segment lists to eliminate customer overlap. I intentionally refer to it as a “feature” rather than a “segment” because its primary purpose is deduplication, which sets it apart from standard segment roles.

For instance, if the same customer appears in multiple lists, Waterfall Segment enables you to exclude that customer from lower-priority lists. This ensures more efficient targeting and streamlined delivery.

If the concept seems abstract, let’s clarify it with an example.

## Example: Event Invitation Campaign

Imagine a company planning multiple events and inviting the most suitable customers to each one. Here’s how Waterfall Segment could be utilized:

### Invitation to Special Events

- **Eligibility:** Customers with an annual purchase amount of 2,000 USD or more, or VIP members.
- **Details**: Exclusive, premium events such as dinner shows or interactions with brand ambassadors

### Invitation to New Product Launch Events

- **Eligibility:** Customers who make purchases at least once a month.
- **Details**: Launch events for new products

### Invitation to Online Seminars

- **Eligibility:** Customers with a purchase history within the past year.
- **Details**: Webinars or online seminars

For clarity, I’ll refer to these sequential lists as “*child segments*”.

## Steps to Configure a Waterfall Segment

Here are the detailed steps to set up a Waterfall Segment.

### 1. Create Child Segments

Start by preparing the child segments you’ll use. Using the example of the event invitation campaign mentioned earlier, create the following segments:

- **Invitation to Special Events** (list of 1 customer)
- **Invitation to New Product Launch Events** (list of 2 customers)
- **Invitation to Online Seminars** (list of 3 customers)

**Customer List Overview**:

- **Customer A**: Included in all lists
- **Customer B**: Included in two lists
- **Customer C**: Included in only one list

![]()

### 2. Set Up the Waterfall Segment

**Step 1: Select the Segment Type**

From the “Segment Type” options, choose **Waterfall Segment**.

**Step 2: Select the Publishing Type**

For the Waterfall (parent) segment, only **Standard Publishing** (12-hour or 24-hour) is available.

For child segments, they must also use **Standard Publishing**, with the Publishing Schedule set to “**Don’t Refresh**”.

**Step 3: Verify Usable Child Segments**

In the Waterfall (parent) segment setup screen, you’ll see a list of usable child segments. If a segment isn’t displayed, it could be due to one of the following reasons:

- It is set to **Rapid Publish**
- A **Publishing Schedule** is active (12-hour or 24-hour)
- It is already used in another Waterfall Segment

**Step 4: Prioritize Child Segments**

Drag and drop the child segments in the canvas to set their priority. You can adjust the order anytime and then click **Save**.

**Step 5: Perform Manual Publishing**

For testing purposes, initiate a manual publish.

### 3. Review Publishing Results

Once the publishing process is complete, review the results to confirm that each customer appears in only one list, avoiding overlaps.

For example, **Customer A** should appear in the highest-priority list and be excluded from the others. If this is the case, the setup was successful.

![]()

### Notes on Child Segment Restrictions

- If you attempt to edit a child segment’s conditions, you will be notified that it is currently being used in a Waterfall Segment.

- Child segments used in a Waterfall Segment cannot have a new publishing schedule (12-hour or 24-hour) assigned.

## Important Considerations When Creating Waterfall Segments

Here are some key points to keep in mind when setting up Waterfall Segments.

### 1. Points to Consider When Creating Child Segments

- **Use Unified Individual Data Model Objects**  
  Child segments must be based on unified individual data model objects.
- **Publishing Type: Standard Publishing**  
  Child segments with **Rapid Publish** cannot be used.
- **Publishing Schedule: Don’t Refresh**  
  Avoid setting a 12-hour or 24-hour publishing schedule for child segments.

### 2. Points to Consider When Creating a Waterfall (Parent) Segment

- **Independence of Child Segments**  
  Ensure that child segments are not part of another Waterfall Segment.
- **Unusable Child Segments**  
  The following types of child segments cannot be used:
- Child segments with **Rapid Publish**
- Child segments with an active **Publishing Schedule** (12-hour or 24-hour)
- Child segments already included in another Waterfall Segment

## Conclusion

By leveraging Waterfall Segments, you can achieve efficient targeting, especially in scenarios where customers may appear in multiple segments. However, it’s important to assess whether this approach is necessary for your specific use case. Overcomplicating segment without a clear benefit may not be the optimal solution.

I hope this guide serves as a helpful reference for designing your segments.

That’s all for this time.

Stay tuned for more Salesforce Marketing Cloud tips! 😊

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
