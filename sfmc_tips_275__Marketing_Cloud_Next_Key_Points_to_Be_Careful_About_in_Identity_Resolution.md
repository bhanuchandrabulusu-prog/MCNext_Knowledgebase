# SFMC Tips #275 : Marketing Cloud Next: Key Points to Be Careful About in Identity Resolution

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-next-key-points-to-be-careful-about-in-identity-resolution-ffa5f9484aed

---

# SFMC Tips #275 : Marketing Cloud Next: Key Points to Be Careful About in Identity Resolution

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--ffa5f9484aed---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--ffa5f9484aed---------------------------------------)

10 min read

·

Apr 5, 2026

--

Photo by [Marcin Sajur](https://unsplash.com/@m_sajur?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

To use Marketing Cloud Next Growth & Advanced Edition, it is assumed that you will utilize Unified Individuals generated through Identity resolution. However, **there are several important points that beginner users in particular should be careful about** when working with Identity resolution.

Based on the default credit design of Marketing Cloud Next, regardless of company size, if sufficient design is not done in the early stages of development, there is a risk that unintended full refreshes will rapidly increase credit consumption.

In particular, when handling profile data on the scale of tens of thousands of records, these precautions can be considered essential.

In this article, I will organize the **key points that beginner Marketing Cloud Next users** should understand in advance.

## 1. How to Check the Number of Records Processed by Identity Resolution

The number of records processed in a day can be checked in the “**Processing History**” tab below. If processing occurs multiple times in a day, the numbers are accumulated on a daily basis.

For example, if processing occurs twice in a day — once for 100 records and once for 500 records — the total of 600 records will be displayed. This is aggregated and displayed immediately after Identity resolution processing is completed.

## 2. How to Check Consumed Credits

Next, here are the steps to check credits:

1. Select the “**Consumption Cards**” tab and click “**View Consumption Insights by Tags**”.

2. Scroll to the bottom and click “**DataCloud\_BatchProfileUnification**” from the “**Consumption by Usage Type**” section.

*If this feature is not enabled, please enable it using the article below.*

[## SFMC Tips #232 : Data Cloud: Viewing Detailed Digital Wallet Consumption Data

### Until now, Data Cloud has primarily used aggregated, consumption-based metrics. However, it has now transitioned to…

medium.com](/@marketingcloudtips/sfmc-tips-232-data-cloud-viewing-detailed-digital-wallet-consumption-data-436dc3bf4f13?source=post_page-----ffa5f9484aed---------------------------------------)

3. You will then be redirected to a report filtered for Identity resolution. Sort “**Event Time**” in descending order.

4. The credit consumption for each Identity resolution is displayed in **Units Consumed**.

*※ Approximately 100,000 credits are consumed per 1 million records.*

5. In the above example, since 11.3 credits are consumed, it can be understood that 113 records were processed in one day. This matches the record count explained in section 1.

### **Considerations**

- This report is updated once every 24 hours. Therefore, it may only be available the next day.
- Also, **Event Time** represents the time when Identity resolution started, not when it was completed.

## 3. Basic Execution Methods of Identity Resolution

Basically, Identity resolution is executed in one of the following ways:

- [Automatic execution at intervals of 60 minutes to 24 hours](https://help.salesforce.com/s/articleView?id=data.c360_a_identity_resolution_processing_frequency.htm&type=5) (only when automation is enabled)
- Manual execution (via the “Run Rule Set” button)
- Execution triggered by flows or APIs

The setup method for schedule-triggered flows will be explained in another article.

[## SFMC Tips #208 : Marketing Cloud Next: Scheduling Identity Resolution and Data Graph

### In Marketing Cloud Next Growth & Advanced Edition, Identity Resolution and Data Graph cannot be executed on a schedule…

medium.com](/@marketingcloudtips/marketing-cloud-next-scheduling-identity-resolution-and-data-graph-a63aecf1904a?source=post_page-----ffa5f9484aed---------------------------------------)

※ Regardless of the execution method, if there are no changes in field values in source profile records (such as Contact or Lead) compared to the previous Identity resolution, the process will be skipped.

## 4. Typical Causes of Full Refresh

If the following changes are made, all records of source profiles (Contact, Lead, etc.) in the data space will be reprocessed during the next Identity resolution:

- Addition/removal of DMOs used in matching rules
- Changes to field mappings connected to DMO

For example, if a new field is newly mapped from a source profile (Contact, Lead, etc.) to the Individual DMO, all records will be reprocessed.

This behavior is natural. Simply adding a mapping creates the field in Unified Individual, but the values themselves are not automatically populated. **Reprocessing through Identity resolution is required to reflect the values**.

※ One particularly difficult concept is “fields used in matching rules.” Even if “Contact Point Address” is not directly used in matching rules, removing something like a mapped Lead “Last Modified Date” can result in all Lead records becoming update targets.

Understanding this behavior is extremely important, but fully grasping the impact scope is not easy. Therefore, it is best practice to assume that **all potentially related fields are affected**, and to implement design changes collectively.

What should especially be avoided is incremental implementation, such as running Identity resolution every time a single field is mapped. This approach leads to repeated full refreshes and increased credit consumption.

## 5. Mechanism of Incremental Updates

So far, we have discussed full refresh. Next, we organize how incremental updates work.

Normal data updates follow this flow:

1. A record is updated on the CRM side
2. The update triggers incremental updates on the DSO/DLO side
3. Only the updated records become targets for Identity resolution

The key point here is:  
**Which records are determined as updated on the CRM side**

※ Updates are not determined by visible value changes, but by whether the last modified timestamp has changed.

※ More precisely, detection is based on changes to **SystemModStamp**.

- **LastModifiedDate: Time changed by a user**
- **SystemModStamp: Time changed by a user or system**

For details, refer to [Salesforce official help](https://help.salesforce.com/s/articleView?id=000387261&type=1).

### **Considerations**

For example, consider the case where “age increases by +1 on a birthday.”

At first glance, it may seem like an update occurs on that day. However, if the age field is calculated using a **formula**, caution is required.

- Formula fields are not stored as data; they are calculated at display time.

Therefore:

- **The CRM record itself is not updated**
- **The last modified timestamp does not change**
- **It is not subject to incremental updates**
- **Identity resolution is not executed**

The number we should pay attention to is the number of records updated in DSO/DLO, which become targets for Identity resolution.

### Notes

[Using the **“Refresh Now (Full Refresh)”** button in the data stream triggers a full refresh](/@marketingcloudtips/data-cloud-full-refresh-for-crm-and-sfmc-data-streams-62b30ba01b10).

While this may not be an issue in early development, it becomes risky after automating Identity resolution.

This process deletes all existing records and re-ingests them, meaning all source records become update targets.

In other words:

- It becomes a full update instead of incremental
- Identity resolution runs for all records

Since both processing volume and credit consumption are high, timing must be handled carefully.

## 6. Constraints of Mapping and Change Detection

As a Data Cloud (Data 360) specification:

Change detection in DLO for Identity resolution  
→ Applies only to fields mapped to DMO

In other words:

Changes in unmapped fields  
→ Not subject to Identity resolution

**You might think that removing “SystemModStamp” and “LastModifiedDate” from mappings would prevent updates**.

That idea is correct!!

However, as of April 2026 in Marketing Cloud Next:

If built from a data kit during setup,  
the environment is based on a **managed package configuration**.

In this configuration, **standard mappings cannot be removed**. Attempting to do so results in an error as shown below.

You can’t delete a component deployed from a managed-package data kit.

Therefore:

- **LastModifiedDate is always mapped**
- **Any change on the CRM side is always detected as an incremental update**

This means **unnecessary updates on the CRM side must be minimized**.

For example, updating all contacts daily is effectively the same as running full refresh daily via Identity resolution, which is very dangerous.

If CRM is already in operation, check the current update state using the processed record history.

**Tips:**  
Avoid making decisions based solely on the update volume from a single week. For example, if a “rank assignment process” is executed at the beginning of each month, updates may be heavily concentrated around the end and beginning of the month.

Therefore, **it is important to monitor update volumes not only from a short-term perspective, but also on a monthly basis**.

## 7. Concept of Data Spaces

In Marketing Cloud Next, using this data space efficiently becomes the key to success.

Data space can be said to be equivalent to a business unit, and it allows you to freely filter which data you handle.

And the **most important point is that the processing target of Identity resolution is only the records within the data space**.

Therefore, for example,

- DSO / DLO source data: 10,000 records
- Within data space: 3,000 records (you can narrow the number by data space filter)

In this state,

- If 1,000 records are updated in DLO source data,
- and among them 100 records are included within the data space,

→ The processing target of Identity resolution is limited to only 100 records.  
This is very efficient.

Actually, such a technique is also written in the following Salesforce help document.

### Example of reducing Identity resolution cost

- In Sandbox, test new rule sets **using a small number of representative data**. If there is no Sandbox and there are multiple data spaces, **consider testing in a data space with a small amount of data**.

[## Salesforce Help

### Edit description

help.salesforce.com](https://help.salesforce.com/s/articleView?id=data.c360_a_billing_considerations_for_identity_resolution.htm&type=5&source=post_page-----ffa5f9484aed---------------------------------------)

## 8. Understanding data space filter

The method of setting data space filter was explained in the following article previously.

[## SFMC Tips #207 : Marketing Cloud Next: How to Configure Data Space Filters

### When you start operating Marketing Cloud Next Growth & Advanced Edition, you install a data kit. At this timing, CRM…

medium.com](/@marketingcloudtips/marketing-cloud-next-how-to-configure-data-space-filters-6880c21093bd?source=post_page-----ffa5f9484aed---------------------------------------)

What should be noted here is that when a filter is set in the data space,

- even if it is a process to reduce the number of target people,
- even if it is a “**deletion process**”, it is counted as the number of processing of Identity resolution.

Example:

A data space with 10,000 records without filter  
 → When narrowed down to 3,000 records by setting data space filter,

**the deletion processing of 7,000 records is counted as the number of processing of Identity resolution**.

For this reason, it is important to set data space filter from the beginning in the early stage of development.

Also remember that changing the condition of data space filter also becomes a trigger of incremental update. Well, if you think about it, this is also understandable.

## 9. Impact of credit consumption

Now, when full refresh occurs, credit consumption becomes very large.

Example calculation:

- Processing of 50,000 records → 5,000 credits are consumed

*※ Approximately 100,000 credits are consumed per 1 million records.*

Let’s convert this with the default values of each edition of Marketing Cloud Next. Assume that there are 50,000 Contact records.

- In the case of Marketing Cloud Next Growth Edition  
  → Default 250,000 credits ⇒ all consumed in 50 times
- In the case of Marketing Cloud Next Advanced Edition  
  → Default 500,000 credits ⇒ all consumed in 100 times

If full refresh runs once a day,  
in the case of Growth Edition, credits will only last for 50 days.

You can intuitively understand that this is quite serious.

In the early stage of development, it is important to firmly understand how long the development environment will last and how many credits have been purchased.

## 10. Expected dangerous operation procedure

The following flow is very dangerous.

- First, execute Identity resolution with 50,000 linked records without thinking  
   ⇒ 5,000 credits consumed
- Add a new field to Individual DMO and execute Identity resolution again for now  
   ⇒ 5,000 credits consumed
- Since the rule set was inappropriate, correct it properly and execute Identity resolution again  
   ⇒ 5,000 credits consumed

With just this, 15,000 credits are consumed.  
This is tough…

## 11. What must be done in initial setup

In the initial phase, be sure to do the following.

**Mandatory check**

- Identity resolution auto run= OFF

- Data stream automatic full refreash interval = None (no update)

**Test policy**

- Narrow targets in advance with data space filter
- Verify with about 1,000 records (with conditions as unbiased as possible)  
  Example: “people whose address is XX prefecture”

**Things to do before full-scale Identity resolution**

- Completely determine fields to be linked from CRM to DSO and link them
- Complete all mappings from DLO to DMO
- Completely finalize rule set (Match Rules and Reconciliation Rules)

## Conclusion

As mentioned at the beginning, this content is organized for beginner Marketing Cloud Next users to first understand.

Therefore, in Data 360 operation in enterprise environments, different design concepts and considerations may be required, so please understand that point in advance when referring.

## Identity Resolution Principles

- Do not enable auto Identity resolution from the beginning
- Use data space filters effectively
- Accept that LastModifiedDate mapping cannot be removed
- Complete all field integrations to DSO at the start
- Complete all mappings to DMO
- Finalize rule sets before execution
- Do not perform full refresh on DSO after operations begin

That’s all for this time.

Stay tuned for more Salesforce Marketing Cloud tips! 😎

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
