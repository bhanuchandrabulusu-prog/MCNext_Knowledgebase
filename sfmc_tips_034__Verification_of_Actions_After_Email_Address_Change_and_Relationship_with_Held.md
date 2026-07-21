# SFMC Tips #34 : Verification of Actions After Email Address Change and Relationship with “Held”…

**Source:** https://medium.com/@marketingcloudtips/verification-of-actions-after-email-address-change-and-relationship-with-held-status-7b25d282a9cb

---

# SFMC Tips #34 : Verification of Actions After Email Address Change and Relationship with “Held” Status

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--7b25d282a9cb---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--7b25d282a9cb---------------------------------------)

4 min read

·

Mar 22, 2024

--

Photo by [Ruben Christen](https://unsplash.com/@ruben_christen?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

In Salesforce Marketing Cloud, the “Held” status refers to a status where, after one or several bounces resulting from email delivery, it is determined that delivery to that email address should be stopped. **When a subscriber is in the “Held” status, no further email sending processing occurs**.

So, what happens to a subscriber’s “Held” status in Salesforce Marketing Cloud after they change their email address?

- **Does it remain in the “Held” status?**
- **Or does it change to an “Active” status?**

We will verify three actions within Salesforce Marketing Cloud to determine the outcome:

## Verifications

**1: Manually swapping the email address in subscriber properties.  
2: Importing a new email address using Automation Studio.  
3: Sending using Journey Builder with a new email address.**

*\*Verification 3 will send using Journey Builder with the setting of “****Use email attribute from Entry Source****” for the “Default Email Address” in place.*

Let’s go through each verification step.

## Verification 1: Manually swapping the email address in subscriber properties.

We’ll prepare a subscriber in the “Held” status and proceed to change their email address in the properties as shown below. Then, we’ll click the OK button.

![]()

Upon doing so, we see that the status has changed to “Active”. It seems that using this method automatically changes the status to “Active”.

![]()

## Verification 2: Importing a new email address using Automation Studio.

Next, we’ll use Automation Studio’s import activity to import a CSV file from an SFTP to all subscriber lists.

The destination configuration for the import activity in Automation Studio is as follows:

The item names to be used in the CSV file placed in the SFTP import directory are as follows:

- Subscriber Key
- Email Address

Please use these item names if you want a perfect match. There will be a space between words.

We will then import two scenarios:

- Subscriber ROR502 has changed their email address.
- Subscriber ROR503 has not changed their email address.

![]()

We will execute the import activity for these two held subscribers.

![]()

The result of the import is as follows: **the status remains “Held” for both cases**. In other words, importing different email addresses for all subscribers does not affect their status.

![]()

## Verification 3: Sending using Journey Builder with a new email address.

Lastly, we’ll store the new email address in the Journey Builder’s entry source data extension and select “***Use email attribute from Entry Source***” in the “Default Email Address” setting before sending.

![]()

We’ll create an entry source and a journey as shown below and send it to the “Held” status subscribers.

![]()

Upon sending, **we observe that the status changes to “Active”**, similar to Verification 1. This indicates that overwriting with a different email address affects the status. Of course, an email has also been sent.

![]()

## In summary:

- Verification 1: Changing email address manually in subscriber properties **changes the status from “Held” to “Active”**.
- Verification 2: Importing a new email address through Automation Studio **does not change the status; it remains “Held”**.
- Verification 3: Sending using Journey Builder with a new email address **changes the status from “Held” to “Active”**.

Was this as expected?

Regarding the issue where the status remains “Held” when importing through Automation Studio, **to change the status, you can create a “Status” field in the CSV with values of “Active” and import it alongside the email addresses**.

- Subscriber Key
- Email Address
- Status

![]()

*\*****Using Automation Studio to activate subscribers requires a mechanism to extract only the records with changed email addresses****. Activating all records could lead to reactivating invalid email addresses, causing future bounces and affecting delivery rates. Always collaborate with Marketing Cloud developers for such tasks.*

That concludes our verification process.

Thank you for reading.

Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
