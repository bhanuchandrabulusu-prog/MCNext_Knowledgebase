# SFMC Tips #232 : Data Cloud: Viewing Detailed Digital Wallet Consumption Data

**Source:** https://medium.com/@marketingcloudtips/sfmc-tips-232-data-cloud-viewing-detailed-digital-wallet-consumption-data-436dc3bf4f13

---

# SFMC Tips #232 : Data Cloud: Viewing Detailed Digital Wallet Consumption Data

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--436dc3bf4f13---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--436dc3bf4f13---------------------------------------)

4 min read

·

Jan 9, 2026

--

Photo by [Matthieu Brajon](https://unsplash.com/@matthieu_brajon?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

Until now, Data Cloud has primarily used aggregated, consumption-based metrics. However, it has now transitioned to more granular, resource-based metrics.

With this new mechanism, administrators can now understand more accurately than ever before  
which processes (definitions, APIs, features)  
and how much Data Cloud service credits they are consuming.

### Notes (Known Issue)

Currently, **only in environments with the Japanese locale**, there is a [known issue](https://help.salesforce.com/s/issue?id=a02Ka00000llWFZ) where data cannot be retrieved when specifying date filters such as **“past 90 days”.**  
If the filter is set to **“All”,** the data can be retrieved.

## What to Do When No Data Is Displayed

1. First, open the **Consumption Cards** and click **“View Consumption Insights by Tags”.**

2. Depending on the environment, there may be cases where **no data is displayed at all**, as shown below.

> *This can occur due to a different cause than the previously mentioned “date filter known issue”.*

3. In this case, the following two points are the most likely causes:

- The required **permission set** has not been assigned to the user
- The target **Data Lake Object (DLO)** has not been associated with a **Data Space**

## Creating a Custom Permission Set

### 1. Create a Permission Set

Create a new permission set and grant the following under **System Permissions**:

- **Allow access to viewing reports in Data Cloud Reporting**
- **Allows user access Data Cloud**

### 2. Configure Data Space Management

Within the same permission set, navigate to **Data Space Management**.

Grant **Data Space access** to associate Data Lake Objects.

### 3. Assign the Permission Set to the User

Assign the created permission set to the target user.

## Associating Data Lake Objects (DLO)

1. Next, navigate to the **Data Spaces** tab.

2. Click **“Add Data Lake Objects”.**

3. From the list, select the DLOs that start with **“Tenant~”**, then click **“Next”.**

4. Check **“Add objects without filters”** and save.

## Data Population and Analysis

1. Immediately after configuration, data has not yet been stored.  
After waiting a few hours, the data will be populated and become visible.

2. From the displayed data, you can select records that appear to be anomalies and perform detailed report analysis by drilling down.

## Conclusion

At this point, due to known issues specific to the Japan region, there are some limitations such as the use of period filters. However, by setting the period to **“All”,** the feature is fully usable in practice.

Most importantly, with this update, it is now possible to visualize — based on **facts rather than assumptions**:

- Which definitions, APIs, and processes
- How many Data Cloud service credits they are consuming
- Where the root cause of abnormal consumption lies

Previously, operations often became somewhat of a black box, with situations such as:

- “We don’t know why credits are suddenly decreasing”, or
- “All we can do is look at total usage”.

Going forward, we have entered a phase where it is possible to clearly determine:

- “What should be fixed, and how much improvement can be expected”.

I strongly recommend enabling this feature early and taking a close look at **what is consuming what, and how much, in your own environment.**

That’s all for this time.

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
