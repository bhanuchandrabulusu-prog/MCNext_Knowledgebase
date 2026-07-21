# SFMC Tips #198 : Bulk Download of Journey History Data from the Interface

**Source:** https://medium.com/@marketingcloudtips/bulk-download-of-journey-history-data-from-the-interface-326ddced9207

---

# SFMC Tips #198 : Bulk Download of Journey History Data from the Interface

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--326ddced9207---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--326ddced9207---------------------------------------)

5 min read

·

Oct 27, 2025

--

Photo by [John Jennings](https://unsplash.com/@john_jennings?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

With the [**Winter ’26 release**](/@marketingcloudtips/marketing-cloud-engagement-winter-26-release-highlights-b32181d3e42a) of Marketing Cloud Engagement, you can now **download all Journey Builder history data directly from the interface**.

Previously, while it was possible to download journey history data from the screen, you could only obtain the records currently displayed. This meant you had to endlessly scroll down — displaying 100 records at a time — until up to 10,000 records were shown before you could download them. This new feature eliminates that tedious process entirely.

### What’s Improved

- You can now download **all history data at once directly from the interface**, removing the need for any scrolling.
- For example, if a journey was stopped midway, you can easily extract all contacts who were waiting in the journey and insert them into another journey to resume processing. This also meets the need to extract only those who had reached a specific activity.
- Even users who are not familiar with the API can now quickly obtain the necessary data through the **GUI alone**. Of course, for those comfortable with APIs, retrieving data via API remains more flexible and faster in some cases — but the convenience of being able to complete everything in the interface is a major advantage.
- If you want to retrieve **all records using the API**, please refer to the article below.

[## Extracting Contacts Passing Through Wait activities Using Journey Builder REST API

### In the ever-evolving landscape of Salesforce Marketing Cloud, developers often grapple with the challenge of…

medium.com](/@marketingcloudtips/extracting-contacts-passing-through-wait-activities-using-journey-builder-rest-api-8d22ff0048a0?source=post_page-----326ddced9207---------------------------------------)

### **Download Steps**

**1. Open the Journey History tab** and specify the date range for the data you want to retrieve. In this example, I selected the **past 30 days (Max)**.

**2. Use the filter function** to narrow down the data by Activity ID, Status, or other criteria you need.

For a quick way to find Journey Activity ID, please refer to the article below.

[## SFMC Tips #10 : Playful Tricks to Snatch Journey Builder Activity IDs Easily

### In the enchanting realm of Salesforce Marketing Cloud, a nifty feature called “Data Views” diligently stores customer…

medium.com](/@marketingcloudtips/playful-tricks-to-snatch-journey-builder-activity-ids-easily-2c208c6a41b2?source=post_page-----326ddced9207---------------------------------------)

**3. Confirm that the number of records does not exceed 10,000.**  
Although not explicitly mentioned in the help documentation, attempting to download more than 10,000 records will result in a **“JOURNEY\_HISTORY\_DOWNLOAD\_ERROR”**, and the data cannot be retrieved.

Once you’ve confirmed the record count, click the **Download** icon.

4. In addition to the traditional “Copy Page to Clipboard” and “CSV download of displayed records only”, you can now **download all results data, including records not currently displayed on the screen**. You can also reselect the fields you want to include in the download at this step.

5. When you click **Continue** on the next screen, a message will appear:  
 “This action downloads only the data on the screen”. Click **Continue** anyway.

6. The download will start, but the screen will not change, and no loading indicator will be shown.  
Wait approximately **1 minute** for the **“Save File dialog**” to appear. During this time, you can work in another tab, but if you close the Journey History tab, the download will be **interrupted**.

7. When the **“Save File** **dialog”** appears, save the file to complete the process.

> *Note that the behavior in this final step can be slightly* ***unstable or unintuitive****, so further improvements are expected in future updates.*

### **Considerations**

- The downloadable history is **limited to data from the past 30 days**.  
  If you need to save or aggregate data older than 30 days, you will need to use a different approach, such as the **“Update Contact”** activity or another method to import the data.
- For **Wait-type activities**, a single contact may have **two types of records**: `waiting` (in progress) and `complete` (wait finished).
- If you only want to retrieve records that have **already completed the wait**, filter by **Status: complete**.
- If you want to retrieve contacts **currently waiting**, include both **Status: complete** and **Status: waiting**, and set conditions to **exclude contacts that have both statuses**.
- Understanding the characteristics of each type of data is important. Carefully adjust your filter conditions to **avoid duplicates** and extract **only the records you need**.
- When retrieving data via the **API**, there is a **1 GB file size limit**, but the **10,000-record limit does not apply**.  
  However, the API also only allows access to **data from the past 30 days**.
- For instructions on retrieving history data in **compressed format**, please refer to the article linked below.

[## SFMC Tips #61 : How to Download Compressed Journey History

### In this post, I’ll walk through the new Summer ’24 feature in Salesforce Marketing Cloud, which allows us to download…

medium.com](/@marketingcloudtips/how-to-download-compressed-journey-history-676042a5ac6d?source=post_page-----326ddced9207---------------------------------------)

That concludes this guide.

Stay tuned for more Salesforce Marketing Cloud tips! 😎

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
