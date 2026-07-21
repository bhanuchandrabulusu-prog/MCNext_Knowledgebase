# SFMC Tips #162 : Marketing Cloud Next: How to Configure Identity Users

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-next-identity-license-support-begins-3a1762e0d87b

---

# SFMC Tips #162 : Marketing Cloud Next: How to Configure Identity Users

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--3a1762e0d87b---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--3a1762e0d87b---------------------------------------)

8 min read

·

Aug 18, 2025

--

Photo by [Quinn Buffing](https://unsplash.com/@qbuffing?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

With the [Summer ’25 new feature release](/@marketingcloudtips/marketing-cloud-on-core-summer-25-release-highlights-4ad6f39c5d6d) for Marketing Cloud Next Growth & Advanced Edition, it became possible to create custom Identity profiles for Marketing Cloud Next and assign them to users, allowing users without full Salesforce licenses to access Marketing Cloud.

With this mechanism, users can access Marketing Cloud with permissions equivalent to “**Marketing Cloud Administrator**”, “**Marketing Cloud Manager**”, or even “**Data Cloud Architect**”, and can use key features such as campaigns, segments, flows, and analytics reports, **with up to 100 users available by default**.

## Benefits of Identity Profiles

- **Cost Savings**  
  You can add users without requiring full licenses, helping to reduce costs.
- **Flexible Access Management**  
  Grant only the minimum required access to functions, such as for specific departments or external partners.
- **Security Controls**  
  Manage restrictions, such as IP access limits, at the profile level.

If you want to grant different permissions to Identity users, you can flexibly handle this by creating multiple custom Identity profiles.

*Tips: By default, up to 100 Identity users can be created.* ***If more are needed, additional licenses can be purchased****.*

## Basic Configuration

### Creating a Custom Identity Profile for Marketing Cloud

1. Open the **Setup** page, enter **Profiles** in the Quick Find box, and select **Profiles**.

2. Copy (Clone) the **Identity User** profile.

*Tip: If the “Clone” option is not displayed, go to* ***Setup → User Management Settings*** *and enable* ***Enhanced Profile List Views****.*

3. Name your custom Identity profile and click **Save**.  
(Example: Marketing Cloud Identity User)

### Registering Identity Users for Marketing Cloud

1. Open the **Setup** page, enter **Users** in the Quick Find box, select **Users**, and click **New User**.

2. From the **User License** dropdown, select **Identity**.   
Then, from the **Profile** dropdown, select the custom Identity profile you created for Marketing Cloud.

3. Click **Save** to apply the changes.

4. Click **Permission Set Assignments**.

5. Click **Edit Assignments**.

6. Add the following permission set:

- **Marketing Cloud Manager**

**Important:** In addition to the permissions listed above, it is also possible to grant higher-level permissions as needed.

**Examples of assignable permissions:**

- Data Cloud Architect
- Marketing Cloud Admin
- Tableau Next Included App Business User
- Manage Subscriptions in Your Account: Identity User
- View Unified Engagement History Dashboard (Spring ’26–)
- Send Distributed Marketing Messages (Spring ’26–)

*“Manage Subscriptions in Your Account: Identity Users” is the permission that allows Identity users to access the “Consumption Card”.*

*Please note that the “View Unified Engagement History Dashboard” permission has a limited number of users. Growth: up to 5 users / Advanced: up to 10 users*

## Creating a Public Group for Identity Users

If there are many Identity users, creating a “**Public Group**” before performing the “Removal of Usage Restrictions” in the next section will make configuration easier.

Create a public group named something like “Marketing Cloud Identity Users” from Setup > Public Groups, and add the Identity users into it.

## Granting Access Permissions

## ① Setting Users as Content “Contributors”

If a profile is set to **System Administrator**, users automatically have access to all CMS workspaces. However, in this case, users need to be set as **Contributors** so they can access the CMS workspace where Marketing Cloud content is stored.

1. A **System Administrator（or Content Admin）**navigates to the **Content** tab and opens the relevant folder.

2. From the gear icon, select **Contributors**.

3. Click the **Add Contributor** button, add the Identity license user, and click **Next**.

4. Assign a role to the contributor and complete the process.

5. Verify that the Identity license user can access the CMS Workspace.

## ② Setting Users as Landing Page “Contributors”

For the same reason as above, users may need to be added as **Contributors** for Marketing Cloud standard forms and landing pages in order to publish them.

*If you encounter an error when publishing a landing page, it may be because the user has not been added as a Contributor and therefore lacks permission to publish forms. Follow the steps below to preemptively add the target user as a Contributor:*

1. Go to **Setup** > search for **All Sites**, then open it. Select the **Workspace** to the left of **Marketing Landing Pages**.

2. Click **Administration**.

3. Select **Members**, choose the **Profile** that includes the user you want to add, add them as a member, and save.

4. Next, select **Contributors** and click the **Add Contributor** button.

5. Select the user you want to add and grant them **Builder** or higher permissions. After this, they will be able to publish forms and landing pages.

![]()

## ③ Access Permissions for Analytics Folders and Reports

For Identity users, the **View Report** feature in the Analytics tab is not available by default.  
Because of this, sharing settings for the analytics folders are also required.

*※ Currently, this has been changed to* ***Flow Performance****, which is part of Tableau Next functionality. (Included in the Spring ’26 new feature release.)*

*As part of this update, the previous* ***View Report*** *button has been removed and replaced with* ***Open Detail****, which navigates to Flow Performance.*

### Sharing Settings

1. Open the **Analytics** tab, select **Browse** from the left-side menu, and search for **Flow Element**.

*The Flow Element folder has been discontinued in new organizations, and also discontinued in new SDOs. (If you want to obtain it, from* [*here*](/@marketingcloudtips/marketing-cloud-next-create-consent-records-with-a-subflow-dc81903fe488)*.)*

2. From the ▼ menu of the **Flow Element** folder, select ****.

3. Configure sharing permissions for **Identity Users** or **Public Groups**, then save the settings.

※ If necessary, apply the same sharing configuration to the following analytics folders as well.

- Flow Email Engagement（※ Retired in newly created organizations）
- Email Engagement Reports
- Email Engagement Dashboard
- SMS Engagement Reports
- SMS Engagement Dashboard
- Forms Engagement Reports
- Form Engagement Dashboard
- Landing Page Engagement Reports
- Landing Page Engagement Dashboard

## ④ Access Permissions for Created Flows

Flows are generally configured as “**Private**”.

1. Open the relevant flow and click “**Sharing**”.

2. Select the Identity user and grant access or edit permissions.

![]()

The following flow types cannot be accessed even if permissions are granted:

- Schedule-Triggered Flow
- Record-Triggered Flow

## ⑤ Access Permissions for Tabs That Are Not Displayed

1. For example, you may want to access the following objects that are not displayed by default.

- Activation Targets
- Data Lake Objects
- Data Streams
- Query Editor

2. Create a new “Permission Set”.  
Example name: Marketing Cloud Identity User Tabs (Custom)

*⚠️ At this time, do* ***not*** *set “License Type: Identity”.*

3. Open “**Object Settings**” in the created permission set.

4. Select the target objects one by one.

5. Enable “Tab Settings Available” for each object and save.  
Repeat the same process for all target objects.

6. Next, click “Manage Assignments”.

7. Assign the target Identity users and save.

8. Next, log in as the relevant Identity user, open “Edit Tabs”, and click “Add More Items”.

9. Add the objects that were enabled earlier and save.

10. You will now be able to access the tabs that were previously hidden.

## Conclusion

By leveraging **Identity licenses**, you can significantly increase the number of available users even with a limited number of full licenses. I encourage you to make the most of this capability.

That’s all for now.

Stay tuned for more Salesforce Marketing Cloud tips! 😊

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
