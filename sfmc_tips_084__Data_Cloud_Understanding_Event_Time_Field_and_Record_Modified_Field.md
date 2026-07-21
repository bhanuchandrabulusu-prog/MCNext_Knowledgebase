# SFMC Tips #84 : Data Cloud: Understanding Event Time Field and Record Modified Field

**Source:** https://medium.com/@marketingcloudtips/data-cloud-understanding-event-time-field-and-record-modified-field-12f1ecf55126

---

# SFMC Tips #84 : Data Cloud: Understanding Event Time Field and Record Modified Field

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--12f1ecf55126---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--12f1ecf55126---------------------------------------)

7 min read

·

Feb 21, 2025

--

Photo by [Samantha Gades](https://unsplash.com/@srosinger3997?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

When creating a data stream in Salesforce Data Cloud, the **Event Time Field** and **Record Modified Field** are crucial configuration fields. These fields are configured in the following section of the data stream settings:

![]()

Failing to understand the roles and appropriate configurations of these fields can lead to *significant issues*. This article aims to help you understand these two fields by comparing their functionality and usage.

This article is related to previous topics such as “**Understanding How to Update Data Extension Integrations**” and “**Key Configuration Insights for Date vs. DateTime**”. It’s recommended to read these articles together for a complete understanding.

[## SFMC Tips #81 : Understanding How to Update Data Extensions in Data Cloud

### One of the essential tasks after connecting Marketing Cloud to Data Cloud is linking your data extensions to data…

medium.com](/@marketingcloudtips/understanding-how-to-update-data-extensions-in-data-cloud-25a44bf180b7?source=post_page-----12f1ecf55126---------------------------------------)

[## SFMC Tips #83 : Date vs. DateTime: Key Configuration Insights for Data Cloud Users

### This article builds on the insights shared in my earlier post, Data Cloud: Marketing Cloud Integration Tips Summary…

medium.com](/@marketingcloudtips/date-vs-datetime-key-configuration-insights-for-data-cloud-users-71bfcc6a62e3?source=post_page-----12f1ecf55126---------------------------------------)

## Fundamental Basics

### Event Time Field

- **Selectable Categories:** Engagement
- **Requirement:** Mandatory

### Record Modified Field

- **Selectable Categories:** Profile, Engagement, Others
- **Requirement:** Optional

### Differences Between Full Refresh and Upsert

- **Full Refresh:** Neither the Event Time Field nor the Record Modified Field is applied.
- **Upsert:** Both the Event Time Field and the Record Modified Field are applied.

## 1. Event Time Field

### Overview

The **Event Time Field** acts like a “**sub-primary key**”, supplementing the primary key in the data.

![]()

**Supported Data Types:**

- DateTime and Date

**Selectable Categories:**

- Engagement only

**Update Method:**

- Applicable only for Upsert. While required for Full Refresh, it is not applied and has no effect.

### **About the Key System Field — “**cdp\_sys\_PartitionDate”

DateTime or Date data selected as the “Event Time Field” is automatically recorded in the system-generated field `cdp_sys_PartitionDate`.

The `cdp_sys_PartitionDate` is a formula field (Date or DateTime). The value of the date field selected as the Event Time Field is input here.

However, in the case of DateTime, the time component (“hours:minutes:seconds”) is **converted to** `00:00:00` using the following formula: `DAYPRECISION(formulaField['EventTimeField_API_Name']);`

\*This formula processes the value ***before* Time Zone Conversion**.

To clarify this explanation, consider the following example with record A001:

The time zone of my environment is JST (Japan Standard Time).

1. The **Created\_Date**, set as the Event Time Field in this case, was imported as **2025/1/20 19:00:00 (UTC)**.
2. The formula converts the time component to **2025/1/20 00:00:00 (UTC)**.
3. Subsequently, Time Zone Conversion adjusts it to **2025/1/20 09:00:00 (JST)**.
4. As a result, `cdp_sys_PartitionDate` becomes **2025/1/20 09:00:00**.

OK?

For details about the “Time Zone Conversion” that occurs with DateTime fields in Data Cloud, refer to the article linked below:

[## SFMC Tips #83 : Date vs. DateTime: Key Configuration Insights for Data Cloud Users

### This article builds on the insights shared in my earlier post, Data Cloud: Marketing Cloud Integration Tips Summary…

medium.com](/@marketingcloudtips/date-vs-datetime-key-configuration-insights-for-data-cloud-users-71bfcc6a62e3?source=post_page-----12f1ecf55126---------------------------------------)

### System Processing of the Event Time Field

How does the Event Time Field utilize `cdp_sys_PartitionDate`? Here is an overview of the processes:

- **If the Event Time Field data matches** `cdp_sys_PartitionDate`**:**

→ The existing record is **updated (overwritten)**.

- **If the Event Time Field data does not match** `cdp_sys_PartitionDate`**:**

→ A new record is **inserted**.

### Points to Note

- If the date in `cdp_sys_PartitionDate` differs even slightly, a new record will be created, even if the primary key is the same.
- The comparison between the imported date data and `cdp_sys_PartitionDate` occurs after the formula converts the time component to `00:00:00`. Therefore, **unless the imported data crosses into the next day**, the formula results in the same date, avoiding duplicate record insertions.💡
- If duplicate new records are created, it pertains to a separate record entirely. Consequently, “Modified Record Fields”, explained below, are ignored.

### Conclusion and Recommended Settings

If you want to update records with the intention of overwriting them, select fields that will not change in the future, such as:

- Record creation date
- Purchase date
- Email open date
- Email click date

Once the Event Time Field is set, it cannot be changed to a different field. Therefore, careful consideration is essential before making this decision.

## 2. Record Modified Field

### Overview

The **Record Modified Field** is a field used to determine whether a record should be overwritten during processing.

When imported, the Record Modified Field is set as a H**igh Water Mark** (maximum value). This High Water Mark serves as the basis for determining whether a record should be updated or ignored.

![]()

**Supported Data Types:**

- Only DateTime (\*Date type is not supported)

**Selectable Categories:**

- Profile, Engagement, Other

**Update Method:**

- Applicable only for Upsert. While it can also be selected for Full Refresh, it has no effect in that case.

### Rules of Operation

- **When the new record’s DateTime exceeds the existing record by at least one second:**

→ The record is **updated (overwritten)**.

- **When the new record’s DateTime matches or is earlier than the existing record**:

→ The update is **ignored**.

### Example

If the current value of the Record Modified Field is **2025/2/19 10:25:45**, the update rules for a record with the same primary key are as follows:

- **For a new value of 2025/2/19 10:25:46 or later**:

→ The record is overwritten.

- **For a new value of 2025/2/19 10:25:45 or earlier**:

→ The update is ignored.

### When This Field is Unnecessary

The Record Modified Field is likely unnecessary in the following scenarios:

1. When data files are expected to always be processed in sequential order.
2. When the processing order of data files does not matter.

### Conclusion and Recommended Settings

In environments where the order of file processing may become disordered, configuring the Record Modified Field helps maintain data integrity. This field is typically set to **Last Modified Date** for most use cases.

## 3. Processing Order of Both Fields

As expected, the **Event Time Field** acts as a sort of sub-primary key. Therefore, it is processed first, followed by the **Record Modified Field**.

- **Processed First**: Event Time Field
- **Processed Next**: Record Modified Field

### Important Notes

If the Event Time Field data does not match the value of `cdp_sys_PartitionDate` and a new record is created, this new record is treated as a completely separate record. In this case:

- There is no corresponding **Record Modified Field** for comparison.
- As a result, a record is created with a duplicate primary key.

## 4. Differences in High Water Mark Behavior

The behavior of the High Water Mark (maximum value) during data extraction and processing varies depending on the target data source.

### For Cloud Storage (e.g., Google Cloud Storage) File Integration

- The High Water Mark is managed on a **per-record basis** using the **Record Modified Field** described in this article.

![]()

### For Data Extension Integration

- The High Water Mark for data extensions is determined based on the **Data Extension Extract Field**.

It is managed on a **per-data-extension basis**, meaning:

- The **Data Extension Extract Field** within the data extension is sorted in ascending order.
- The maximum value from this sorting is recorded as the High Water Mark.

Additionally, the High Water Mark for data extensions can be managed via **Email Studio > Interaction Tab > Data Factory Utility**, as explained in a previous article.

[## SFMC Tips #81 : Understanding How to Update Data Extensions in Data Cloud

### One of the essential tasks after connecting Marketing Cloud to Data Cloud is linking your data extensions to data…

medium.com](/@marketingcloudtips/understanding-how-to-update-data-extensions-in-data-cloud-25a44bf180b7?source=post_page-----12f1ecf55126---------------------------------------)

## Quick Summary

### **Event Time Field**:

- Acts as a sub-primary key.
- Matching dates trigger updates, while mismatched dates can cause duplicate records with the same primary key.

### **Record Modified Field**:

- Based on comparing the selected field’s DateTime value.
- Updates (overwrites) are allowed only when the new value exceeds the High Water Mark. Otherwise, the record is ignored.

## Conclusion

Understanding how to configure these fields accurately will help ensure **data integrity** and improve **processing performance**.

That’s all for today!

Thank you for reading.

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
