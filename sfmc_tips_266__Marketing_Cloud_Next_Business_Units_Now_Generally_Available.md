# SFMC Tips #266 : Marketing Cloud Next: Business Units Now Generally Available

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-next-business-units-now-generally-available-b01e49c09a9a

---

# SFMC Tips #266 : Marketing Cloud Next: Business Units Now Generally Available

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--b01e49c09a9a---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--b01e49c09a9a---------------------------------------)

5 min read

·

Mar 12, 2026

--

Photo by [oxana v](https://unsplash.com/@arttravelling?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

In **Marketing Cloud Next Growth & Advanced Edition**, **Business Units** were introduced as a new feature in the [**Spring ’26 release**](/@marketingcloudtips/marketing-cloud-next-spring-26-release-highlights-24c0c804b0cb).

Until now, operations in Marketing Cloud Next have primarily been centered around **Data Spaces**, but with this feature update, the concept of **Business Units** has now been officially introduced.

However, this does not mean that Data Spaces have simply been renamed to Business Units. In the configuration screen, **Data Spaces and Business Units are linked in a 1:1 relationship**.

As clearly stated in the official help documentation, **one Data Space cannot be linked to multiple Business Units**.

With this **1:1 relationship**, data can be separated while marketing content can be organized and managed for each individual Business Unit.

### Overview of Business Units

- **Expanded reach and separated management:**  
   Marketing activities can be separated by region or product line while expanding overall reach.
- **Separation of content and contacts:**  
   Data and content can be managed independently by region, product line, or brand.
- **Audience-aligned adjustments:**  
   Deliver the right message to the right target audience.
- **Target analysis visibility:**  
   Performance can be analyzed both at the Business Unit level and at the overall company level.

### First Business Units

To enable Business Units, you must first create **the first two Business Units**.  
If there are not two Business Units, the feature cannot be enabled.

The current marketing configuration (**Data Spaces, default content workspace, and others**) will be assigned to the **first Business Unit created**, and will continue to be used as is.

### Business Unit Member Roles

Users can be added as Business Unit members with one of the following roles.

### ① Marketer-Standard

Only users who have the **Marketing Cloud Admin** or **Marketing Cloud Manager** permission sets can be added to this role.

Only members with this role can **activate flows** for campaigns within the Business Unit.

In the **Business Unit marketing workspace**, these users will also have the **Content Manager role**, allowing them to perform the following actions:

- Create content
- Edit content
- View content
- Publish content

### ② Marketer-ReadOnly

Members with this role **cannot activate Business Unit campaigns**.

However, they can perform the following actions:

- Send promotional messages
- View performance dashboards

On the other hand, they **cannot access the Business Unit marketing workspace**.

### Business Unit Considerations

There are several important limitations regarding Business Units.

- Business Units **cannot be deleted or modified once created**.
- A Business Unit can have **multiple Marketing CMS Workspaces**, with **one CMS Workspace designated as the default**.
- All campaign elements operate **within the selected Business Unit**, helping maintain **data integrity and compliance**.
- You can create **up to 50 Business Units**.

## Setup Steps

Configuration is performed from **Marketing Features → Business Units** in Setup.

1. First, **enable Business Units**.

> *Note: This setting can only be executed in organizations where* ***two or more Data Spaces exist****.*

2. When configuration begins, you first set up the **Business Unit associated with the default Data Space**.

You decide the **Business Unit name** and choose one of the following settings:

-  default channels and subscriptions across all Business Units
- Use them only within this (default) Business Unit

3. Next, enter the **address**.  
You can also retrieve and use the **existing organization address**.

4. Here you can select the **Marketing Cloud Administrator** or **Marketing Cloud Manager** permission sets.

When this configuration is applied, **existing users with those permission sets are automatically added as members of the default Business Unit**.

5. Next, create the **second Business Unit**.

Search for the **Data Space you added**, and set the **Business Unit name** associated with it.

6. The organization’s **default marketing workspace** will be assigned as the **default workspace for the first Business Unit**.

Since the second Business Unit does not yet have a CMS workspace, you must **create a new CMS workspace here**.  
The **address is also entered here**.

7. Once a Business Unit is created, **it cannot be deleted or modified**.

Therefore, a **final confirmation screen** appears to review the configuration.

8. The Business Units are now created.

9. By clicking the link, you can **check the details of the Business Unit**.

10. If you scroll down the screen, you can also **add members**.

11. Basic settings and other configurations can also be managed from this screen.

12. Once the release is completed, the campaign record will display information such as which Business Unit the campaign belongs to.

13. You can also check the current setup status of each Business Unit in progress from **Assistant Home** in Setup.

## Conclusion

Until now, **the absence of Business Units** had been one of the major challenges of **Marketing Cloud Next**, but with this release, that issue appears to have been addressed for the time being.

However, the question still remains:  
**“Will the data truly be completely separated?”**

In **Marketing Cloud Engagement**, Business Units functioned almost like **mini-organizations**, allowing a fairly strict level of separation.

How far the **Business Units in Marketing Cloud Next** can operate at the same level is something that may be difficult to determine without actually using them in practice.

Personally, I plan to continue testing this while using it in real scenarios, and I will provide additional reports in the future.

That’s all for this time.

Stay tuned for more Salesforce Marketing Cloud tips! 😎

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
