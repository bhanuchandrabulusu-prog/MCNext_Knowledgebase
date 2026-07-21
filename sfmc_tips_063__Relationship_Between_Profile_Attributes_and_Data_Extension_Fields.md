# SFMC Tips #63 : Relationship Between Profile Attributes and Data Extension Fields

**Source:** https://medium.com/@marketingcloudtips/relationship-between-profile-attributes-and-data-extension-fields-3edefdc64240

---

# SFMC Tips #63 : Relationship Between Profile Attributes and Data Extension Fields

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--3edefdc64240---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--3edefdc64240---------------------------------------)

5 min read

·

Nov 12, 2024

--

Photo by [Nadi Whatisdelirium](https://unsplash.com/@whatisdelirium?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

When crafting messages tailored to individual customers in Salesforce Marketing Cloud, you might wonder which value is used if profile attribute fields and data extension fields share the same name. Let’s clarify how this works.

### 1. When a Data Extension Field Exists and Has a Value:

⇒ **The data extension value takes precedence**. This allows for flexible personalization, as you can prepare values tailored to specific campaigns and targeting.

### 2. When a Data Extension Field Exists but Its Value is NULL:

⇒ **The profile attribute value is used**. This ensures that even if the data extension lacks information, the profile attribute value is utilized smoothly.

### 3. When the Data Extension Field Does Not Exist:

⇒ **The profile attribute value is adopted**. With profile attribute data in place, basic customer information is always available.

Let’s test this behavior in the Marketing Cloud interface.

Profile attributes can be added, edited, or deleted in the “Profile Management” screen. These attributes apply to “All Subscribers”. Once fields are configured, you can manually input values or import them using Automation Studio.

*\*For subscribers connected through Marketing Cloud Connect where the “****Addition Method****” is set to “****SalesforceSubscriber****”, manual input and imports aren’t possible. Editing must occur on the Salesforce CRM side.*

In this example, the profile attribute Last Name has the value “Watanabe”, and First Name is set to “Nobuyuki”.

In the data extension, however, we’ve created a Last Name field with the Japanese kanji value “渡邊” and left out First Name.

Notice that the Last Name fields in both profile attributes and the data extension have the same name. Let’s confirm how they display in Email Studio’s “Preview & Test”.

As you can see, Last Name is sourced from the data extension field, while First Name comes from the profile attribute.

From this, we’ve verified the following:

**1. When a data extension field exists and has a value (Last Name)**

**3. When the data extension field doesn’t exist (First Name)**

Next, let’s confirm the following:

**2. When a data extension field exists but its value is NULL**

Using Contact Builder, we’ll set the Last Name field to NULL (empty).

In the “Preview & Test”, instead of the NULL value from the data extension field, the profile attribute value is displayed.

As a side experiment, let’s input a space in the Last Name field.

This results in Last Name not being displayed.

This confirms scenario 2.

## About SalesforceSubscriber

One important point to note: As mentioned earlier, when using Marketing Cloud Connect with the “Addition Method” set to “SalesforceSubscriber”, manual input or imports are not possible, and editing must happen on the Salesforce CRM side.

While this allows updates to “All Subscribers” properties for “SalesforceSubscriber”, updating in Salesforce CRM alone may cause display inconsistencies in Marketing Cloud.

To avoid this, take one of the following actions:

### Option 1:

Use a synchronized data extension and schedule regular imports into “All Subscribers” through an Automation Studio import activity.

### Option 2:

After making updates in Salesforce CRM, click the OK button below.

![]()

For “SalesforceSubscriber”, my understanding is that there are “front” and “back” settings:

### “Front” settings:

Updated from the Salesforce CRM side

### “Back” settings:

Updated by manually clicking the OK button or importing into “All Subscribers” through Automation Studio.

Since manually clicking the OK button each time can be impractical, it’s advisable to ensure synchronization between “front” and “back” settings by regularly importing into “All Subscribers” in Automation Studio.

If these “front” and “back” values are not in sync, it could impact email delivery as expected.

![]()

For example, when using attribute data in personalization strings, the applied value may vary depending on the sending method and the “Do Not Update Subscriber values with send time values” checkbox setting.

Below is a summary of which values are used when “front” and “back” settings are inconsistent:

### Behavior with “Addition Method” as “SalesforceSubscriber”

*\*In this case, the “front” data overrides the “back” data in Journey Builder sends, while in Marketing Cloud sends, the “back” data remains unchanged.*

Note that while we refer to it as “back” data, it’s simply the value displayed in the “All Subscribers” list, which may cause inconsistencies with the property screen when the “Addition Method” is “SalesforceSubscriber”.

How was this overview?

As we’ve seen, the relationship between profile attributes and data extension fields works rather seamlessly.

This functionality of profile attributes can still be used, such as when triggering emails using data actions from Data Cloud, as mentioned in the previous article. It’s not an obsolete feature yet! Let’s stay on top of this behavior to avoid delivery errors.

[## SFMC Tips #62 : How to Trigger Journey Builder with Data Actions

### Leveraging Data Cloud’s Data Actions allows you to send emails in Content Builder or start journeys in Journey Builder…

medium.com](/@marketingcloudtips/how-to-trigger-journey-builder-with-data-actions-73d26c5810a7?source=post_page-----3edefdc64240---------------------------------------)

Thank you for reading.

Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
