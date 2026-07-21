# SFMC Tips #251 : Marketing Cloud Next: More Flexible Scheduling for Segment-Triggered Flows

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-next-more-flexible-scheduling-for-segment-triggered-flows-b49477a93001

---

# SFMC Tips #251 : Marketing Cloud Next: More Flexible Scheduling for Segment-Triggered Flows

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--b49477a93001---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--b49477a93001---------------------------------------)

4 min read

·

Feb 18, 2026

--

Photo by [Behnam Norouzi](https://unsplash.com/@behy_studio?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

In the [Spring ’26 new feature release](/@marketingcloudtips/marketing-cloud-next-spring-26-release-highlights-24c0c804b0cb) for Marketing Cloud Next Growth & Advanced Edition, the configuration of recurring schedules for Segment Triggered Flows has been significantly improved.

Until now, recurring settings were limited to relatively simple options:

- **Daily** (run at the same time every day)
- **Weekly** (run at the same time every week)

Therefore, for use cases such as:

- “I want it to run hourly”
- “I want it to run only on weekdays”
- “I want it to run on a specific date every month”
- “I want to set up an annual batch”

there were practical limitations in flexibility compared to Marketing Cloud Engagement.

The following settings have now been newly added:

1. **Hourly**
2. **Daily on Weekdays**
3. **Weekly on specific days**
4. **Monthly on specific days**
5. **Yearly**

In this article, I will review each of these one by one.

## 1. Hourly

The hourly setting is very simple.  
You can configure a schedule within a range of 1 hour to 168 hours (7 days).

## 2. Daily on Weekdays

In addition to the previous “Daily (run at the same time every day)” option,  
“**Monday through Friday** (run at the same time)” has been added.

> *Note: It does not take “public holidays” into account, so it will also send on holidays.*

## 3. Weekly on specific days

![]()

Previously, delivery was limited to a simple weekly schedule (run at the same time). Now, for example, you can choose intervals such as every 2 weeks, selectable from every 1 week up to every 52 weeks.

You can also select multiple “specific days of the week” for delivery.

## 4. Monthly on specific days

![]()

For monthly settings, you can select intervals from 1 month up to 12 months. For example, if you want to send quarterly, set it to “3”.

Additionally, you can specify options such as “**End of Month (On last day)**” or a “**Specific date (On day)**”.

\*The example in the figure above shows a configuration to send on the 15th of every month.

> ***Note:***  
> *If you select a number from the pull-down, you cannot set “End of Month”.*

## 5. Yearly

There are no special configuration items for the yearly setting.  
In the above example, it will send every year on February 18 at 12:00.

## Conclusion

Honestly, this is an update that can be said to have finally reached a level of flexibility comparable to Marketing Cloud Engagement.

It strongly conveys that Marketing Cloud Next is evolving to a “production-ready level”.

There are also several points to be aware of.

- If you want to automatically exclude country-specific “public holidays” from delivery, separate logic implementation (development work) is required.
- Complex schedules based on relative dates, such as “send 5 days before the end of each month”, are not supported by standard functionality and also require development.

If you need such advanced date control, continued careful design and implementation will be required. Please take note.

That is all for this time.

Stay tuned for more Salesforce Marketing Cloud tips! 😎

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
