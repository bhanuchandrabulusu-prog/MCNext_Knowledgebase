# SFMC Tips #75 : Understanding the Wait By Attribute Activity in Journey Builder

**Source:** https://medium.com/@marketingcloudtips/understanding-the-wait-by-attribute-activity-in-journey-builder-6f26b95f1df6

---

# SFMC Tips #75 : Understanding the Wait By Attribute Activity in Journey Builder

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--6f26b95f1df6---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--6f26b95f1df6---------------------------------------)

4 min read

·

Jan 30, 2025

--

Photo by [Boris Smokrovic](https://unsplash.com/@borisworkshop?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

In this article, I will explain the **Wait By Attribute** activity, one of the wait activities in Journey Builder. This activity specifically uses **date-type attributes**.

### Common Use Cases

Here is an example scenario where this activity is useful:

Suppose I have multiple events scheduled as follows:

- **Event 1**: May 29, 2025 (Wed) at 3:00 PM
- **Event 2**: May 30, 2025 (Thu) at 1:00 PM
- **Event 3**: May 31, 2025 (Fri) at 6:00 PM

When a contact registers for any of these events, a **welcome email (first email)** is sent immediately.

Later, on the **morning of the event date at 9:00 AM**, a **reminder email (second email)** is sent to each event participant.

- **Event 1**: Reminder email sent on May 29, 2025 (Wed) at 9:00 AM
- **Event 2**: Reminder email sent on May 30, 2025 (Thu) at 9:00 AM
- **Event 3**: Reminder email sent on May 31, 2025 (Fri) at 9:00 AM

In this type of scenario, the Wait By Attribute activity can be used between the first and second emails, allowing each contact to wait until a specific date.

### Key Characteristics of Wait By Attribute Activity

The Wait By Attribute activity can be configured to use either “Contact Data” or “Journey Data”.

And its primary characteristic is as follows:

- When a contact reaches this activity, it evaluates the date field specified in the selected “Contact Data” or “Journey Data”.
- Even if “Contact Data” is used, the expiration date is **locked** based on the value in the referenced date field. **Once determined, it remains unchanged**.

In other words, the expiration date must already be defined before the contact enters the Wait By Attribute activity.

## Considerations

### 1. Multiple Entries

If the same contact enters the journey multiple times, the wait deadline will be evaluated separately for each entry. A date fixed during the first entry will not apply to subsequent entries.

### 2. Blank or Past Dates

If the referenced date field is blank or contains a past date at the time the contact reaches this activity, the contact will **bypass** the activity without waiting.

### 3. Using Birthdates

Birthdates are a typical example of pre-determined date data. For scenarios like “Wait until X days before the birthdate”, keep in mind that all birthdates are in the past. For instance, a birthdate of “September 1, 1990” needs to be transformed into a future date (e.g., “September 1, 2025”) using SQL or another method.

### 4. Time Settings

If the date field contains only a date without a time, the wait activity will default to **12:00 AM** (midnight!!) for sending messages.

To avoid this, you should configure the setting “**Extend wait duration until specific time**” to specify the desired send time.

### 5. Contact Data Behavior

If the “Contact Data” in Contact Builder contains multiple date records for the same contact, the **first date** retrieved will be used.

For example: If a contact has multiple records like the following in the data extension.

![]()

The system will adopt the first date (“February 5, 2025”) for the wait activity for BOR501.

To ensure the correct date is used, consider storing the dates in the **entry source data extension** and using them as “**Journey Data**” instead.

### 6. Duration Settings

When using the “**Duration**” setting, calculations like adding or subtracting days will apply even to past dates.

On the other hand, the “**Extend wait duration until specific time**” setting will only apply to times **after the contact reaches the activity**.

### Example

Here’s a specific example:

- Arrival at Wait By Attribute activity: February 1 at 2:00 PM
- Date field value: January 15 at 12:00 AM
- Duration setting: 5 days later
- Extended wait duration setting: 10:00 AM

In this case:

- Adding 5 days to January 15 results in **January 20 at 12:00 AM**, a past date.
- The contact would normally bypass the activity, but the extended wait duration setting ensures the activity ends at **February 2 at 10:00 AM**.

### 7. Using Real-Time Data

If you require near real-time data, consider the following:

- Use the **Wait Until Event** activity.
- Split the latter part of the scenario into a new journey that entries when the necessary date is updated.

I hope this guide helps you effectively utilize the Wait By Attribute activity in your Journey Builder scenarios!

Thank you for reading!

Stay tuned for more Salesforce Marketing Cloud tips! 😊

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
