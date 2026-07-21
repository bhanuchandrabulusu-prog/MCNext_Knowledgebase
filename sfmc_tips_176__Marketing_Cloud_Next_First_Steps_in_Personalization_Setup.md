# SFMC Tips #176 : Marketing Cloud Next: First Steps in Personalization Setup

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-next-initial-setup-for-personalization-be47931cef01

---

# SFMC Tips #176 : Marketing Cloud Next: First Steps in Personalization Setup

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--be47931cef01---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--be47931cef01---------------------------------------)

6 min read

·

Sep 25, 2025

--

Photo by [COSMOH](https://unsplash.com/@cosmoh?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

**Marketing Cloud Next’s Personalization** is an application that integrates with Data Cloud to deliver optimized experiences for each individual user. By leveraging objective-based and rule-based content targeting, you can deliver personalized recommendations and content tailored to each user.

This article provides a **step-by-step guide** for the initial setup of Personalization.

***Note:*** *You can test this in an SDO, but you can only build up to three data graphs in an SDO. This personalization uses two data graphs, so if you are already using two, please test in a new SDO environment.*

### **① Checking the Personalization Home**

1. For contracted accounts, the installation of the Personalization app and basic configuration is usually already completed. Therefore, “Personalization” should appear in the App Launcher.

2. Clicking **Personalization** from the App Launcher opens the standalone Personalization application home screen, from which you can access various features.

### **② Creating and Updating Permission Sets**

Before using Personalization, you need to prepare the necessary permission sets in advance. Follow the steps in the official help documentation to create and update the following two permission sets:

**1. Create the Personalization Admin Permission Set**  
Assign it to system administrators so they can perform various Personalization management operations.

[## Salesforce Help

### Edit description

help.salesforce.com](https://help.salesforce.com/s/articleView?id=mktg.persnl_setup_permission_set_create.htm&type=5&source=post_page-----be47931cef01---------------------------------------)

*\*Please also add the Personalization Intelligence User at the same time.*

**2. Update the Data Cloud Salesforce Connector Permission Set**  
Grant the permissions required to integrate Salesforce CRM, Data Cloud, and Personalization.

[## Salesforce Help

### Edit description

help.salesforce.com](https://help.salesforce.com/s/articleView?id=mktg.persnl_setup_permission_set_update_data_cloud_connector_permissions.htm&type=5&source=post_page-----be47931cef01---------------------------------------)

*Depending on your environment, these may already be configured. Even if so, make sure they are correctly assigned.*

### **③ Releasing Foundational Data**

1. First, complete the release in Data Cloud. Once confirmed, open **Personalization Setup** from the gear icon at the top right of the screen.

2. Usually, the Setup Status will show **Successful**, so you can proceed to release the **Foundational Data**. This process deploys the objects and predefined computed insights required for Personalization to function.

3. The release typically takes about **5 minutes**.

**Deployed Mapped DMOs:**

- Personalization Point
- Personalization Decision
- Personalization Response Template
- Personalizer
- Personalization Log

*Even if a DMO with the same name already exists, running the release will* ***automatically map it****.*

![]()

**Deployed Predefined Computed Insights:**  
Two types of computed insights are deployed: **Daily Personalization Requests** and **Daily Personalization Uniques**.

- Daily Personalization Requests
- Daily Personalization Uniques

*These insights are* ***not scheduled immediately after release****, so you must manually set up the schedule. Also, if some insights are not deployed in a single release, pressing the* ***Release button again*** *may install them.*

### **④ Setting Up the Pipeline Intelligence Dashboard**

1. After confirming that the computed insights were released in the previous step, if **CRM Analytics** is not enabled in your environment, click the **Enable** button.

2. Enable **CRM Analytics**.

3. The enablement process takes approximately **1 minute**. Once completed, return to **Personalization Setup**.

4. Install the **Pipeline Intelligence Dashboard**.

5. Installation takes about **10–15 minutes**.

6. After installation, confirm that analytics are accessible from the **Personalization Intelligence** tab.

### **⑤ Optional Settings for Attribution Intelligence**

1. If you want to track and analyze attributions for **Add to Cart**, **Orders**, or **Sales**, you can optionally release pre-configured attribution data.

This analysis requires the use of the following three standard DMOs:

- Product Browse Engagement
- Shopping Cart Engagement
- Product Order Engagement

2. Attribution data can be released to any data space of your choice. Even if it is already configured, duplicate checks are automatically performed.

3. When the release is executed, the following will be set up in the selected data space:

- Required DLOs
- Pre-configured attribution model
- First Touch (FT): first interaction
- Last Touch (LT): last interaction

*An attribution model determines* ***how much credit is assigned to each touchpoint****.*

4. Occasionally, errors may occur due to insufficient mapping, such as:

![]()

This happens if the `deviceId` in **All Event Data** of the `Experience_Cloud_Event_Connector` DLO in the Engagement category is not mapped to the `individualId` in **Shopping Cart Engagement**.

*Before executing the release, make sure to complete and save all mappings.*

5. The release process takes approximately **5 minutes**.

### **⑥ Default Personalization Point Authentication Setup**

In the last section, you can choose whether to enable the **Authentication Setting** for Personalization Points by default. Click the pencil icon to display the checkbox.

When enabled, only authenticated endpoints will be used when sending real-time events to Data Cloud or retrieving recommendations from Data Cloud within the Personalization Point configuration. This feature was introduced in the **Spring ’25 release**.

By default, the checkbox is selected as shown below, but you can toggle it on or off as needed. The default setting itself can also be changed later.

## Conclusion

This article provided a step-by-step guide for the initial setup of Personalization, covering:

- Checking the application
- Preparing permission sets
- Releasing foundational data
- Setting up the analytics dashboard
- Optional settings for attribution analysis

These steps form the **basic foundation for using Personalization**.

For the Salesforce Personalization setup that follows, I recommend proceeding in line with the **official workshops**. They are the most reliable resource and provide a structured way to understand the configuration, so using them as your reference is the best approach.

[## Setup Personalization

### Gain hands-on experience with this next-generation platform through self-guided, practical workshops.

agentforce-marketing-9cf347fa7db7.herokuapp.com](https://agentforce-marketing-9cf347fa7db7.herokuapp.com/workshops/salesforce-personalization/setup-personalization.html?source=post_page-----be47931cef01---------------------------------------)

That concludes this guide.

Stay tuned for more Salesforce Marketing Cloud tips! 😊

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
