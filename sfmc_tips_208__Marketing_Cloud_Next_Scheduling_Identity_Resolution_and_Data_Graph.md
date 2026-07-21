# SFMC Tips #208 : Marketing Cloud Next: Scheduling Identity Resolution and Data Graph

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-next-scheduling-identity-resolution-and-data-graph-a63aecf1904a

---

# SFMC Tips #208 : Marketing Cloud Next: Scheduling Identity Resolution and Data Graph

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--a63aecf1904a---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--a63aecf1904a---------------------------------------)

8 min read

·

Nov 29, 2025

--

Photo by [YUNAN WANG](https://unsplash.com/@eysmanpics?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

In Marketing Cloud Next Growth & Advanced Edition, **Identity Resolution** and **Data Graph** cannot be executed on a schedule with the standard functionality.  
Therefore, if you want to run them at any desired time, it is necessary to configure a “**Schedule-Triggered Flow**” to launch the flow.

Here, I clearly explain the procedure for scheduling Identity Resolution and Data Graph.

## Scheduled Execution of Identity Resolution

**Preparation:** Since Identity Resolution will be executed on a schedule via a flow, first disable the **Auto-Run** setting of Identity Resolution.

1. Open the schedule-triggered flow and configure the **Start Date/Time** and **Frequency**. In this example, it will run once per day at **7:00 AM**.

2. Next, add an **Action** element in the flow, search for “**Identity Resolution**” in the search box, and select the **“CDP Run Identity Resolution”** action.

3. After setting the action label and API name, enter the **Salesforce ID (18 digits)** **of the Identity Resolution**.

> *You can obtain the Salesforce ID from the URL of the Identity Resolution detail page.*

![]()

4. This completes the configuration.  
If you want to schedule only Identity Resolution, activate the flow as is.

![]()

***Tip:*** *By using the* ***Publish Calculated Insight (cdpPublishCalculatedInsight)*** *action, you can also schedule publishing for calculated insights in the same way. Note that for calculated insights, you should enter the* ***API Reference Name****, not the* ***Calculated Insight ID****.*

*If you need to place two or more calculated insights consecutively in a path,* ***make sure to add a 1-minute wait between them. If you do not configure this, an error will occur****.*

## Scheduled Execution of Data Graph

Next is the schedule configuration for **Data Graph**.

**Preparation:** Since this will also be executed on a schedule via a flow going forward, change the existing Data Graph schedule to the maximum value, **“Monthly”.**

1. Since no standard action is provided for executing a Data Graph, you must develop a process that calls the API to execute it.

First, refer to the following article to obtain the **Consumer Key** and **Consumer Secret**.

[## SFMC Tips #181 : Marketing Cloud Next: Obtaining an Access Token for the REST API

### Previously, I wrote an article on how to obtain an access token when using the REST API in Marketing Cloud Engagement.

medium.com](/@marketingcloudtips/marketing-cloud-next-obtaining-an-access-token-for-the-rest-api-156eca392584?source=post_page-----a63aecf1904a---------------------------------------)

2. Once you have obtained the **Consumer Key** and **Consumer Secret**, search for **Named Credentials** from Setup, and select the **External Credentials** tab.

3. Click **New**.

4. Decide the **Label** and **Name**, and set the **Authentication Protocol** to **OAuth 2.0**.

5. Next, in **Authentication Flow Type**, select “**Client Credentials with Client Credentials Flow”**.

6. Check ”**Pass client credentials in request body**”, and enter the following in **Identity Provider URL**, then save:

> *https://[My Domain Name].my.salesforce.com/services/oauth2/token*

7. Next, in the **Principals** section below, click **New**.

8. Choose any Parameter Name, and enter the previously obtained **Consumer Key** and **Consumer Secret**, then save.

9. Then, from the left menu, click **Named Credentials** again, and create a new item on the **Named Credentials** tab.

10. Decide the **Label** and **Name**, and enter the following in the **URL**. The trailing “/” is not required.

> *https://[My Domain Name].my.salesforce.com*

11. Select the previously created **External Credential**, check **Generate Authorization Header**, ensure that **Outbound Network Connection** remains set to **— None —** , and save.

12. Next, search for **Permission Sets** in Setup, and create a new permission set.

13. Enter the Label and API Name of the permission set, and save.

14. In the created permission set, click **External Credential Principal Access**.

15. Enable the previously created **External Credential Principal**, then save.

16. Still within the same permission set, open **Object Settings**.

17. Search for **User**, and select **User External Credentials**.

18. Check the bottom two items (**Modify All Records, View All Fields**). The screen will look like the example below. Then save.

19. Next, return to the **External Client App Manager**, and open the created **External Client Application**.

20. Click **OAuth Policies**, and confirm the **Username** for **Enable Client Credentials Flow**.

21. After confirming, return to the permission set and click **Manage Assignments**.

22. Click **Add Assignments**.

23. Select the user you confirmed earlier, and click **Next**.

*Tip: To keep the steps in this article simple, the instructions use a System Administrator user. However, for production environments, consider using an Integration User (with a Salesforce Integration User license) from a security and operational best practices perspective.*

24. Click the **Assign** button.

25. After completing all of the above, return to the flow, select **Action**, and click **Create HTTP Callout** at the bottom.

26. Decide the Name, select the previously created **Named Credential**, and proceed to the next step.

27. Again, set a Label, and select **POST** for the method.

28. Enter the following in the **URL Path**.  
※ Replace the Data Graph API name with your own.

```
/services/data/v65.0/ssot/data-graphs/[Data Graph API name]/actions/refresh
```

29. This endpoint can be executed **without a request body**. Do not enter a sample JSON request — proceed as is.

30. Next, select **Use Example Response**, and continue.

31. In the **Sample JSON Response**, enter the following, click **Review**, and then save.

```
{  
  "errors": [  
    {  
      "errorCode": "",  
      "message": ""  
    }  
  ],  
  "success": true  
}
```

32. Finally, enter the **Action Label** and **API Name**, and save.

33. Enter the **Flow Label** and **Flow API Name**, and save.

34. You can test it by running **Debug**.

35. Click **Run**.

36. If it completes without errors, the implementation is successful!!

> ***Important Notes****If no data changes have occurred in the Data Model Objects since the previous Identity Resolution run:  
>  → The Data Graph will be treated as* ***Skipped = Error****.  
>  → Make some data change before running Debug.*

- Identity Resolution is confirmed to be running.

- The Data Graph has also started.

37. Finally, place a **Wait** element. In this example, I simply wait for 1 hour.

38. As noted earlier, when there are no data changes, the Data Graph run will be skipped (treated as an error). Therefore, it is important to configure a **Fault Path** so that the flow does not stop.

39. After that, place a **1-minute Wait** on the fault path.

> *If you don’t add this wait, the subsequent Data Graph action will also be skipped.*

40. Next, because we want to return to the Data Graph action, click **Add Element (+)** and select “**Connect to element**”.

41. Connect to the **Data Graph Action**.

42. This completes the configuration! Save and activate.

## Conclusion

Identity Resolution has a limit of **up to 4 runs per 24 hours**.  
Therefore, if you have already run it manually 4 times, Identity Resolution will not run at the scheduled execution time and will be treated as an error.  
Note: Debug runs also count as 1 execution.

Additionally, by using the **Named Credentials** created this time, you can run various APIs from flows.  
Not only Data Graph — feel free to automate other APIs as well.

That’s all for now.

Stay tuned for more Salesforce Marketing Cloud tips! 😎

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
