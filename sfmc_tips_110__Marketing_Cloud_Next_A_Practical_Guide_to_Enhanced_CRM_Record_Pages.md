# SFMC Tips #110 : Marketing Cloud Next: A Practical Guide to Enhanced CRM Record Pages

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-on-core-a-practical-guide-to-enhanced-crm-record-pages-34650d05475b

---

# SFMC Tips #110 : Marketing Cloud Next: A Practical Guide to Enhanced CRM Record Pages

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--34650d05475b---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--34650d05475b---------------------------------------)

7 min read

·

May 4, 2025

--

Photo by [Nahid Hatami](https://unsplash.com/@i_am_nah?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

Using **Marketing Cloud Next** (Marketing Cloud Growth & Advanced Edition) requires integration with Sales Cloud and Service Cloud. Customer data managed in these clouds serves as the data source for Marketing Cloud Growth & Advanced Edition. This integration enables data to be fed back into the record pages of Contacts and Leads, enhancing their display and adding valuable insights.

By leveraging these expanded display features, you can seamlessly enrich your records with data-driven insights, fostering deeper customer understanding and operational efficiency.

In this article, I’ll introduce the four key features:

1. **Data Cloud Profile Engagement**
2. **Data Cloud Profile Insights**
3. **Data Cloud Copy Field**
4. **Privacy Consent Status**

## 1. Data Cloud Profile Engagement

This feature displays “Engagement Activity” from the past 7 days related to a unified individual profile. For example, it shows which emails were sent, opened, or clicked, along with their timestamps, enabling real-time insight into customer interests.

### **How to configure:**

1. Open the edit page for Contact or Lead records.
2. From the component list on the left, select **Data Cloud Profile Engagement** and drag it onto the canvas.

### **Configuration details for Contacts:**

- **Matching field:** Contact ID (use Lead ID for Leads)
- **Data Space:** default
- **Unified Individual DMO:** Unified Individual
- **Unified Individual Link:** Unified Link Individual
- **Engagement DMO:** Select all

By default, data from the last 7 days is displayed, but you can click the filter icon to extend the range to 30 or 90 days.

### **Notes:**

- Displaying data for Unified Individuals consumes **Data Cloud credits**. Expanding the data range increases credit usage.
- Switching screens resets the view to the default 7-day range.
- Open metrics include activity from Apple Mail’s MPP (Mail Privacy Protection) and Google apps’ auto-opens.

## 2. Data Cloud Profile Insights

With **Data Cloud Profile Insights**, you can display specific metrics from calculated insights configured in Data Cloud for unified individual profiles.

### **How to configure:**

1. Open the edit page for Contact or Lead records.
2. From the component list on the left, select **Data Cloud Profile Insights** and drag it onto the canvas.

### **Configuration details for Contacts:**

- **Matching field:** Contact ID (use Lead ID for Leads)
- **Data Space:** default
- **Unified Individual DMO:** Unified Individual
- **Unified Individual Link:** Unified Link Individual
- **Calculated Insights:** Overall Marketing Score
- **Metric:** Engagement\_Score

### **Notes:**

- Only metrics from calculated insights with a single dimension can be displayed.
- For metrics that represent monetary values, check the **Format as currency** box below the metric selection screen to enable currency formatting.

By the way, the names of preconfigured calculated insights, such as those shown below, are determined by the **language setting at the time of initial setup**, and currently, they cannot be changed afterward. Even if you prefer English, unfortunately, you’ll need to accept this limitation.

In addition, there is a [**known issue**](https://help.salesforce.com/s/issue?id=a02Ka00000ixogJ) at the moment where, depending on your account, you may not be able to select the following two calculated insights:

- Overall Marketing score
- Marketing Engagement score

## 3. Data Cloud Copy Field

Using **Data Cloud Copy Field**, you can display Data Cloud values in record page fields. This feature functions similarly to **Data Cloud Profile Insights**.

### Configuration Steps:

1. First, create a new numeric field named “Engagement Score” following the standard procedure.

2. For users with the **Data Cloud Data Aware Specialist** permission set, click **New** under Data Cloud Copy Field.

3. If you encounter the error message: “We couldn’t find your data space. Make sure at least one data space exists and that you have access to all data spaces you want data from.” and are unable to proceed, follow the steps below:

**Steps**

1. Go to **Setup** > **Permission Sets**, and select **Data Cloud Architect** (formerly **Data Cloud Administrator**).
2. In the **Apps** section, select **Data Cloud Data Space Management**.
3. Under **Data Space**, click **Edit**.
4. **Enable** the **Default** data space.
5. Click **Save**.

4. Select the **Calculated Insight** you want to use.

5. Choose the field you want to display on the record page.

6. Decide on the definition name for the copy field. This name will not be visible in the UI.

7. Map the copy field to the contact field you created earlier.

8. Start synchronization.

9. If a permissions error occurs for a new field, click the link highlighted in blue.

10. Navigate to the Contact object, select **Modify All Records** under **Object Permissions**, and enable **Edit Access** for the CRM field name mapped in Step 6.

11. After resolving the error, restart the synchronization process.

12. Once the synchronization completes, the data will be reflected.

## 4. Privacy Consent Status

The final feature, **Privacy Consent Status**, was previously covered in the article “A Guide to Consent Management”. Here’s a recap of its functionality.

> *As of Spring ’26 and later, it is now supported for Person Accounts as well.*

[## SFMC Tips #90 : Marketing Cloud on Core: A Guide to Consent Management

### The Importance of Consent Management in MCC

medium.com](/@marketingcloudtips/marketing-cloud-on-core-a-guide-to-consent-management-5ca95a1602a0?source=post_page-----34650d05475b---------------------------------------)

### Configuration Steps:

1. Open the edit screen of the Contact or Lead record page, create a custom tab called **“Consent”**, then select **“Privacy Consent Status”** from the list of components on the left and drag & drop it onto the canvas.

2. This will immediately allow you to view the consent status for each subscription directly on the record page.

3. By clicking the dropdown menu displayed on the far right of the screen, you can manually update the consent (including adding new subscriptions).

4. You can choose either **Opt-in** or **Opt-out** and save the changes. It takes about **2–3 minutes** before the changes appear in the data model object **“Communication Subscription Consent”**. On the CRM record page, the update is reflected right away, but the data in **Data Cloud** should be regarded as the source of truth for Opt-in information.

## Additional Use Cases

For instance, the copy field **Engagement Score** can be displayed in list views. Sorting records by score allows for more effective marketing approaches by targeting highly engaged customers.

These features rely on Marketing Cloud Growth & Advanced Edition, which integrates Sales Cloud and Service Cloud and operates on the Data Cloud platform. By leveraging these tools, you can unlock new efficiencies and insights.

That’s all for this time!

Stay tuned for more Marketing Cloud Growth & Advanced Edition tips! 😊

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
