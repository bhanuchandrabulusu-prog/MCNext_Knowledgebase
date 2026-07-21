# SFMC Tips #214 : Data Cloud: Local File Upload

**Source:** https://medium.com/@marketingcloudtips/data-cloud-local-file-upload-dab22b9dd918

---

# SFMC Tips #214 : Data Cloud: Local File Upload

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--dab22b9dd918---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--dab22b9dd918---------------------------------------)

4 min read

·

Dec 12, 2025

--

Photo by [rishi](https://unsplash.com/@beingabstrac?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

In Data Cloud, you can upload files directly from your local machine to the Data Cloud data lake without any complex configuration. This feature lets you import CSV files directly into Data Cloud with just a few clicks.

## Feature Updates (Including Legacy Behavior)

As of November 2024, this capability was available as a **beta feature**.  
 → It became **generally available in March 2025**.

Initially, the limit was **10 MB per CSV file**.  
 → In March 2025, this increased to **100 MB**.

In the June 2025 release, Data Cloud introduced a new button option that allows **re-uploading (Full Refresh)** — not just one-time ingestion.

In the November 2025 release, several major enhancements arrived:

- **Upsert** became available as a third option.
- The maximum file size increased to **2 GB**.
- Support expanded to **up to 100 columns per file**.
- **Formula fields** can now be created at the DLO creation stage.

## Typical Use Cases

### ✔ Pre-production Testing

Before moving to automated cloud-based integrations, teams can upload data manually to validate their data model, check field mapping issues, and identify gaps early.

### ✔ Rapid Prototyping for Custom Data Models

You can quickly upload sample datasets and immediately use them to create segments, Calculated Insights, or test downstream flows.

## How to Set It Up

1. Navigate to **Data Streams** in Data Cloud and click **New**.

2. Select **File Upload**.

3. Choose your CSV file (either by browsing or drag-and-drop).

4. The upload will begin immediately.

5. Configure the **Data Stream** and **DLO**.

- Here, you can only create a **new Data Lake Object (DLO)**. Reusing an existing DLO is not supported.
- Enter a name for the new DLO and proceed.

> ***Tip:*** *Starting in* ***November 2025****, you can “add formula fields” when creating a DLO.*

6. Give the data stream a name and click **Deploy**.

That’s it.

## Important Notes & Limitations

A **header row is required**, and column names must use alphanumeric characters.

**Each upload creates a brand-new Data Stream and a brand-new DLO.**  
 You cannot upload into an existing Data Stream or DLO.

After ingestion completes, the Data Stream still shows blank values for:

- Last Run Status
- Last Processed Records
- Total Records
- Last Update Date

## Release Timeline (for reference)

- **November 2024:** The beta version was released.
- **March 2025:** The feature became generally available.
- **March 2025:** The upload size limit increased from 10 MB to **100 MB**.
- **June 2025:** The **Full Refresh (re-upload)** capability was introduced.
- **November 2025:** The **Upsert** option was added.
- **November 2025:** The maximum file size increased to **2 GB**.
- **November 2025:** Support expanded to **100 columns**, and **formula fields** became available during DLO creation.

## Final Thoughts

Even though the feature started as a beta release, it has improved rapidly and continues to be refined. If you haven’t tried it yet, this is an excellent way to explore the flexible possibilities of Data Cloud — especially for rapid prototyping or testing data models before going live.

That’s it for now.

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
