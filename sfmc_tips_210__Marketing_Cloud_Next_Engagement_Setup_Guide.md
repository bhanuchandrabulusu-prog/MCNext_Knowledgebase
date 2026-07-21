# SFMC Tips #210 : Marketing Cloud Next: Engagement+ Setup Guide

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-next-engagement-integration-setup-6fae8c535337

---

# SFMC Tips #210 : Marketing Cloud Next: Engagement+ Setup Guide

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--6fae8c535337---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--6fae8c535337---------------------------------------)

8 min read

·

Dec 4, 2025

--

Photo by [Richard Brutyo](https://unsplash.com/@richardbrutyo?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

As of November 2025, both new and existing Marketing Cloud Engagement customers can use Marketing Cloud Next by purchasing the “**+ (Plus)**” license. In this article, I will clearly explain the steps for connecting Marketing Cloud Engagement with Marketing Cloud Next.

“**Using Marketing Cloud Next**” here refers to having access to the following tools:

- **Data Cloud**
- **Agentforce (Marketing-related)**
- **Salesforce CRM (Enterprise Edition or higher)**
- **Marketing Cloud Growth or Advanced Edition**

> *Note: Even in environments where Salesforce CRM is not used, the “****System Administrator****” permission in Salesforce CRM is required to perform the Marketing Cloud setup.*

## Access and Permission Setup

1. Once you have access to Marketing Cloud Engagement, create a connection user, such as an “**API User**”, and assign the following roles. This API user will be used when connecting with Data Cloud.

- **Administrator**
- **Marketing Cloud Administrator**

Note:

- The connecting user must be **enabled as an API user**.
- The Marketing Cloud Administrator role includes the permissions required to access Marketing Cloud Next.
- If you are using the Corporate Edition, you may create up to 45 users. Use one of them as the API user.

2. Next, log in to Marketing Cloud Engagement using the “API User” that you created above. Open the menu from your name in the upper-right corner, and you will see “**Marketing Cloud Next Setup**”. Click it.

3. Log in to Salesforce CRM using a “**System Administrator**” user.

![]()

4. You will then be redirected to the Marketing Cloud Next “**Assistant Home**” screen.

5. After logging in, assign the following **permission sets** to the System Administrator user:

- **Data Cloud Architect**
- **Marketing Cloud Administrator**
- **Tableau Next Included App Business User**

6. Open “Permission Sets” from Setup and assign the permission sets to the user. You may keep any permission sets the user already has.

## Marketing Cloud Next Setup

1. Configure Marketing Cloud Next Growth & Advanced Edition by navigating to Setup → Marketing Cloud → Basic Settings.

> *Tips: You may begin from the Marketing Cloud Engagement integration, but* ***installation of the Marketing Data Kit is a prerequisite for installing Marketing Performance****, so begin there first.*

2. If “Add Data Protection Details to Records” has not been enabled in your environment, go to the settings page (**Data Protection and Privacy**), click Edit, enable the checkbox, and save.

3. Return to Basic Settings and select the Data Space. If you have not purchased additional Data Spaces, select “**Default**”.  
If you cannot select a Data Space here, the permission sets mentioned earlier have not been assigned.

4. When the Data Space is selected, the installation of the Marketing Cloud Next Growth & Advanced Edition application will automatically begin (about 2 minutes).

5. Once completed, you will be able to install the Marketing Data Kit. Click Install. (about 15 minutes)

6. After the installation is complete, set up Identity Resolution for the Unified Individual. Click “Generate Ruleset” and complete the setup.

> *\* If Identity Resolution cannot be executed from this screen,* ***configure it******manually from the Data Cloud Identity Resolution screen****. The manual setup steps are below.*

### Manual Identity Resolution Setup

1. Click the following link (**manually create one**).

2. On the Identity Resolution screen, click “New”.

3. Click “Create New Ruleset” and proceed.

4. In Primary Data Model Object, select “**Individual**”, and set the Ruleset ID to a four-digit value. If you only plan to create one Identity Resolution, leaving it **“blank” is recommended**.

5. For the Ruleset Name, choose something clear such as “**Individual Identity Resolution**”, **stop automation**, and save.

> *Note: Configure “Match Rules” according to your environment.*

This completes the basic setup on the Marketing Cloud Next side!!

## Integration Setup with Marketing Cloud Engagement

1. In Salesforce CRM Setup, go to Marketing Cloud → “**Marketing Cloud Engagement**” and continue following the instructions on this screen.

2. Click “**Go to Data Cloud Setup**” to begin connecting Marketing Cloud Engagement and Marketing Cloud Next.

3. On the connection screen, click New.

4. Enter a connection name and save.

5. Click Manage.

6. You will be redirected to the Marketing Cloud Engagement login screen. Log in using the “API User” created earlier.

![]()

7. After logging in, you will be redirected back to the connection screen, where you can confirm that the connection has been completed.

### Note

If an **internal error message appears when connecting Marketing Cloud Engagement**, please check the following three points:

- Clear your **browser cache and cookies**, then reload the page.
- Ensure that the **MCE integration user** has both the **Administrator** and **Marketing Cloud Administrator** roles assigned.
- In the **Business Unit Management** settings for the MCE integration user, make sure that the **enterprise-level Business Unit is set as the default**.

8. Next, since you will later need to install the data bundle, click Manage in section ② (Data Source Setup).

9. The next screen is only an introduction to the bundles. Click “Start”. Installation is not performed here.

10. Select which Business Unit to use as the data source. Even if you only have one Business Unit, **this configuration is required; otherwise, the data bundle cannot be used**.

11. Select the “Business Unit” and save.

12. In section ④ (Activation Target), click “Manage”.

13. Select the “Business Unit” and save.

14. Connection setup is now complete!

## Data Bundle Installation

1. Access Data Cloud, open “**Data Streams**”, and click New.

2. Because the Data Source configuration has been completed, “**Marketing Cloud (Engagement)**” will now be available as a selectable Data Source. Select it.

3. Connect the Business Unit and Data Space.

4. Select a Data Bundle. Because multiple bundles cannot be selected simultaneously, begin with the **Email Studio data bundle**. Install other bundles as needed depending on your Marketing Cloud Engagement channels.

5. Scroll down and select “[**Journey Activity Run**](/@marketingcloudtips/data-cloud-journey-activity-run-added-to-starter-data-bundle-bbbe73434dd0)” (new in Winter ’26), then click Next.

6. Proceed to the next screen without changes.

7. Release the Data Bundle (about 5 minutes).

## Marketing Performance Installation

1. Once the Data Bundle release has fully completed, go to Setup → Marketing Cloud → **Marketing Performance**.

2. The prerequisites will already be completed, so click Install to complete the installation (about 5 minutes).

## Verification

1. Return to “Assistant Home” and confirm that the setups for both Marketing Cloud Engagement and Marketing Cloud Next have been completed.

> *Although Identity Resolution is not fully completed, Identity Resolution for unified accounts is based on business needs and does not need to be forced. (Advanced Edition only.)*

2. Create a temporary Journey in Journey Builder and click Connect to Campaign to verify that you can transition to the Campaign.

3. Also verify that you can add a Journey to a Campaign from the Marketing Cloud Next side. (Note: At this time, a Journey added to a Campaign cannot be removed.)

## Conclusion

Going forward, Marketing Cloud Engagement is expected to be sold as Engagement+. Therefore, knowledge of Marketing Cloud Next will become essential. Be sure to keep up.

Finally, here are some of my articles related to initial setup:

- [Official Quick Start Guide — Initial Setup](/@marketingcloudtips/marketing-cloud-on-core-official-quick-start-guide-initial-setup-3bf835cc889a)
- [Steps for Email Domain Authentication](/@marketingcloudtips/marketing-cloud-next-email-authentication-steps-424e9cbbf76d)
- [Adding From Addresses & Reply Mail Management](/@marketingcloudtips/marketing-cloud-next-adding-from-addresses-reply-mail-management-8cc7bd2ce258)
- [Setting Domains for Landing Pages](/@marketingcloudtips/marketing-cloud-next-landing-page-domain-settings-6367a4c1e663)
- [Setting Domains for Email Tracking Links](/@marketingcloudtips/marketing-cloud-next-setting-domains-for-email-tracking-links-1195027cb56d)
- [Manually Deploying Updated Data Streams](/@marketingcloudtips/marketing-cloud-next-manually-deploying-updated-data-streams-8655b4a56296)
- [How to Configure Data Space Filters](/@marketingcloudtips/marketing-cloud-next-how-to-configure-data-space-filters-6880c21093bd)
- [How to Configure Identity Users](/p/3a1762e0d87b)
- [Testing with Sandbox](/@marketingcloudtips/marketing-cloud-next-testing-with-sandbox-22f23d92eef0)
- [A Guide to Consent Management](/@marketingcloudtips/marketing-cloud-on-core-a-guide-to-consent-management-5ca95a1602a0)
- [Disabling Consent Management](/@marketingcloudtips/marketing-cloud-next-disabling-consent-management-41d58a4acbef)
- [How to Configure Data Graphs](/p/1af8d9aa9026)

For a **my complete list related to Marketing Cloud Next**, please refer to the article below.

[## SFMC Tips #28 : Overview and Explanation of Marketing Cloud Growth Edition

### On February 20, 2024, Salesforce announced an entirely new marketing tool called Marketing Cloud Growth Edition. This…

medium.com](/@marketingcloudtips/unveiling-salesforces-latest-innovation-marketing-cloud-growth-edition-announcement-1e504a859f8e?source=post_page-----6fae8c535337---------------------------------------)

That’s all for now.

Stay tuned for more Marketing Cloud Growth & Advanced Edition tips! 😊

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
