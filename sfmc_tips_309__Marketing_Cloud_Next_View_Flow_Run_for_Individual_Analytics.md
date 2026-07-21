# SFMC Tips #309 : Marketing Cloud Next: View Flow Run for Individual Analytics

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-next-view-flow-run-for-individual-analytics-70ebedf158bb

---

# SFMC Tips #309 : Marketing Cloud Next: View Flow Run for Individual Analytics

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--70ebedf158bb---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--70ebedf158bb---------------------------------------)

4 min read

·

Jun 14, 2026

--

Photo by [Resource Database](https://unsplash.com/@resourcedatabase?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

The **View Flow Run for Individual** analytics feature, which was announced in the [Spring ’26 release notes](/@marketingcloudtips/marketing-cloud-next-spring-26-release-highlights-24c0c804b0cb) for Marketing Cloud Next Growth & Advanced Editions but was subsequently delayed, has finally become available with the Summer ’26 release.

If you have used Marketing Cloud Engagement, it may be easiest to think of this as equivalent to the **Contact Path** feature in the **Health** section.

With this feature, you can specify a particular audience member who currently exists within a flow and visualize which path that individual has passed through and which element they have currently progressed to.

## Supported Flows

Currently, this feature is available for the following flow types:

- Segment Flows
- Record Query Flows
- List Flows
- Campaign Flows
- Some Event-Triggered Flows
- Activation-Triggered Flows

## How to Use

The usage is very simple.

Click the **Analytics** button at the top of the flow canvas and select **View Flow Run for Individual**.

When the modal window appears, search for the individual whose execution status you want to review.

This feature uses data from the **Flow Run DMO** in the backend. Therefore, the information is not reflected immediately after a flow executes. Considering the ingestion time into Data Cloud, there is approximately a 10-minute delay.

If there are many individuals, you can also use the filter functionality to narrow down the results.

## Fields Displayed by Default

By default, the following information is displayed.

- **Flow Run ID**  
  The identifier for each Flow Run.
- **First Name and Last Name**  
  Displayed when available from the individual’s profile.
- **Data Source Object**  
  The data source, such as Contact or Lead.
- **Flow Status**  
  Displays the current execution status, such as Completed, In Progress, or Error.
- **Flow Execution Scheduled Time**  
  Displays the date and time when the flow started.  
  *If the same Individual has executed the same flow multiple times, identify the target execution by its start time.*
- **Flow Completion Time**  
  Displays the date and time when the flow completed.  
  *If the flow has not yet completed, this field remains blank.*

## Customizing Displayed Fields

The displayed fields can be freely customized.

By adding fields that exist in the Flow Run DMO, you can also display information such as error reasons and error descriptions.

*However, detailed error information is not always available. For example, even if* ***Internal\_Error*** *is displayed, the actual cause may not be retrievable, and the detailed contents may remain unknown.*

## Visualizing the Execution Path

When you select an individual, the path that the individual has passed through is highlighted in blue on the flow canvas.

This allows you to intuitively understand:

- Which branch the individual passed through
- Which element is currently processing the individual
- Where the flow has stopped due to an error

In addition, the side panel on the right side of the screen displays the execution history of each element in chronological order.

For each element, you can review the following information:

- Scheduled Time
- Completion Time
- Current Status
- Error Information (if available)

## Conclusion

The ability to visually confirm on the canvas which path an individual actually passed through can be considered a major advantage.

Incidentally, the **Contact Path** feature in Marketing Cloud Engagement also included functionality to forcibly remove the target contact from the journey.

On the other hand, the current version of **View Flow Run for Individual** does not appear to include such a forced exit capability yet.

Therefore, as needed, I recommend either using the custom implementation that I introduced previously or incorporating the **Exit from a Flow** element into your design to properly control exits.

[## SFMC Tips #247 : Marketing Cloud Next: How to Forcefully Exit Audiences from a Flow

### In Marketing Cloud Next Growth & Advanced Edition, you can use various flows such as Segment-Triggered Flows…

medium.com](/@marketingcloudtips/marketing-cloud-next-how-to-forcefully-exit-contacts-from-a-flow-bfb9bd74e071?source=post_page-----70ebedf158bb---------------------------------------)

[## SFMC Tips #297 : Marketing Cloud Next: How to Use the “Exit from a Flow” Element

### In the Summer ’26 new feature release of Marketing Cloud Next Growth & Advanced Editions, it is now possible to…

medium.com](/@marketingcloudtips/marketing-cloud-next-how-to-use-the-exit-from-a-flow-element-6398bef93977?source=post_page-----70ebedf158bb---------------------------------------)

That’s all for this time.

Stay tuned for more Salesforce Marketing Cloud tips! 😎

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
