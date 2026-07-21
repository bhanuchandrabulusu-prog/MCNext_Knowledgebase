# SFMC Tips #154 : Marketing Cloud Next: Converting Prospects via Flow

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-next-converting-prospects-via-flow-7f95b7f6270c

---

# SFMC Tips #154 : Marketing Cloud Next: Converting Prospects via Flow

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--7f95b7f6270c---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--7f95b7f6270c---------------------------------------)

5 min read

·

Aug 5, 2025

--

Photo by [Bruno Guerrero](https://unsplash.com/@pray4bokeh?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

In **Marketing Cloud Next** (Marketing Cloud Growth & Advanced Edition), you can convert prospects into leads or contacts either manually or by using trigger flows.

> ***Tip:*** *With the new Summer ’25 release, it is now possible to convert prospects directly into* ***Contacts****.*

## How to Convert Prospects

1. Manually convert a prospect into a Lead
2. Manually convert a prospect into a Contact
3. Convert prospects into Leads or Contacts using Trigger Flows

The manual conversion methods have already been explained in a previous article, so please refer to that. In this article, I will focus on how to perform conversions using Trigger Flows.

[## SFMC Tips #153 : Marketing Cloud Next: Leveraging Prospects

### In Marketing Cloud Next (Marketing Cloud Growth & Advanced Edition), marketers can leverage “prospects” to ensure that…

medium.com](/@marketingcloudtips/marketing-cloud-next-leveraging-prospects-8aa701aea983?source=post_page-----7f95b7f6270c---------------------------------------)

## Converting Prospects to Leads or Contacts Using Data Cloud Trigger Flow

In this example, I will convert prospects who meet specific conditions in the **Marketing Engagement Score** (a Calculated Insight Object in Data Cloud) into Leads or Contacts using a Data Cloud Trigger Flow.

### Configuration Steps

1. Create a **New Flow** and select **Data Cloud-Trigger Flow**.

2. In the **Start** element settings, select **Marketing Engagement Score** from the object dropdown.

3. For the trigger condition, choose **A record is created or updated**. In the condition requirements dropdown, select **All Conditions Are Met (AND)** and set the following condition:

- **Engagement\_Score\_\_c** is greater than or equal to **50**.

4. Next, add a **Get Records** element to retrieve data from the Data Cloud object **Unified Link Individual**.

5. For the condition, on the left side select **Unified Individual ID** from the **Unified Link Individual** object, and on the right side select **Triggering …**.

6. Continue by selecting **Unified\_Individual** from **Triggering …** and leave other settings as default.

7. Add another **Get Records** element to retrieve records from the Salesforce **Prospect** object.

8. On the left, choose **Prospect ID**, and on the right, select the **Unified Link Individual from Get …** resource from the **Get Records** action.

9. On the right side, select **Individual Id**. Leave other settings as default.

10. Next, add a **Decision** element to determine whether the contact in the flow is a **Prospect**, and create a branch accordingly. For the first condition, select **Unified Link Individual from Get …** from the **Get Records** resource on the left.

11. Choose **Data Source Object**. (Be careful not to select **Data Source**.)

12. On the right side, input **Prospect**.

13. For the second condition, select **Prospect from Get …** from the **Get Records** resource.

14. On the left, select **Prospect Status** from the picklist.

15. Change the operator to **Does Not Equal**, and on the right side, select **Converted**.

16. Finally, on the **Prospect** path, add an **Action** element. From the list, select the **Convert Prospect** action.

17. Set the **Label** and **API Name** for the action. For **Prospect ID**, select **Prospect from Get …** from the **Get Records** resource.

![]()

18. For the field, select **Prospect Id**.

![]()

19. In **Converted Status**, enter **Converted**.

20. Choose whether to update an existing Lead or create a new Lead upon conversion.

- If you want to create a **new Lead**, toggle ON the option. The input field that appears afterward can be left blank.
- If you want to convert to an **existing Lead**, only empty fields in the existing Lead will be updated with values from the Prospect.

21. Finally, save the flow and click **Activate** to complete.

## Conclusion

In this article, I introduced an example using a **Data Cloud-Trigger Flow**, but it’s also possible to perform lead conversion using a **Record-Triggered Flow** when the Prospect Status is updated to **“Qualified”**.

Additionally, by leveraging a **Form Trigger Flow**, you can check whether a Prospect record already exists during a signup form campaign. This helps prevent unnecessary creation of duplicate Leads by converting existing Prospects into Leads in a controlled manner.

By choosing the appropriate **Flow Trigger Type** based on the situation, you can build more flexible automations. Be sure to actively explore and make the most out of Flows in your processes!

That’s all for now.

Stay tuned for more Marketing Cloud Growth & Advanced Edition tips! 😊

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
