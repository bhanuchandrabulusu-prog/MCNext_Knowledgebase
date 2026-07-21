# SFMC Tips #205 : Data Cloud: Introduction of Batch DMO Activation (Manual Version)

**Source:** https://medium.com/@marketingcloudtips/data-cloud-batch-dmo-activation-has-arrived-0b44883c57e9

---

# SFMC Tips #205 : Data Cloud: Introduction of Batch DMO Activation (Manual Version)

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--0b44883c57e9---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--0b44883c57e9---------------------------------------)

5 min read

·

Nov 19, 2025

--

Photo by [Bioregion Institute](https://unsplash.com/@bioregioninstitute?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

With the **October 2025 Data Cloud release**, the long-awaited **Batch DMO Activation** feature has finally been introduced.

This new capability allows companies to send “Profile”, “Engagement”, and “Other” category data stored in Data Cloud **more flexibly and at much larger scale** to external destinations such as **Marketing Cloud Engagement** or **cloud storage platforms**.

Until now:

- **Streaming DMO Activation** was available
- But **batch-level exports of full DMO datasets** were limited

This article provides a comprehensive overview of how Batch DMO Activation works, its supported use cases, capabilities, specifications, and practical scenarios.

## What Is Batch DMO Activation?

Batch DMO Activation is a new method that sends **all records contained in a Data Model Object (DMO)** to an external destination in batch format.

It supports a wide variety of use cases, such as:

- Sending the full customer profile dataset to analytics platforms (BI / reporting use cases)
- Sending recommendation-related datasets to **Marketing Cloud Engagement**
- Storing DMO snapshots in SFTP for audit / compliance
- Batch export to cloud storage or data warehouses (S3 / GCS / Azure, etc.)

While Streaming DMO Activation sends **only new or updated records**,  
 **Batch Activation exports the entire DMO as-is**, which is its biggest advantage.

## Supported Destinations

Batch DMO Activation supports the following major platforms:

### Activation Destinations

- **Marketing Cloud Engagement**
- **Data Cloud (different data spaces or instances)**
- **Amazon S3**
- **Google Cloud Storage (GCS)**
- **Microsoft Azure**
- **SFTP**

This covers use cases ranging from analytics to marketing activation to long-term historical archiving.

### Supported DMO Types

Batch DMO Activation supports:

- **Profile DMO** (customer profiles)
- **Engagement DMO** (behavioral / event data)
- **Other DMO** (miscellaneous data models)

### ❌ Unsupported Special DMO Types

The following special DMO categories are not supported:

- Audience DMO
- Segment Membership DMO
- Unified Link DMO, etc.

## Specifications

Batch DMO Activation supports many of the same capabilities available in segment activations.

### ① All DMO Records Are Included

When Batch Activation is executed,  
 **every record inside the DMO is sent** to the destination.

Unlike Streaming Activation, it is not limited to incremental records based on triggers.

### ② Fields Must Be Selected Manually

There are **no default fields selected**.  
 Users must manually choose which fields to include in the output.

### ③ Supported Features

Batch DMO Activation supports:

- **Contact Point Filtering** (limit output by email or phone)
- **Activation Membership Filtering**
- **Add Attributes** (include additional fields)
- **Filter Attributes**

These are configured similarly to standard segment activation settings.

### ④ Engagement DMO Output Includes Only the Last 90 Days

For Engagement-type DMOs:

- Only records from the **past 90 days** are included.
- Full historical event logs are **not** exported.

### ⑤ No Scheduling Available Yet

Batch DMO Activation **does not currently support scheduling**.  
 You must manually publish from each activation’s detail page.

💡 A scheduling feature is likely on the future roadmap.

## How to Use Batch DMO Activation (Step-by-Step)

1. From the Activation page, click “New” and select the DMO option.

2. Choose whether the activation should be Streaming or Batch. Select **Batch**.

3. Select the **target DMO**.  
This includes all DMO types except the unsupported special DMOs.  
In this example, an “**Other**” category dataset is selected.

4. Select “**Marketing Cloud Engagement**” as the activation destination.

5. Contact point selection (email address or phone) is **optional**.For segment activation this was mandatory,  
but for DMO activation it is optional —   
meaning you can activate **all records** without restrictions.

6. By default, only the “URL” is sent — so you must add attributes.

7. Select only the fields required for Marketing Cloud Engagement.

8. After choosing the attributes, click Next.

9. Enter an activation name and refresh type, then save.

10. After saving, a “**Publish Now**” button appears in the top-right corner.  
Unlike segment activation — where publishing the segment also publishes the activation —   
Batch Activation requires pressing **this specific Publish button** to execute.

> ***Scheduling is not supported yet, so publishing must be done manually****.*

11. Activation completes in **~15–30 minutes**.  
In this example, all 16 records were successfully activated.

12. The 16 activated records were confirmed in Marketing Cloud Engagement.  
These ranking values can be used directly inside content.

13. A SubscriberKey field exists, but — as shown — it was delivered as **NULL**.

## Conclusion

Batch DMO Activation — combined with Marketing Cloud Engagement or data lake platforms — significantly enhances:

- Personalization accuracy
- Analytical capabilities
- Enterprise-level data governance

With full-batch activation now available (in addition to streaming), the scope of Data Cloud expands dramatically and can scale enterprise data strategies even further.

That said…  
many of us — including myself — are probably thinking:

**“Please add scheduling soon!”**

Let’s look forward to future updates.

Thanks for reading.

Stay tuned for more Salesforce Marketing Cloud tips! 😎

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
