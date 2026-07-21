# SFMC Tips #67 : Common Pitfalls in Marketing Cloud Connect

**Source:** https://medium.com/@marketingcloudtips/common-pitfalls-in-marketing-cloud-connect-36f34db6b85a

---

# SFMC Tips #67 : Common Pitfalls in Marketing Cloud Connect

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--36f34db6b85a---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--36f34db6b85a---------------------------------------)

10 min read

·

Dec 6, 2024

--

Photo by [Philip Veater](https://unsplash.com/@veato?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

Marketing Cloud Connect, the connector used to integrate Salesforce CRM with Salesforce Marketing Cloud, comes with its own set of potential challenges. This article compiles key “pitfalls” to help you during setup and troubleshooting.

## Table of Contents

1. **Three Objects That Are Billed as Contacts**
2. **Formula Fields Cannot Be Used in Sync Filters**
3. **Synced Objects Cannot Be Unsynced Once Linked**
4. **Not All Records Are Always Synced**
5. **Objects or Fields Are Not Displayed in the Sync Field Selection Screen**
6. **Changes to Field Lengths in CRM Do Not Reflect in MC**
7. **Changing Field API Names in CRM Breaks the Integration**
8. **The Difference Between Date and Datetime Fields**
9. **Troubleshooting “An Exception Occurred While Saving the Integration”**
10. **Lead Conversion is Not Supported**
11. **Unable to View “Email Thumbnails” in Individual Email Results**

### 1. Three Objects That Are Billed as Contacts

In Marketing Cloud, the following three objects are counted as billable contacts:

- **Contact**
- **Lead**
- **User**

When these objects are synced with Marketing Cloud, they are automatically counted as billable contacts.

**⚠️ Notes on Contact Builder**  
When integrating various objects in Contact Builder, the **Contact**, **Lead**, and **User** objects are treated as “prerequisites”, meaning they may need to be integrated beforehand.

Even within **Data Designer**, these objects serve as the foundational elements of the MCC data model.

- The MCC data model is automatically generated when Marketing Cloud Connect is configured. Using this MCC data model allows you to leverage synced data extensions in “decision splits” and “exit conditions” immediately.
- Apart from the Contact, Lead, and User objects, there are “intermediate table” objects in the MCC data model. These may act as prerequisites when integrating other objects. Which objects serve as prerequisites is determined automatically by the system, so follow the system prompts to complete the integration.

However, if you start syncing Contact, Lead, or User objects without careful planning, they will be counted as billable contacts as soon as the sync begins.

**Recommendation**  
To control the records synced to Marketing Cloud, configure filters on the CRM side using a checkbox (Boolean) field before setting up the sync.

For instance, create a field like `MC_connect__c` to manage the sync:

- Make sure the checkbox field is selected as a target field for syncing; otherwise, it cannot be used in the “sync configuration”.

If you do not use the MCC data model, the prerequisite objects can be synced even if they have zero records. However, note that these objects cannot be used in decision splits or exit conditions because their absence will cause errors.

### 2. Formula Fields Cannot Be Used in Sync Filters

In sync configuration filters, checkbox fields created with formulas cannot be used. These fields do not appear in the dropdown list of filter options. Instead, use standard checkbox fields.

This limitation was changed in the Spring ’23 release.

[## Help And Training Community

### Edit description

help.salesforce.com](https://help.salesforce.com/s/articleView?id=000394026&type=1&source=post_page-----36f34db6b85a---------------------------------------)

While formula checkbox fields cannot be used in filters, their data is correctly synced to synchronized data extensions, so there is no issue with using the data itself.

### 3. Synced Objects Cannot Be Unsynced Once Linked

Once a specific object is synced with Marketing Cloud, the sync cannot be canceled or removed.

**To remove the sync:**  
You must disconnect Marketing Cloud Connect, which will reset all object integrations.

**Key Considerations:**

- **Manual reconfiguration required:** After reconnecting, you must manually reconfigure the integration fields for each object.
- **Automation errors:** Forgetting to reconfigure fields used in SQL query activities after reconnecting can cause automation errors.
- **Solution:** Run each automation manually once to confirm proper operation after reconfiguration.

This behavior is documented in Salesforce Help:

[## Help And Training Community

### Edit description

help.salesforce.com](https://help.salesforce.com/s/articleView?id=000384349&type=1&source=post_page-----36f34db6b85a---------------------------------------)

*If you would like to delete a single synchronized object, this currently is NOT possible. The only way to remove entities from the UI is to disconnect your integration. This will then remove any data extensions and associated attribute group that were synced.*

### 4. Not All Records Are Always Synced

The sync timing can be set to intervals of 15 minutes, 30 minutes, or 1 hour.

During these intervals, only **new records** and **records with an updated Last Modified Date** in Salesforce CRM are synced to Marketing Cloud.

The key point here is that for updates, **only records with a changed Last Modified Date** are considered, and only those are synced.

### What is the “Last Modified Date”?

This refers to the **last modified timestamp** of the system audit fields in Salesforce CRM.

![]()

Therefore, the synchronization intervals of “15 minutes”, “30 minutes”, or “1 hour” correspond to records updated within **the last 15 minutes, 30 minutes, or 1 hour** based on the Last Modified Date.

For example, if the synchronization interval is set to “15 minutes”, it means that any changes made to the records will be synced by **2024/12/5 17:12**.

### Causes of Data Discrepancies Between Salesforce CRM and Marketing Cloud

Occasionally, discrepancies may arise between data in Salesforce CRM and Marketing Cloud. In most cases, this is due to updates that **do not trigger a change in the Last Modified Date**.

To troubleshoot data discrepancies, first check if the **Last Modified Date** has been updated in Salesforce CRM.

### Why Doesn’t the “Last Modified Date” Update?

Although a bit outdated, the following Salesforce Help document provides some insights:

[## Help And Training Community

### Edit description

help.salesforce.com](https://help.salesforce.com/s/articleView?id=000385707&type=1&source=post_page-----36f34db6b85a---------------------------------------)

I am not an expert on Salesforce CRM, but one common scenario involves updates to **related object fields** causing changes to **formula fields**, which do not trigger an update to the Last Modified Date.

For example, in the relationship between the Opportunity and Account objects:

- A formula field, `Account_Industry__c`, is created in the Opportunity object.
- This field references the **Industry** field in the related Account object with the formula: `TEXT(Account.Industry)`
- When the **Industry** field in the Account object is updated, the value of the formula field `Account_Industry__c` in the Opportunity object changes.

However, the **Last Modified Date** of the Opportunity record remains **unchanged**.

As a result, the updated value of `Account_Industry__c` is **not synced**, leading to discrepancies between Salesforce CRM and Marketing Cloud.

### 5. Objects or Fields Are Not Displayed in the Sync Field Selection Screen

Access (or visibility) to **objects** and **fields** in Marketing Cloud depends on the **permissions of the API user** in Salesforce CRM (the user used for the integration).

If certain objects or fields are not displayed in the synchronization field selection screen, ensure that the **API user in Salesforce CRM** has the necessary access permissions for those objects or fields. Granting the appropriate permissions should resolve the issue.

Conversely, be cautious: for example, if the **Field-Level Security** for the API user in Salesforce CRM is accidentally unchecked and saved, the integration with Marketing Cloud will be disrupted.

Make sure to handle these settings with care to avoid breaking the connection.

### 6. Changes to Field Lengths in CRM Do Not Reflect in MC

To illustrate this issue: imagine a custom field, **URL\_\_c**, in the Opportunity object with a field length of 100.

![]()

### Example Scenario:

1. When this field is synced to Marketing Cloud (MC), its length is set to **100** in MC as well.

2. Later, you decide to add parameters to the URL values and increase the field length in CRM to **255 characters**, saving the changes.

3. However, when you check the synced field in MC, the field length remains **100**. Any text exceeding the 100-character limit will not be synced.

### How to Adjust the Field Length in MC:

To change the field length from **100** to **255** in MC, you need to temporarily disable the field synchronization:

1. In Contact Builder, deselect the field’s checkbox in the synchronization settings and save the changes to **break the field’s sync**.
2. Reload the Contact Builder page, and then re-access the synchronization settings.
3. After refreshing, the field length in MC should now display as **255**.
4. Re-enable the synchronization for this field, and it will accept text longer than 100 characters.

By following this process, the field length change will be applied, and text exceeding the original limit will be properly synced moving forward.

### 7. Changing Field API Names in CRM Breaks the Integration

For example, let’s say the field **URL\_\_c** is already synchronized with Marketing Cloud (MC).

### Scenario:

1. In Salesforce CRM, you rename this field from **URL** to **URL2**.

2. During the renaming process, you might encounter a warning message, but if you proceed and ignore it, the API reference name of the field will be updated in CRM.

3. After making this change, if you check the synchronization in MC, you’ll find that the field is no longer visible in the synced data extension.

### Implications:

- While it’s possible to re-establish the synchronization manually, leaving the field unsynchronized may lead to **automation errors**.
- In some cases, the renamed field might still appear in the synced data extension in MC. However, on the backend, the field has been effectively **removed**. If any record in CRM triggers a data update for that field, the field will disappear from the synced data extension in MC, making it unavailable.

### Best Practice:

After renaming a field in Salesforce CRM, promptly update the synchronization settings in MC to reflect the changes. This will prevent potential errors and ensure smooth data flow between CRM and MC.

## 8. The Difference Between Date and Datetime Fields

There is a difference in how **Date** and **Datetime** types are handled in Salesforce CRM and Marketing Cloud. Not understanding this distinction can lead to unexpected results during data synchronization and usage. Here is the conclusion:

### For Date Type:

- **CRM:** December 1st, 12:00 AM
- **Marketing Cloud:** December 1st, 12:00 AM

### For Datetime Type:

- **CRM:** December 1st, 12:00 AM
- **Marketing Cloud:** November 30th, 9:00 AM

This means that for **Datetime** types, there is a 15-hour difference in synchronization, assuming the **JST time zone**, as they are synchronized in the **CST time zone**.

### Example:

In Salesforce CRM, the following values are entered:

- The top field is **Date** type.
- The bottom field is **Datetime** type.

When these values are synced with Marketing Cloud, the following discrepancies are observed:

- The **Date** value remains the same in both systems.
- The **Datetime** value is adjusted by the time zone difference.

![]()

## 9. Troubleshooting “An exception occurred while saving the integration”

This is a well-known error that occurs when attempting to connect to Salesforce CRM using **Marketing Cloud Connect**.

For detailed troubleshooting, please refer to Salesforce’s official help documentation.

[## Help And Training Community

### Edit description

help.salesforce.com](https://help.salesforce.com/s/articleView?id=000380463&type=1&source=post_page-----36f34db6b85a---------------------------------------)

## 10. Lead Conversion is Not Supported

In Salesforce CRM, when a Lead is converted, the Lead in Marketing Cloud is not automatically transformed into the Contact. These are treated as entirely separate entities within Marketing Cloud.

A common question is whether engagement data from the Lead can be transferred to the Contact. Unfortunately, this is not possible.

Even if a Lead is no longer needed, it will remain in Marketing Cloud as a “Billable Contact”. If it is unnecessary, you will need to delete it. However, please note that deleting it will also erase all engagement data associated with the Lead.

Additionally, extra caution is required when using the synchronized data extension for Leads to delete contacts. If there are converted records, you may inadvertently delete the Contact.

This is due to a mechanism called [ContactAlternateKeyStore (CAKS)](https://help.salesforce.com/s/articleView?id=000389954&type=1). In this system, the \_ContactKey is replaced from the Lead’s ID to the account Contact’s ID. As a result, deleting the Lead from the synchronized data extension could also delete the Contact linked to the SubscriberKey.

For more details, please refer to the help documentation below.

[## Help And Training Community

### Edit description

help.salesforce.com](https://help.salesforce.com/s/articleView?language=ja&id=000381003&type=1&source=post_page-----36f34db6b85a---------------------------------------)

## 11. Unable to View “Email Thumbnails” in Individual Email Results

In some organizations, while users can access individual email results, the “Email Thumbnails” may not be displayed due to insufficient permissions. To resolve this issue, you can either grant the necessary permissions to the appropriate **Profile** or create a read-only **Permission Set** and assign the required permissions.

### Method 1: Grant Permissions via Profile

1. Navigate to **Setup** and go to **Profiles**.
2. Select the profile you want to grant permissions to.
3. Click **Enabled Visualforce Page Access** and then click **Edit**.
4. Enable the Visualforce page named **et4ae5.ierImage**.

### Method 2: Grant Permissions via Permission Set

1. Navigate to **Setup** and go to **Permission Sets**.
2. Click **New** to create a new Permission Set.
3. Assign an appropriate name to the Permission Set and save it.
4. Select **Visualforce Page Access**.
5. Enable the Visualforce page **et4ae5.ierImage**.
6. Assign the Permission Set to the necessary users.

## Conclusion

By understanding these common pitfalls with Marketing Cloud Connect, you can better manage integration between Salesforce CRM and Marketing Cloud, avoid issues, and ensure a smoother experience.

If anyone who has read this article has encountered other “Pitfalls” in Marketing Cloud Connect, please let us know in the comments section.

That’s it for now. Hope this was helpful!

Stay tuned for more Salesforce Marketing Cloud tips! 😊

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
