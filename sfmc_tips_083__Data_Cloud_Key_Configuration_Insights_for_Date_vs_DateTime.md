# SFMC Tips #83 : Data Cloud: Key Configuration Insights for Date vs. DateTime

**Source:** https://medium.com/@marketingcloudtips/date-vs-datetime-key-configuration-insights-for-data-cloud-users-71bfcc6a62e3

---

# SFMC Tips #83 : Data Cloud: Key Configuration Insights for Date vs. DateTime

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--71bfcc6a62e3---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--71bfcc6a62e3---------------------------------------)

9 min read

·

Feb 18, 2025

--

Photo by [SJ 📸](https://unsplash.com/@uxsj_ph?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

This article builds on the insights shared in my earlier post, *Data Cloud: Marketing Cloud Integration Tips Summary*. Given the importance of this topic, I decided to dedicate a standalone post to help you deepen your understanding of Date and DateTime data types.

[## SFMC Tips #78 : Data Cloud: Marketing Cloud Integration Tips Summary

### In this article, I will share tips for integrating Data Cloud and Marketing Cloud Engagement. I plan to update this…

medium.com](/@marketingcloudtips/data-cloud-marketing-cloud-engagement-integration-tips-9e160167cda8?source=post_page-----71bfcc6a62e3---------------------------------------)

## What Are the Most Critical Data Types in Data Cloud?

Among the various data types in Data Cloud, I believe **Date** and **DateTime** are particularly crucial. These two types significantly impact data imports, mapping, and operational accuracy, requiring careful configuration.

In this article, I’ll summarize the key points for configuring Date and DateTime data types. Let’s dive in!

## 1. Mapping Requirements with Standard DMO Fields

In Salesforce Data Cloud, the **Individual DMO** (Data Model Object), a standard object, includes fields like **Birth Date**. Some date fields in this object require mapping to the **DateTime** type, not the **Date** type.

For example, even if the imported date data in the data stream is automatically classified as the **Date** type, you may need to change it to **DateTime** to ensure compatibility.

**Tips:** The only acceptable type mismatch when mapping **DLO** (Data Lake Object) to **DMO** is when a Number field in DLO is mapped to a Text field in DMO.

## 2. Key Considerations When Changing Between Date and DateTime Types

When switching between Date and DateTime types, always adhere to the format automatically determined by Data Cloud.

### Example 1: From Date to DateTime

If the auto-detected format for Date is `MM/dd/yyyy`, retain this exact format when converting to DateTime.

### Example 2: From DateTime to Date

If the auto-detected format for DateTime is `MM/dd/yyyy HH:mm:ss ZZZ`, retain this exact format when converting to Date.

You might assume that DateTime formats always require time components (hours, minutes, seconds). However, this is unnecessary. It’s highly recommended to use the auto-detected format as-is

![]()

**Tips:** After importing, verify whether the time components have been captured correctly. If not, check the **pattern string** (e.g., MM, dd) and adjust the format as needed.

## References

- [Date and DateTime Formats Help Documentation](https://help.salesforce.com)

## 3. Differences in Formatting Across Salesforce Products

In Salesforce CRM:

- **Date** fields are auto-detected as **Date** type.
- **DateTime** fields are auto-detected as **DateTime** type.

In **Marketing Cloud**, however, all Date fields are auto-detected as **DateTime** type. This difference is critical to note.

**Tips:** Even if a field is auto-detected as DateTime in Marketing Cloud, consider changing it to Date if the field’s purpose aligns better with the Date type. Adjust as necessary.

## 4. Time Zone Conversion for DateTime Type

When importing date data, the **Date type** is treated as a “**fixed value**”, while the **DateTime type** is subject to **Time Zone Conversion**.

First, if DateTime data does not contain a time zone value within the data, it is imported as being in the **UTC time zone**. *(This is important!)* 💡

Next, **Time Zone Conversion** refers to the process where DateTime fields are influenced by the time zone of the organization configured in Data Cloud, resulting in changes to the displayed values.

For example, if the organization’s time zone in Data Cloud is set to JST (Japan Standard Time), the values are converted from UTC to JST for display purposes.

To make this clearer, let’s break it into two processes:

1. **Process ①:** When data is imported in the UTC time zone
2. **Process ②:** When Time Zone Conversion occurs

## Process ①: When Data Is Imported in the UTC Time Zone

*For this example, assume the organization’s time zone is set to* ***JST****.*

**Marketing Cloud DataTime:**  
The data is imported in UTC, not in the local time zone of Marketing Cloud (CST). Because the difference between UTC and CST is 6 hours, the data is adjusted by **+6 hours** when imported into Data Cloud.

**Salesforce CRM DataTime:**  
If the Salesforce CRM time zone is JST, the data is imported in UTC, not JST. As the difference between UTC and JST is 9 hours, the data is adjusted by **-9 hours** and imported in UTC.

**Salesforce CRM Date (Exception):**  
If a field originally of **Date type** is converted to **DateTime type** during import (e.g., for handling fields like Birth Date), the data is not adjusted by **-9 hours**. Instead, it is imported as `YYYY/MM/DD 00:00:00 (UTC)`.

**Cloud Storage (e.g., Google Cloud Storage) DataTime:**  
The data is imported in UTC without any adjustments (**±0 hours**) and remains in its original state.

This is the state before the Time Zone Conversion, but it’s already quite complex at this point. Next, we’ll move on to after the Time Zone Conversion.

## Process ②: When Time Zone Conversion Occurs

*For this example, assume the organization’s time zone is set to* ***JST****.*

**Marketing Cloud DateTime Data:**  
After being adjusted by **+6 hours** during import into UTC, the data is converted from UTC to JST through **Time Zone Conversion**, adding an additional **+9 hours**. This results in a total adjustment of **+15 hours** for display.

- **Imported Data:** +6 hours
- **Displayed Data:** +15 hours (in JST environment)

**Salesforce CRM DateTime Data:**  
If the data originates from a CRM organization set to JST, it is first adjusted by **-9 hours** during import into UTC. Then, **Time Zone Conversion** from UTC to JST adds **+9 hours**, resulting in **±0 hours** in the display.

- **Imported Data:** -9 hours (in JST environment)
- **Displayed Data:** ±0 hours

**Salesforce CRM Date Exception:**  
As mentioned earlier, for Date fields converted to DateTime, **no -9 hour adjustment** occurs (“***fixed value”***). However, the data is still converted from UTC to JST during **Time Zone Conversion**, resulting in **+9 hours** for display.

- **Imported Data:** ±0 hours
- **Displayed Data:** +9 hours (in JST environment)

**Cloud Storage DateTime Data:**  
When Cloud Storage data does not contain time zone values, the displayed time is always adjusted by **+9 hours**. Unlike Salesforce CRM, no exceptions apply.

- **Imported Data:** ±0 hours
- **Displayed Data:** +9 hours (in JST environment)

What did you think? It’s quite confusing, isn’t it?

By the way, the screen display above is an example from Data Explorer. In fact, the displayed content can vary depending on the tool you use. This will be explained in the next section.

## 5. Differences in Display Across Various Tools

*For this example, assume the organization’s time zone is set to JST.*

## ① Data Explorer

As explained in the previous section, in **Data Explorer**, DateTime fields are displayed with the **Time Zone Conversion applied** rather than retaining their original UTC values.

**Marketing Cloud**: DateTime data is displayed with a **+15 hours** offset.

**Salesforce CRM**:

- **DateTime → DateTime**: Displayed as is, with **no offset (±0 hours)**.
- **Date → DateTime**: Displayed as is, with a **+9 hours** offset.

**Cloud Storage**: If the DateTime data lacks a time zone value, a **+9 hours** offset.

**Tips:** Although seconds and fractional seconds are not displayed on the UI, they remain stored in the data. If such values exist, filtering may not work as expected.

## ② Profile Explorer

In **Profile Explorer**, DateTime fields are also displayed with the T**ime Zone Conversion applied**, similar to Data Explorer.

**Marketing Cloud**: DateTime data is displayed with a **+15 hours** offset.

**Salesforce CRM**:

- **DateTime → DateTime**: Displayed as is, with **no offset (±0 hours)**.
- **Date → DateTime**: Displayed as is, with a **+9 hours** offset.

**Cloud Storage**: If the DateTime data lacks a time zone value, a **+9 hours** offset.

## ③ Reports

In **Reports**, DateTime fields are similarly displayed with the T**ime Zone Conversion applied**.

**Marketing Cloud**: DateTime data is displayed with a **+15 hours** offset.

**Salesforce CRM**:

- **DateTime → DateTime**: Displayed as is, with **no offset (±0 hours)**.
- **Date → DateTime**: Displayed as is, with a **+9 hours** offset.

**Cloud Storage**: If the DateTime data lacks a time zone value, a **+9 hours** offset.

**Tips:** Seconds and fractional seconds are omitted in the UI but are still retained in the data. Filtering may not work as expected if these values are present.

## ④ Query Editor

Unlike the first three tools, **Query Editor** displays DateTime fields **before Time Zone Conversion** (i.e., in their original UTC format).

**Marketing Cloud**: DateTime data is displayed with a **+6 hours** offset.

![]()

**Salesforce CRM**  
**DateTime → DateTime**: Displayed as is, with a **-9 hours** offset.

![]()

**Salesforce CRM**  
**Date → DateTime**: Displayed as is, with **no offset (±0 hours)**.

![]()

**Cloud Storage:** If the DateTime data lacks a time zone value, **no offset (±0 hours)**.

**Pro Tips:** When filtering DateTime fields in Query Editor’s `WHERE` clause, use the **pre-conversion values** displayed in the Query Editor. For example:

```
WHERE "date__c" = cast('2025-01-21 02:15:48' as timestamp(1))
```

![]()

## ⑤ Segments

In **Segments**, which is critical for creating delivery data, **post-Time Zone Conversion** values are used, similar to the first three tools. However, **hours, minutes, and seconds** are excluded from the data and cannot be used. Only records between **00:00:00 AM and 23:59:59 PM** are retrieved.

**Marketing Cloud**: DateTime data is displayed with a **+15 hours** offset.

**Salesforce CRM**:

- **DateTime → DateTime**: Displayed as is, with **no offset (±0 hours)**.
- **Date → DateTime**: Displayed as is, with a **+9 hours** offset.

**Cloud Storage**: If the DateTime data lacks a time zone value, a **+9 hours** offset.

### Important Note:

Time Zone Conversion may result **in crossing date boundaries**, causing discrepancies between the actual date in the data source and the extracted date.

For example:  
If Marketing Cloud contains the data `2025-02-22 10:00:00 (CST)`, it will be converted to `2025-02-23 01:00:00 (JST)`in Data Cloud. Thus, Segments will extract it under `2025/2/23`, not `2025/2/22`. 😱

## Conclusion

The handling of **Date** and **DateTime** types is crucial when working with Data Cloud. In particular, it’s important to pay attention to the format and time zone discrepancies when importing data to avoid impacting operations and analysis. Specifically, if the format is entered incorrectly, the data might not be imported correctly later, so always use the system-detected format.

This might seem a bit complicated, but as you start using various connectors to import data, it’s crucial to check how much time zone shift occurs in DateTime data. Regularly confirming this will help prevent issues later.

By making these practices a habit, you can ensure accurate data management and smooth operations. I highly recommend giving it a try!

Finally, I realized the “Time Zone Conversion section” got a bit disorganized, so I’ve summarized it below for clarity:

## Time Zone Conversion Summary

*For this example, assume the organization’s time zone is set to* ***JST****.*

**Marketing Cloud**

- Import Data: +6 hours
- Screen Display Data: +15 hours (in a JST environment)

**Salesforce CRM (DateTime → DateTime)**

- Import Data: -9 hours (in a JST environment)
- Screen Display Data: ±0 hours

**Salesforce CRM (Date → DateTime)**

- Import Data: ±0 hours
- Screen Display Data: +9 hours (in a JST environment)

**Cloud Storage**

- Import Data: ±0 hours
- Screen Display Data: +9 hours (in a JST environment)

**Things Using Import Data (Before Time Zone Conversion)**

- Query Editor

**Things Using Screen Display Data (After Time Zone Conversion)**

- Data Explorer
- Profile Explorer
- Reports
- Segments

Thank you for reading.

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
