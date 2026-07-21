# SFMC Tips #278 : Data Cloud: On-Demand Publish Feature for Batch DMO Activation

**Source:** https://medium.com/@marketingcloudtips/data-cloud-on-demand-publish-feature-for-batch-dmo-activation-8c44ac69cf48

---

# SFMC Tips #278 : Data Cloud: On-Demand Publish Feature for Batch DMO Activation

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--8c44ac69cf48---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--8c44ac69cf48---------------------------------------)

5 min read

·

Apr 17, 2026

--

Photo by [Slav Romanov](https://unsplash.com/@slavromanov?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

In a previous article, I introduced “**Batch DMO Activation**” as a feature that allows you to send (publish) an entire DMO to external destinations such as **Marketing Cloud Engagement** or **cloud storage**. However, this feature was limited to manual publishing and had to be executed through the UI.

[## SFMC Tips #205 : Data Cloud: Batch DMO Activation Has Arrived

### With the October 2025 Data Cloud release, the long-awaited Batch DMO Activation feature has finally been introduced.

medium.com](/@marketingcloudtips/data-cloud-batch-dmo-activation-has-arrived-0b44883c57e9?source=post_page-----8c44ac69cf48---------------------------------------)

With the April 2026 release, an **on-demand capability** — meaning the ability to automatically send (publish) at any timing — has finally become available.

I had expected this to be provided through scheduling options on the UI, but in reality, it has been delivered as an on-demand execution using the **Data 360 Connect REST API**.

That said, by incorporating this API as a custom action, it is also possible to execute it from a **schedule-triggered flow**. As a result, automatic sending at any timing can be achieved.

In this article, I will explain the specific implementation steps.

## Enabling the DMO to Send

In this example, all records of **Goods Product (product data)**, which belongs to the “Other” category, will be sent to a data extension in Marketing Cloud Engagement.

When creating the activation, select **“Batch”** for the **Data Model Object**. There is also a confusing option called “API Activation”, but that is not used in this case.

As you proceed with the setup, you can freely add the fields you want to send to Marketing Cloud Engagement. Additionally, if there are related **Calculated Insights**, those can also be included in the send.

![]()

Previously, this activation had to be manually published from the UI, but this time the process will be executed via API.

While the activation settings screen is open, check the URL to obtain the Salesforce ID that starts with **“85R”**. This ID will be used in the subsequent API execution, so be sure to note it down.

Example: `85RTK0000000Jyj2AE`

## REST API Details

Next, here are the resource details:

```
--- Method  
  
POST  
  
  
--- Endpoint  
  
https://{dne_cdpInstanceUrl}/services/data/v{version}/ssot/activations/{activationId}/actions/publish  
  
  
--- Headers  
  
Content-Type: application/json  
Authorization: Bearer [access token]  
  
  
--- Body Sample  
  
{  
  "fullRefresh": true  
}  
  
  
--- Response Sample  
  
{  
  "errors": [  
    {}  
  ],  
  "success": true,  
  "publishStatus": "Publishing"  
}
```

**\*The behavior of** `"fullRefresh"` **varies depending on the DMO configuration.**

**For Full Refresh DMOs:**

- A full refresh is always performed, regardless of this value.

**For Incremental DMOs:**

- **Initial publish (Day 0):**  
  A full refresh is always performed, regardless of this value.
- **Subsequent publishes:**  
  If false or omitted, incremental update is executed by default.  
  If set to true, a full refresh is forcibly executed.

## Setup Steps

The detailed setup procedure follows the same general flow as the previously introduced article on “**Scheduling Identity Resolution and Data Graph**”. If you have not reviewed it yet, it is recommended to check that first.

[## SFMC Tips #208 : Marketing Cloud Next: Scheduling Identity Resolution and Data Graph

### In Marketing Cloud Next Growth & Advanced Edition, Identity Resolution and Data Graph cannot be executed on a schedule…

medium.com](/@marketingcloudtips/marketing-cloud-next-scheduling-identity-resolution-and-data-graph-a63aecf1904a?source=post_page-----8c44ac69cf48---------------------------------------)

In this article, I will focus on the changes from **Step 28 onward**.

**28.** Enter the following in the URL path.

- *Replace “****activationId****” with your own value.*
- *This API works with* ***Version 66.0 or later****.*

```
/services/data/v66.0/ssot/activations/{activationId}/actions/publish
```

**29.** Enter the following in the request body, click Review, and then save.

```
{  
  "fullRefresh": true  
}
```

**30.** Select **“Use Example Response”** and proceed.

**31.** Enter the following in the sample JSON response, click Review, and save.

```
{  
  "errors": [  
    {}  
  ],  
  "success": true,  
  "publishStatus": "Publishing"  
}
```

**32.** Return to the flow and enter the **Label** and **API Name** for the action element, then save.

**33.** At this point, enter and save the **Flow Label** and **Flow API Name**.

**34.** Next, create a “**Variable**” resource with the following settings:

- **Resource Type: Variable**
- **API Name: reqBody**
- **Data Type: Apex-Defined**
- **Apex Class: ExternalService\_\_BacthDMOActivation\_Bacthx20DMOx20Activation\_IN\_body**

**35.** Place an **Assignment** element before the action element and configure as follows:

- **Variable: reqBody > fullRefresh**
- **Operator: =**
- **Value: True**

*\*This example assumes a Full Refresh DMO process.*

**36.** Return to the action element and set the previously created variable `reqBody` in **Set Request Body**.

**37.** The configuration is now complete. Save again.

**38.** Execute from **Debug** and click **Run**.

**39.** If it completes without errors, the implementation is successful!!

**40.** Enable the **Schedule-Triggered Flow** and configure it to send (publish) at any desired timing.

**41.** Finally, verify the actual data and confirm that the records are correctly reflected.

## Conclusion

Until now, many of you may have implemented similar processes using Script Activities on the Marketing Cloud Engagement side. As shown in this article, by leveraging standard Data 360 functionality, it is now possible to retrieve and send data more simply.

If you are not aware of this approach, you may continue relying on traditional methods. I encourage you to try it at least once and use it when needed.

That’s all for this time.

Stay tuned for more Salesforce Marketing Cloud tips! 😎

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
