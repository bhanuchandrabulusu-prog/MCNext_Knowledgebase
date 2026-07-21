# SFMC Tips #196 : Marketing Cloud Next: Testing with Sandbox

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-next-testing-with-sandbox-22f23d92eef0

---

# SFMC Tips #196 : Marketing Cloud Next: Testing with Sandbox

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--22f23d92eef0---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--22f23d92eef0---------------------------------------)

11 min read

·

Oct 20, 2025

--

Photo by [Eric Muhr](https://unsplash.com/@ericmuhr?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

With the [**Winter ’26 release**](/@marketingcloudtips/marketing-cloud-next-winter-26-release-highlights-81240775f843) of **Marketing Cloud Next Growth & Advanced Edition**, Salesforce introduced **Sandbox environments**, allowing users to safely explore Marketing Cloud Next features and content **without making any changes to the production environment**.

Marketing Cloud Next supports **all Sandbox types** — **Developer**, **Developer Pro**, **Partial Copy**, and **Full (Copy)**. However, the **available features and the scope of copied data** vary depending on the Sandbox type, so it’s important to understand these differences before using them.

As of the **initial release in Winter ’26 (October 2025)**, **most Marketing Cloud Next features (except Mobile App Messaging)** work in Sandbox environments.  
 However, whether a feature can be **copied from production to Sandbox** or **deployed from Sandbox to production** depends on the specific functionality.

The following section summarizes the **feature compatibility** and **deployment behavior** for each Sandbox type.

## **Feature Support Summary in Sandbox Environments**

## Campaign-Related

**Brief**

- ❌ Cannot be copied to Developer or Developer Pro Sandbox.
- ⭕ Can be copied to Partial Copy and Full Sandbox.
- ❌ Cannot be deployed to Production.

**Campaign**

- ❌ Cannot be copied to Developer or Developer Pro Sandbox.
- ⭕ Can be copied to Partial Copy and Full Sandbox.
- ❌ Cannot be deployed to Production.

## Communication Subscription-Related

- ❌ Cannot be copied to Developer or Developer Pro Sandbox.
- ⭕ Can be copied to Partial Copy and Full Sandbox.
- ❌ Cannot be deployed to Production.

## Content-Related

**CMS Marketing Workspace**

- ❌ Cannot be copied to Developer or Partial Copy Sandbox.
- ⭕ Can be copied only to Full Sandbox.
- ⭕ Can be deployed to Production.

**Brand Content**

- ❌ Cannot be copied to Developer or Partial Copy Sandbox.
- ⭕ Can be copied only to Full Sandbox.
- ⭕ Can be deployed to Production.

**Email Content / Template**

- ❌ Cannot be copied to Developer or Partial Copy Sandbox.
- ⭕ Can be copied only to Full Sandbox.
- ⭕ Can be deployed to Production.

**Form Content**

- ❌ Cannot be copied to Developer or Partial Copy Sandbox.
- ⭕ Can be copied only to Full Sandbox.
- ⭕ Can be deployed to Production.

**Expression Content**

- ❌ Cannot be copied to Developer or Partial Copy Sandbox.
- ⭕ Can be copied only to Full Sandbox.
- ❌ Cannot be deployed to Production. (*Exception within Content*)

**Tracked Link Content**

- ❌ Cannot be copied to Developer or Partial Copy Sandbox.
- ⭕ Can be copied only to Full Sandbox.
- ❌ Cannot be deployed to Production. (*Exception within Content*)

**Image Content**

- ❌ Cannot be copied to Developer or Partial Copy Sandbox.
- ⭕ Can be copied only to Full Sandbox.
- ⭕ Can be deployed to Production.

**Landing Page**

- ❌ Cannot be copied to Developer or Partial Copy Sandbox.
- ⭕ Can be copied only to Full Sandbox.
- ⭕ Can be deployed to Production.

**SMS Content / WhatsApp Content**

- ❌ Cannot be copied to Developer or Partial Copy Sandbox.
- ⭕ Can be copied only to Full Sandbox.
- ⭕ Can be deployed to Production.

**Mobile App Messaging Content**

- ❌ Currently not available in any Sandbox environment.

## Flow-Related

**Event-Triggered Flow**

- ⭕ Can be copied to all Sandbox types.
- ⭕ Can be deployed to Production.

**Segment-Triggered Flow**

- ⭕ Can be copied to all Sandbox types.
- ⭕ Can be deployed to Production.

## Summary

To summarize briefly:

- **Flows:** Can be copied and deployed across all Sandbox types.
- **Campaigns:** Can be copied to Partial Copy Sandboxes, but cannot be deployed to Production.
- **Content:** Can only be copied to Full Sandboxes and can be deployed to Production.  
   (*Expression Content and Tracked Link Content are exceptions.*)

These specifications may change in future releases, but for now, the above summary reflects the current behavior accurately.

## **How to Set Up a Sandbox**

In this article, I’ll explain how to create a **Developer Sandbox** and how to deploy using **Change Sets**.

1. Before you begin, please note that in the Developer Sandbox you are about to create, it’s necessary to **create a “Public Group”**.

Follow the steps below:

a. Log in to your **Production Org**.  
b. In **Setup**, search for **Public Groups**.  
c. Click **New** to create a new group and save it.

**Example:**

- Display Label: Sandbox Users
- Group Name (API Name): Sandbox\_Users

Add the users you want to grant access permissions to as members of the Public Group.

2. From **Setup**, search for **Sandbox**, then select **New Sandbox**.

3. Enter a **Sandbox name** within 10 characters and select the **Sandbox type** you want to create — **Developer**, **Developer Pro**, **Partial Copy**, or **Full**.

4. Select the **Public Group** you created earlier and click **Create**.

5. When the status changes to **Completed**, the Sandbox is ready for use.  
*Note:* The time required for completion depends on the Sandbox type and the size of your production environment.

6. Once the creation is complete, log in to your **Sandbox organization**.

7. Start by **enabling Data Cloud**.

8. Next, in **Marketing Cloud Setup**, if the **Salesforce CRM Connector** is disabled, click the button shown in the red box below.

9. From the left-hand menu, select **Salesforce CRM** and click **Activate**.

10. After enabling the connector, return to **Marketing Cloud Setup** and enable **Marketing Cloud**.  
From this point onward, the steps are almost the same as in the production environment, so they will be omitted here.

### Known Issues and Workarounds for Marketing Data Kit

In SDOs or Sandbox environments, the following error may appear:  
**“A required package is missing. Package “Salesforce Standard Data Model”, Version x or later must be installed first.”**

This may prevent the Data Kit from being deployed. In such cases, please refer to the [help documentation](https://help.salesforce.com/s/articleView?id=002234049&type=1) below and install the latest version of the Salesforce Standard Data Model.

Data Cloud: Resolve “Salesforce Data Model Version x.xx or later must be installed first” error.

11. Although **flows** are copied, **campaigns** themselves are **not included in the copy**.  
Therefore, in the copied flows, the campaign references that existed in the production org will be **blank**.

12. Existing **segments** are also copied; however, **CRM records** are not copied from the production org.  
As a result, immediately after Sandbox creation, all segments will display “0”.

In addition to segments, key **Data Cloud configurations and structures** such as **Identity Resolution**, **Data Graphs**, and **Calculated Insights** are copied to the Sandbox.  
However, **CRM person records** (such as Contacts or Leads) are not copied, so if you want to verify functionality, you need to create **sample records** and re-run the process.

Even when executing processes in the Sandbox, **credits are still consumed**.  
However, credit usage in a Sandbox org is **calculated at 20% less** than in a production environment. 💡

## **Deploying to Production Using Change Sets**

Content and flows created in a **Sandbox organization** can be deployed to the **production environment** using **Change Sets**.

*Note: There is currently a known issue where deployment of a small subset of Content and Flow components may fail. If you encounter this issue, the current workaround appears to be recreating the affected components from scratch. Please keep this in mind when deploying. Thanks to Zuzanna-san for sharing this information!* 🙏

<https://help.salesforce.com/s/issue?id=a02Ka00000mH4NjIAK>

Follow the steps below:

### ① Configure Deployment Connections (in Production Org)

First, set up a **deployment connection** between the production org and the Sandbox org.  
This configuration must be done **in the production org** (the receiving side).

1. In the **production org**, go to **Setup** and search for **Deployment Settings**.
2. A list of available connections will appear. Click **Edit** next to your Sandbox organization.

3. Enable **Allow Inbound Changes** and click **Save**.

4. The deployment connection from the Sandbox org to the production org is now complete.

### ② Create a Change Set (in Sandbox Org)

Next, create a **Change Set** in the Sandbox organization.

1. In **Setup**, search for **Outbound Change Sets**, and click it.
2. Click **New**.

3. Enter a name for the Change Set and click **Save**.

### ③ Add Components

Add the components you want to include in the Change Set.

1. Click **Add**.

2. Under **Component Type**, select **Flow Definition**.

3. Check the box for the target flow(s), then click **Add to Change Set**.

### ④ Add CMS Components

Once you’ve confirmed that the flow has been added, proceed to include **CMS-related components** such as forms, landing pages, and images.

1. Click **Add** again.

2. For **Component Type**, select **Digital Experience Bundle**.

3. Choose the workspace **marketing/Default\_Content\_Workspace**, then click **Add to Change Set**.

4. Next, click **View/Add Dependencies**.

5. Select all other components used within the flow, and click **Add to Change Set**.

### ⑤ Upload the Change Set

Once all components have been added, upload the Change Set to the production environment.

1. Click **Upload**.

2. Select the **target organization (production environment)**, then click **Upload** again.

> *⚠️ Once a Change Set is uploaded, it cannot be edited or recalled from the target org.*

3. The upload process will begin, and once completed, a **notification email** will be sent.

### ⑥ Deploy in the Production Organization

1. In the production org, go to **Setup** and search for **Inbound Change Sets**.
2. From the list of pending Change Sets, select the one received and click **Deploy**.

3. On the next screen, leave the setting as **Default** and click **Deploy**.

4. Deployment will start. Click the **Deployment Status** link to check the progress.

5. If all processes complete successfully, the deployment has been succeeded.

> *⚠️ Note: If you deploy the same flow again, the* ***API name from the Sandbox*** *will be carried over to the* ***production org****, causing duplication and resulting in an error. Please be cautious.*

### ⑦ Reconfiguring and Verifying Campaigns

Once deployment is complete, the flow created in the Sandbox will appear in the production org.  
However, since **Campaigns are not copied** via Change Sets, you’ll need to reconfigure them manually.

1. On the flow details page, the **Campaign field** will be blank. Click the **pencil icon** to edit it.

2. Select the appropriate **Campaign** and click **Save**.

3. Open the **Campaign Flow** screen to confirm that forms and landing pages have been properly deployed.

- Note: At this point, the flow will still be in **Draft** status.

4. Open the **Landing Page** to verify that images and other assets are correctly displayed.  
Once confirmed, the deployment is complete.

## **Conclusion**

In the example above, I explained that **Campaigns cannot be deployed using Change Sets**. Similarly, **Communication Subscriptions** are **not included in deployments** either.

Therefore, when running your flow in the production environment, you’ll need to **manually reconfigure the Communication Subscription settings** within the flow. Please keep this in mind to ensure everything functions properly.

Also, Salesforce MVP Zuzanna Jarczynska-san has shared some insights on this topic. Please take a look at the following.

[## Deploying Marketing Cloud Next from Sandbox to Production: What Actually Works Today

### If you're coming from the Salesforce platform, you're probably expecting a familiar deployment process. You build your…

sfmarketing.cloud](https://sfmarketing.cloud/2026/07/02/deploying-marketing-cloud-next-from-sandbox-to-production-what-actually-works-today/?source=post_page-----22f23d92eef0---------------------------------------)

Finally, here’s a summary of the **different Sandbox types**.  
The availability of each type depends on your **contract and edition**. For more details, please refer to the [official documentation](https://help.salesforce.com/s/articleView?id=platform.data_sandbox_environments.htm&type=5).

### ① Developer / Developer Pro

Only **configuration and metadata** (such as settings, flows, and object structures) are copied.  
Actual record data — for example, Leads, Accounts, or Data Extension contents — are **not copied**.

This is a **lightweight Sandbox** ideal for development and testing.  
 It can be **refreshed once per day**.

The only difference between **Developer** and **Developer Pro** is the **storage capacity**:

- Developer: 200 MB
- Developer Pro: 1 GB (5× larger)

### ② Partial Copy

In addition to metadata, **sample data** (a limited set of records based on a selected template) is copied.  
For example, it can include up to **5 GB of data**, allowing you to test with a subset of real data.  
A **Sandbox Template** must be created beforehand.

It can be **refreshed once every 5 days**.

### ③ Full (Copy)

This type copies **all production data and metadata in full**.  
It provides an environment that closely mirrors production, suitable for **validation, training, and UAT**.

It can be **refreshed once every 29 days**.

That’s all for this time.

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
