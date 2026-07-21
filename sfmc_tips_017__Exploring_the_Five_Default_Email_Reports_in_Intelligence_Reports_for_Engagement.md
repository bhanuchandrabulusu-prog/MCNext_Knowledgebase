# SFMC Tips #17 : Exploring the Five Default Email Reports in Intelligence Reports for Engagement

**Source:** https://medium.com/@marketingcloudtips/exploring-the-five-default-email-reports-in-intelligence-reports-for-engagement-c43f8ed71a0e

---

# SFMC Tips #17 : Exploring the Five Default Email Reports in Intelligence Reports for Engagement

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--c43f8ed71a0e---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--c43f8ed71a0e---------------------------------------)

10 min read

·

Jan 16, 2024

--

Photo by [Isaac Smith](https://unsplash.com/@isaacmsmith?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

In Salesforce Marketing Cloud’s Intelligence Reports for Engagement, the “**Pivot Tables” tab** comes with **Five Default Email Reports**.

### **Five Default Email Reports:**

1. **Journey Performance**
2. **Campaign Performance**
3. **Email — Audience Engagement Over Time**
4. **Campaign — Best Performing Send Day**
5. **Email — Daily Send Summary**

Some of you reading this article may already be utilizing the Tracking reports of Email Studio and the Reports (standard reports) of Analytics Builder. However, there might be those who haven’t fully leveraged the relatively new Intelligence Reports for Engagement, as compared to these other reporting features.

So, in this article, let’s eliminate any hesitations or reluctance towards Intelligence Reports for Engagement by exploring the contents of these fundamental five reports and understanding what they entail.

*Note: As of January 2024, Intelligence Reports for Engagement* ***doesn’t support reports for SMS or LINE deliveries****.*

## 1. Journey Performance

Firstly, let me introduce Journey Performance, as it is probably the most versatile and practical as a report, so I’ll introduce it ahead of others.

This report allows you to **review Engagement Data for “Email Activities” within Journeys in a summarized format**.

Firstly, there are three Rows:

![]()

You can also choose to hide the Journey Version item if you want to display versions collectively. However, you can also set it to “Hidden” as shown above.

*Note: If you set it to “Hidden” here, please be aware that it will be exported in a hidden state when exporting.*

By the way, for the easy usage of Intelligence Reports for Engagement’s pivot table, you’ll create reports by combining Rows, Columns, and Values.

As the terms Rows, Columns, and Values might be a bit confusing, understanding them as follows might make it clearer:

- **Rows**: These primarily represent “**Dimensions”** or “**Qualitative Data”**.
- **Columns**: If Rows alone are not sufficient for clarity, Columns can be used.
- **Values**: These represent “**Measures”** or “Q**uantitative Data”**.

*Note: If you try to place measurements (quantitative data) for Rows, it cannot be set. It will result in drag-and-drop being rejected, so there’s no chance of setting it incorrectly.*

Please check the definitions of dimensions and measurements below link.

[## Help And Training Community

### Edit description

help.salesforce.com](https://help.salesforce.com/s/articleView?id=sf.mc_dat_dimensions_and_measurements.htm&type=5&source=post_page-----c43f8ed71a0e---------------------------------------)

Next, let’s confirm Columns and Values. In this report, Columns are blank. And in Values, there are six items, including:

There are some points to note.

*\* Email Sends represent the* ***actual number of emails sent*** *to customers, mirroring the* ***Total Sent*** *count in Email Studio “Tracking”.*

*\* On the other hand, Journey Builder’s* ***“success” in sending includes contacts in pending, unsubscribed status, or those targeted by exclusion scripts,*** *making it slightly higher than Email Sends.*

*\* There’s also a metric similar to Email Sends called Email Deliveries, subtracting various bounced contacts from the Email Sends count.*

*\* Email Click To Open Rate (CTOR) is the ratio of Email Unique Clicks to Email Unique Opens.*

That concludes the explanation of Journey Performance.

For those who find it a bit challenging, I recommend starting by hiding items, adding bounce information to Values, and experimenting with various adjustments. You’ll get used to it eventually. You can also save it under a different name, so please use this report as a reference to create various types of reports.

This is my first time covering Intelligence Reports for Engagement on my Medium, so I’d also like to share with you **how to switch between pivot tables and flat tables**, and **how to export them**.

By default, it is displayed on the pivot table side. To switch to the flat table side, click the button below. Please switch according to your preference.

Also, when outputting this report, you can choose whether to output it in the pivot table or flat table. If you just want to look at the output report as it is, the pivot table may be fine, but if you plan to process it in Excel or similar software, the flat table is recommended.

And you can schedule to export or export immediately (Quick Download) from the “**More Actions**” button.

As an additional feature, **there is also the functionality of filters**. This feature works literally, allowing you to, for example, pinpoint and display only the results of a specific journey or show journeys with a sending count of over 10,000 emails. Since displaying everything at once can be overwhelming, using filters can help enhance visibility. Please make the most of this feature.

![]()

Additionally, there is a **“Date Range”** in the upper left corner. **This date range is based on the Event Date. The key point is that it is not based on the Send Date**. For example, even if the date range is set to the past week from today, if an email sent two months ago was opened three days ago, it will be included in the extraction. This applies even if the Value does not include engagement data. This is why, unlike Tableau, Intelligence Reports is a tool specialized in marketing engagement data.

## 2. Campaign Performance

Next is Campaign Performance.

This report is **based on “Campaigns”** that can be configured in Salesforce Marketing Cloud, and it allows you to **review the performance of each Email associated with those campaigns**.

There are two Rows. (Columns are blank.)

![]()

A campaign is a function that helps aggregate results in a lump with a “tagging” setting that can encompass multiple strategies. You can configure these campaigns in the **“Campaign” tab on the Salesforce Marketing Cloud top-page**.

As far as I understand, campaigns need to be set up before sending emails, and once emails are sent, you cannot tag them later. Therefore, planning for pre-campaign tagging is necessary. Most people may not perform campaign settings and just send emails. In such cases, it might be fine to hide the campaign-related items in the Campaign Performance report.

*Note: If you have information like “You can tag them later!” regarding campaigns, please let me know in the comments. I might just not be aware of it.*

Next, let’s also confirm Values, but it is exactly the same as in [1] Journey Performance, so I will skip the explanation.

![]()

## 3. Email — Audience Engagement Over Time

Next is Email — Audience Engagement Over Time.

This report allows you to **review the total number of “unique clicks” on a weekly basis for each publication list at the time of sending**.

The report includes the following elements:

- **Rows**: Audience Name (referring to the publication list at the time of sending)
- **Columns**: Send Week (weekly summary)
- **Values**: Email Unique Clicks (total number of unique clicks)

![]()

Unlike reports [1] and [2] , this report provides an example of using Columns. If you want to review summaries on a “weekly” or “monthly” basis, consider creating a report based on this example, as shown in the illustration below.

## 4. Campaign — Best Performing Send Day

Now, Campaign — Best Performing Send Day.

This report is designed to determine “**Which day of the week performs the best**”.

Since this report is also related to campaigns, if you are not using campaigns, it may be suitable to set it to “Hidden”.

The **Rows** consist of the following two elements. In this case, instead of using journey or email names, it utilizes the dimension of Send Weekday (day of the week).

![]()

The **Values** include the following three elements. Use this report to identify the weekdays that are more likely to be opened and clicked on, and maximize your performance.

![]()

## 5. Email — Daily Send Summary

Finally, Email — Daily Send Summary.

This report **displays the sending performance on a “daily” basis**.

*Note: This report tends to have a large number of records. The maximum number of records for displaying Intelligence Reports for Engagement is 8,000, so there may be limitations on the display of the report. Please be mindful of the set ‘Period’ size.*

The **Rows** include the following four elements.

![]()

Since Email Job ID is included in Rows, you can review performance not at the email message level but at the sending unit (job level).

The Values include the following 11 items. These 11 items represent the basic form when collecting engagement data, so feel free to use them as a reference when creating other reports.

![]()

That concludes it.

By reviewing these five standard reports, I hope you can visualize how to utilize the pivot table in Intelligence Reports for Engagement. While using these reports as a reference, feel free to create your original reports.

As a bonus, I’ll provide an example of my original report: “Bounce Analysis by Email Domain”.

## 6. Bounce Analysis by Email Domain

Please try creating a report in the following format. Feel free to adjust the reporting period and the lower limit for the email send count (Email Sends) in the filters.

![]()

You should be able to create a report as follows. Based on this report, check if there are any anomalies in terms of increased bounces for specific domains.

Closing with some key considerations for Intelligence Reports for Engagement:

### Important Notes:

- The following data is not guaranteed for accuracy and completeness. Please use it at a reference level. Additionally, it can only be used for open and click counts.

***- Email Browser Model****: Browser model of the sent emails (e.g., Firefox, Chrome).*

***- Email Browser Name****: Browser name of the sent emails (e.g., Chrome 96, Edge 96).*

***- Email Device Model****: Device model of the sent emails.*

***- Email Device Name****: Device name of the sent emails.*

***- Email Client Model****: Mail client model of the sent emails (e.g., Outlook).*

***- Email Client Name****: Mail client name of the sent emails (e.g., Outlook 2013).*

***- Email Device OS Model****: Operating system model used for the sent emails.*

***- Email Device OS Name****: Operating system device name used for the sent emails.*

***- Email Device Type****: Type of device used (Mobile or Desktop).*

***- Email Feature Phone****: Indicates whether the message was received on a feature phone. Feature phones are old-generation mobile phones, primarily used in Japan.*

***- Email Link Alias****: Actual link clicked within the email. Works only for links assigned with link aliases.*

- The term “Email Click Event Lag Days” may be unclear, but it refers to a type of metric, specifically the “average number of days it takes from the time of sending to a click”.
- Regarding Complaints data, most email providers do not have this data, so this value may not be very informative.
- If you want to exclude test sends from the “Preview and Test” feature in Email Studio, set the **Email Test Indicator to “False”** in the filter. In other words, Email Test Indicator being True indicates test sends with the test send flag.
- Two recommended filters to set when creating a report on email delivery are as follows. By applying these filters, only emails sent during the specified period are included.

***1. Email Sends >= 1  
2. Email Test Indicator = False***

- While Data Views typically retain data for the past 6 months, Intelligence Reports for Engagement holds data for **up to 2 years**.
- The timezone for Intelligence Reports for Engagement is based on the **“Parent Business Unit’s timezone”**.

I hope this exploration proves insightful as you navigate Intelligence Reports for Engagement.

Thank you for reading.

Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
