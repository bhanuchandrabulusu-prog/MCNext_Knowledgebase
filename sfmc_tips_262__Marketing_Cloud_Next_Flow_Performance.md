# SFMC Tips #262 : Marketing Cloud Next: Flow Performance

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-next-flow-performance-analytics-feature-8301c6431cb3

---

# SFMC Tips #262 : Marketing Cloud Next: Flow Performance

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--8301c6431cb3---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--8301c6431cb3---------------------------------------)

5 min read

·

Mar 2, 2026

--

Photo by [Clayton Cardinalli](https://unsplash.com/@clayton_cardinalli?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

As part of the [Spring ’26 new feature release](/@marketingcloudtips/marketing-cloud-next-spring-26-release-highlights-24c0c804b0cb) for Marketing Cloud Next Growth & Advanced Edition, the **Flow Performance analytics feature** has been added in addition to the existing **Marketing Performance analytics feature**.

> *Note: This feature may not yet be released depending on your organization. Please use this as reference information for now and verify the functionality after the actual release.*

### Roles of Each Feature

- **Marketing Performance**  
   → Performance analysis of campaigns and content
- **Flow Performance**  
   → Execution analysis at the flow element and flow version level

*\*The naming is separated based on the difference in analysis targets.*

This feature is available for both **Segment-Triggered Flows** and **Event-Triggered Flows**. The analytics display leverages **Tableau Next technology**, enabling deeper insights than before and supporting more data-driven decision-making.

### ⚠ Important Change

The previous “**View Report**” button that navigated to the traditional flow element-level report page has been discontinued. It has now been replaced with the “**Open Details**” button, which navigates to the Flow Performance analytics screen.

This appears to reflect Salesforce’s direction of moving away from traditional reports and standardizing on **Tableau Next-based analytics**.

### About Flow Version Analytics

*The image above shows a UI example of Flow Element Analytics.*

Flow Version Analytics appears to be not yet released at this time.  
In the future, a UI similar to the following is planned:

### What Will Be Possible with [Version Analytics](https://help.salesforce.com/s/articleView?id=platform.flow_monitor_version_analytics.htm&type=5)

It will enable tracking the exact path within a flow at the individual level, allowing detailed troubleshooting.

For example:

- **Which branch path was selected**
- **Which elements were completed**
- **Where errors or delays may have occurred**

Because issue analysis will be possible at the individual level, an early release is highly anticipated.

## Installing Flow Performance

1. To enable this feature, go to Setup and search directly for “Flow Performance”, or navigate from within the Marketing Performance settings screen.

> *Important: Marketing Performance must be installed in advance in order to successfully install Flow Performance.*

2. Assign the required **permission sets** to users.

To enable Flow Performance, both of the following permission sets are required:

- **Data Cloud Architect**
- **Marketing Cloud Admin**

To view the Flow Performance dashboard, the following permission set is required:

- **Tableau Next Included App Business User**

3. Next, navigate to the Flow Performance settings screen. After selecting the data space to associate with Flow Performance Analytics, click Install in the Data Cloud Integration installation section.

4. Select the source object type for Flow Performance. “Individual” is a required source object.

5. In the “**Install Analytics Workspace**” section, click “**Install**”.

6. Once installation is complete, you will automatically be redirected to the “Flow Performance Analytics” tab, where you can confirm that the installation was successful.

## Example of Flow Element Analytics

*Since Flow Version Analytics is not yet released, this section introduces an example of Flow Element Analytics.*

1. After Flow Performance installation is successful, navigate to the “**Analytics**” tab of an email element within a **completed-status flow**.

Under:

- **Element Metrics (current execution status)**
- **Email Engagement Metrics (delivery results status)**

The “**Open Details**” button becomes enabled for each.

2. Click “**Open Details**” under Element Metrics.

3. You will be taken to the “**Performance**” tab of the flow element record. Here, you can quickly check the status of this flow element at the **individual level**.

4. Next, click “**Open Details**” under Email Engagement Metrics.

5. Similarly, you will be taken to the “**Performance**” tab of the flow element record. You can again quickly check the results of this flow element at the **individual level**.

> *Tip: If “****\_w\_Email****” is appended to the end of the URL, the Email Engagement Metrics view is displayed.*

## Conclusion

In a previous article, I mentioned that a “**Unified Engagement History**” dashboard powered by Tableau Next technology was added to the CRM record page.

[## SFMC Tips #257 : Marketing Cloud Next: Unified Engagement History Dashboard

### Marketing Cloud Next Growth & Advanced Edition introduces a new feature in the Spring ’26 release: the Unified…

medium.com](/@marketingcloudtips/marketing-cloud-next-unified-engagement-history-dashboard-ee97fd1d217f?source=post_page-----8301c6431cb3---------------------------------------)

With the addition of Flow Performance:

- **Enhanced individual-level analysis**
- **Visualization of execution paths (planned)**
- **Advanced troubleshooting capabilities**

The direction is becoming clearer.

Going forward, the shift from report-centered analytics to Tableau Next-centered analytics is expected to accelerate.

### Recommendation for Reinstallation

For both Flow Performance and Marketing Performance, **it is recommended to uninstall and reinstall once for each of the three annual releases**.

- They are not automatically updated to the latest version.
- Reinstallation does not affect past marketing data.
- Reinstallation is also recommended in the official help documentation.

Be sure not to forget this step at the time of each new feature release.

That’s all for this time.

Stay tuned for more Salesforce Marketing Cloud tips! 😎

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
