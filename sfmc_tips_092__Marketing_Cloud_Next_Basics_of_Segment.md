# SFMC Tips #92 : Marketing Cloud Next: Basics of Segment

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-on-core-basics-of-segmentation-d240bb357d3d

---

# SFMC Tips #92 : Marketing Cloud Next: Basics of Segment

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--d240bb357d3d---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--d240bb357d3d---------------------------------------)

8 min read

·

Mar 26, 2025

--

Photo by [Guilherme Stecanella](https://unsplash.com/@guilhermestecanella?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

When leveraging Marketing Cloud Next (Marketing Cloud Growth & Advanced Edition), designing effective segments is essential. Marketing Cloud Next utilizes the segmentation capabilities of Data Cloud. This article covers the basics of Data Cloud segmentation while highlighting the unique aspects of segmentation in Marketing Cloud Next.

## Key Points About Marketing Cloud Next Segmentation

**1. Utilizing Unified Individual**  
Segments used in Marketing Cloud Next must be based on the “Unified Individual” data model object as the segmentation criteria (Segment On). This requirement makes “Identity Resolution” a critical step in Marketing Cloud Next. Proper identity resolution ensures that data from multiple sources is consolidated, avoiding duplicate sends.

**2. Activation of Segments Is Not Required**  
In the standard Data Cloud process, segment activation is a prerequisite for utilization. However, in Marketing Cloud Next, activation is unnecessary. After creating a segment, simply publishing it enables its use in campaigns and communications.

## Key Points for Configuring Data Cloud Segments

### Choosing the Update Type

Selecting the right update type is essential for aligning segment behavior with campaign goals.

**1. Static Segments**

- **Update Frequency:** “Don’t refresh”.
- **Characteristics:** Functions as a fixed, unchanging list.
- **Use Case:** Suitable for one-time campaigns or stable lists.

**2. Standard Publish**

- **Update Frequency:** Every 12 or 24 hours.
- **Data Scope:** Utilizes up to two years of engagement data.
- **Use Case:** Ideal for steady operations requiring regular refreshes.
- **Changeability:** Cannot switch to Rapid Publish.

**3. Rapid Publish**

- **Update Frequency:** Every 1 or 4 hours.
- **Data Scope:** Utilizes up to one week of engagement data.
- **Use Case:** Best for real-time scenarios and dynamic campaigns.
- **Changeability:** Can switch to Standard Publish.
- **Limitations:** Maximum of 20 Rapid Publish segments.

***Note:*** *While Rapid Publish typically supports activation for targets like Marketing Cloud Engagement, SFTP, and Cloud File Storage, activation is not necessary in Marketing Cloud Next.*

## Lookback Window

The **lookback window** is a crucial setting for managing data processing efficiently. For standard publication, the default configuration uses up to two years of engagement data. However, it is recommended to evaluate whether processing the entire dataset is necessary.

For example, if your analysis focuses only on engagement data from the past month, shortening the lookback window to 30 days can significantly reduce unnecessary data processing and conserve credits. This setting offers flexibility, allowing adjustments ranging from “1 day to 360 days” or “within 1 year, within 2 years”, enabling you to choose the optimal period based on your needs.

## Basic Segment Structure

### **Segment On**

Displays which Data M**odel Object (DMO) the segment is based on.**

### **Publication Schedule**

Shows the frequency of segment publication.

### **Attribute Tab and Segment Tab**

You can select **Attributes** or **Segments** as filter conditions. In cases where segments are used, they are referred to as “**Nested Segments**”, allowing the reuse of existing segments across multiple segments to maintain consistency.

### **Direct Attributes vs. Related Attributes**

- **Direct Attributes:** Typically demographic data (e.g., age, gender) that have a one-to-one relationship with the segment target.
- **Related Attributes:** Represent one-to-many relationships, such as purchase history or email engagement data (e.g., opens, clicks).

### **Include | Exclude**

In addition to standard inclusion conditions, exclusion conditions can also be set.

## Grouping by Containers

When defining filters based on **Related Attributes**, a “container” that includes rule options for those attributes is added to the canvas. The **Data Model Object (DMO)** associated with the related attribute serves as the base for the container.

Adding additional related attributes to the same container ensures that those attributes act based on the **same data row**. The attribute library displays objects related to the container’s base DMO, up to five relationships away. Attributes from these related objects can be included in the container, providing up to six selectable DMOs: the base DMO and five related DMOs.

**\*Best Practice:** When selecting attributes, choose those that create the shortest container path for optimal performance.

Attributes placed in **different containers** are not related to one another and are filtered independently. These filters may or may not operate on the same data row.

### Scenario Examples

**Scenario 1: Attributes in the Same Container**

- Placing the attributes “Blue” and “Skirt” in the same container applies **AND logic**.
- This setup identifies customers who purchased a **blue skirt** as a single order item.

**Scenario 2: Attributes in Separate Containers**

- Placing the attribute “Blue” in one container and “Skirt” in another identifies customers who:
- Have purchased a **blue product** in the past.
- Have also purchased a **skirt of any color**.

*Note: Attributes from unrelated DMOs cannot be included in the same container.*

## Aggregation Types and Marketing Segmentation Examples

In marketing strategy, leveraging specific aggregation types enables effective segmentation based on customer behavior. Below are examples of configurations for each aggregation type:

### Count

- **Purpose:** Target customers who made at least **three purchases** via apps or websites in the past six months.
- **Key Detail:** A count of visits is effective, and no “numeric” attribute is required.

### Sum

- **Purpose:** Identify customers who purchased a total of **five or more items** through apps or websites in the past six months.
- **Key Detail:** Requires a “numeric” attribute.

### Average

- **Purpose:** Segment customers whose **average number of items per order** exceeds three over the past six months.
- **Key Detail:** Requires a “numeric” attribute.

### Minimum (Min)

- **Purpose:** Extract customers who made a **single purchase worth at least $150** in the past six months.
- **Key Detail:** Requires a “numeric” attribute.

### Maximum (Max)

- **Purpose:** Target customers who spent **$15 or more on shipping or delivery fees** in the past six months.
- **Key Detail:** Requires a “numeric” attribute.

## Calculated Insights in Segmentation

Calculated insights are used in segmentation to generate audiences based on complex metric calculations such as Lifetime Value (LTV).

**Example:** For an upcoming marketing campaign, a segment of all customers whose lifetime order amount in the glass category exceeds $20 is required. To meet this requirement, a calculated insight called “LTV” is created by combining unified individual data with order data and summing the order amounts of all records containing glass products.

Calculated insights appear in the segmentation interface, for example, directly under the attribute display of the related Unified Individual when linked accordingly.

![]()

***Note:*** *For a calculated insight to appear in segmentation, it must have a relationship with the Segment On object, and the primary key attribute of the Segment On object must exist as a dimension in the calculated insight.*

## Segment Preview Feature

### **① Preview from the Data Cloud Segment Screen**

With the September 2025 release of Data Cloud, a new segment preview feature has been introduced, accessible directly from the Data Cloud segment screen. For details, please see the following article.

[## SFMC Tips #178 : Marketing Cloud Next: New Segment Preview Feature

### Marketing Cloud Next (Marketing Cloud Growth & Advanced Edition) now offers a new feature that allows you to preview…

medium.com](/@marketingcloudtips/marketing-cloud-next-new-segment-preview-feature-be716460c70f?source=post_page-----d240bb357d3d---------------------------------------)

*Note: This preview feature allows you to check a segment before it is published.*

### **② Preview within Campaign-Integrated Flows**

As part of the Spring ’25 release, a segment preview feature was added to campaign-integrated flows. With this feature, you can review a list of up to 1,000 people before sending.

### **Considerations**

- Campaign-integrated flows include a **“Preview”** button.

![]()

- Each time you click the **Preview** button, Data Query credits are consumed. If you don’t click it, credits are not consumed.
- The list displayed represents the **segment data at the time of final publication**.

At the top of the preview screen:

![]()

- The **left side** shows the “segment count at the time of final publication.”
- The **right side** shows the “segment count immediately after segment creation.”

To understand this discrepancy, keep in mind:

- A segment right after creation is still in a **temporary state**.
- It is only when you **publish** the segment that it becomes finalized as a list.

*Note: Be aware that the segment right after creation is in a* ***floating temporary state****. The segment in this state is not used for sending. Instead, the* ***final published segment*** *is considered authoritative and is what is used for actual sends.*

### **③ Preview via “Debug” in Flow Builder**

While campaign-integrated flows have a **Preview** button, Flow Builder itself does not. However, after saving a flow, you can click the **Debug** button and then select **“Select Data Cloud Record”** to preview a segment.

You can display up to 25 subscribers at a time. It is also possible to select the fields to display and apply filters.

## Comparison with Marketing Cloud Account Engagement

Finally, let’s compare this with the standard segmentation features in **Marketing Cloud Account Engagement (MCAE, formerly Pardot)**. This comparison highlights specific advantages that Data Cloud offers over MCAE:

**1. For Marketing Cloud Account Engagement**

- **Target Objects**: Only directly linked child objects (grandchild objects and beyond are excluded).
- **Maximum Objects**: Up to 10 objects.
- **Record Limit**: Approximately 800,000 records per object.

**2. For Segments Using Data Cloud**

- **Relationship Hierarchy**: Supports up to 5 levels of hierarchy.
- **Number of Objects**: Up to 7,500 objects.
- **Data Size**: No limits.

## Conclusion

This time, I introduced the **“Standard Segment”.**

### Data Cloud Segment Features Covered in This Article

1. ⭕ [**Standard Segment**](/p/d240bb357d3d)
2. ✖️ [Waterfall Segment](/@marketingcloudtips/marketing-cloud-on-core-waterfall-segment-fbe99d4af303)
3. ✖️ [Real-Time Segment](/@marketingcloudtips/marketing-cloud-next-leveraging-real-time-segments-868c0f591205)
4. ✖️ [Dynamic Segment](/@marketingcloudtips/marketing-cloud-next-how-to-use-dynamic-segments-06ee41977c2a)
5. ✖️ Einstein Segment Creation (AI-Driven Segment)

I also hope to introduce the other segment types one by one in the future.

By properly understanding and utilizing these segmentation technologies, you can run highly effective campaigns. Be sure to manage your segment definitions and publication schedules accurately to maximize results.

That’s all for now!

Stay tuned for more Marketing Cloud Growth & Advanced Edition tips! 😊

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
