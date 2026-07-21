# SFMC Tips #80 : Q&A Collection on Interactive Email Forms and Smart Capture

**Source:** https://medium.com/@marketingcloudtips/q-a-collection-on-interactive-email-forms-and-smart-capture-f432ca611c3e

---

# SFMC Tips #80 : Q&A Collection on Interactive Email Forms and Smart Capture

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--f432ca611c3e---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--f432ca611c3e---------------------------------------)

9 min read

·

Feb 11, 2025

--

Photo by [Nik](https://unsplash.com/@helloimnik?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

Salesforce Marketing Cloud includes a feature called **Interactive Email Forms**, allowing you to embed survey forms directly within email messages. For recipients, such emails are quite rare, creating a highly impactful communication opportunity.

This time, I have compiled a **Q&A** focusing on both **Interactive Email Forms**, which enable response collection directly within the email, and **Smart Capture**, a survey tool in Marketing Cloud that redirects users to a website to submit their responses.

## Table of Contents

### Interactive Email Forms Q&A

1. Timing of Super Message consumption
2. What timestamp is stored when using `%%=Now()=%%`?
3. How to record the timestamp of responses
4. Storing survey responses as historical records instead of overwriting
5. Considerations when using AMPscript and personalization strings
6. Utilizing the “00 IC Error Log” in the Interactive Contents Folder
7. Why Does the Interactive Email Form Section Appear Blank?
8. Causes and Solutions When Email Forms Don’t Display
9. Why are radio buttons displayed for some fields in Gmail?
10. Is the feature optimized for mobile devices?
11. Is it possible to align checkboxes horizontally?
12. Can forms be dynamically personalized for each recipient?

### Smart Capture Q&A

1. Troubleshooting a 500 Error When Using `CloudPagesURL()`
2. Using CloudPages Surveys in LINE Messages

## Interactive Email Forms Q&A

### 1. Timing of Super Message Consumption

Super Messages are consumed in the following two scenarios:

**a. Sending an email containing Interactive Email Forms**

- **Consumption:** 2 Super Messages  
  (Includes 1 Super Message for the email send itself.)

**b. When a recipient submits a survey response**

- **Consumption:** 1 Super Message per submission  
  (If a recipient submits responses multiple times, each submission consumes a Super Message, as this process uses CloudPages functionality.)

### 2. What timestamp is stored when using `%%=Now()=%%` ?

**For Interactive Email Forms**

When `%%=Now()=%%` is used in Interactive Email Forms, the **time the email was sent** is recorded.

- **Note:** This does not store the time the recipient submitted their response. If you want to record the response time, refer to section **3. How to record the timestamp of responses**.
- **Localized Time:** By default, `%%=Now()=%%` stores the system time (CST).(e.g., 15 hours earlier than Japan Standard Time)
- To localize it , use: `%%=SystemDateToLocalDate(Now())=%%`

![]()

**For Smart Capture**

In Smart Capture, `%%=Now()=%%` records the **time the form was opened**. This is typically close to the actual response time, but it’s important to note that it logs **the form-opening time**, **not the submission time**.

### 3. How to Record the Timestamp of Responses

To capture the **time a response was submitted** in Interactive Email Forms, follow these steps:

**How to Record Response Time**

1. Add a date field to the data extension where survey results will be stored.
2. Set the default value of the field using the “Use Current Date” feature.

- Note: In the case of the Japan time zone, the time stored upon record creation will reflect **15 hours prior to the response time**.

**Important Notes**

- “Use Current Date” does not retrieve the “latest date” each time a response is submitted.
- Only the date initially entered will be recorded, so please keep this in mind.

**Regarding the Send Timestamp Setting**

In the block settings, there is an option called “Send Timestamp” under Hidden Items. However, even if you input this, it only inserts `%%=Now(1)=%%`. As explained in 【2】, setting this will only record the **send time of the email containing the Interactive Email Forms**, but it will not record the **response time**.

![]()

### 4. Storing Survey Responses as Historical Records

Here are the key points to ensure that survey results are saved as individual records for each survey, without overwriting data on a subscriber basis.

**Handling Customer Key IDs**

If you set the mandatory `Id` field in the survey storage data extension to `%%_subscriberkey%%`, the survey results will be overwritten.

To prevent this, create a new management ID field, such as `Id2`, separate from the `Id` field, and link the customer ID to this new field.

By leaving the mandatory `Id` field empty, the same customer can have multiple response records. The mandatory `Id` field will automatically be populated with a **random GUID**, which I refer to as the Survey ID. Meanwhile, the custom `Id2` field should contain the customer ID.

### In the Case of Smart Capture…

Simply ensure that the `Id` field in the data extension is **not set as a primary key**. This will prevent existing records from being overwritten.

Since `Id` is a mandatory field for Interactive Email Forms, the configuration requirements will differ accordingly.

### 5. Key Considerations When Using AMPscript and Personalization Strings

When using AMPscript or personalization strings, keep the following points in mind:

**Behavior When Using Fallback Features**

- AMPscript and personalization strings can be used for labels, descriptions, and placeholders on forms. However, note that when fallback features are activated, these strings will appear as-is on the fallback CloudPage.
- This is not a bug but rather the expected behavior, and Salesforce has no plans to address this.

**Scenarios to Avoid**

- Given the above behavior, you should only use AMPscript or personalization strings if fallback features are not being used.

Below is an example of how the form appears in a sent email:

Here is an example of the form on the fallback CloudPage, where AMPscript and personalization strings are displayed as-is:

**Workaround**  
To avoid this issue:

1. Uncheck “Include Automatic Fallback”.
2. Under “Type of Fallback”, select a custom fallback button that you have created.
3. For the button link, use `%%view_email_url%%` (View As Web Page).

![]()

When using `%%view_email_url%%`, AMPscript and personalization strings function correctly. While viewing via the web is free, submitting responses will eventually redirect users to the CloudPage, consuming one Super Message.

**Caution**

- However, in this case, the “Include Automatic Fallback” checkbox is unchecked, so please be aware that it will no longer be possible to support the plain text version as explained in the following article.

[## SFMC Tips #50 : Handling Plain Text Versions of Interactive Email Forms

### The content I’m about to share is not listed in Salesforce help documentation, as far as I know. Therefore, please…

medium.com](/@marketingcloudtips/handling-plain-text-versions-of-interactive-email-forms-97b764c40607?source=post_page-----f432ca611c3e---------------------------------------)

### 6. Utilizing the “00 IC Error Log” in the Interactive Contents Folder

When survey results fail to write to the data extension correctly, you can use the “00 IC Error Log” in the “Interactive Contents” folder to troubleshoot.

This dedicated error log data extension records the following information:

**Logged Error Information**

- **Time stamp**: Date and time the error occurred
- **Is Test Send**: Indicates whether the error occurred during a test send (`true` or `false`)
- **Subscriber Key**: The subscriber key associated with the email recipient
- **Email Address**: The email address of the recipient
- **Target Data Extension Name**: Name of the target data extension for writing
- **Target Data Extension Customer Key**: Customer key of the target data extension
- **Submission**: Data attempted to be written (in JSON format)
- **Error Message**: The error message logged during the write process
- **Email Web Link**: Web view link of the email at the time of the error

Using this information, you can identify the cause of the problem and work towards a prompt resolution.

### 7. Why Does the Interactive Email Form Section Appear Blank?

Some email clients do not support Interactive Email Forms. In Japan, the most notable unsupported email clients include:

- Outlook (both web and app versions)
- Yahoo Japan (both web and app versions)

*Note*: If these emails are opened in the Apple Mail app or other compatible clients, the forms will be displayed correctly.

To accommodate unsupported clients, a “Fallback” feature is provided. I recommend always testing on the two email clients mentioned above and confirming how the fallback functionality, such as displaying a button instead of the form, behaves.

Below is an example of a form being displayed:

Here is an example where the form is not displayed, and the fallback button appears instead:

### 8. Causes and Solutions When Email Forms Don’t Display

When Interactive Email Forms are not displayed properly in email clients that should support them, the main causes and solutions are as follows:

**Issues Due to CSS Conflicts**

- Conflicts between other email code and the code inserted via the email form content block may cause display issues.
- Troubleshooting Steps:

1. Remove all other code from the email and confirm if the form works as expected.
2. Gradually reintroduce other code, testing which specific code is causing the conflict.

**Gmail-Specific Limitations**

- If the issue occurs only in Gmail, check the following restrictions:
- **Email Size Limit**: Gmail truncates HTML exceeding 102 KB, which can prevent proper form display.
- **CSS Style Tag Character Limit**: Gmail imposes a 16,000-character limit on CSS within `<style>` tags. Exceeding this limit causes ignored styles, impacting the display.

### 9. Why are radio buttons displayed for some fields in Gmail?

In Gmail, some CSS attributes are unsupported. As a result, radio buttons or checkboxes that were intended to remain hidden may appear when designing interactive elements.

**Affected Input Types**  
The following input types might display radio buttons or checkboxes in Gmail’s web client or app:

- Single-selection images
- Multi-selection images
- Single-selection buttons
- Multi-selection buttons
- Ratings

**Background and Impact**  
Because Gmail doesn’t support certain CSS attributes, these input elements may appear with default browser styling. However, this visual difference does not affect the form’s functionality or performance.

### 10. Is the feature optimized for mobile devices?

Yes, interactive email forms are designed to render appropriately across all screen sizes in supported email clients. However, keep the following points in mind:

**Template Matters**  
The type of email template used can influence the form’s appearance:

- **Responsive Templates**: These adjust based on device and screen size, ensuring optimal form display on mobile devices.
- **Non-Mobile-Optimized Templates**: Templates that aren’t responsive may not render forms correctly.

### 11. Is it possible to align checkboxes horizontally?

Unfortunately, checkboxes cannot be aligned horizontally in interactive email forms.

**Alternative Approach**  
If horizontal alignment is a design requirement, consider using **image selection** instead. Image selection can be displayed horizontally, providing a visually acceptable alternative.

### 12. Can forms be dynamically personalized for each recipient?

Regrettably, it is not possible to use dynamic content to display different forms for each recipient.

## Smart Capture Q&A

### 1. Troubleshooting a `500 Error` When Using `CloudPagesURL()`

**Problem Overview**  
For accounts with web analytics connectors or GA integration that automatically append UTM parameters, using the `CloudPagesURL()` method to generate links may result in a `500 error` during redirection.

This issue arises in the following situations:

- A `?qs=` parameter is added to links generated with `CloudPagesURL()`.
- Simultaneously, GA integration appends a `?utm=` parameter.
- The subsequent `?utm=` parameter is not properly converted to `&utm=`, causing a conflict.

**Solution**  
To avoid this error, wrap the `CloudPagesURL()` method with `RedirectTo()`.

**Incorrect Example (Error Occurs)**

```
%%=CloudPagesURL(217)=%%
```

**Correct Example (Error Avoided)**

```
%%=RedirectTo(CloudPagesURL(217))=%%
```

**Explanation of the Fix**  
By wrapping `CloudPagesURL()` with `RedirectTo()`, subsequent `?utm=` parameters are properly converted to `&utm=`, resolving the conflict. This method ensures that the `500 error` is avoided.

### 2. Using CloudPages Surveys in LINE Messages

**Problem Overview**  
`CloudPagesURL()` cannot be used within LINE messages. When creating a survey link with hidden fields such as `%%_SubscriberKey%%`, the standard method does not work.

**Solution**  
Follow these steps to use CloudPages surveys within LINE messages:

**Step 1**  
Add a parameter to the CloudPages URL.  
Append one of the following parameters to the end of your CloudPages URL:

- `?u=%%LINE_SUBSCRIBER_ID%%` (LINE\_SUBSCRIBER\_ID represents the ContactID)
- `?u=%%LINE_ADDRESS_ID%%` (LINE\_ADDRESS\_ID represents the UID)

Example:

```
https://yourcloudpagesurl.com/?u=%%LINE_SUBSCRIBER_ID%%
```

**Step 2**  
Configure the hidden field in Smart Capture.  
Set one of the following codes in the hidden field of Smart Capture to retrieve the ContactKey based on the URL parameter:

**When Using ContactID:**

```
%%=Lookup('_MobileLineAddressContactSubscriptionView', 'ContactKey', 'ContactID', RequestParameter('u'))=%%
```

**When Using AddressID:**

```
%%=Lookup('_MobileLineAddressContactSubscriptionView', 'ContactKey', 'AddressId', RequestParameter('u'))=%%
```

**Points to Note:**

- The parameter name (`u`) is arbitrary but must match the field used in Smart Capture.
- `_MobileLineAddressContactSubscriptionView` is a system view where LINE integration data is stored.

## Conclusion

These questions and solutions are based on real-world issues I have encountered.

If you have additional knowledge to share, feel free to leave a comment!

Thank you for reading!!

Stay tuned for more Salesforce Marketing Cloud tips! 😊

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
