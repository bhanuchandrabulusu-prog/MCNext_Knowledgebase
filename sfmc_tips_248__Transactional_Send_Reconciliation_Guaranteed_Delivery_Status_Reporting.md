# SFMC Tips #248 : Transactional Send Reconciliation: Guaranteed Delivery Status Reporting

**Source:** https://medium.com/@marketingcloudtips/transactional-send-reconciliation-guaranteed-delivery-status-reporting-a0877520c3e3

---

# SFMC Tips #248 : Transactional Send Reconciliation: Guaranteed Delivery Status Reporting

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--a0877520c3e3---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--a0877520c3e3---------------------------------------)

6 min read

·

Feb 12, 2026

--

Photo by [PhilCreates](https://unsplash.com/@philcreates?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

In the [**Summer ’25 new feature release**](/p/6af46f09309e) **of Marketing Cloud Engagement**, a new **“Sendable Reconcilable Data Extension” data extension template** was introduced.

This enables you to **track and record the delivery results (sent / not sent) of transactional emails and SMS**, such as order confirmations and shipping notifications.

Delivery status is stored in the new data view **“Reconcilable Disposition (\_ReconcilableDispositionView)”**, where you can specify **any time window up to 72 hours**.

By leveraging this feature, you can more accurately understand message delivery success or failure, and strengthen operations such as delivery monitoring, troubleshooting, and resend control.

> ***Note:*** *Although this feature was released in Summer ’25 and appeared in the transactional email UI for about six months, it did not actually function. It is now finally officially available.*

### Example Use Cases for the 72-Hour Time Window

The time window can be selected from **1 hour to 72 hours**, depending on business process needs.

- For example, in business processes that prioritize immediacy — such as **checking delivery status immediately after sending an order confirmation email and notifying via another channel if not delivered** — a shorter time interval should be set.
- On the other hand, for use cases such as **weekly or monthly reporting, or aggregating data over a certain period for regulatory reporting**, where immediacy is less critical, a longer time interval can be configured.

### Supported Send Methods

- Email Studio send definition emails
- Automation Studio email activities
- Journey Builder email activities
- (REST API) Transactional send journeys

### Considerations When Using This Feature

- By setting the send classification to **“Transactional”** in **Message Settings**, the **“Transactional Reconciliation”** configuration appears in the **Delivery Options** section.
- Within **Delivery Options**, you can enable **Transactional Reconciliation** for each email activity.
- The default time window is **12 hours**, meaning data is saved to the data view within 12 hours after delivery.
- If message processing is not completed within the time window, the message is marked as **expired**, preventing delivery after the specified period.
- For Journey Builder sends, enable **High Throughput Sending (HTS)**.  
   (\**HTS is not available in Hyperforce environments.*)
- The **MessageKey** of sent messages is automatically added to the **Sendable Reconcilable Data Extension template**. If left blank, the system generates a MessageKey at send time.
- The **MessageKey** value is kept unique for 72 hours. If, for any reason, the same message is sent to Salesforce multiple times, Salesforce will process and send it only once.

> ***Important:*** *In Transactional send journeys,* ***Sendable Reconcilable Data Extensions cannot be selected due to specifications****. Therefore, create the data extension using the* ***Triggered Send Data Extension template*** *instead. The transactional sending mechanism works correctly even when using this template.*
>
> *Also, in a* ***Triggered Send Data Extension****, the* ***messageKey field is not required****. If you want to store messageKey in the data extension, include messageKey in the* ***attributes*** *as well.*

### Example of a Transactional Send Journey

```
{  
  "definitionKey": "reservation_api",  
  "recipients": [  
    {  
      "contactKey": "BOR501",  
      "messageKey": "reservation_202602200001",  
      "to": "n.watanabe@nac-plus.co.jp",  
      "attributes": {  
        "CustomerName": "Nobuyuki Watanabe",  
        "ReservationDate": "2026-02-20T19:00:00",  
        "StoreName": "NAC-Plus Shibuya",  
        "MessageKey": "reservation_202602200001"  
      }  
    }  
  ]  
}
```

## Reconcilable Disposition Data View

Using this data view, you can confirm per subscriber:

✅ Whether it was actually sent  
✅ Whether it only entered the queue  
✅ Whether it failed to send due to an error  
✅ Failure reason (error code / details), e.g., missing required values

In other words, you can verify the **final delivery status (Disposition)**.

### Where Can It Be Used?

You can use it in **Automation Studio Query Activity**.

```
SELECT  
    JobId,  
    Channel,  
    Disposition,  
    MessageKey,  
    SubscriberKey,  
    SubscriberId,  
    ErrorCodeId,  
    ErrorName,  
    StartTime  
FROM _ReconcilableDispositionView
```

### ⚠ Notes

Retention period is **7 days only**.

If long-term storage is required, export to a data extension.  
→ Automation of log storage is recommended.

> *Currently, “****ErrorDescription****” is excluded from the query above because it is returned only during errors.*

## Available Fields

### ① JobId

Identifier of the send job.  
Determines which send job it belongs to.

### ② Channel (delivery channel)

Indicates the channel used for sending.

- 0 = Email
- 1 = SMS

For normal email sends, **0 (Email)** is stored.

### ③ Disposition (delivery status)

The most important field, representing the final result per subscriber.

- 0 = Queued
- 1 = Sent
- 2 = NotSent

**Examples:**

- Extract Sent → confirm actual delivery count
- Extract NotSent → analyze errors

### ④ MessageKey

Key used to match with the customer’s system.  
Can be specified during API or triggered sends.

This enables accurate reconciliation between:

> *Marketing Cloud results = your system’s send logs*

This is extremely important for external system integrations.

### ⑤ SubscriberKey

Subscriber key defined by your system.  
Used for standard send analysis and joining with existing data extensions.

### ⑥ SubscriberId

Unique internal ID in Marketing Cloud.  
⚠ May be NULL for invalid subscribers.

### ⑦ ErrorCodeId / ErrorName / ErrorDescription

Detailed information for send failures. Populated when NotSent.

Examples:

- Invalid email address
- Suppression
- Bounce
- System error

Useful for troubleshooting and improving delivery quality.

### ⑧ StartTime

Send start time.  
Meaning varies by send method.

- For data extension sends:  
  → Time when the job started
- For API sends:  
  → Time when the API request was received

Useful for verifying real-time send timing.

## How to Create the Data Extension

1. Select **“Create from Template”** when creating a new sendable data extension.

2. Select **“Sendable Reconcilable Data Extension”.**

3. SubscriberKey and MessageKey are prepared by default. Add any other fields needed for your transactional emails.

> *This data extension is used as the entry source.*

## Conclusion

This new data view **(\_ReconcilableDispositionView)** is an **official log that guarantees, per subscriber, whether messages were truly delivered.**

It will likely become essential especially for:

- **Transactional emails**
- **API sends**
- **External system integrations**
- **Delivery audits**
- **Send error analysis**

Compared to the standard **\_Sent** data view, it is easier to understand if you remember it as a **data view specialized for guaranteed results and reconciliation purposes.**

Finally, according to [**Lukas Lunow**](https://digitalmarketingoncloud.com/)-san, a Marketing Cloud expert:

> *One needs to add that while this new data view tells you about a successful send, it can’t confirm that the message actually made it to the recipient’s inbox. It might still be silently rejected by spam filters, routed to the junk mail folder, or even disappear altogether.*

That’s absolutely true. It was a very important and valuable insight.

That’s all for today.

Stay tuned for more Salesforce Marketing Cloud tips! 😎

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
