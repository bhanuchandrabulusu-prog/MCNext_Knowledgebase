# SFMC Tips #62 : Data Cloud: Triggering Journey Builder with Data Actions

**Source:** https://medium.com/@marketingcloudtips/how-to-trigger-journey-builder-with-data-actions-73d26c5810a7

---

# SFMC Tips #62 : Data Cloud: Triggering Journey Builder with Data Actions

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--73d26c5810a7---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--73d26c5810a7---------------------------------------)

10 min read

·

Nov 8, 2024

--

Photo by [Jelleke Vanooteghem](https://unsplash.com/@ilumire?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

Leveraging Data Cloud’s Data Actions allows you to send emails in Content Builder or start journeys in Journey Builder in near real-time, triggered by changes in data within Data Cloud.

Here are some example use cases where Data Actions can be effective:

- **Installation Support**  
  When customers who have purchased a product with installation support search for the “Installation Manual” on the website, this action can trigger the automatic sending of an email containing installation steps and how-to videos. This mechanism ensures that customers receive the support information they need at the optimal time, promoting a seamless user experience.
- **Fraud Detection**  
  Financial institutions can leverage Data Cloud’s transaction streaming capabilities to send real-time notifications to customers via email or SMS when fraudulent transactions are detected. This enables swift action and ensures customer security.
- **Customer Tier Updates**  
  Based on recent purchase history, when a customer’s lifetime value reaches a new service level, a platform event is sent to the CRM to automatically update the customer’s status.
- **Welcome Journey**  
  After completing their first purchase, customers are enrolled in a Welcome Journey, where they receive information about warranty coverage and additional services.
- **Financial Services**  
  If a customer’s average monthly deposit amount shows a significant year-over-year increase, a journey introducing investment options is automatically initiated.
- **Higher Education**  
  When predictive models detect a dropout risk based on a student’s academic performance, a platform event triggers a case to investigate and address potential issues.
- **Location-Based Engagement**  
  When a customer checks into a hotel, prompts are sent to encourage visits to the hotel’s bar or provide information on luxurious vacation activities, enhancing the customer’s overall stay experience.

With just the combination of Salesforce CRM and Journey Builder, similar handling is possible; however, in scenarios such as fraud detection in financial institutions, Data Cloud offers the advantage of deriving insights from the massive volume of transaction data streamed in real-time and instantly issuing notifications.

### Types of Data Actions in Integration with Marketing Cloud

Data Actions can be used for the following two purposes when integrating with Marketing Cloud:

- **Email Triggers:** Real-time emails triggered by customer actions through Marketing Cloud’s Transactional API.
- **Journey Builder API Events**: Triggering a journey based on customer actions, allowing engagement through appropriate channels such as email, SMS, or LINE.

### Types of Events that Trigger Data Actions

Data Actions can be triggered by the following events:

- **Data Model Objects (DMO)**: When records are added, updated, or deleted within a Data Model Object.
- **Streaming Events**: Data flowing in from Web SDK, Mobile SDK, API, or Marketing Cloud Personalization.
- **Calculated Insights**: Insights derived from streaming data into Data Cloud.

### Prerequisites for Data Actions

- [Help And Training Community](https://help.salesforce.com/s/articleView?id=sf.c360_a_create_a_marketing_cloud_data_action_target.htm&type=5) — Data Action Prerequisites
- [Help And Training Community](https://help.salesforce.com/s/articleView?id=sf.c360_a_streaming_insight_data_action_limits.htm&type=5) — Data Action Limits

This time, let’s focus on implementing a Journey Builder API Event triggered by Calculated Insights. Although this is a demo environment, it will give you a hands-on feel for the process.

## Creating Calculated Insights

In this scenario, I have linked the Salesforce CRM “Opportunity” object in my Data Cloud demo environment. Here, I’ll create a simple scenario where a journey is triggered to send a LINE message once the total “Amount” for a Contact surpasses a certain threshold.

First, I created the following Calculated Insight:

```
SELECT Opportunity_00D5Y000002TccE__dlm.ContactId__c AS ContactId__c,  
       SUM(Opportunity_00D5Y000002TccE__dlm.Amount__c) AS TotalAmount__c  
FROM Opportunity_00D5Y000002TccE__dlm  
GROUP BY Opportunity_00D5Y000002TccE__dlm.ContactId__c
```

When defining fields in Calculated Insights, be sure to use aliases (AS) with “\_\_c” at the end, as these serve as API references. Omitting “\_\_c” will result in an error.

First, there’s a reason for creating this calculated insight. The “ContactId\_\_c” that will serve as the subscriber key is required when setting up fields in the data extension on the Marketing Cloud side, so we set that up in advance.

Additionally, please note that the way the field names are written for this data extension is a bit unique. The naming format is as follows:

- **Field Naming Format Example**: `Opportunity_Total_Amount__cio_ContactId__c`

**This format connects the API reference name of the calculated insight with the field name using a hyphen**. The API reference name is listed under “Details”.

Now, let’s proceed with the setup on the Journey Builder side.

## Configuring the Journey

This journey will use an **API Event** as its entry source.

Create a data extension for the API Event entry source and be mindful of field names, **as they will map to Data Cloud**. Set up these fields:

- `Opportunity_Total_Amount__cio_ContactId__c` **(Text)**
- `Opportunity_Total_Amount__cio_TotalAmount__c` **(Number)**
- `EventDate` **(Date, with default set to Current Date)**

**Notes**:

- Set all fields to allow NULL values.
- Make the data extension sendable.

Since this journey involves LINE messaging, email-specific configurations are unnecessary. **However, if using email activities, ensure the subscriber’s current email is registered in “All Subscribers”, and select “Use email attribute from Contacts” for the default email address**.

Personalization strings in messaging can use the data extension fields:

```
Example:  
%%Opportunity_Total_Amount__cio_TotalAmount__c%%
```

After setting up the API Event entry source in the data extension, configure the LINE activity. For journeys with repeat entries, set the entry condition to “Re-entry anytime”. Save and Activate the journey.

## Setting the Data Action Target

Next, we’ll move on to the configuration in Data Cloud. First, set up the Data Action Target. Please create a new one.

When selecting “Manual” creation, you’ll come to the following branching point. Here, choose **Journey Builder API Event**.

After selecting it, a list of active API events in Journey Builder will appear. Choose the event named “**DataAction”**, which you activated earlier, and click the “Save and Publish” button.

This completes the creation of the Data Action Target. Note that there is a limit to the number of Data Actions you can create. **Each one is created per API event**.

## Creating the Data Action

Next, let’s proceed with creating the data action, which is the key part of this process.

Click on “New” and select “Manual” creation. Then, as shown below, the data action target you created earlier will load. Select it and click “Next”.

Next, select “Calculated Insight” as the Object Type.

In the primary object field, select the calculated insight you created, then choose the Subscriber Key. If the calculated insight is unable to retrieve the Subscriber Key, execution will fail.

Since we selected a calculated insight, no options are displayed this time. However, if you select a data model object, you can optionally choose related objects (DMO or Data Graph) associated with the primary object. This feature allows you to use attributes from related objects when configuring data action rules and enhances the data sent to Journey Builder.

If you select DMO as the related object, **you can add up to 10 additional attributes**. If you want to use these additional attributes in Journey Builder, include their names in the data extension as described above.

When choosing Data Graph, you cannot select individual attributes. Instead, the entire payload is sent to the data action target. **Reference**: [Configuring Data Extensions to Store Data Action Payloads](https://help.salesforce.com/s/articleView?id=sf.c360_a_data_extension_data_action_payload.htm&type=5)

If you select a data model object as the primary object and it is mapped to an external data lake object, such as Amazon Redshift, Google BigQuery, or Snowflake, you cannot select it as the primary object.

Finally, we set up the rule for “when to trigger” the action. In this scenario, when the total “Amount” for a contact exceeds a certain threshold, the journey will be activated to send a LINE message. Here, we set the amount to 50 million yen or more. Click “Next”.

- The “Trigger Data Action for Updated Records” option is only available if you select “Record Updated” as the event rule.
- If any action rule condition uses a change operator (such as “Has Increased” or “Is Changed”), you cannot change the “Trigger Data Action for Updated Records” setting. To modify this setting, remove all change operators from the conditions.

After setting the action definition name, click “Save and Publish”.

The data action setup is now complete. You can edit it anytime by clicking the edit button.

## Testing

Now that all settings are complete, let’s test them. Currently, I manage a contact with a total deal amount of 38.1 million yen. I’ll add a deal worth 11.9 million yen.

As shown below, I created and saved the deal.

Now, we just wait for the journey entry.

The deal data will be linked to the data stream, calculated in the calculated insight, and then entered into the journey. Depending on your account, this may take some time. The Event Results screen below updates automatically without requiring a refresh, so you can leave it open for a while.

After a short wait, the calculated insight has completed the calculation.

As shown below, the contact was successfully linked, and the count changed to 1.

Success! That’s all.

## Additional Information: About Email Triggers

For reference, if the Data Action Target is set to “**Email**” (email trigger), the configuration process is essentially the same as for the “Journey Builder API Event”.

However, there are a few important points to keep in mind:

**[Note 1]**  
**Pre-registration in “All Subscribers” is required**, and the email address used will be the one registered in “All Subscribers”. This is noted in the following help document:

[## Help And Training Community

### Edit description

help.salesforce.com](https://help.salesforce.com/s/articleView?id=sf.c360_a_create_a_data_action_in_customer_data_platform.htm&type=5&source=post_page-----73d26c5810a7---------------------------------------)

A subscriber key is the unique identifier of a message recipient in Engagement and determines the email address to use for communication. **You can’t send a data action event if a subscriber key doesn’t exist in Marketing Cloud**.

**[Note 2]**  
Messages are sent using the **Transactional API**, meaning all messages will be sent as transactional sends. Therefore, **emails will still be sent even if the subscriber status in Marketing Cloud is “Unsubscribed”**.

**[Note 3]**  
The HTML preference follows the settings in Marketing Cloud. If the HTML preference is set to HTML, an HTML email is sent; if set to TEXT, a plain text email is sent.

**[Note 4]**  
If you edit the email template in Content Builder, emails will continue to send with the content of the template as it was when the Data Action Target was initially configured.

If you modify an existing email template and **want to send another email, create another data action target** with the updated email template.

**[Note 5]**  
HTML emails automatically include “Click here to view this email as a webpage” at the top.

**[Note 6]**  
**Only personalization strings that correspond to profile attributes in “All Subscribers” can be used in the selected email template**. To manage these attribute values, use the Import Activity in Automation Studio.

If an error occurs when saving the Data Action Target, it’s likely that the personalization strings in the selected email template do not match the attribute names in “All Subscribers” profile attributes.

![]()

This is similar to how Marketing Cloud Connect checks personalization strings when sending from Sales Cloud or Service Cloud through Marketing Cloud. You might have seen a “Callout Exception: 400 — Bad Request” error in the preview screen before sending. This is the Data Cloud version of that process, and **syntax checks are performed instantly**.

For example, if the profile attribute “Last Name” is specified as “Last Name” but is used as `%%LastName%%` (without a space) in the content, this will cause an issue.

This Data Action enables seamless interaction between Data Cloud and Marketing Cloud based on data changes, optimizing customer engagement. Please make full use of this feature.

Thank you for reading.

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
