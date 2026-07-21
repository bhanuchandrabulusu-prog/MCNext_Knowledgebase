# SFMC Tips #252 : Marketing Cloud Next: “Path Experiment” Enhancements — Spring ‘26

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-next-path-experiment-enhancements-spring-26-424bc50ec961

---

# SFMC Tips #252 : Marketing Cloud Next: “Path Experiment” Enhancements — Spring ‘26

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--424bc50ec961---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--424bc50ec961---------------------------------------)

4 min read

·

Feb 19, 2026

--

Photo by [Vladislav Babienko](https://unsplash.com/@garri?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

In the [Spring ’26 new feature release](/@marketingcloudtips/marketing-cloud-next-spring-26-release-highlights-24c0c804b0cb) of Marketing Cloud Next, several important enhancements have been made to the **“Path Experiment”** in flows.

## What is Path Experiment?

Path Experiment is a feature that enables the following within a flow:

✅ A/B testing (automatic optimization of path selection)  
✅ Random branching that distributes paths based on a specified percentage

Because it can automatically verify and optimize which path produces the highest performance, it greatly contributes to improving the accuracy of marketing initiatives.

[## SFMC Tips #188 : Marketing Cloud Next: A/B Testing with the “Path Experiment” Element

### The “Path Experiment” element in Marketing Cloud Next Growth & Advanced Edition combines the capabilities of “Random…

medium.com](/@marketingcloudtips/marketing-cloud-next-a-b-testing-with-the-path-experiment-element-5e39af4e0210?source=post_page-----424bc50ec961---------------------------------------)

> *⚠* ***This feature is available only in Advanced Edition*** *※ Not available in Growth Edition.*

## Four New Features Added in Spring ’26

1. **Automatic notifications of Path Experiment results**
2. **Manual path selection during debug execution**
3. **Change tracking via the History tab**
4. **Enhanced Analytics tab (viewable within the canvas)**

Let’s look at each in order.

## ① Automatic Notification of Path Experiment Results

Users who activate a flow can now receive in-app automatic notifications when a Path Experiment is completed. (※ No additional configuration required)

![]()

The notification includes the following information:

- Winning path selection result
- Fallback processing status
- Result when no conclusion was reached

This allows you to stay informed of experiment results at all times without additional setup.

## ② Manual Path Selection During Debug Execution

When debugging a flow that includes a Path Experiment, you can now manually control the path assignment.

Previously, paths were forcibly assigned randomly, and the process would complete without any option to select.

Going forward, you can choose either to continue selecting randomly or to manually select the winning path.

By using manual selection, you can reliably test a specific path you want to validate, without depending on chance. This enables you to efficiently confirm whether intended branches and subsequent processes function correctly.

## ③ Change Tracking via the History Tab

With the newly added **History** tab in the Path Experiment panel, you can now understand what occurred during the Path Experiment.

You can review all changes made since activation, including:

- **Timestamp (date and time of change)**
- **User who made the change**
- **Whether it was an automated process or manual operation**

You can also track events such as:

- **Start of the Path Experiment**
- **Winning path selection**
- **Release of delayed groups**
- **Fallback processing**

The History tab is displayed when the Segment Triggered Flow progress status is “Activated”, “Canceled”, or “Error”. It is not displayed in “Draft”.

## ④ Enhanced Analytics Tab (Viewable Within the Canvas)

You can now monitor Path Experiment results without leaving the Flow Builder canvas.

![]()

In the “Analytics” tab of the Path Experiment panel, you can now view:

- **Total participants**
- **Evaluation metrics**
- **Confidence level in path comparison**

With this embedded summary, you can quickly grasp Path Experiment results **at a glance**, in a format consistent with analytics information available for other flow elements.

## Conclusion

With this update, Path Experiment has significantly evolved in terms of:

✅ Improved visibility (notifications and history)  
✅ Improved testing efficiency (manual debugging)  
✅ Improved analytical usability (in-canvas display)

That’s all for this time.

Stay tuned for more Salesforce Marketing Cloud tips! 😎

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
