# SFMC Tips #314 : Marketing Cloud Next: Configuring Identity Resolution Filters

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-next-configuring-identity-resolution-filters-72508fa04654

---

# SFMC Tips #314 : Marketing Cloud Next: Configuring Identity Resolution Filters

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--72508fa04654---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--72508fa04654---------------------------------------)

4 min read

·

Jun 22, 2026

--

Photo by [Aaron Huber](https://unsplash.com/@aahubs?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

In the July 2026 Data 360 (Data Cloud) feature release, a new filtering capability was added to Identity Resolution.

**This allows you to pre-filter the data used for Identity Resolution and run Identity Resolution against only specific data sets**.

For example, you can now:

- **Perform Identity Resolution separately for B2B and B2C data**
- **Validate matching rules using only test data**
- **Exclude low-quality data**

## Difference Between Data Space Filters and Identity Resolution Filters

Previously, similar requirements could be achieved using **Data Space Filters**.

[## SFMC Tips #207 : Marketing Cloud Next: How to Configure Data Space Filters

### When you start operating Marketing Cloud Next Growth & Advanced Edition, you install a data kit. At this timing, CRM…

medium.com](/@marketingcloudtips/marketing-cloud-next-how-to-configure-data-space-filters-6880c21093bd?source=post_page-----72508fa04654---------------------------------------)

However, Data Space Filters and Identity Resolution Filters differ significantly in both when they are applied and the scope of their impact.

## Data Space Filters

- Applied when data is ingested into a Data Space
- Only a single condition logic type can be used: either **AND** or **OR**
- Data is no longer available for Segmentation
- Data is no longer available for Calculated Insights
- Data is no longer available for Data Graphs
- Data is no longer available for Identity Resolution

## Identity Resolution Filters

- Applied only when a specific Identity Resolution process runs
- Combined condition logic using both **AND** and **OR** is supported
- Data generally remains available for Segmentation
- Data generally remains available for Calculated Insights
- Data generally remains available for Data Graphs
- Data can continue to be used by other Identity Resolution rules

***Tip:*** *From a Marketing Cloud Next perspective, it is important to determine whether the data should remain stored within the Data Space while being excluded from a specific Identity Resolution process, or whether the data does not need to be ingested into Data Cloud at all.*

## Configuration Steps

### 1. Open a Specific Identity Resolution Rule

### 2. Add a Filter

### 3. Configure Conditions

For example:

```
Industry = Banking  
AND  
Title = Manager  
  
OR  
  
Industry = Insurance  
AND  
Title IN (Director, Manager)
```

**Not only can you use AND conditions, but you can also add additional groups to create OR conditions**.

The following options are available:

### Trim Spaces

Ignores leading and trailing spaces when comparing string values.

### Case Sensitive

Determines whether uppercase and lowercase characters are treated as different values during comparison.

## Limitations

### Group Configuration

- Currently, a maximum of **3 groups** can be configured.
- Groups are automatically treated as **OR** conditions.

### Conditions Within a Group

- Each group can contain up to **3 conditions**.
- Conditions within a group are automatically treated as **AND** conditions.

## Considerations

### Not Intended for Record-Level Exclusion

Salesforce describes this feature as being intended for **partitions (large data segments)**.

- Appropriate examples:

```
Account Type = B2B  
Industry = Banking  
Data Source = CRM
```

- Inappropriate examples:

```
Email = test@example.com  
CustomerID = 12345
```

This feature is recommended for filtering large categories of data rather than excluding individual records.

## Full Refresh Occurs When Filters Are Changed

When a filter is added to or modified within an existing Identity Resolution rule, the Identity Graph is recalculated.

As a result, a **Full Refresh** is performed and all records are reprocessed.

In large environments, this may impact processing time and Data Cloud credit consumption, so use caution.

## Summary

With the introduction of Identity Resolution Filters, you can now:

- **Separate B2B and B2C data**
- **Validate matching rules using test data**
- **Exclude unnecessary data from Unified Profile creation**

One of the biggest advantages is the ability to validate matching rules using sample data before applying them to all production data. Additionally, excluding low-quality or unintended data can help improve the accuracy of Unified Profile creation.

Furthermore, this feature serves a different purpose than Data Space Filters. While Data Space Filters control the data that is ingested into a Data Space, **Identity Resolution Filters control only the data used to create Unified Profiles while keeping the data stored in the Data Space**.

As a result, data excluded by an Identity Resolution Filter can still be used for Segmentation, Calculated Insights, Data Graphs, and other use cases. At the same time, it is excluded from Identity Resolution processing, enabling more flexible and safer data utilization.

To operate Data Cloud Identity Resolution more accurately and efficiently, be sure to take advantage of this new feature.

That’s all for this article.

Stay tuned for more Salesforce Marketing Cloud tips! 😎

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
