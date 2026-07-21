# SFMC Tips #201 : Data Cloud: Journey Activity Run Added to Starter Data Bundle

**Source:** https://medium.com/@marketingcloudtips/data-cloud-journey-activity-run-added-to-starter-data-bundle-bbbe73434dd0

---

# SFMC Tips #201 : Data Cloud: Journey Activity Run Added to Starter Data Bundle

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--bbbe73434dd0---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--bbbe73434dd0---------------------------------------)

6 min read

·

Nov 11, 2025

--

Photo by [Maximalfocus](https://unsplash.com/@maximalfocus?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

With the [**Winter ’26 release**](/@marketingcloudtips/marketing-cloud-engagement-winter-26-release-highlights-b32181d3e42a), the integration between **Data Cloud** and **Marketing Cloud Engagement** has been further strengthened. This enhancement enables **Journey history data** from Marketing Cloud Engagement to be ingested into Data Cloud, allowing for **deeper visibility and analysis** of each customer’s journey experience.

This new capability is provided through the “**Marketing Cloud Starter Data Bundle”**.

For an overview of the conventional “Starter Data Bundle”, please refer to the following article.

[## SFMC Tips #85 : Data Cloud: A Guide to Marketing Cloud Starter Data Bundle

### Connecting Data Cloud and Marketing Cloud

medium.com](/@marketingcloudtips/data-cloud-a-guide-to-marketing-cloud-starter-data-bundle-cecea33400c4?source=post_page-----bbbe73434dd0---------------------------------------)

Previously, the Journey-related data included in the Starter Data Bundle consisted of only the following two items:

1. **SFMC Journey** (Category: Other)
2. **SFMC Journey Activity** (Category: Other)

The details of each are as follows.

### **1️⃣ SFMC Journey (Category: Other)**

This dataset stores information for each Journey version saved in Journey Builder. You can think of it as similar to the “**Journey**” data view.

The following fields are automatically mapped to the **Marketing Journey DMO**:

- **ID:** Journey Version ID
- **Name:** Journey Version Name
- **VersionID:** Journey Version ID
- **Created Date:** Journey Version Creation Date
- **Modified Date:** Last Updated Date of the Journey Version

Only the above fields are automatically mapped. If you wish to use the following fields, you’ll need to **map them manually**:

- **Version Number:** Journey Version Number
- **Description:** Description of the Journey Version
- **Status:** Current Status of the Journey Version
- **Original Definition ID:** Journey ID
- **Last Published Date:** Last Published Date

### **2️⃣ SFMC Journey Activity (Category: Other)**

This dataset stores information for each Journey Activity saved in Journey Builder — conceptually similar to the “**Journey Activity**” data view.

The following fields are automatically mapped to the **Marketing Journey Activity DMO**:

- **ID:** Journey Activity ID
- **Name:** Journey Activity Name
- **Journey ID:** Journey Version ID
- **Created Date:** Activity Creation Date
- **Modified Date:** Activity Last Modified Date

### **3️⃣ SFMC Journey Activity Run (Category: Engagement)**

This is the **newly added dataset** introduced in the **Winter ’26 release**. It contains **Journey history data**, enabling you to ingest the execution status of each activity into Data Cloud.

**⚠️**However, note that certain activity types (e.g., **Wait Activity**) are currently **not supported** for integration — an area I hope will be expanded in future updates.

Data synchronization from **Marketing Cloud Engagement** runs **every 15 minutes**, providing near real-time updates.

The following fields are mapped to the **Marketing Journey Activity Run DMO (Category: Other)**:

- **Individual:** Subscriber Key
- **Marketing Journey ID:** Journey ID
- **Marketing Journey Activity:** Journey Activity ID
- **Name:** Journey Activity Name (\*value suggestion recommended)
- **Type:** Activity Type (\*value suggestion recommended)
- **Status:** Status (\*value suggestion recommended)
- **Transaction DateTime:** Date and Time of History Record Creation
- **Created Date:** Date and Time of History Record Creation (same as above)

### How to Use This Feature

With this new functionality, you can now create **custom reports** under the **“Analysis”** tab in **Marketing Cloud Next**, covering:

- Journey entry and exit events
- Goal conditions
- Messaging activity performance

You can also leverage this **Journey history data** to:

- Build **targeted segments**
- Define **conditional logic** for decision splits  
   …leading to more precise audience design and engagement optimization.

> ***⚠️ Important Note:*** *The* ***Marketing Journey Activity Run DMO*** *belongs to the* ***“Other” category****, meaning* ***lookback periods are not applied*** *in segmentation.*
>
> *Therefore, if a large volume of Journey history data is ingested, be mindful of* ***query cost*** *and* ***performance impact*** *when building segments. 🤔*

## **Installation Guide**

If you’re installing the **Starter Data Bundle** for the first time, you can install it together with other starter bundles — no special steps are required.

However, even if the Starter Data Bundle has already been installed in your environment, you can **reinstall only the newly added data**. The steps below explain how to do that.

> *⚠️* ***Important Note:*** *Past historical data will* ***not*** *be imported. Only the history data generated after installation will be ingested into the data stream.*

## Step-by-Step Instructions

1. On the **New Data Stream** creation screen, select **Marketing Cloud**, then click **Next**.

2. Link your **Business Unit** and **Data Space**, then click **Next**.

3. A message will appear in the **Email Studio** data bundle indicating that one dataset is not yet linked. Select **Email Studio Data Bundle** and click **Next**.

4. Choose **SFMC Journey Activity Run** and click **Next**.

5. When the **Review** screen appears, simply click **Next** again.

6. On the following review screen, you’ll see that this dataset belongs to the **Engagement** category and that **data synchronization occurs every 15 minutes**.

7. If you’re using a **demo environment** and encounter an error like the one shown below, reinstall the **latest data model** from [this link](https://help.salesforce.com/s/articleView?id=002234049&type=1) provided.

8. Installing the **latest data model** will allow you to complete the installation successfully.

9. The created **Data Stream** and **DLO** are automatically mapped to the **Marketing Journey Activity Run DMO**.

10. Since this DMO is already related to the **Individual** object, you can immediately use it for **segment creation** and **analytics**.

## Practical Use Case

Here’s an example of how to create a segment using **Marketing Journey Activity Run**.

1. Suppose you have a sample Journey as shown below.  
In this example, I’ll extract data from the **“BOR YAHOO 2”** email activity where **delivery failed**, and rebuild a segment for resending via another channel.

In this case, there are **13 hard errors** recorded.

2. In Data Cloud, open the **Segment Creation** screen, start a new **Individual-based** segment, and select **Marketing Journey Activity Run** from the related attributes.

3. Within the same container, configure the following conditions:

- **Journey Activity Name (Name)** = “BOR YAHOO 2”
- **Message Activity Status (Status)** = “Failed”

💡 When **value suggestions** are enabled, you can input these strings accurately without typos.

4. Once saved, a segment with **13 records** will be created — successfully isolating failed deliveries for re-engagement through another channel. ✅

## Key Takeaways

As you can see, Journey history data is synced to **Data Cloud every 15 minutes**, allowing you to act almost in real time.

However, as mentioned earlier, **some Journey Activity types** (e.g., **Wait Activity**) are **not yet supported** for synchronization. **⚠️**

If you’d like to perform deeper analysis or more advanced segmentation, consider using the **“CSV Export from Journey Builder History Page”** feature, which was also introduced in the **Winter ’26 release** of Marketing Cloud Engagement.

For details, please refer to the following article.

[## SFMC Tips #198 : Bulk Download of Journey History Data from the Interface

### With the Winter ’26 release of Marketing Cloud Engagement, you can now download all Journey Builder history data…

medium.com](/@marketingcloudtips/bulk-download-of-journey-history-data-from-the-interface-326ddced9207?source=post_page-----bbbe73434dd0---------------------------------------)

That’s all for this overview.

Stay tuned for more Salesforce Marketing Cloud tips! 😎

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
