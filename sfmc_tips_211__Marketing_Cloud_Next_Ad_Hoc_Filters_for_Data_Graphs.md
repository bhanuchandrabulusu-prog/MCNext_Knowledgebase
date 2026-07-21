# SFMC Tips #211 : Marketing Cloud Next: Ad Hoc Filters for Data Graphs

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-next-ad-hoc-filters-for-data-graphs-466c231740fe

---

# SFMC Tips #211 : Marketing Cloud Next: Ad Hoc Filters for Data Graphs

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--466c231740fe---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--466c231740fe---------------------------------------)

4 min read

·

Dec 9, 2025

--

Photo by [Marcos Paulo Prado](https://unsplash.com/@marcospradobr?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

With the October 2025 release of Data Cloud, **Ad Hoc Filters** have been added to Data Graphs.

Until now, Sort & Limit Filters (ascending/descending + limit) were already available, and now **Ad Hoc Filters** can be used in addition to those.

“Ad hoc” means “**for a specific purpose**”, and — as the name suggests — this feature allows you to more precisely narrow down Data Model Objects (DMOs) included in a Data Graph based on your specific use case.

By leveraging this filter, you can expect benefits such as:

- **Reducing the cost of data graph refresh (full refresh)**
- **Optimizing storage usage**

## Perfect match with Repeater Components

One major point is that Ad Hoc Filters work extremely well with **Repeater Components** in Marketing Cloud Next.

While Repeater Components currently have restrictions on which data types can be used in conditions, **Ad Hoc Filters allow Boolean fields** which is a huge advantage.

## Define the logic on the CRM side

In practice, you can prepare conditions on the CRM side using checkbox fields or formula fields, and then include the results in the Ad Hoc Filter. Ultimately, those results can flow into the Repeater Component.

For example:

**If you want to display only records from today onward:**

- Create a Boolean formula field in CRM that returns TRUE if the record is “future or today”
- Include only records that are TRUE into the Data Graph for display

*\*Currently, there is no operator for comparing with “today” either ① in Data Graph filters, or ② in the expression editor of Repeater Components.*

By implementing a Repeater Component with this setup, unnecessary records won’t enter the Data Graph in the first place, which keeps the UI configuration much simpler.

## Key Considerations When Connecting the Engagement DMO

When you connect the Engagement DMO to a data graph, the following limitations are applied to filtering conditions by default:

- **Record limit:** Up to 10 records (*can be extended to 100*)
- **Time limit:** Last 7 days (*can be extended to 30 days*)

### **What These Limits Mean**

The most important point is that, by default, only data from the past 7 days can be retrieved. Therefore, depending on your use case, you may need to extend this setting to up to 30 days.

**Most Critical Point to Watch**

Special caution is required when using the data graph for the following purposes:

- **Exit Criteria**
- **Decision elements**

Since the Engagement DMO can only retain data for up to the most recent 30 days, evaluations based on these conditions are limited to data (such as record creation dates) within that 30-day window.

Because of this limitation, depending on the scenario, you may need to keep the flow duration within 30 days. If you need the flow to run longer than 30 days, you will need to design a workaround — such as using **Calculated Insights** (which do not have time limit restrictions) as condition fields.

## Conclusion

Although Repeater Components already support conditional configuration, there were limitations such as not being able to use Boolean fields and limited expression options.

*TIPS: If you want to use a Boolean field in a Repeater Component’s expression, convert it to* ***Text*** *using a* ***Formula field in Data Cloud****.*

Ad Hoc Filters overcome these weaknesses and make it much easier to control how data is displayed.

### Summary

- Ad Hoc Filters are a filtering capability for Data Graphs
- They help reduce refresh and storage costs
- A great match for Repeater Components
- Boolean fields can be used, enabling flexible conditions

### Limitation

- Currently only “All Conditions Are Met” (AND condition) is available
- In the case of the Engagement DMO, the maximum time limit is 30 days

That’s all for now.

Stay tuned for more Salesforce Marketing Cloud tips! 😎

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
