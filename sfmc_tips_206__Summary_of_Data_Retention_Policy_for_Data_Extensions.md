# SFMC Tips #206 : Summary of Data Retention Policy for Data Extensions

**Source:** https://medium.com/@marketingcloudtips/summary-of-data-retention-policy-for-data-extensions-4f46f53fa9e9

---

# SFMC Tips #206 : Summary of Data Retention Policy for Data Extensions

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--4f46f53fa9e9---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--4f46f53fa9e9---------------------------------------)

5 min read

·

Nov 20, 2025

--

Photo by [Link Hoang](https://unsplash.com/@linkhoang?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

Starting around November 2025, the **Data Retention Policy** option began to be enabled by default in Marketing Cloud Engagement.

Many users may wonder:

- **“When does the data get deleted?”**
- **“Should I configure Retention?”**
- **“Should I keep all historical data?”**

This article organizes the core specifications, precautions, and best practices of the Data Retention Policy in the clearest possible way.

## What Is the Data Retention Policy?

The Data Retention Policy is a configuration that allows Marketing Cloud to automatically delete data stored in a Data Extension.

Once configured, it behaves as follows:

- Automatically deletes **records** that have exceeded a specified period (all or partial)
- Automatically deletes **the Data Extension itself**, including its records, when it reaches the defined retention period
- Managed on a **time basis** (days)
- No automation required — maintenance is performed automatically

If no Data Retention Policy is configured, data will remain permanently.

## How to Configure the Data Retention Policy

You can set it when creating a Data Extension in Email Studio / Contact Builder,  
or from the edit screen of a Data Extension in Contact Builder.

> *※ You cannot configure the retention policy from the Data Extension edit screen in Email Studio. Email Studio only allows configuration* ***at creation time****.*
>
> *Also, when adding a retention policy to an existing Data Extension, the option* ***“Delete individual records”*** *is only available if the Data Extension contains* ***fewer than 1 billion records****.*

There are two major configuration sections:

## 1. Type of Deletion Target

① Delete individual records  
② Delete the entire DE including all records  
③ Delete all records

## 2. Retention Period

- Configure based on days, weeks, months, or years (“retain for X days”, etc.)
- For “delete all records”, you may specify a date directly using a calendar selector

> *If you select either:*
>
> *② Delete the entire DE including all records  
> ③ Delete all records*
>
> *The “Next Scheduled Deprecation” (deletion date) will appear in the Data Extension properties in Contact Builder.  
> You can assume that all records will be deleted* ***after that date****.  
> This date is re-calculated based on the day the retention policy was turned “on”.*

## How the Deletion Schedule Works

Deletion based on the Data Retention Policy does **not** occur *immediately* when the defined period is exceeded.

Instead:

- After the retention period elapses, the deletion process begins **within 24 hours**
- This process runs on Salesforce’s **non-public internal schedule**

The start timing varies depending on:

- System load
- Overall service performance
- Total volume of data to be deleted

> *In principle, the deletion is completed within 24 hours. However, if the process does not fully finish, the next execution will resume the deletion from where it left off.*
>
> *Additionally, this time lag can be considered an “adjustment buffer” designed to prevent the relevant data from being deleted immediately at the moment the Data Retention Policy is configured. Therefore, it is easier to understand the mechanism if you think of the deletion as being executed safely* ***after a certain grace period has been provided****.*

## Why the Data Retention Policy Is Important

### ① Storage Optimization (Cost Control)

Marketing Cloud Engagement also has limits on storage usage.

> *The recently released* ***Data Extension Storage dashboard*** *provides reporting on DE storage usage and also shows how many retention policies exist in the account.  
> In my environment, 3 GB is currently in use.*

### ② Faster, More Stable Automations

Large Data Extensions slow down query performance.  
 Keeping Data Extensions at an appropriate size through retention policies is very important for performance.

## Best Practices for Configuring Retention Policies

### ① Define the Policy Based on the Role of Each Data Extension

- **Master:** No retention policy
- **Temporary work tables:** 7–30 days
- **Send results:** 90–180 days (depends on organizational requirements)

### ② Understanding the Hidden Field \_CreatedDate

To check the start date for when a record becomes eligible for deletion, you can inspect the hidden field **\_CreatedDate** (record creation date) in Query Studio.

```
SELECT    
    Id,  
    Email,  
    DATEADD(HOUR, 15, _CreatedDate) AS CreatedDate,  
    DATEDIFF(DAY, DATEADD(HOUR, 15, _CreatedDate), DATEADD(HOUR, 15, GETDATE())) AS Period  
FROM    
    [Data Extension Name]
```

### Notes on “\_CreatedDate”

- The timestamp of **\_CreatedDate** is recorded in **CST**, so timezone adjustments may be required.
- When using **\_CreatedDate**, you must always provide an alias (`AS`).
- When values in a record are **updated** (via import or SQL query), `_CreatedDate` is preserved.
- When a record is **overwritten** (via filter, import, SQL query), `_CreatedDate` is reset to **0**.  
   This is because overwriting internally deletes the original record and inserts a completely new one.

### ③ Intentionally Reduce Heavy Data Extensions (Improve Query Speed)

If older records are not needed, aggressively apply retention policies.

### ④ Take Backups as Needed

For data that must not be lost, maintain backups in:

- Your own SFTP
- Cloud storage
- Data Cloud

## Final Thoughts

The Data Retention Policy is an important configuration for operating data **safely**, **efficiently**, and **cost-effectively**.

Especially in projects involving large volumes of Data Extensions, consider:

- Appropriate retention periods
- Distinguishing between master data and everything else
- Future estimated record counts
- Backup rules

However, for small and mid-sized organizations, there may be no need to be overly strict.  
In many such environments, all retention policies have been turned off without any major issues.

Just because the default is now “on” does not mean you must follow it rigidly.  
My conclusion is: **create an operation model that fits your organization.**

That’s all for now.

Stay tuned for more Salesforce Marketing Cloud tips! 😎

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
