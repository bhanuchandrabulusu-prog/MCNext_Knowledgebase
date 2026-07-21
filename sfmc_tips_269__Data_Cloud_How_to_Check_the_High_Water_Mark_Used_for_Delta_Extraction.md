# SFMC Tips #269 : Data Cloud: How to Check the High Water Mark Used for Delta Extraction

**Source:** https://medium.com/@marketingcloudtips/data-cloud-how-to-check-the-high-water-mark-used-for-data-cloud-delta-extraction-efa89612b71e

---

# SFMC Tips #269 : Data Cloud: How to Check the High Water Mark Used for Delta Extraction

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--efa89612b71e---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--efa89612b71e---------------------------------------)

3 min read

·

Mar 21, 2026

--

Photo by [Andrew Ly](https://unsplash.com/@nineteen?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

In data integration between Data Cloud and Marketing Cloud Engagement, “delta extraction” (incremental extraction) is often used. In particular, when data is not being integrated as expected, checking the value of the “high water mark (last value)” is the first step in troubleshooting.

## Verification Steps

### Step 1

From the **Email Studio** menu, open **Interactions > Data Factory Utility**.

### Step 2

A list of Data Factory Utilities will be displayed. Click any utility you prefer. The same content will ultimately be displayed, so any utility is fine.

### Step 3

Use “Ctrl + F” or similar to search for the relevant data stream information. The **Table** column corresponds to the Data Extension name used in the data stream.

Up to 250 records are displayed per page. If you cannot find the relevant data, switch pages using pagination.

When a data stream is created, this Data Factory Utility and the automation that runs it are automatically created.

For your information, even if you delete the data stream, the above Data Factory Utility and its associated automation are not deleted.

## Items to Check

- **Extract Last Value**: Current high water mark (HWM) value
- **Column Name**: Field name used in CDC (date/time or number)
- **Extract Type**: Extraction type (Full refresh or delta extraction)
- **Table**: Data Extension name

## Tips

If data synchronization fails during delta updates, check whether the numeric or date values of the relevant records are below the high water mark. This may be the reason why the records are not included in the delta extraction.

## Conclusion

By properly understanding this mechanism, you will be able to handle data integration and troubleshooting more efficiently.

This content was previously published by me in the [help documentation](https://help.salesforce.com/s/articleView?id=005104641&type=1).

[## Salesforce Help

### Edit description

help.salesforce.com](https://help.salesforce.com/s/articleView?id=005104641&type=1&source=post_page-----efa89612b71e---------------------------------------)

If you found this article helpful, I would appreciate it if you could click “👍 Yes” on “Did this article solve your problem?” at the bottom of the help document.

That’s all for this time.

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
