# SFMC Tips #102 : How to Avoid the “999 Occurrences” Bug in Journey Builder

**Source:** https://medium.com/@marketingcloudtips/how-to-avoid-the-999-occurrences-bug-in-journey-builder-9e472753cf95

---

# SFMC Tips #102 : How to Avoid the “999 Occurrences” Bug in Journey Builder

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--9e472753cf95---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--9e472753cf95---------------------------------------)

3 min read

·

Apr 17, 2025

--

Photo by [Pat Whelen](https://unsplash.com/@patwhelen?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

*This article is based on a LinkedIn post I shared earlier, but given its importance, I decided to document it here on Medium for wider visibility.*

Have you ever encountered an issue in Journey Builder where a recurring schedule unexpectedly changes to **“After 999 occurrences”**? 🤔

This peculiar behavior was observed by one of my clients and later confirmed with others. The result? Journeys suddenly stop running after approximately three years.

## Steps to Reproduce the Issue

Through research and testing, I pinpointed the steps that lead to this bug:

1️⃣ First, create a recurring schedule with a daily frequency, setting the end to “Never”.  
2️⃣ Save the schedule and the journey.  
3️⃣ Return to the Journey Dashboard and reopen the journey.  
4️⃣ You’ll likely see a schedule end date in the year 2075, even though it was initially set to “Never”. \*Sometimes it remains as “Never”, so you may need to save and reopen the journey several times.  
5️⃣ Go back to the schedule configuration screen.  
6️⃣ Here, you’ll notice that the schedule is set to “**After 18263 occurrences**”.  
7️⃣ After clicking the “Every 1 day” section, click elsewhere on the screen, click the “Summary” button, press the Alt key, or press the Tab key.  
8️⃣ The occurrences will now change to “**After 999 occurrences**”.

If you activate the journey without noticing this change, it will automatically stop in approximately three years.

Is this a critical flaw in Journey Builder? Or just a joke? 🤡

## A Quick Solution

Instead of focusing on the problem, let’s shift to the solution.

One of my clients had nearly 100 recurring journeys, and I managed to check their schedules in just **10 minutes**! 😏

I previously detailed the method in my blog post:

[## SFMC Tips #66 : How to Retrieve All Entry Source Information Using REST API

### Have you ever wondered which Data Extensions are being used as entry sources in your currently active journeys, or how…

medium.com](/@marketingcloudtips/how-to-retrieve-all-entry-source-information-using-rest-api-d595e48e73e7?source=post_page-----9e472753cf95---------------------------------------)

Here’s how you can quickly identify potentially problematic journeys:

- Filter journeys where `"publishedInteractionCount" = 1` (indicating active journeys).
- Check if `"schedule.occurrences"` is set to **999**.

## Conclusion

The cause of this issue is actually quite clear: the previous screen only allows manual input up to 999. Therefore, if any changes are made, the system automatically resets the value to the maximum of 999. This is likely a defect, but since it’s a minor issue, I doubt Salesforce will prioritize fixing it. Let’s proactively avoid it ourselves.

That’s it for now.

Stay tuned for more Salesforce Marketing Cloud tips! 😊

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
