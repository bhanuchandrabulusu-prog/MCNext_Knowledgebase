# SFMC Tips #151 : Marketing Cloud Next: Setup Steps for SDO (Demo)

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-next-basic-setup-procedure-for-the-demo-environment-be441f7c37d8

---

# SFMC Tips #151 : Marketing Cloud Next: Setup Steps for SDO (Demo)

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--be441f7c37d8---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--be441f7c37d8---------------------------------------)

10 min read

·

Jul 22, 2025

--

Photo by [Reuben Rohard](https://unsplash.com/@reubenrohard?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

Salesforce provides an environment called a **Simple Demo Org (SDO)** for users who belong to Salesforce partner companies for evaluation and demonstration purposes. An SDO can be requested on an individual basis through **Partner Learning Camp (PLC)**, making it relatively easy to get started.

By using an SDO, you can actually operate **Marketing Cloud Next** features while conducting functional validation, demonstrations, and even exploring use cases and learning the platform.

In this article, we will introduce how to obtain an **SDO and the basic setup procedures** required to use Marketing Cloud Next.

## A Free Development Environment Is Now Available for General Users

With the release of a new [Trailhead](https://trailhead.salesforce.com/content/learn/modules/marketing-cloud-next-email-sending-essentials) at the end of May 2026, a free development environment for Marketing Cloud Next has also been made available to general users.

Please refer to the following article.

[## SFMC Tips #301 : Marketing Cloud Next: A Free Developer Edition Available to Everyone

### As of May 2026, when it came to a free development environment for Marketing Cloud Next Growth & Advanced Editions, the…

medium.com](/@marketingcloudtips/marketing-cloud-next-a-free-developer-edition-available-to-everyone-9afcac83f318?source=post_page-----be441f7c37d8---------------------------------------)

## How to Extend an SDO

An SDO can be requested on an individual basis rather than a company basis, and there is no limit to the number of requests. The initial validity period is 30 days, but it can be extended for up to one year.

If, after gaining access, you feel that you are likely to continue using it, we recommend submitting an extension request as early as possible. Once the expiration date passes, it may become impossible to retrieve the organization information, making it difficult to reapply. We recommend noting down your Organization ID in advance.

### Extension Procedure

1. [Log in to Partner Community](https://partners.salesforce.com/pdx/s/) and launch **Ask Agentforce** from the bottom-right corner of the screen.
2. Click **Extend a Trial Org**.
3. Enter the **Organization ID** of the SDO you would like to extend. You can find the Organization ID under **Setup > Company Information**.

[## Salesforce Help

### Edit description

help.salesforce.com](https://help.salesforce.com/s/articleView?id=000387818&type=1&source=post_page-----be441f7c37d8---------------------------------------)

## Getting Started with Marketing Cloud Engagement+

Since March 2026, the Marketing Cloud Engagement demo environments provided to Salesforce partners have been automatically migrated to Marketing Cloud Engagement+.

Send customers from a Flow to a Journey using the Send to Journey action

While some functionality is already available, not all features are currently enabled. When performing testing and validation, it is recommended to assume that certain features may not yet be available.

[## SFMC Tips #210 : Marketing Cloud Next: Engagement+ Setup Guide

### As of November 2025, both new and existing Marketing Cloud Engagement customers can use Marketing Cloud Next by…

medium.com](/@marketingcloudtips/marketing-cloud-next-engagement-integration-setup-6fae8c535337?source=post_page-----be441f7c37d8---------------------------------------)

## Email Sending from Flows Is Available in SDO Orgs

Since March 2026, email sending has become available because the **Default From Address** under **Unified Messaging > Email > Settings** is enabled.

In environments where this setting is enabled, you can use sender addresses such as:

- Example: **[No Reply: no-reply@cdp2.mx.salesforce.com]**

as the From Address.

### Other Considerations

- Landing Pages and Forms are also available.
- SMS and WhatsApp are not available.

## **Setup Procedure**

### **How to Obtain an SDO**

1. Go to [**Partner Learning Camp (PLC)**](https://partnerlearningcamp.salesforce.com/s/learner-dashboard) and click on the **“Demo Org”** tab.

2. Next, select **SDO** as the **Demo Type**.

3. The **Username (Login ID)** will be filled in automatically. You can leave it as is — it’s typically helpful since it includes the creation date of the SDO, making it easy to tell when it was generated. Check the agreement box and click **Submit**.

4. After clicking **Submit**, you’ll receive around 20 to 30 emails within approximately 6 hours. Among them, the only important one is the **“Welcome to Salesforce: Verify your account”** email, usually sent as the 2nd or 3rd message. Be sure to save that email and feel free to delete the rest.

5. The contents of this email include the following:

- **Top section (Verify Account)**: Password reset link (you’ll need to complete this only the first time).
- **Middle section**: The URL to access your org (be sure to bookmark it).
- **Bottom section**: Your **Username (Login ID)** (make sure to save it).

![]()

6. You now have access to your Salesforce SDO. At this stage, **Marketing Cloud is not yet available**, so try navigating to **Sales Cloud** or another app from the App Launcher first.

### **Assigning Permission Sets**

1. From **Setup**, go to **Users**, and in the **View** dropdown, select **All Users**.

2. Click on **your own** **user name**.

3. Select **Permission Set Assignments**.

4. Click on **Edit Assignments**.

Add the following five permission sets:

- **Data Cloud Architect**
- **Marketing Cloud Admin**
- **Tableau Next Included App Business User**
- **View Unified Engagement History Dashboard (Spring ’26 onward)**
- **Send Distributed Marketing Messages (Spring ’26 onward)**

Once added, click **Save**.

### **Data Cloud Setup**

1. Let’s start by setting up **Data Cloud**. Click the gear icon in the upper-right corner and select **Data Cloud Setup**.

2. You’ll be taken to the setup screen. Scroll all the way to the bottom and click **Get Started**.

3. The initial setup of Data Cloud is very simple — just one click, and it will start configuring automatically. This process takes about **one hour**, so please wait patiently.

4. No confirmation email will be sent after setup is complete. After about one hour, return to this screen to verify the setup. You’ll see a screen like the one below, indicating completion.

### **Marketing Cloud Setup**

1. Next, go to the regular **Setup** page, search for **“Marketing Cloud”**, and click on **Basic Settings**.

2. In the SDO, you should see that **Marketing Cloud is already enabled**.

3. Scroll down and click **Update** to install the **Data Kit**.

4. The installation will begin and may take around **30 minutes** to complete.

5. Installation errors are quite common, so if an error occurs, please retry the installation several times.

\*If the error still persists, please check the following known issues.

### Known Issues and Workarounds for Marketing **Data Kit**

In SDOs or Sandbox environments, the following error may appear:  
**“A required package is missing. Package “Salesforce Standard Data Model”, Version x or later must be installed first.”**

This may prevent the Data Kit from being deployed. In such cases, please refer to the [help documentation](https://help.salesforce.com/s/articleView?id=002234049&type=1) below and install the latest version of the Salesforce Standard Data Model.

**Data Cloud: Resolve “Salesforce Data Model Version x.xx or later must be installed first” error.**

### **Identity Resolution (Creating Unified Individuals)**

1. Scroll down slightly and you’ll find the section for configuring **Identity Resolution**. Click the **“Generate Ruleset”** button.

2. The status will change to **“In Progress”.**

3. After about **5 minutes**, try refreshing the page. The status should now show as **“Success”.**

If you receive the error message:

> “We couldn’t generate a ruleset because your org is missing the required Party Identification DMO. Set up the Party Identification DMO and try again.”

you can avoid this error by creating it from the **New** button under the **Identity Resolution** tab in Data 360. When created from there, the error does not occur.

4. Open the **App Launcher** and search for **“Marketing”.** You will see two versions — select the one with the **white icon**, which corresponds to **Marketing Cloud Advanced Edition**.

5. This will take you to the **Marketing Cloud homepage**. From there, click on **Identity Resolution**.

6. The previously created **Ruleset** should appear. Click on **“Individual Identity Resolution”.**

7. A **warning message** may be displayed, but you can proceed with the identity resolution. Click **“Run Ruleset”.**

*Important:* After clicking, it may take around 10 seconds before any response is visible — **do not click multiple times.**

8. A green banner saying **“Your ruleset job is running.”** will appear.

9. After about **10 minutes**, refresh the page. Identity Resolution should be completed, and you’ll see the number of **Unified Individual IDs** that have been created.

*Note:* You can only run a **Ruleset up to 4 times within a 24-hour period**, so for any additional runs, follow the same manual execution steps as outlined above.

### **Registering Your Organization’s Physical Address**

1. Go to **Setup**, then navigate to **Channels > Email**, and click on **“Go to Company Information”.**

2. Click the **Edit** button.

3. Enter your company’s **physical address**. Since this is a demo organization, you can enter any placeholder information.

### **Enabling Einstein Features**

1. Still under **Channels > Email**, scroll all the way to the bottom of the page.

2. These are **optional setup**, but it’s recommended to enable each of the **Einstein features** for testing purposes.

### Reference: Common Pitfall When Viewing the SDO Landing Page

When clicking the public URL of a landing page, you may encounter an error saying “**URL No Longer Exists**”. This error is typically caused by **login IP address restrictions**. You can resolve this issue by following the steps below:

1. Go to **Settings > Digital Experiences > All Sites**, and click the **Builder** for **Marketing Landing Pages**.

![]()

2. From the left-hand menu, click the gear icon, then go to **General > Guest User Profile**, and click the link for **Marketing Landing Pages Profile**.

![]()

3. Select **System > Login IP Ranges**.

![]()

4. Delete the currently configured IP restrictions.

![]()

After completing these steps, the landing page should be viewable. Please give it a try.

## Conclusion

With that, you’ve completed all the essential steps required for the **basic setup**.

The following steps typically come next:

1. **Import consent records**
2. **Create segments**
3. **Create content**
4. **Build and run a flow**
5. **Analyze performance**

For details on each of these steps, please refer to the other basic articles I’ve previously written.

### 1. Import consent records

- [A Guide to Consent Management](/@marketingcloudtips/marketing-cloud-on-core-a-guide-to-consent-management-5ca95a1602a0)

### 2. Create segments

- [Content Creation and Components](/@marketingcloudtips/marketing-cloud-on-core-content-creation-and-components-bf9046db9978)
- [Understanding the “Preview and Test Send” Feature](/@marketingcloudtips/marketing-cloud-on-core-understanding-the-preview-and-test-send-feature-a91b0f6a1ecf)
- [How to Configure Data Graphs](/@marketingcloudtips/marketing-cloud-on-core-personalization-1af8d9aa9026)

### 3. Create content

- [Basics of Segment](/@marketingcloudtips/marketing-cloud-on-core-basics-of-segmentation-d240bb357d3d)

### 4. Build and run a flow

- [Introduction to Flow Builder Features](/@marketingcloudtips/marketing-cloud-on-core-introduction-to-flow-builder-features-fd65d9ea0b97)
- [Understanding the Basic Elements of Flow Builder](/@marketingcloudtips/marketing-cloud-on-core-understanding-the-basic-elements-of-flow-builder-1a749ecf92fa)
- [Einstein Send Time Optimization (STO)](/@marketingcloudtips/marketing-cloud-on-core-einstein-send-time-optimization-sto-3cd4c104b162)
- [Einstein Engagement Frequency & Engagement Scoring](/@marketingcloudtips/marketing-cloud-on-core-einstein-engagement-frequency-and-scoring-a8c75c105b47)

### 5. Analyze performance

- [Exploring Standard Reports and Dashboards](/@marketingcloudtips/marketing-cloud-on-core-exploring-standard-reports-and-dashboards-3fdd7ec3194c)
- [Transforming Campaign Insights with Marketing Performance](/@marketingcloudtips/marketing-cloud-on-core-transforming-campaign-insights-with-marketing-performance-7c3f91f77304)
- [How to Check Engagement Data](/@marketingcloudtips/marketing-cloud-on-core-how-to-check-engagement-data-5452bfbc1ae3)
- [How to Utilize Engagement Data](/@marketingcloudtips/marketing-cloud-on-core-how-to-utilize-engagement-data-a9b1f492b7d6)

### 6. Landing Page & Form

- [Creating a Signup Form](/@marketingcloudtips/marketing-cloud-on-core-creating-a-signup-form-dcb43bbe9fea)
- [Embedding Forms into External Sites](/@marketingcloudtips/marketing-cloud-on-core-embedding-forms-into-external-sites-fe21918045e2)
- [Tracking Landing Pages with a Consent Banner](/@marketingcloudtips/marketing-cloud-on-core-tracking-marketing-cloud-landing-pages-with-a-consent-banner-3672df5f9e73)
- [Tracking Landing Pages without a Consent Banner](/@marketingcloudtips/marketing-cloud-on-core-tracking-marketing-cloud-landing-pages-without-a-consent-banner-d23c0ba6da52)
- [Tracking External Websites with a Consent Banner](/@marketingcloudtips/marketing-cloud-on-core-tracking-external-websites-with-a-consent-banner-2492904a799c)
- [Tracking External Websites without a Consent Banner](/@marketingcloudtips/marketing-cloud-on-core-tracking-external-websites-without-a-consent-banner-467326874412)

### 7. Agentic Marketing

- [Agentforce Campaign Creation](/@marketingcloudtips/marketing-cloud-on-core-agentforce-campaign-creation-697c992adbe6)

### 8. Scoring

- [Understanding Default Scoring Rules](/@marketingcloudtips/marketing-cloud-on-core-understanding-default-scoring-rules-1f45d9c9333f)

### 9. CRM Record Page

- [A Practical Guide to Enhanced CRM Record Pages](/@marketingcloudtips/marketing-cloud-on-core-a-practical-guide-to-enhanced-crm-record-pages-34650d05475b)

That’s all for now!

Stay tuned for more Marketing Cloud Growth & Advanced Edition tips! 😊

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
