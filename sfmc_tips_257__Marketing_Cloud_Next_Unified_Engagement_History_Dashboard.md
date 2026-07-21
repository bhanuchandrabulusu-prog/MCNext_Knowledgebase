# SFMC Tips #257 : Marketing Cloud Next: Unified Engagement History Dashboard

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-next-unified-engagement-history-dashboard-ee97fd1d217f

---

# SFMC Tips #257 : Marketing Cloud Next: Unified Engagement History Dashboard

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--ee97fd1d217f---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--ee97fd1d217f---------------------------------------)

4 min read

·

Feb 24, 2026

--

Photo by [Kelly Sikkema](https://unsplash.com/@kellysikkema?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

Marketing Cloud Next Growth & Advanced Edition introduces a new feature in the [**Spring ’26** release](/@marketingcloudtips/marketing-cloud-next-spring-26-release-highlights-24c0c804b0cb): the **Unified Engagement History Dashboard**, powered by Tableau Next technology.

By enabling this feature and adding the component to the record pages of **Contacts, Leads**, **Person Account, and Accounts**, marketing and sales users can leverage customer engagement data in a more intuitive and effective way.

**Number of included licenses by edition**

- **Growth Edition: 5 licenses**
- **Advanced Edition: 10 licenses**

Because email opens, clicks, and various interaction histories can be visualized directly on the CRM screen, this helps improve the accuracy of customer understanding and supports better decision-making for appropriate actions.

> ***Important:*** *This feature retrieves engagement history based on the* ***Unified Individual ID****.*

## Required Permissions

To use this feature, each user who will view it must be assigned the following two permission sets:

### a. New Permission Set

- **“View Unified Engagement History Dashboard”** permission set

＋

### b. Existing Permission Set

- If using Salesforce Foundations:  
   → **“Tableau Next Limited Viewer”** permission set
- For other organizations:  
   → **“Tableau Next Included App Business User”** permission set

**Note:** To display unified engagement data for a specific business unit, the target user must have a profile associated with that business unit.

In this article, I will explain the overview and setup procedure of this new feature.

## Setup Procedure

### 1. Enable Unified Engagement History Dashboard

1. Go to **Setup > Marketing Features** and select **“Unified Engagement History Dashboard”.**

2. Enable **“Unified Engagement History Dashboard”.**

### 2. Reinstall Marketing Performance

1. If **Marketing Performance** is not installed, go to **Setup > Marketing Features**, select **“Marketing Performance”,** and install it.

> *Note: Installation may take several minutes to complete.*

2. If it is already installed, delete the previous installation from the Setup screen. Select the **“Marketing Performance”** tab and click the **“Delete”** button displayed in the upper right corner.

> *Note: The deletion process may also take several minutes.*

3. After waiting a few minutes and refreshing the installation screen, the **“Install”** button will become active again. Click it to reinstall. Reinstalling will not affect past data.

> ***Note:*** *If you do not reinstall Marketing Performance, the following error message will appear.*

### 3. Add the Component to the Record Page

1. Finally, add the **“Unified Engagement History Dashboard” component** to the record page. Open the page editor and drag and drop the component.

> *Because this dashboard requires a large display area, it is recommended to create a* ***custom tab*** *for better visibility.*

2. Refresh the page to display the dashboard.

## Final Thoughts

Compared to the traditional simple engagement history data, this feature provides a far more comprehensive and multi-dimensional view of engagement data.

The CRM record page evolves into an analytical mode at once, making it an exciting experience for marketers.

Please try implementing it and experience it yourself.

The extended display components of Marketing Cloud Next that can be implemented in other CRMs are summarized in the following article, so please feel free to refer to it as well.

[## SFMC Tips #110 : Marketing Cloud Next: A Practical Guide to Enhanced CRM Record Pages

### Using Marketing Cloud Next (Marketing Cloud Growth & Advanced Edition) requires integration with Sales Cloud and…

medium.com](/@marketingcloudtips/marketing-cloud-on-core-a-practical-guide-to-enhanced-crm-record-pages-34650d05475b?source=post_page-----ee97fd1d217f---------------------------------------)

> *By the way, as of the Spring ’26 release,* ***Privacy Consent Status is now supported for Person Accounts****, so I would like to share that update with you.*

That’s all for this time.

Stay tuned for more Salesforce Marketing Cloud tips! 😎

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
