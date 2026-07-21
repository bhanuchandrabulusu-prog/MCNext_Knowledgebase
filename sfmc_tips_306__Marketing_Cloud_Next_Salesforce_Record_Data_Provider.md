# SFMC Tips #306 : Marketing Cloud Next: Salesforce Record Data Provider

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-next-salesforce-record-data-provider-df07d9206206

---

# SFMC Tips #306 : Marketing Cloud Next: Salesforce Record Data Provider

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--df07d9206206---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--df07d9206206---------------------------------------)

4 min read

·

Jun 10, 2026

--

Photo by [Kevin Schmid](https://unsplash.com/@lighttouchedphotography?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

The [Summer ’26 release](/@marketingcloudtips/marketing-cloud-next-summer-26-release-highlights-04f6c5abdee6) for Marketing Cloud Next Growth & Advanced Editions introduced merge fields that can use a new data source called “**Salesforce Record”**.

*\*This feature is referred to as the “****Record Data Provider”****.*

This feature caught my attention, and after testing it in Segment Flows, List Flows, and Record Query Flows, I found that its behavior was somewhat different from what I had originally expected. I would like to share those findings here.

## My Initial Impression

When I first saw this feature, I thought:

*“A powerful new data source has arrived that allows completely flexible, customer-level personalization using Salesforce records.”* 🎉

However, after actually using it, that impression changed significantly. 🤔

## Verifying the Actual Behavior

This feature retrieves the value of the **record that has the most recent Last Modified Date** for a specific field within Salesforce records.

Furthermore, that value is displayed **to everyone**, not individually for each recipient.

For example, let’s use the **First Name** field from the Lead object as a merge field.

- You must configure at least one search condition.
- If multiple conditions are specified, only **AND** conditions are supported.

![]()

![]()

If the First Name of the most recently updated Lead record is **“Nobuyuki”**, then **every recipient** will see “Nobuyuki” in the email, regardless of who the email is sent to.

![]()

## Everyone Receives First Name = Nobuyuki

This feature **cannot be used for customer-level personalization**.

If used incorrectly, there is a risk of displaying the wrong customer name to all recipients.

Therefore, if you need recipient-specific personalization, you must continue using the following methods:

- **Data Graph**
- **Content Variables**
- **Apex**

## Use Cases for This Feature

So, what kinds of scenarios can this feature actually support?

One use case I thought of is inserting **shared information that is managed as a single record in CRM** into emails.

For example, a system maintenance announcement.

- Maintenance Start Date and Time: July 1, 2026 22:00
- Maintenance End Date and Time: July 2, 2026 05:00
- Announcement Title: Scheduled System Maintenance

![]()

Normally, whenever the maintenance schedule changes, you would need to update the email content.

However, if this information is managed as a CRM record, you can simply update the CRM fields and have the changes reflected in the email automatically.

![]()

![]()

In a sense, it can be used similarly to the **AMPscript Lookup function**.

Replace the CRM data.

![]()

The email content changes easily.

## Be Careful: It Does Not Necessarily Mean “Latest Record”

However, even for this use case, there is an important limitation.

For example, suppose you manage information such as **“Latest Seminar Date”** using multiple records.

Although this feature supports filtering, it does **not** provide a way to sort records by a specific field.

As a result, even if a seminar record contains outdated information, if someone updates that record, its Last Modified Date becomes the most recent, and the email may display old seminar information.

In other words, this feature is:

- **Not a feature that retrieves the latest record.**
- **It is a feature that retrieves the last updated record.**

This distinction is extremely important.

## Final Thoughts

What do you think?

To be honest, my impression at this point is that the practical use cases for this feature are fairly limited.

However, it may still be useful when you want to:

- Manage values that are shared by all recipients
- Manage content from CRM without editing email content
- Reference configuration information stored in a single CRM record

If I discover additional compelling use cases that are uniquely suited to this feature, I will be sure to share them in a future article.

That’s all for this time.

Stay tuned for more Salesforce Marketing Cloud tips! 😎

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
