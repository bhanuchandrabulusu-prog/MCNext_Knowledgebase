# SFMC Tips #82 : Data Cloud: Faster Field Access with View All Field (Global)

**Source:** https://medium.com/@marketingcloudtips/a-game-changing-update-in-data-cloud-faster-field-access-with-view-all-field-global-64614afe4a83

---

# SFMC Tips #82 : Data Cloud: Faster Field Access with View All Field (Global)

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--64614afe4a83---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--64614afe4a83---------------------------------------)

5 min read

·

Feb 15, 2025

--

Photo by [AbsolutVision](https://unsplash.com/@alterego_swiss?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

In the past, when syncing newly created fields in Salesforce CRM to Data Cloud data streams, it was necessary to configure **Field Permissions** in the **Data Cloud Salesforce Connector** permission set and grant **Read Access** to the desired fields.

This process was explained in the following **TIPS** article.

[## SFMC Tips #78 : Data Cloud & Marketing Cloud Engagement Integration Tips

### In this article, I will share tips for integrating Data Cloud and Marketing Cloud Engagement. I plan to update this…

medium.com](/@marketingcloudtips/data-cloud-marketing-cloud-engagement-integration-tips-9e160167cda8?source=post_page-----64614afe4a83---------------------------------------)

With the release of the new **View All Field (Global)** system permission in the **Spring ’25 Release**, you can now set access to Data Cloud fields more quickly.

This new system permission allows you to display and utilize all CRM fields in Data Cloud’s data streams, **including fields created in the future**.

As the feature is now live, let’s review the setup process.

### 1. Configuring for All Objects

1. Navigate to **Lead** in Data Cloud and click **Add Source Field**.

2. Three fields are displayed, indicating that these fields have **Read Access** but are not yet utilized in Data Cloud.

3. Go to the **Data Cloud Salesforce Connector** permission set and click **System Permissions**.

4. Click **Edit**.

5. Scroll down to locate the **View All Field (Global)** permission. This will likely be unchecked.

6. **Check** the box.

7. And **Save**. Don’t forget this step!

8. A confirmation screen appears. If you’re okay with applying this to all standard and custom objects, click **Save**.

9. With the settings complete, return to the **Leads** data stream and click **Add Source Fields** again.

10. Additional fields are now available for use in Data Cloud. Success!

This configuration applies the **View All Field** permission to **all objects**, but it is also possible to grant this permission on a per-object basis.

Let’s look at that process next.

### 2. Configuring for Individual Objects

1. Open **Contact** in Data Cloud and click **Add Source Field**.

2. Four fields are displayed, indicating that these fields have **Read Access** but are not yet utilized in Data Cloud.

3. Go to the **Data Cloud Salesforce Connector** permission set and click **Object Settings**.

4. Search for and select **Contacts**.

5. On the **Contacts** screen, click **Edit**.

6. You’ll notice that **View All Fields** is unchecked and that some fields do not have **Read Access**.

7. By checking **View All Fields**, all fields will be automatically checked. Newly created fields will also have this checked by default. **Save** your changes. Don’t forget to save!

8. Return to the **Contacts** data stream and click **Add Source Fields** again.

9. Additional fields are now available for use in Data Cloud. Success!

How was that?

Previously, individual permissions had to be granted for each new field created in CRM. However, with this new feature, **Read Access** can be granted for all fields moving forward. This is an incredibly efficient update — a true **Game Changer!!**

Going forward, you can decide whether to grant permissions for the entire object, for individual objects, or continue managing field-specific permissions based on your organization’s security policies.

### Notes

- Once permissions are checked and saved, unchecking them and saving will not revert to the original settings. Please confirm carefully before applying these settings.
- When the system permission “View All Fields (Global)” is enabled, the View All Fields option for all fields across all objects will be selected in bulk.
- I created a new field in Salesforce CRM and immediately confirmed that it was available for use in the Add Source Field of Data Stream.

It’s so convenient!

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
