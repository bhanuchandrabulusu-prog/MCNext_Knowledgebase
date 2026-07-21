# SFMC Tips #164 : Data Cloud: License, Credits, and Permission Set Changes (Effective September 4…

**Source:** https://medium.com/@marketingcloudtips/data-cloud-license-changes-effective-september-4-2025-bd69b78a128c

---

# SFMC Tips #164 : Data Cloud: License, Credits, and Permission Set Changes (Effective September 4, 2025)

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--bd69b78a128c---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--bd69b78a128c---------------------------------------)

4 min read

·

Aug 22, 2025

--

Photo by [Aziz Acharki](https://unsplash.com/@acharki95?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

Between **September 4–8, 2025**, license changes for Data Cloud will be automatically rolled out to all accounts.

The major change is that the **Segment & Activation add-on SKU will be consolidated into the “Data Service Credits SKU”.**  
This will significantly impact how segmentation and activation features are consumed, as well as how permission sets are managed. Since this is an important update, please make sure to review the details carefully.

**🔗 [**[**Official Announcement**](https://help.salesforce.com/s/articleView?id=005131350&type=1)**]**

**Important:** *Data Cloud Admin* has been automatically renamed to *Data Cloud Architect*. The following four permission sets are now legacy, so please consider transitioning to other permission sets:

- (Legacy) Data Cloud Marketing Admin
- (Legacy) Data Cloud Data Aware Specialist
- (Legacy) Data Cloud Marketing Manager
- (Legacy) Data Cloud Marketing Specialists

> ***Regarding Credit Consumption Cards:*** *Although Segmentations Activations is marked with the label “Deprecated,” as of September 7, the total has not yet been converted into Data Services Credits.*
>
> *⇒ The conversion was successfully completed, and the Segmentations Activations credits have been added to the total number of Data Services credits. (September 11)*

## Overview

### Easier Access to Segment & Activation

With the updated Data Cloud license, **segmentation, activation, and related features** will now be included as standard. Customers will no longer need to purchase a separate Segment & Activation add-on SKU.

### Credit Consolidation in Digital Wallet

Previously issued **Segment & Activation credits will be converted to Data Service Credits at a 1:1 ratio.**  
Going forward, usage of segmentation and activation features will consume credits from the Data Service consumption card.  
(*Note: A new rate card is expected to be published on the Help site in August.*)

### Updates to Data Cloud Standard Permission Set Licenses (PSL)

Some existing permission sets will be deprecated and replaced with new ones.  
Organizations already using Data Cloud will need to migrate users to the new permission sets.

🔗 [[Permission Set Migration Guide](https://resources.docs.salesforce.com/rel1/doc/en-us/static/pdf/DC_StandardPermSet_TransitionGuide.pdf)] (**Important!**)

### Temporary Pause on Overage Billing

Overage billing for Data Cloud will be temporarily paused until **November 3, 2025.**  
However, customers remain responsible for their usage. It is strongly recommended to monitor your usage continuously via the **Digital Wallet**, which provides near real-time visibility into account consumption.

## Permission Set Migration

Starting **September 4, 2025**, the permission sets currently in use will become **“Legacy”.**  
They can still be used as-is, but **no new features will be added** to legacy permission sets. Therefore, migrating to the new permission sets is strongly recommended at the earliest opportunity.

### 1. Name Change: Data Cloud Admin → Data Cloud Architect

- The existing **“Data Cloud Admin”** permission set will be renamed **“Data Cloud Architect”** to better reflect its role.
- Access to Data Cloud setup will still require either the **Salesforce Admin role** or the **“Customize Application”** permission.

### 2. Permission Sets Becoming Legacy

The following permission sets will become **Legacy**:

- (Legacy) Data Cloud Marketing Admin
- (Legacy) Data Cloud Data Aware Specialist
- (Legacy) Data Cloud Marketing Manager
- (Legacy) Data Cloud Marketing Specialists

These legacy sets can continue to be used, but since they will not receive new feature updates, **migrating to the new permission sets is strongly recommended.** The recommended replacements are:

- **Data Cloud Activation Manager**
- **Data Cloud Activation Specialist**

Compared to the former “Marketing Manager” and “Marketing Specialists” permission sets, these new activation-related permission sets provide **broader access rights**.

### 3. New AI-Related Standard Permission Sets

Later in **late September 2025**, additional standard Data Cloud permission sets will be introduced to support **data governance and AI-related functionality**:

- **Data Cloud AI Specialist**
- **Data Cloud Governance Specialist**

These new permission sets will grant access to specific subsets of Data Cloud features that are most relevant to these specialized roles.

## Wrapping Up

To quickly summarize, here are the **four key points**:

1. **Automatic SKU consolidation** will roll out in early September 2025.
2. **Segment & Activation features** will be unified under **Data Service Credits.**
3. **Some permission sets will become legacy** → Migration to new permission sets is recommended.
4. **Overage billing will be paused** until **November 3, 2025.**

Among these, **permission set migration is the most important action item.**  
For administrators, it’s best to review and begin preparing for the migration as soon as the changes are released to ensure a smooth transition.

That’s all for now.

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
