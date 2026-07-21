# SFMC Tips #32 : Automation Studio Performance Boosted by 162%

**Source:** https://medium.com/@marketingcloudtips/automation-studio-performance-boosted-by-162-aff6be525d7c

---

# SFMC Tips #32 : Automation Studio Performance Boosted by 162%

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--aff6be525d7c---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--aff6be525d7c---------------------------------------)

3 min read

·

Mar 7, 2024

--

Photo by [todd kent](https://unsplash.com/@churchoftodd?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

Have you recently felt that Salesforce Marketing Cloud’s automation processes are completing faster? Well, you’re not alone in that observation.

Thanks to the new feature update in Spring ’24 (released between February 16 and March 8, 2024), it seems that Automation Studio’s performance has seen a substantial improvement of around 62%.

I’m usually a bit skeptical about improvements labeled as “% enhancement”, but this time, I can personally vouch for the noticeable increase in speed, prompting me to highlight it in this article. ✨

*Regarding this automation improvement, it likely doesn’t involve changes in on-screen displays. Therefore, regardless of the stack your account belongs to, it appears that there was a universal enhancement across all stacks as of February 16, 2024. If this information is incorrect, I apologize.*

Now, let’s take a look at the actual automation history.

![]()

Automation has indeed powered up significantly. It’s evident that there’s a clear improvement. Given the considerable time difference between my location in Japan and the United States, it seems like the enhancement started from February 17.

Considering that most of these automations involve SQL query activities, it’s not an exaggeration to say that the performance of SQL query activities has improved by approximately 62%. This is a fantastic improvement! 🚀

Now, let’s examine how much has actually improved and check the time aspect. The table below illustrates the Before/After comparison, where, for example, a task that previously took 20 minutes is now completed in 12 minutes, reflecting a 162% improvement.

![]()

Looking at the attached automation history, tasks that used to take about 54 minutes before February 16 now finish in approximately 33 minutes after February 17. It aligns perfectly with the table. After checking with several automations, it seems that the longer the steps in the automation, the more this improvement applies. For automations with short steps, where each step originally took less time, there might not be a significant reduction in overall processing time.

As previously discussed in the article “How to find SQL query activities that take more than 15 minutes processing time on Automation Studio”, the efficient processing of SQL queries in a short timeframe has long been a challenge for Marketing Cloud developers. The improvement in performance this time is highly appreciated, as it signifies a significant reduction from the previous 30-minute duration to approximately 20 minutes for the completion of SQL processes.

[## SFMC Tips #1 : How to find SQL query activities that take more than 15 minutes processing time on…

### Are you effectively utilizing the new data views, \_AutomationInstance and \_AutomationActivityInstance, released for…

medium.com](/@marketingcloudtips/how-to-find-sql-query-activities-that-take-more-than-15-minutes-processing-time-on-automation-7af2df10efca?source=post_page-----aff6be525d7c---------------------------------------)

However, keep in mind that this update doesn’t guarantee time savings in every case. So, even if you don’t see improvements, let’s refrain from complaints. 😂 The example I provided happened to show a 62% improvement, and results may vary for each automation.

Thank you for reading.

Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
