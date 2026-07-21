# SFMC Tips #64 : Understanding Field Mapping in Marketing Cloud Connect

**Source:** https://medium.com/@marketingcloudtips/understanding-field-mapping-in-marketing-cloud-connect-16c7cc253b29

---

# SFMC Tips #64 : Understanding Field Mapping in Marketing Cloud Connect

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--16c7cc253b29---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--16c7cc253b29---------------------------------------)

4 min read

·

Nov 18, 2024

--

Photo by [Jean-Philippe Delberghe](https://unsplash.com/@jipy32?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

In this article, let’s dive into the field mapping settings in **Marketing Cloud Connect**.

**Trailhead Resource: Marketing Cloud Connect Testing Guide**

[## Marketing Cloud Connect Testing Guide | Salesforce Trailhead

### Learn how to test Marketing Cloud Connect setup successfully. Create field mappings, test connections, and send email…

trailhead.salesforce.com](https://trailhead.salesforce.com/content/learn/modules/marketing-cloud-connect/test-the-connection?source=post_page-----16c7cc253b29---------------------------------------)

The detailed guide on field mapping settings is available on the Trailhead page above. It mentions:

> One of the coolest features of Marketing Cloud Connect is its **automatic synchronization** of data between Marketing Cloud Engagement and Salesforce CRM. To make this work, we need to configure some basic field mapping.

However, this explanation might give the impression that data entered in Marketing Cloud is automatically synchronized to Salesforce CRM and vice versa. This is not the case.

The synchronization applies only to the **properties of** **All Subscribers** in Marketing Cloud when the **Add Method** is set to `SalesforceSubscriber`. Moreover, synchronization flows only in one direction: **from Salesforce CRM to Marketing Cloud**.

![]()

## Key Behavior of the Add Method `SalesforceSubscriber`

When the **Add Method** is set to `SalesforceSubscriber`, you can no longer edit subscriber properties directly in Marketing Cloud.

This happens when a contact or lead is first added to **All Subscribers** via a **Salesforce-originated send**, such as:

- Sending an email from the contact or lead details page
- Sending through a Salesforce report or campaign
- Sending via Journey Builder using Salesforce Data

## **Querying Add Method in Data Views**

The **Add Method** can also be checked using a query in the `_ListSubscribers` Data View. Here’s an example query:

```
SELECT SubscriberKey, AddMethod    
FROM _ListSubscribers    
WHERE SubscriberKey IN ('0035Y00006d4AL0QAM', '0035Y00006ZtxwrQAB')
```

### Classification of Add Method Values

**Automatically synchronized values:**

- `Unknown` (Add Method: `SalesforceSubscriber`)

**Non-synchronized values (examples):**

- `WebApplication` **(Add Method:** `Application`**)**  
  Added manually via All Subscribers.
- `Imported` **(Add Method:** `Import`**)**  
  Imported via Automation Studio.
- `DataExtensionSend` **(Add Method:** `CustomObject`**)**  
  Added through a Data Extension Send.

Since the **Add Method** is determined at the time of the first registration, achieving full control over it is challenging. Regular workflows often involve activities like imports or Data Extension sends before any Salesforce-originated sends take place.

## Synchronizing Values Between Salesforce CRM and Marketing Cloud

To maintain synchronization, ensure that you schedule regular **imports into All Subscribers using Automation Studio**. While this approach might introduce some lag, it resolves discrepancies for all Add Method types.

If this is not synchronized, the drawbacks are as described in my previous article. There is a possibility that unintended values may be sent.

[## SFMC Tips #63 : Relationship Between Profile Attributes and Data Extension Fields

### When crafting messages tailored to individual customers in Salesforce Marketing Cloud, you might wonder which value is…

medium.com](/@marketingcloudtips/relationship-between-profile-attributes-and-data-extension-fields-3edefdc64240?source=post_page-----16c7cc253b29---------------------------------------)

## Benefits of Field Mapping

Now, let’s discuss the advantages of field mapping. Field mapping enables personalization in Salesforce CRM-based Marketing Cloud sends.

When you send emails using **Content Builder** in Marketing Cloud from Salesforce CRM, personalization strings are derived from the **Profile Attributes** stored in **All Subscribers**, rather than relying on Data Extensions or lists.

By mapping Salesforce CRM fields to Marketing Cloud attributes, you can define which CRM data corresponds to specific profile attributes.

## How to Set Up Field Mapping

1. Navigate to **Email Studio** and select **Subscribers > Profile Management**.

2. Create a new attribute and provide a name (e.g., `Last Name`). If your Profile Center is public, ensure the name is user-friendly.

![]()

3. Go to the **Salesforce tab** to link the attribute with a CRM field.

![]()

## Testing the Configuration

The link setup is now complete. Next, let’s create a simple email and test it using the personalization string “%%Last Name%%”.

Then, navigate to the Marketing Cloud “**Email Send**” screen, select the email, and click “Preview Email”.

You’ll see that the last name has been populated.

Success!

### Important Notes

**1. Correct Personalization Syntax:**  
Incorrect usage (e.g., `%%Last_Name%%` or `%%LastName %%`) will cause a “**Callout Exception: 400 — Bad Request**” error in the preview and result in failed sends. Always double-check your personalization strings.

**2. Delay in Updated Values:**  
If you update a field in Salesforce CRM, wait 15–30 minutes before initiating a Marketing Cloud send to ensure the updated values are reflected.

These features involve configuration areas with limited official documentation, so I wanted to document them for reference.

Thank you for reading.

Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
