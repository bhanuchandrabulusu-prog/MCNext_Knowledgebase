# SFMC Tips #72 : Error Handling with AMPscript: The RaiseError Function

**Source:** https://medium.com/@marketingcloudtips/error-handling-with-ampscript-the-raiseerror-function-10c4fb343173

---

# SFMC Tips #72 : Error Handling with AMPscript: The RaiseError Function

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--10c4fb343173---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--10c4fb343173---------------------------------------)

4 min read

·

Jan 9, 2025

--

Photo by [Priscilla Du Preez 🇨🇦](https://unsplash.com/@priscilladupreez?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

In this article, I will explain the **RaiseError** function, which plays a crucial role in error handling during email sends. By using this function, you can skip sending emails that contain empty personalization variables, invalid data, or missing data.

Ideally, you should design your processes to avoid needing the **RaiseError** function. However, if you want to achieve safer email sending, consider utilizing this function.

## Syntax of the RaiseError Function

```
① RaiseError('Text displayed on error') <--- Currently not functioning as expected    
② RaiseError('Text displayed on error', False) <--- Currently not functioning as expected    
③ RaiseError('Text displayed on error', True)
```

[## Salesforce Developers

### Utility Functions

developer.salesforce.com](https://developer.salesforce.com/docs/marketing/marketing-cloud-ampscript/references/mc-ampscript-utilities/mc-ampscript-reference-utilities-raise-error.html?source=post_page-----10c4fb343173---------------------------------------)

### Example Usage of the RaiseError Function

If data is found, the “Event Name” is retrieved from the `Event_Data` data extension and displayed. If no data is found, the send for that subscriber is skipped.

```
%%[  
SET @event = Lookup('Event_Data', 'Event', 'Id', _SubscriberKey)  
  
IF EMPTY(@event) THEN  
    RaiseError(CONCAT("Event not found for the given SubscriberKey: ", _SubscriberKey), true)  
ELSE  
    /* Output the value if data exists */  
    SET @message = CONCAT("Event Name: ", @event)  
ENDIF  
]%%  
  
<!-- Display @message if data is found -->  
%%=v(@message)=%%
```

## When Set to False

If you specify `False` as the second parameter, the entire job will stop when an error occurs. If no second parameter is provided, the default is also `False`.

With this setting, the send is aborted at the point where the error occurs, and no further emails are sent. However, all emails sent before the error are delivered successfully.

⚠️ **2022 — Present:**  
A bug currently causes the behavior to deviate from expectations. Even if `False` is specified, the job does not stop at the point of error. Instead, the email send process continues to retry and sends emails to subsequent subscribers, acting as if `True` were specified.

### Details of the Known Issue:

Salesforce has acknowledged the following discrepancy:

> *The documentation states that when the second parameter of the RaiseError function is set to* `False`*, the job should stop at the error and prevent further sending. However, due to internal retry processes, the job does not stop immediately and continues sending subsequent emails.*

This issue is documented in the [Known Issue here](https://issues.salesforce.com/issue/a028c00000j5kCwAAI/).

### Considerations When Set to False

- In Email Studio, the tracking status of the job will initially appear as “In Progress”. When the job stops due to an error, the status will update to “Canceled”.
- Subscribers excluded due to the error will not appear in the **Not Sent Extract** because no sending attempts were made for these subscribers.
- The error text specified in the AMPscript will appear during the **Preview and Test Send** phases.
- If you configure the **Alert Manager**, you will receive an email titled **“Email Send Job Canceled”**. The “**Additional Error Details**” section of this email will include the error text specified in the AMPscript.

## When Set to True

If you specify `True` as the second parameter, only the subscriber with the error will be excluded, and the job will continue sending emails to subsequent subscribers.

### Considerations When Set to True

- Email Studio Sends: The job status in tracking changes from “In Progress” to “Complete”.
- Subscribers excluded due to errors will appear in the **Not Sent Extract** with the reason labeled as “**Send Failure**”. However, the error text specified in the AMPscript will not appear in the extract report.
- **Journey Builder Sends:** The total number of subscribers excluded due to errors will be displayed in tracking.

⚠️ Unlike with `False`, the **"Email Send Job Canceled"** alert will not be sent for errors when using `True`.

## Behavior of Error Text Display

The error text specified in the AMPscript appears in the following scenarios:

1. During **Preview and Test Sends** in Email Studio.

2. In the **Additional Error Details** section of the **“Email Send Job Canceled”** alert email (when using `False`).

By configuring the **Alert Manager**, you can receive emails like “Email Send Job Canceled” with the error details included.

For other error types managed through the Alert Manager, see:

[## Help And Training Community

### Edit description

help.salesforce.com](https://help.salesforce.com/s/articleView?id=000393037&type=1&source=post_page-----10c4fb343173---------------------------------------)

## Best Practices and Recommendations

- **Minimize Errors:**  
  Validate and prepare data beforehand to reduce the need for error handling. The best approach is to design your processes to avoid using the **RaiseError** function entirely.
- **Be Aware of the False Parameter Bug:**  
  Given the current bug with `False`, make sure you test thoroughly to avoid unexpected behavior.

By incorporating the **RaiseError** function, you can achieve safer email operations. However, the ultimate goal should always be to proactively prevent errors through careful planning and design.

Stay tuned for more Salesforce Marketing Cloud tips! 😊

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
