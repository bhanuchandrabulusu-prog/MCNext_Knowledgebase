# SFMC Tips #98 : Marketing Cloud Next: How to Utilize Email Engagement Data

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-on-core-how-to-utilize-engagement-data-a9b1f492b7d6

---

# SFMC Tips #98 : Marketing Cloud Next: How to Utilize Email Engagement Data

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--a9b1f492b7d6---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--a9b1f492b7d6---------------------------------------)

5 min read

·

Apr 10, 2025

--

Photo by [Federica Giusti](https://unsplash.com/@federicagiusti?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

In the previous article, I explained how to check email engagement data (such as sends, opens, clicks, bounces, and unsubscribes) in Marketing Cloud Growth & Advanced Edition.

[## SFMC Tips #97 : Marketing Cloud on Core: How to Check Engagement Data

### I investigated whether Marketing Cloud on Core (Marketing Cloud Growth Edition / Advanced Edition) has an equivalent to…

medium.com](/@marketingcloudtips/marketing-cloud-on-core-how-to-check-engagement-data-5452bfbc1ae3?source=post_page-----a9b1f492b7d6---------------------------------------)

These engagement history records — sends, opens, clicks, bounces, unsubscribes — are managed in the following objects:

### Management Objects

**Data Stream and its corresponding Data Lake Object:**

- **MessagingEventsEmail-EmailEngagement** (before Summer ‘25)
- **MessagingEventsEmailV2-EmailEngagement** (after Summer ’25)

**Data Model Object:**

- **Email Engagement**

> *Previously, records were created in MessagingEventsEmail-EmailEngagement, but starting from Summer ’25, they are created in MessagingEventsEmailV2-EmailEngagement. The V1 object is now deprecated.*

It’s important to note that only part of the fields from the Data Lake Object are mapped to the Data Model Object, not all of them. In this sense, the Data Lake Object provides more available fields. However, in the following cases, you must use the Data Model Object **Email Engagement**:

- **Segment Creation**
- **Using Decision Splits (as Engagement Split)**

In these cases, the Data Model Object is required, and the Data Lake Object cannot be used directly.

## Segment Creation

As an example of a segment, let’s try retrieving “people who clicked a specific URL within a certain email element”.

> *If you are a Marketing Cloud Engagement user, you may recognize this as the equivalent of the* ***“Measure”*** *feature.*

With Measures, you can use engagement data from the past 6 months. However, in Marketing Cloud Growth & Advanced Edition, segments can leverage up to **2 years of engagement data**.

In this case, I will create a segment for “people who clicked a specific URL in an email sent from a certain flow, three times”.

For this example, I will use the following four pieces of information:

1. **Flow Name**: `SignupTaskReg3`  
    (DMO: Flow / Field: Name)
2. **Flow Version Number**: `1`  
    (DMO: Flow Version / Field: Version Number)
3. **Email Element API Name**: `Email`  
    (DMO: Flow Element / Field: Name)
4. **Clicked Link URL**: `https://www.salesforce.com/jp/`  
    (DMO: Email Engagement / Field: Resolved URL)

These objects have the following relationships, so when creating the segment, you select them in the order of **① → ② → ③ → ④ → ⑤**.

![]()

**Note:**  
When setting the clicked link URL, you may notice a field named “Link URL”. However, you should select **“Resolved URL”** instead.

Also, when selecting **③ Flow Element**, as shown in the diagram, there are two possible paths:

- via *Flow Element Run → Flow Element*
- via *Flow Element Run → Outcome*

Be sure to choose the **Flow Element Run → Flow Element** path.

Once executed, the segment was successfully retrieved as shown below. Success!

## **Using Decision Splits (as Engagement Split)**

Next, let’s set conditions in a decision element and create a flow that says:  
“After waiting for a certain period, send a different message to people who opened the email that was sent just before the wait”.

> *In Marketing Cloud Engagement, this functionality was available as* ***Engagement Split****. However, in Marketing Cloud Growth & Advanced Edition, there is currently no built-in Engagement Split, so it needs to be configured manually.*

Before setting up the flow, configure **Email Engagement** in the data graph. For this scenario, I’ll use the following three pieces of information:

- **DMO**: Email Engagement / **Field**: Engagement Channel Action → Engagement type
- **DMO**: Email Engagement / **Field**: Engagement Date Time → Engagement timestamp
- **DMO**: Email Engagement / **Field**: Flow Element Run → Contains the API name of the email element

**Important:**  
When selecting multiple DMOs from different data graphs in a decision element, they are treated as separate containers (similar to segments). As a result, strict filtering may not work as expected ([see details here](/p/d240bb357d3d)). That’s why, although I used different DMOs for segments earlier, in decision elements it is **best practice to use only Email Engagement**.

Once an open event occurs, the data graph is updated, and ideally, all three pieces of information should be present in a single engagement record, as shown below.

![]()

Now, let’s actually build the flow as follows and activate it. After sending an email, if only one person opens it, I wait until the defined waiting period elapses.

- **Engagement Channel Action = OPEN**
- **Engagement Date Time >= InterviewStartTime (Flow start time)**
- **Flow Element Run Contains Email Element API Name**

Note: The value in **Flow Element Run** is not exactly the email element’s API name. For example, it may look like: `10pHu0000008PQfIAM_0_2#OpenSegmentV5` In this case, **“OpenSegmentV5”** is the API name of the email element. Therefore, I use **“Contains”** for matching.

After the wait period ends, the contacts are split into the opened path and the unopened path, as shown below. Success!

![]()

## Conclusion

I confirmed that even in **Marketing Cloud Growth & Advanced Edition**, it’s possible to achieve functionalities similar to Marketing Cloud Engagement’s **“Measure”** and **“Engagement Split”.**

With the introduction of **V2 (Version 2)** for Data Lake Objects in Summer ’25, it’s likely that future versions such as V3 may also be released. Even if V3 appears, as long as you’re using the standard **Email Engagement** object, you shouldn’t encounter any issues. Therefore, it’s best to make use of the standard data model whenever possible.

That’s all for now.

Stay tuned for more Salesforce Marketing Cloud tips! 😊

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
