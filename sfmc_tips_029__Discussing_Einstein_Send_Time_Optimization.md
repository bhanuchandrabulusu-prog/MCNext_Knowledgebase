# SFMC Tips #29 : Discussing Einstein Send Time Optimization

**Source:** https://medium.com/@marketingcloudtips/discussing-einstein-send-time-optimization-6dd825a5d2b3

---

# SFMC Tips #29 : Discussing Einstein Send Time Optimization

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--6dd825a5d2b3---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--6dd825a5d2b3---------------------------------------)

7 min read

·

Feb 23, 2024

--

Photo by [Hannes Richter](https://unsplash.com/@harimedia?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

In this article, I would like to **discuss Einstein Send Time Optimization**. This feature, currently available for companies using the Corporate Edition and Enterprise Edition, is accessible for **“free”**, so let’s make the most of it.

## ■ Feature Overview

Einstein Send Time Optimization utilizes machine learning to analyze engagement data from the **past 90 days** for the targeted contacts. **This automatic analysis predicts the optimal send time with a high likelihood of engagement for the messages sent**.

*\*The “engagement data” consists of approximately 20 elements, but specific details such as content and calculation logic remain undisclosed.*

Since this feature relies on machine learning from the past 90 days of engagement data, **for new customers or instances where the engagement data from the past 90 days is insufficient, the contact will receive messages based on a “generalized model”**. (The system’s determined optimal time.)

*\*While it’s possible to change the Salesforce Marketing Cloud setup to “send immediately” upon the arrival of Einstein STO activity,* ***Salesforce recommends using the “optimal default time”****.*

Regarding this evaluation, please note the following key points:

**1. Engagement data is evaluated only once a week.  
2. Emails classified under Transactional for sending are not evaluated.**

And if you aim to improve the data quality score, it goes without saying that sending to a large number of contacts is necessary. However, **it’s also possible to enhance the score by distributing the sends as evenly as possible across multiple times throughout the week**.

## ■ Considerations during Setup

Understanding this Einstein STO activity as **a type of “Waiting Activity”** should suffice. When it becomes the optimal time for each contact, the waiting period concludes, and the activity flows into email activities.

After the waiting period ends in the Einstein STO activity, **the timing for flowing into email activities is always at the “top of the hour”**.

The term “top of the hour” refers to **“◯ o’clock 00 minutes”**.

Here, let’s consider a specific scenario as an example: “Starting sending from 10:00 AM and completing sending by 5:59 PM”.

In this case, the following eight “top of the hour” times are included.

```
① 10:00 AM  
② 11:00 AM  
③ 12:00 PM (noon)  
④ 1:00 PM  
⑤ 2:00 PM  
⑥ 3:00 PM  
⑦ 4:00 PM  
⑧ 5:00 PM
```

At these eight scheduled times, envision the transition of contacts from Einstein STO activity to the email activity side. Contacts begin flowing from Einstein STO activity, reach the email activity, undergo the sending process, and eventually arrive in the inbox.

In this example, the setting on the Einstein STO activity in this case will be configured as “8 hours”.

To determine the rationale behind the “8 hours” setting, it is helpful to envision it in terms of eight distinct **time periods**. The illustration is as follows:

```
① "10 o'clock range" starting from 10:00 AM  
② "11 o'clock range" starting from 11:00 AM  
③ "12 o'clock range" starting from 12:00 PM  
④ "13 o'clock range" starting from 1:00 PM  
⑤ "14 o'clock range" starting from 2:00 PM  
⑥ "15 o'clock range" starting from 3:00 PM  
⑦ "16 o'clock range" starting from 4:00 PM  
⑧ "17 o'clock range" starting from 5:00 PM
```

Also, another important point is that starting at 10:00 for Einstein STO activities, it means moving away from them. **Therefore, it is necessary to arrive at the Einstein STO activity before 9:59 and be evaluated in the Einstein STO activity (i.e., be in a WAIT state)**.

**(↑ This is very important. ↑)**

For example, in the case of an entry source with 10,000 records, if you start entering at 9:50, you can deliver those 10,000 records to the Einstein STO activity and have them evaluated within the 10 minutes until 9:59. However, what about entry sources with over 1 million records? It is likely that it will take more than 10 minutes to deliver all 1 million records to the Einstein STO activity and complete the evaluation.

In such cases, it is necessary to allow some time flexibility for entries. For instance, if you start the entry at 9:00 in advance, evaluations will be completed by 9:59, even with 1 million records.

The Einstein Send Time Optimization (STO) feature, by design, calculates the “top of the hour” after arrival as the starting time for each contact. Therefore, even if contacts arrive at the Einstein STO activity after 10:00 in the example above, they will be evaluated with the same ‘8 hours’ setting, as shown below.

```
① "11 o'clock range" starting from 11:00 AM  
② "12 o'clock range" starting from 12:00 PM  
③ "13 o'clock range" starting from 1:00 PM  
④ "14 o'clock range" starting from 2:00 PM  
⑤ "15 o'clock range" starting from 3:00 PM  
⑥ "16 o'clock range" starting from 4:00 PM  
⑦ "17 o'clock range" starting from 5:00 PM  
⑧ "18 o'clock range" starting from 6:00 PM
```

As you can see, contacts that arrive late will **result in a one-hour delay** in delivery time, so please be aware of this.

*\*The acceptable time window for sending emails may vary depending on the country of residence and can also be influenced by corporate culture. Another factor to keep in mind is* ***the retry time for soft bounces****. Companies that prefer not to send emails during late-night hours should also take into account the retry time for soft bounces.*

Below, I will provide another specific example.

The entry schedule for this journey is at 10:55 AM. Let’s assume that the top path reaches the STO activity at 10:58 AM. On the other hand, the middle path has a wait activity of 3 hours before the STO activity, so it will reach the STO activity at a delayed time of 1:58 PM.

Now, in the top path, a 3-hour setting is applied in the STO activity, while in the middle path, a 4-hour setting is applied. As a result, email sending will commence during the following time frames:

```
<Upper Path>  
① "11 o'clock range" starting from 11:00 AM  
② "12 o'clock range" starting from 12:00 PM  
③ "13 o'clock range" starting from 1:00 PM  
  
<Middle Path>  
① "14 o'clock range" starting from 2:00 PM  
② "15 o'clock range" starting from 3:00 PM  
③ "16 o'clock range" starting from 4:00 PM  
④ "17 o'clock range" starting from 5:00 PM
```

As indicated, the arrival time of each contacts at the STO activity will determine the sending time, so please be mindful of this.

## ■ Preview Feature

Einstein Send Time Optimization includes a preview feature that allows you to examine the distribution of contacts within the specified time slots in advance.

The benefit of previewing is that, for the given data extension, you can gain insights into when to send bulk emails without utilizing the Einstein STO activity. **This insight is valuable when deciding the optimal time to conduct bulk sending**.

The steps are as follows:

1. Open **“Einstein Overview”**.

2. Open the **“Preview”** tab.

![]()

3. After **selecting a specific data extension**, **choose the desired time period** for confirmation.

4. Review the display. From the results below, it can be observed that the **13 o’clock range is the most voluminous zone**.

## ■ Conclusion

I encourage each one of you to tap into the potential of Einstein Send Time Optimization! This outstanding feature utilizes advanced machine learning to predict the optimal email send times based on 90 days of engagement data. For those managing substantial email campaigns, STO offers invaluable insights.

However, configuring STO activities demands strategic placement and careful consideration of time settings, especially when dealing with multiple email activities.

Approach the setup with the utmost attention and embark on the finest marketing journey by harnessing the power of STO!!

Thank you for reading.

Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
