# SFMC Tips #45 : How to Bulk Retrieve Automation Activity Execution Times

**Source:** https://medium.com/@marketingcloudtips/how-to-bulk-retrieve-execution-times-of-automation-activities-in-each-step-of-automation-studio-16903798fc9a

---

# SFMC Tips #45 : *How to Bulk Retrieve Automation Activity Execution Times*

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--16903798fc9a---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--16903798fc9a---------------------------------------)

2 min read

·

Jun 15, 2024

--

Photo by [Stephan Louis](https://unsplash.com/@stephanlouis?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

Have you ever wanted to find out:

1. **What time the automation activities placed in the steps of Automation Studio in Salesforce Marketing Cloud started,**
2. **What time they ended, and**
3. **How many minutes and seconds it took to complete them?**

All summarized in one view?

You can easily find out this information using the following SQL query. **Just replace “XXXXXXXXXXXXXXX” in the WHERE clause with the name of the automation you want to investigate and run it in Query Studio**.

```
SELECT TOP 10000   
    AutomationName,  
    ActivityName,  
    ActivityInstanceStep,  
    CONVERT(VARCHAR(19), DATEADD(HH, 9, ActivityInstanceStartTime_UTC), 120) AS [ActivityInstanceStartTime],  
    CONVERT(VARCHAR(19), DATEADD(HH, 9, ActivityInstanceEndTime_UTC), 120) AS [ActivityInstanceEndTime],  
    FORMAT(DATEDIFF(S, ActivityInstanceStartTime_UTC, ActivityInstanceEndTime_UTC) / 60, '00') + ':' +   
    FORMAT(DATEDIFF(S, ActivityInstanceStartTime_UTC, ActivityInstanceEndTime_UTC) % 60, '00') AS [Duration]  
FROM   
    _automationactivityinstance  
WHERE   
    AutomationName = 'XXXXXXXXXXXXXXX'  
    AND DATEADD(HH, 9, ActivityInstanceStartTime_UTC) >= CONVERT(DATE, DATEADD(HH, 15, GETDATE()), 111)  
ORDER BY   
    CONVERT(DECIMAL, ActivityInstanceStep) ASC,   
    DATEDIFF(S, ActivityInstanceStartTime_UTC, ActivityInstanceEndTime_UTC) DESC
```

- The sample query above retrieves data for today’s execution.
- **The extracted dates (ActivityInstanceStartTime\_UTC etc.) are in the UTC time zone**, so you will need to adjust them for your country’s time zone. The current 9-hour adjustment is based on my country’s time zone, Japan.
- **The Getdate() function extracts dates in the CST time zone**, so you will need to adjust them for your country’s time zone. (In my country, Japan, there is a 15-hour time difference, so to extract the data as the previous day’s data, we need to subtract 9 hours.)
- The results will be sorted by step order. Within the same step, activities will be sorted in descending order of processing time (Duration).

**Update: October 7, 2024**  
This article has been updated following the Winter ’25 release (between October 4 and October 25, 2024). Previously, the data retrieval range was limited to “1 day to 31 days ago,” but now it is possible to retrieve “data for the current day.” The article has been adjusted accordingly.

[## SFMC Tips #58 : Winter ’25 Release Highlights: Notable New Features in Marketing Cloud

### The release notes for Salesforce Marketing Cloud Winter ’25, focusing on new features, have been published. I would…

medium.com](/@marketingcloudtips/winter-24-release-highlights-notable-new-features-in-marketing-cloud-f9ab85aac8b1?source=post_page-----16903798fc9a---------------------------------------)

Is this magic? No, it’s just a clever idea. 😎

Feel free to use it!

Thank you for reading.

### Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
