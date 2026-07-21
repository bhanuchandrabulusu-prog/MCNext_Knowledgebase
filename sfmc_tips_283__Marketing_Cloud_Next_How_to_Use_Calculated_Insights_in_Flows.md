# SFMC Tips #283 : Marketing Cloud Next: How to Use Calculated Insights in Flows

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-next-how-to-use-calculated-insights-in-flows-a83a3eb48909

---

# SFMC Tips #283 : Marketing Cloud Next: How to Use Calculated Insights in Flows

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--a83a3eb48909---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--a83a3eb48909---------------------------------------)

5 min read

·

Apr 27, 2026

--

Photo by [Magnus Jonasson](https://unsplash.com/@magnusjonasson?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

In this article, I would like to organize the **key considerations when using calculated insights in Segment Triggered Flows** in Marketing Cloud Next Growth & Advanced Edition.

At first glance, it may look simple, but there are several common **pitfalls**, so it is recommended to understand them before implementation.

The main points are the following three:

- **Dimension configuration is required**
- **Use resources instead of Get Records**
- **Prepare records that could not be calculated**

I will explain each one.

## Dimension configuration is required

This is the basic setting.

When using calculated insights in a flow, you must specify a **dimension** as a WHERE condition.

In Marketing Cloud Next, data graphs are generally based on Unified Individuals, and calculated insights are also created based on the Unified Individual ID (the same applies to standard scoring).

Therefore, you need to set the **Unified Individual ID as the dimension**.

If this setting is not configured, an error will occur when saving the flow, as shown below, making it relatively easy to notice.

![]()

## Use resources instead of Get Records

Next, the handling of the Unified Individual ID is important.  
*\*In some cases,* ***operators cannot be selected, and only “Equals” is available****.*

At that time, you may be tempted to use the Get Records element to retrieve the Unified Individual ID, but with this method, **the value becomes NULL**.

![]()

This happens both in debug and production, and as a result, all records flow into the default path.

To avoid this issue:

- **Create a new resource as a “variable”**
- **Assign the triggered Unified Individual ID to that variable**

By using this variable as the dimension, it will work correctly in both debug and production.

![]()

***Tips:*** *If operators can be selected, you can also avoid creating a resource variable by setting “Is Null = False”.*

## Prepare records that could not be calculated

This is the most commonly overlooked point.

For standard scoring calculated insights, values are prepared for all Unified Individuals. Even if a score does not exist, it is stored as “0”.

But what about custom calculated insights?

For example, if you aggregate based on sales data (such as Sales Order Product Engagement), naturally only data for “people who purchased” will exist. For instance, if you count the number of purchases:

- **People who purchased → Record exists in calculated insight**
- **People who did not purchase → No record in calculated insight**

In this state, if you use calculated insights in decision conditions:

- **People who purchased (records exist) → Branch works normally**

- **People who did not purchase (no records) → Forced exit from the flow due to error**

This behavior also occurs in production:

If it is acceptable for the flow to exit in such cases, it may be fine. However, in scenarios such as “sending emails to non-purchasers”, this becomes critical.

Therefore, when creating custom calculated insights:

👉 **Always prepare records where “no value exists = 0”**

This design is essential.

- **If records for non-existing values are prepared → No error occurs, and the flow proceeds to the End.**

How was it?

Among the points introduced this time, only the missing **dimension configuration** is clearly detected as an error. The other issues only appear during execution, **making them difficult to identify without debugging**.

Since Marketing Cloud Next is composed of multiple mechanisms, it has a tendency to produce “**silent errors**” where behavior looks correct but is not as intended.

The points in this article can be identified through careful debugging, but conversely, they are also easy to overlook if debugging is not performed.

Therefore, for “Decision” elements and “Exit Criteria”, it is strongly recommended to test repeatedly while considering multiple scenarios.

Additionally, **related attributes also require a dimension in the WHERE clause**. However, unlike calculated insights, related attributes do not cause errors even if data such as “people who purchased” does not exist. **Errors occur only with calculated insights**.

In that case, you might think it is better to always use related attributes, but there is a difference in the data time limits that can be retrieved.

- **Time limit for related attributes**: Default 7 days  
   \*[*Can be extended up to 30 days*](/p/6880c21093bd)
- **Time limit for calculated insights**: No limit

For this reason, there are cases where calculated insights must be used. When doing so, be sure to consider the points above.

That’s all for this time.

Stay tuned for more Salesforce Marketing Cloud tips! 😊

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
