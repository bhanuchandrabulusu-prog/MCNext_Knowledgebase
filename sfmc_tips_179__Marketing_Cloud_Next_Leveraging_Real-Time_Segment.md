# SFMC Tips #179 : Marketing Cloud Next: Leveraging Real-Time Segment

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-next-leveraging-real-time-segments-868c0f591205

---

# SFMC Tips #179 : Marketing Cloud Next: Leveraging Real-Time Segment

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--868c0f591205---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--868c0f591205---------------------------------------)

4 min read

·

Oct 1, 2025

--

Photo by [Reza Heydar](https://unsplash.com/@molek_8?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

In **Marketing Cloud Next** (Marketing Cloud Growth & Advanced Edition), the **Summer ’25** release introduces a new feature: you can now use **Segment Membership (Unified Individual — Latest)** in **Real-Time Data Graph Triggered Flows**.

> ***Note:*** *Only* ***real-time segments*** *can be selected as event trigger conditions.  
>  Standard segments are not displayed.*

With this update, you can now execute **triggered sends** to members who have joined **real-time segments** created from a real-time data graph.

## Considerations for Real-Time Data Graph Triggered Flows

### **① Timing of flow triggers**

- “Every time an event meets entry conditions” is **not available**.
- Only “If the current event meets entry conditions and the previous event didn’t meet entry conditions” is supported.

### **② Wait period before the flow becomes active**

- To prepare the necessary resources, the system cannot receive or process events for up to **1 hour after activation**.
- Any events sent during this waiting period will be ignored, so be sure to configure your setup in advance.

## Considerations for Real-Time Segments

When using **real-time segments**, it’s important to keep in mind the balance between **costs and benefits**.  
That said, they can be leveraged in a way similar to **Dynamic Lists** in **Marketing Cloud Account Engagement**.

**Tip:** A Dynamic List is a list where members are automatically added or removed based on predefined conditions, ensuring the list always remains up to date.

To use real-time segments in a **data graph**, you must add the following fields from the **Segment Membership DMO** into the **Real-Time Profile Data Graph**:

- **Segment Id** (Text)
- **Timestamp** (Date)

Please also be aware of the following **limitations**:

- Segments containing **nested segments** or **exclusion conditions (Exclude)** cannot be created.
- Features such as **real-time display of segment counts** or **manual publishing** are not available.
- If both **Account** and **Individual** objects are included in the same source data graph, real-time segments will not run.

For details about features like **nested segments** in standard segments, please refer to the following article.

[## SFMC Tips #92 : Marketing Cloud Next: Basics of Segment

### When leveraging Marketing Cloud Next (Marketing Cloud Growth & Advanced Edition), designing effective segments is…

medium.com](/@marketingcloudtips/marketing-cloud-on-core-basics-of-segmentation-d240bb357d3d?source=post_page-----868c0f591205---------------------------------------)

## Conclusion

This time, I was able to explore the concept of **real-time segments**. However, I must admit that I have not yet translated this fully into concrete use cases for **Real-Time Data Graph Triggered Flows**.  
That’s an area I intend to continue researching and experimenting with moving forward.

### Data Cloud Segment Features Covered in This Article:

1. ✖️ [Standard Segment](/p/d240bb357d3d)
2. ✖️ [Waterfall Segment](/@marketingcloudtips/marketing-cloud-on-core-waterfall-segment-fbe99d4af303)
3. ⭕ [**Real-Time Segment**](/@marketingcloudtips/marketing-cloud-next-leveraging-real-time-segments-868c0f591205)
4. ✖️ [Dynamic Segment](/@marketingcloudtips/marketing-cloud-next-how-to-use-dynamic-segments-06ee41977c2a)
5. ✖️ Einstein Segment Creation (AI-Driven segments)

With this, I believe I’ve covered the key updates released in **Summer ’25**.  
It was quite a packed update, wasn’t it? In fact, it’s already been **five months** since I last wrote a summary article.

[## SFMC Tips #106 : Marketing Cloud Next: Summer ’25 Release Highlights

### Exciting updates for Marketing Cloud Next (Marketing Cloud Growth & Advanced Edition) have been unveiled. For the first…

medium.com](/@marketingcloudtips/marketing-cloud-on-core-summer-25-release-highlights-4ad6f39c5d6d?source=post_page-----868c0f591205---------------------------------------)

And now, in **October 2025**, the long-awaited **Winter ’26 release** is just around the corner. I’m looking forward to reviewing its new features as well.

[## Marketing Cloud Next: Winter ’26 Release Highlights

### The Winter ’26 new feature release for Marketing Cloud Next (Marketing Cloud Growth & Advanced Edition) has been…

medium.com](/@marketingcloudtips/marketing-cloud-next-winter-26-release-highlights-81240775f843?source=post_page-----868c0f591205---------------------------------------)

That’s all for this time!

Stay tuned for more Salesforce Marketing Cloud tips! 😊

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
