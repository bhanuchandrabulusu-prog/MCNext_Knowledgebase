# SFMC Tips #207 : Marketing Cloud Next: How to Configure Data Space Filters

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-next-how-to-configure-data-space-filters-6880c21093bd

---

# SFMC Tips #207 : Marketing Cloud Next: How to Configure Data Space Filters

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--6880c21093bd---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--6880c21093bd---------------------------------------)

7 min read

·

Nov 23, 2025

--

Photo by [Natalie Chaney](https://unsplash.com/@naaatsnaps?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

When you start operating Marketing Cloud Next Growth & Advanced Edition, you install a data kit. At this timing, CRM (Contact and Lead) records are automatically ingested into DLO / DMO within the data space.

What is important here is that **at the time of ingestion, all records are ingested in full once**. At this installation stage, it is not possible to narrow down (filter) the data in advance.

Therefore, if you want to exclude records that are not necessary for marketing, you need to **set up a data space filter after ingestion**.

## What is a Data Space Filter

A data space filter is a function that is easy to imagine for those who have experience using Marketing Cloud Connect, which is familiar in integrations between CRM and Marketing Cloud Engagement.

Just like MCC, you can control which records are inserted into and visualized in the data space with conditions such as:

- Insert only people who have an email address into the data space
- Include only records created after a specified date
- Sync only when a specific boolean field is TRUE

Data Cloud does not have the concept of “billable contacts” like Marketing Cloud Engagement, however:

“**We want to exclude records that should not be used for marketing**”

This need definitely exists.

In such cases, this **data space filter** is useful.

In this article, I will clearly explain how to configure this filter, along with concrete steps and key points.

## Steps on the CRM Side

First, create a formula field on the CRM side that serves as a flag for integration.

### 1. Create a new “Formula Field” on the target object

In this example, I use Contact. Select “Formula” as the data type.

### 2. Set field name and data type

- Field Name:  
  **Data Space Integration**  
   → A name that remains meaningful even if product names change and can be used long-term is recommended
- Formula Return Type:  
  **Checkbox**

What I want to achieve this time is:

❌ Matches NG conditions → FALSE (unchecked)  
✅ Does not match NG conditions → TRUE (checked)

### 3. Define NG conditions

The following are the “NG conditions” for this example:

- Email is NULL
- Email Opt Out is TRUE
- FirstName or LastName contains SAMPLE
- FirstName or LastName contains BLOCKED

We want to set TRUE only when none of these apply, so we use **NOT(OR())**.

```
AND(  
    NOT(ISBLANK(Email)),  
    NOT(HasOptedOutOfEmail = TRUE),  
    NOT(  
        OR(  
            AND(  
                NOT(ISBLANK(FirstName)),  
                OR(  
                    CONTAINS(UPPER(FirstName), "SAMPLE"),  
                    CONTAINS(UPPER(FirstName), "BLOCKED")  
                )  
            ),  
            AND(  
                NOT(ISBLANK(LastName)),  
                OR(  
                    CONTAINS(UPPER(LastName), "SAMPLE"),  
                    CONTAINS(UPPER(LastName), "BLOCKED")  
                )  
            )  
        )  
    )  
)
```

✔︎ Key points of this formula

- Use **OR() to group NG conditions**
- Use **NOT() to invert and make only OK records TRUE**

### 4. Set field-level security

Configure access permissions and click Next.

### 5. Dynamic Forms setting

You can leave the default settings for adding to dynamic forms.

### 6. Add to page layout

This is optional, but in this case, I display it on the page.

### 7. Verify on actual records

After completion, when checking actual Contact records:

- Contains SAMPLE / BLOCKED in name
- No Email
- Email Opt Out is TRUE

For records that meet the above conditions, you can confirm that **Data Space Integration is unchecked**.

## Steps on the Data Cloud Side

First, retrieve the Data Space Integration field in the data stream. At this point, a **full refresh of the data stream occurs**, and the latest values (True / False) are retrieved.

### 1. Check current data

After the full refresh, when you look at Data Explorer in Data Cloud, since data space filters are not yet set:

- Records containing SAMPLE / BLOCKED
- Records with empty Email

still exist as-is.

### 2. Set Data Space Filter

Next, from the “Data Space” tab, find Contact\_Home (Contact), click the action button, and click **Set Filters**.

*Tips: You can also configure data space filters for Marketing Cloud Engagement data extensions from this screen.*

### 3. Configure filter conditions

Here, set the filter condition. In this case, enter:

**Data Space Integration = True**

and save.

***Note:*** *As condition logic, you can use either* ***AND*** *or* ***OR****, but you can’t use a combination of* ***AND*** *and* ***OR*** *within the same filter logic.*

### 4. Verify filter results

Once saved, it is applied **immediately (within about 1 minute)** to already integrated data, and the display in Data Explorer is also updated immediately.

As shown below:

- People containing SAMPLE / BLOCKED
- People without Email

are **no longer included in the data space**.

### 5. Impact on Marketing Cloud Next

In Marketing Cloud Next:

- Segments
- Identity Resolution
- Data Graph

all processes reference the **data space**, so with this setting, unnecessary Contacts are excluded from the data space and will not be targeted going forward.

How was it?

The filter set this time does not exclude records themselves from being integrated into Data Cloud, but only **restricts which records are visualized and available within the data space**.

Therefore, note that **the total number of records ingested by the data stream does not change**.

There is no need to worry if the “number of integrated records” in the data stream does not decrease. This is unrelated to filter settings, and it is by design that the total count does not change.

## Time until CRM updates are reflected via incremental sync

Earlier, I explained that data filters for existing data are applied immediately, but what many people are concerned about is:

“How long it takes from updating the flag in CRM until it is reflected in Data Cloud”

Currently, **incremental sync runs approximately every 10 minutes**.  
 In practice, depending on internal processing, it feels like **about 15 minutes**.

This is almost the same as Marketing Cloud Connect, so it is easy to remember.

## Important Points

Records are reflected in the data space with the latest state in the following cases:

### Cases where incremental sync occurs

- When a record is edited in CRM in a way that updates **LastModifiedDate**

※ More precisely, it is detected when **SystemModStamp is updated  
-** LastModifiedDate: Timestamp updated by human actions  
- SystemModStamp: Timestamp updated by human or system actions

※ If LastModifiedDate is updated, SystemModStamp is also updated.

### Cases where full sync occurs

- When an automatic full replacement (full refresh) runs
- When a new CRM field is added to the data stream
- When a manual “Update Now” (Full Refresh) is executed in the data stream

Manual Full Refresh feature was introduced in Data Cloud in November 2025

In other words, **the latest state of CRM is not always fully synchronized automatically**.

In particular, even if the value of a formula field changes, if the LastModifiedDate is not updated, **it will not be reflected in the data space**.

Be sure to keep this behavior in mind during operations.

## Reference: Cases where formula value changes but LastModifiedDate does not update

### Example 1

When a formula field is updated due to changes in a related object

For example, in the relationship between Opportunity and Account:

- Create a formula field Account\_Industry\_\_c on Opportunity that references Account Industry  
  Formula: TEXT(Account.Industry)

When the Industry field on Account is changed, the value of the formula field on Opportunity changes.

At this time, the LastModifiedDate of Account is updated and Industry is synced, but the LastModifiedDate of Opportunity is not updated, so Industry is not synced.

### Example 2

When calculating “Age” based on Contact’s birthday

Even though the birthday date arrives automatically as the calendar progresses, the Contact record is not updated on that day to recalculate age.

Therefore, LastModifiedDate is not updated, and the latest value is not reflected in Data Cloud.

That’s all for this time.

Stay tuned for more Salesforce Marketing Cloud tips! 😎

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
