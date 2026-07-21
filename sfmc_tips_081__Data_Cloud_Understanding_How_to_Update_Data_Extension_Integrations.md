# SFMC Tips #81 : Data Cloud: Understanding How to Update Data Extension Integrations

**Source:** https://medium.com/@marketingcloudtips/understanding-how-to-update-data-extensions-in-data-cloud-25a44bf180b7

---

# SFMC Tips #81 : Data Cloud: Understanding How to Update Data Extension Integrations

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--25a44bf180b7---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--25a44bf180b7---------------------------------------)

11 min read

·

Feb 14, 2025

--

Photo by [Alejandro Luengo](https://unsplash.com/@aluengo91?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

One of the essential tasks after connecting Marketing Cloud to Data Cloud is linking your data extensions to data streams. This enables the records within your data extensions to be imported into Data Cloud, making them accessible for further utilization.

However, there are several options for extracting data, which can be a source of confusion for beginners managing Data Cloud. This article aims to clarify these extract modes and enhance your understanding of how to handle data extension updates effectively.

## Data Extension Extract Modes

There are two primary modes for extracting data extensions:

1. **Full Refresh**
2. **Delta Extract**

When imported into Data Cloud, these modes correspond to the following terms:

![]()

- **Full Refresh Import**: Equivalent to an “**Overwrite**” Import in Marketing Cloud.
- **Upsert Import**: Equivalent to an “**Add and Update**” Import, which updates or inserts records without deleting existing ones.

Delta extract, often referred to as **Change Data Capture (CDC)**, is further divided into two types:

- **Numeric CDC**
- **DateTime CDC**

## Full Refresh

This Full Refresh refers to what is called “**Overwrite**” in Marketing Cloud. It deletes all the data and replaces it with new data.

**Conditions:** It is only available if the number of data rows is 100 million or smaller.

\*Previously, there was a hard limit of 10 million rows, but this has now been updated to 100 million rows. I checked with Salesforce Support about this, and they mentioned that the change was made in mid-November 2024.

## Delta Extract

Delta extraction, corresponding to an “**Upsert**” action in Marketing Cloud, **does not delete records**. It can be based on:

### Numeric CDC

- Uses a numeric field (e.g., Claim Number) as a baseline.
- Data is sorted in ascending order, and only records exceeding the highest numeric value (High Water Mark) are extracted.

### DateTime CDC

- Uses a date field (e.g., Updated Date) as a baseline.
- Data is sorted in ascending order, and only records with a timestamp exceeding the latest date (High Water Mark) are extracted.

*\*As of now, if you select delta extract (Upsert), there is no way to delete records, and* ***you will need to recreate the data stream****.*

[## Help And Training Community

### Edit description

help.salesforce.com](https://help.salesforce.com/s/articleView?id=000396417&type=1&source=post_page-----25a44bf180b7---------------------------------------)

## Use Cases for Extract Modes

To provide clarity, let’s illustrate these modes using the following example data extension:

![]()

**Data Example:**

- **Day 1:** Initial data (3 rows)

![]()

- **Day 2:** Updated data (5 rows, with new records and updates)

![]()

Changes between Day 1 and Day 2:

- New records (4, 5) were added.
- Record 2 was updated (Status and Updated Date).

### Comparison of Modes:

**Option 1: Full Refresh**

- **Day 1:** Sends all records (3 rows).
- **Day 2:** Sends all records (5 rows).
- **Result:** Includes all the latest data but processes more rows.

**Option 2: Numeric CDC (Claim Number)**

- **Day 1:** Sends all records (3 rows, HWM: 3).
- **Day 2:** Sends only new records (4, 5, HWM: 5).
- **Result:** Updates to record 2 are not captured.

**Option 3: DateTime CDC (Updated Date)**

- **Day 1:** Sends all records (3 rows, HWM: 2019/12/01).
- **Day 2:** Sends updated and new records (2, 4, 5, HWM: 2019/12/02).
- **Result:** Includes all relevant updates and additions.

**Option 4: DateTime CDC (Created Date)**

- **Day 1:** Sends all records (3 rows, HWM: 2019/12/01).
- **Day 2:** Sends only new records (4, 5, HWM: 2019/12/02).
- **Result:** Updates to record 2 are not captured.

## Conclusion

![]()

The following results were obtained:

- In the case of Delta Extrac, the HWM (High Water Mark: Maximum Value) is recorded with each extract, and the next extract is limited to records greater than or equal to that maximum value.
- In the Full Refresh, a total of 8 records were processed (3 + 5), whereas in the DateTime CDC (Updated Date), the update was completed with only 6 records (3 + 3).

Therefore, considering scalability, using DateTime CDC (Updated Date) is the most efficient extract mode.

## Cost Implications

Data Cloud operates on a pay-per-record processing model. While a few records may seem insignificant, the costs can accumulate over time.

- **Cost per record:** $0.00002 USD
- **Credits:** 100,000 credits cost $1,000 USD

![]()

**Example:**

- A full Refresh for a 500,000-record data extension incurs:
- **Daily cost:** $10 USD
- **Monthly cost:** $300 USD
- **Yearly cost:** $3,600 USD

These costs highlight the importance of choosing the right extract modes.

### [Important Update]

Starting April 15, 2025, a new rate of **500 credits per 1 million rows** will apply to “structured data” ingested into data streams from internal Salesforce data sources, including Salesforce CRM, Marketing Cloud Engagement, Marketing Cloud Personalization, and Commerce Cloud. This rate covers both “batch processing” and “streaming processing”.

This represents a 75% reduction compared to the previous rate of **2,000 credits per 1 million rows**, leading to substantial cost savings.

Pricing structure before April 14, 2025

Pricing structure after April 15, 2025

[## SFMC Tips #101 : Data Cloud: Significant Price Reduction for Data Pipeline Credit Usage

### In Salesforce Data Cloud, the consumption of Data Cloud credits varies depending on the type of feature being used…

medium.com](/@marketingcloudtips/data-cloud-significant-price-reduction-for-data-pipeline-credit-usage-85e6a574d83e?source=post_page-----25a44bf180b7---------------------------------------)

*Note:* The above article was calculated based on the previous rate of 2,000 credits per 1 million rows, so now it can simply be calculated **as one-fourth of that**.

## Tips for Data Extract Modes

Here, I’ll outline some tips related to data extract modes. The topics covered are as follows:

1. Changing the Data Extension Extract Mode
2. How to Check the Current High Water Mark
3. Troubleshooting Update Issues

### 1. Changing the Data Extension Extract Mode

For data streams created from Data Extensions in Marketing Cloud, **you cannot edit the extract mode settings after creation**.

**Workarounds**  
If you need to modify the settings, consider one of the following approaches:

**Create a New Data Extension**

- Create a new Data Extension as a replacement for the existing one, with a different name.
- Use this new Data Extension to create a new data stream in Data Cloud and use it to replace the existing functionality.

**Rename the Existing Data Extension**

- Rename the existing Data Extension in Marketing Cloud.
- Delete the current data stream in Data Cloud and create a new data stream using the renamed Data Extension.

**Important Notes**  
If you create a new Data Extension with the same name as the existing one, the previously selected extract mode will automatically be applied, and you won’t be able to change it during the data stream creation process.

This behavior underscores the importance of understanding the relationship between data streams and Data Extensions in Data Cloud. Specifically, the **file-based mechanism** behind data streams must be considered.

**Background and Mechanism**  
Data streams are managed based on the Data Extension name specified at the time of creation, and this name is treated as a file name. This alignment of the Data Extension name with the file name can be confirmed in the data stream definitions.

Even if you rename the Data Extension in Marketing Cloud, the file name within the associated data stream is not automatically updated. Manual changes are also not possible.

Moreover, **even if you delete a data stream, its configuration information remains preserved**. If you recreate a data stream using a Data Extension with the same name, the previously configured file name and settings are automatically reapplied.

**Understanding the File-Based Mechanism**  
Although data streams derived from Data Extensions may not appear file-based, they are fundamentally designed in a similar way. As such, consider the following points:

- Data streams are managed by file names, making the **Data Extension name a critical key** within the system.
- Once created, the data stream settings persist even after deletion.
- Renaming a Data Extension after creating a data stream can cause operational confusion and should be avoided.

**Key Takeaway**  
Since data streams and Data Extensions are tied together through a file-based mechanism, avoid renaming Data Extensions. ** this understanding with Marketing Cloud administrators**.

In my view, managing Data Extension folders is similar to the concept of “buckets and folders” in Amazon S3. In S3, it’s only natural for integration to break if you change a file name. Likewise, you should avoid renaming Data Extensions.

So, what happens if you replace the original Data Extension name with the name of another Data Extension? In this case, as long as the field structure matches, the integration will switch to the new Data Extension. This behavior is quite similar to how files work.

By thoroughly understanding these mechanisms and operating them correctly, you can achieve efficient and trouble-free data management.

### 2. How to Check the Current High Water Mark

The **High Water Mark (HWM)** refers to the maximum value or timestamp recorded during delta extraction. As previously explained, there are two types of delta extraction:

1. **Numeric CDC** (e.g., Claim Number)
2. **DateTime CDC** (e.g., Updated Date)

You can check the current High Water Mark value using **Email Studio**! ✨

**Steps**

1. Open **Email Studio**, and go to **Interactions > Data Factory Utility**.

2. A list of Data Factory Utilities will appear. Click any utility of your choice. The content displayed will be the same, so it doesn’t matter which one you choose.

3. Use **Ctrl + F** or a similar search function to find information about the relevant data stream. The column labeled “Table” represents the Data Extension name being used in the data stream.

- Each page displays a maximum of 250 entries. If you don’t find the relevant data, navigate through the pages using the paginator.
- When a data stream is created, a corresponding Data Factory Utility and an associated automation are automatically created.

- Even if the data stream is deleted, the associated Data Factory Utility and automation are not removed.

**Fields to Check**

- **Extract Last Value**: The current High Water Mark (HWM) value.
- **Column Name**: The datetime field used for delta extraction.
- **Extract Type**: The extraction type (Full Refresh or Delta Extraction).
- **Table**: The Data Extension name (= file name).

**Quick Tip**  
If delta updates fail, check whether the record’s number or date is lower than the High Water Mark. This could be the reason why records are not being extracted.

By understanding this process, you can efficiently manage data integration and troubleshoot issues.

## 3. Troubleshooting Update Issues

When selecting a **Full Refresh**, the system retains 24 records of history for each day, but only one hour’s worth of data is updated. The remaining updates succeed with zero records. This is a feature, not a bug.

Additionally, after creating a data stream, it may take approximately 24 hours before it becomes usable. It’s also expected that the initial few runs may succeed with zero records. This is by design.

While some updates may not be executed due to these specifications, what should you check if no updates occur after waiting a full day? Let’s go through some potential troubleshooting steps.

### ① Check if the Data Extension Name Has Been Renamed

As mentioned earlier, the Data Extension name given during data stream creation should not be changed. This Data Extension corresponds to the “file name”, as stated previously. If there is a mismatch between the file name and the Data Extension name, integration will stop.

Please check the following areas to verify the correct file name and ensure that the Data Extension name in Marketing Cloud has not been altered.

**Quick Tip**  
By restoring the original Data Extension name, integration will resume.

### ② Check if the Automation Has Been Stopped

As previously mentioned, when a data stream is created, the **Data Factory Utility** automatically creates and schedules an associated automation. Stopping this automation will interrupt the integration.

It’s important to note:

- This automation does not trigger imports on the **Data Cloud** side.
- Running the automation manually (e.g., “Run Once”) will have **no effect**.
- Pausing the automation or modifying the schedule serves no purpose and may cause issues.

Ensure the automation has not been paused or deleted, and confirm that the schedule has not been altered.

### ③ Check if Updates Are Executing with Zero Records

This issue has been addressed in a previous article. Even if the Data Extension contains zero records, the data stream will not process updates, and the number of records will remain unchanged.

[## SFMC Tips #78 : Data Cloud & Marketing Cloud Engagement Integration Tips

### In this article, I will share tips for integrating Data Cloud and Marketing Cloud Engagement. I plan to update this…

medium.com](/@marketingcloudtips/data-cloud-marketing-cloud-engagement-integration-tips-9e160167cda8?source=post_page-----25a44bf180b7---------------------------------------)

Verify whether the number of records in the Data Extension is zero.

## Extra: Deleting Marketing Cloud Data is Not Supported in ‘Upsert’ Data Streams

### Current Limitations

- **Upsert Mode**: Deleting data within a data extension is **not supported** in this mode.
- **Full Refresh Mode**: Since all content is replaced, deletion is possible with this option.

If deletion of data from a data extension is still necessary, the only option is to delete unwanted records from the data extension within Marketing Cloud and then create a new data stream.

[## Help And Training Community

### Edit description

help.salesforce.com](https://help.salesforce.com/s/articleView?id=000396417&type=1&source=post_page-----25a44bf180b7---------------------------------------)

## Final Thoughts

For many readers, this may be the first time exploring the inner workings of the **Data Factory Utility**.

As a side note, the automations associated with the Data Factory Utility are not subject to additional charges in Marketing Cloud. While a typical **Corporate Edition** account has an **annual limit of 45,000 automation runs**, **those related to the Data Factory Utility are excluded from this count**.

That’s all for now. 😊

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
