# SFMC Tips #178 : Marketing Cloud Next: New Segment Preview Feature

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-next-new-segment-preview-feature-be716460c70f

---

# SFMC Tips #178 : Marketing Cloud Next: New Segment Preview Feature

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--be716460c70f---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--be716460c70f---------------------------------------)

4 min read

·

Sep 26, 2025

--

Photo by [COSMOH](https://unsplash.com/@cosmoh?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

**Marketing Cloud Next** (Marketing Cloud Growth & Advanced Edition) now offers a new feature that allows you to **preview** the data included in your segments directly from the segment screen.

> *This feature is part of the September release of Data Cloud and is now available for use in the interface.*

The preview functionality is powered by the **Data Lens**, inspired by **Tableau Prep**. Its main features include:

### **1. Data Default View**

- Automatically aggregates and visualizes null (no data) values and the distribution of values (percentage of the whole) for each field.
- Enables quick checks of **data quality** and **segment accuracy**.

### **2. Data Grid View**

- Displays data at the record level in a tabular format.
- Allows users to review long or complex values with ease.

The preview supports up to **1,000 rows displayed** and **profiling for up to 1 million records**, with random sampling from the dataset. This allows users to safely test filters, verify expected results, and make adjustments while reducing trial-and-error costs.

Another key benefit is that “**Publishing is not required”**. You can preview segments even before they are published, improving workflow efficiency.

### **Q: How do I access it?**

By enabling it in the Data Cloud **Feature Manager**, a “**Preview”** button will appear in the upper-right corner of the screen where you create segment conditions.

> *Tips: Before checking the screen, go to* ***Data Cloud Settings****, search for “****Feature Manager****”, and enable the Segment Preview feature.*

### ① Data Default View

**Advantages**  
You can check what types of data exist in each column, roughly when the data was created, and which records contain null (no data) values. This makes it easy to quickly assess whether there are any anomalies or if it’s safe to exclude null values.  
Additionally, clicking on a specific data type automatically filters the table below, allowing you to focus on the values of interest immediately.

**Limitations**  
Since cell widths cannot be adjusted, long values such as Unified Individual Ids need to be reviewed one record at a time by hovering over them. However, even if the content is not fully visible, it can still be copied and pasted.

### ② Data Grid View

Cell widths can be freely adjusted, allowing long values to be fully displayed. The Grid View is synchronized with the Default View, so you can first review the overall data in the Default View and then switch to the Grid View to adjust column widths as needed.

### Field List View

This view lets you choose which fields to display or hide in both the Default and Grid Views, enabling you to focus on the data that matters most.

### Credit Consumption

This feature is enabled by default at no additional license cost. Usage is billed at **2 credits per 1 million records processed**.

## Conclusion

The feature introduced here is **not part of the Winter ’26 release**, but rather included in the monthly Data Cloud updates. Marketing Cloud Next features are also being enhanced alongside these updates, so it’s worth keeping an eye on future releases.

In particular, the **Segment Preview feature** is a long-awaited addition for Marketing Cloud Next users. By using it in your day-to-day work, you can quickly experience how much more efficient segment validation and testing can be.

That’s all for this update.

Stay tuned for more Salesforce Marketing Cloud tips! 😊

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
