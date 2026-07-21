# SFMC Tips #287 : Marketing Cloud Next: Behavior of Exit Rules

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-next-behavior-of-exit-criteria-7f55f708ecea

---

# SFMC Tips #287 : Marketing Cloud Next: Behavior of Exit Rules

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--7f55f708ecea---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--7f55f708ecea---------------------------------------)

5 min read

·

May 2, 2026

--

Photo by [tabitha turner](https://unsplash.com/@tabithaturnervisuals?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

In this article, I summarize the behavior of **Exit Rules** in Marketing Cloud Next Growth & Advanced Edition.

## Exit Rule Basics

- You can define exit conditions based on Global Attributes, Data 360 Data Graph attributes, Related Attributes, or Calculated Insights.
- Starting with Summer ’26, Exit Rules can also be configured based on events.

![]()

## Behavior #1: Exit Rules are evaluated at the Entry Source

First, an important point:

**Exit Rules are evaluated even at the Entry Source (the moment of entry)**.

In other words:

- If the conditions are met at the moment a contact enters the flow  
  → they are excluded at that point

## Behavior #2: However, it doesn’t appear that way in Debug

This is the most confusing part.

**In Debug mode, it does not appear as though the contact exits at the Entry Source**.

When you test it:

- The flow appears to pass through the Email element,
- then proceeds to the Wait element,
- and is excluded at the Wait element.

Because of this, it’s easy to misunderstand and think:  
“Are Exit Rules not working at the Entry Source?”

## Behavior #3: Exit is evaluated after Wait (← the most fundamental behavior)

- Exit Rules are evaluated when the Wait ends.
- At that point, the contact is excluded.

## Behavior #4: However, the status does not become “Stopped”

This is another key point.

At this time, the status is:

- ❌ Not “Paused” or “Stopped”
- ✅ It remains “Waiting”  
  ※ The wait will never be released afterward.

## Additional Information #1

In the [Summer ’26 release](/@marketingcloudtips/marketing-cloud-next-summer-26-release-highlights-04f6c5abdee6) introduced support for the following aggregation functions on numeric values from Related Attributes retrieved through Data Graphs and other related data sources:

- **Average**
- **Sum**
- **Max**
- **Min**

Previously, the only available option was to evaluate conditions based on the number of related records, such as **“Count >= 1”**.

In addition, date-based conditions have been significantly enhanced. Twenty new operators are now available for Date fields, including options such as “Is Anniversary of Today”, “Is Today”, and “Last Number of Days”.

New Date Operators:

- Is Anniversary of Today
- Is Not Anniversary of Today
- Is Today
- Is Tomorrow
- Is Yesterday
- Is This Month
- Is Next Month
- Is Last Month
- This Year
- Next Year
- Last Year
- Is On
- Is Before
- Is After
- Greater Than Last Number of Days
- Last Number of Days
- Next Number of Days
- Last Number of Months
- Next Number of Months
- Last Number of Years

*Note: Datetime fields continue to support the same eight operators that were previously available.*

*Previously, it was difficult to create flexible conditions based on numeric or date values stored in related attributes. As a result, implementing complex decision logic often required additional data preparation or segment creation beforehand.*

*With these enhancements, it is now possible to directly evaluate conditions within a flow, such as:*

- *Customers whose* ***average purchase amount is greater than or equal to $100 and who have not made a purchase in the last 14 days***
- *Customers whose* ***last purchase date falls on the same anniversary date as today***

*This enables more sophisticated and precise audience targeting than ever before.*

## Additional Information #2

The [Summer ’26 release](/@marketingcloudtips/marketing-cloud-next-summer-26-release-highlights-04f6c5abdee6) also introduces a significant enhancement to Exit Rules.

Previously, audiences could only exit a flow based on conditions derived from Data Graphs or Calculated Insights. With this enhancement, **standard events and custom events can now be used as exit criteria**.

![]()

For example, you can now configure exit conditions such as:

- Exit the flow when a customer **opens a specific email** (standard event)
- Exit the flow when an **engagement signal is received** (custom event)

This allows audiences to leave a flow based on customer actions and real-time events, making it possible to create more responsive and context-aware customer journeys.

How was it?

This behavior is generally as expected, but we hope this helps clarify some previously confusing points and resolves any lingering uncertainty.

At this time, there does not appear to be a report that clearly confirms that a contact exited a flow due to Exit Rules.  
**There is also no report for the Entry Source, and in the Flow Element Run report, the status is only shown as “Waiting.”** For your reference.

In addition, the Spring ’26 new feature release introduced the ability to exit individuals from flows using the Exit Individuals API.

[## SFMC Tips #247 : Marketing Cloud Next: How to Forcefully Exit Contacts from a Flow

### In Marketing Cloud Next Growth & Advanced Edition, you can use various flows such as Segment-Triggered Flows…

medium.com](/@marketingcloudtips/marketing-cloud-next-how-to-forcefully-exit-contacts-from-a-flow-bfb9bd74e071?source=post_page-----7f55f708ecea---------------------------------------)

Furthermore, the Summer ’26 new feature release also introduced the ability to exit individuals from flows using the Exit from a Flow element.

[## SFMC Tips #297 : Marketing Cloud Next: How to Use the “Exit from a Flow” Element

### In the Summer ’26 new feature release of Marketing Cloud Next Growth & Advanced Editions, it is now possible to…

medium.com](/@marketingcloudtips/marketing-cloud-next-how-to-use-the-exit-from-a-flow-element-6398bef93977?source=post_page-----7f55f708ecea---------------------------------------)

That’s all for this time.

Stay tuned for more Salesforce Marketing Cloud tips! 😎

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
