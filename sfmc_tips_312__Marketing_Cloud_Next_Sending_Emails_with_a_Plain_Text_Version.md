# SFMC Tips #312 : Marketing Cloud Next: Sending Emails with a Plain Text Version

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-next-sending-emails-with-a-plain-text-version-8576936e9a02

---

# SFMC Tips #312 : Marketing Cloud Next: Sending Emails with a Plain Text Version

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--8576936e9a02---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--8576936e9a02---------------------------------------)

5 min read

·

Jun 18, 2026

--

Photo by [Shane](https://unsplash.com/@theyshane?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

Salesforce itself has not widely announced this beyond release notes and official help documentation, but in the Marketing Cloud Next Growth & Advanced Editions [Summer ’26 new feature release](/@marketingcloudtips/marketing-cloud-next-summer-26-release-highlights-04f6c5abdee6), the ability to create plain text email versions was added.

Starting June 17, 2026, emails are now sent using multipart MIME format by default when sending email (sending both the traditional HTML version and a plain text version together).

## Benefits of Adding a Plain Text Version

### 1. The Optimal Format Can Be Displayed Based on the Recipient Environment

With multipart MIME format, a single email contains both an HTML version and a plain text version.

As a result, the recipient’s email client can automatically select the most appropriate format.

- Gmail → HTML display
- Outlook → HTML display
- Environments where HTML display is disabled → Text display

### 2. It Can Be Beneficial for Spam Evaluation

In general, emails that contain:

- An HTML version
- A plain text version

tend to be evaluated more favorably as legitimate marketing emails.

Of course, this does not necessarily improve deliverability, but it is certainly a structure that is closer to the industry standard.

### 3. Improved Accessibility

Some users access email in environments such as:

- Using text email
- Using screen reader software
- Restricting HTML display

Having a plain text version allows emails to properly support these environments.

## The Same Mechanism as Marketing Cloud Engagement

The screen used to edit plain text is implemented almost identically to Marketing Cloud Engagement.

A plain text version is automatically generated based on the HTML email content.

- It is also possible to edit it by clicking the Edit button, but once the plain text version has been edited manually, subsequent changes to the HTML version are no longer automatically reflected.
- If everything needs to be redone, the plain text version can be regenerated from the current HTML version.

## When Did Multipart MIME Start Being Used?

As far as I have confirmed, **multipart MIME sending became active on June 17, 2026**.

The reason I can say this with confidence is that I had been checking the source of emails received from Salesforce every day since the preview environment before the production release.

I also checked on the day of the Summer ’26 release and for several days afterward, and the emails being sent were HTML-only emails.

However, starting with emails received on June 17, 2026, they were clearly changed to multipart MIME format.

*My assumption is that Salesforce was gradually applying plain text generation processing to existing email assets immediately after the release. There is no official explanation, so this is only my personal assumption.*

## Checking the Headers

### Before the Change

Previous email headers looked like the following:

```
MIME-Version: 1.0  
Content-Type: text/html; charset=UTF-8
```

Only HTML was being sent, and there was no boundary used for multipart messages.

### After the Change

Starting June 17, 2026, they look like this:

```
MIME-Version: 1.0  
Content-Type: multipart/alternative; boundary="----=Part_Alternative_Boundary=----"
```

**multipart/alternative** is being used.

Furthermore, the body contains both:

```
------=Part_Alternative_Boundary=----  
Content-Type: text/plain; charset="utf-8"
```

and

```
------=Part_Alternative_Boundary=----  
Content-Type: text/html; charset="utf-8"
```

(text/plain and text/html).

In other words, it can be confirmed that both the HTML version and the plain text version are being sent as a single email.

## Existing Emails Are Also Affected

Naturally, this change does not apply only to emails created going forward.

Previously created emails and automated emails will also be sent in multipart MIME format.

For that reason, I recommend reviewing the content of the plain text versions for emails that are currently active in flows.

Since the plain text version is automatically generated from the HTML version, it is unlikely to become a critical issue even if no action is taken. However, brands that prioritize email quality, or companies that sell premium products and services, should review it sooner rather than later.

## In Some Environments, Editing May Not Be Available

Unfortunately, it appears that in some environments, an issue occurs where the plain text version cannot be edited.

As expected, in my environment as well, the editing screen does not appear when the user language is set to English.

On the other hand, when the user language is changed to Japanese, editing works normally.

If the plain text editing screen does not appear, try changing your user language and testing again.

## Conclusion

With this change, Marketing Cloud Next can finally send industry-standard multipart MIME emails.

This is a very important improvement from the perspectives of:

- Supporting different recipient environments
- Improving spam evaluation considerations
- Enhancing accessibility

One thing to note is that this change is automatically applied to existing emails as well, so I recommend reviewing the content of your plain text versions at least once.

That’s all for this time.

Stay tuned for more Salesforce Marketing Cloud tips! 😎

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
