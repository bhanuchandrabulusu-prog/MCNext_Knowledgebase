# SFMC Tips #268 : Marketing Cloud Next: Send Marketing Cloud Engagement Emails from a Flow

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-next-send-marketing-cloud-engagement-emails-from-a-flow-450b1173ace2

---

# SFMC Tips #268 : Marketing Cloud Next: Send Marketing Cloud Engagement Emails from a Flow

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--450b1173ace2---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--450b1173ace2---------------------------------------)

5 min read

·

Mar 19, 2026

--

Photo by [Nicholas Ng](https://unsplash.com/@nicholasng210?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

With the [Spring ’26 new feature release](/@marketingcloudtips/marketing-cloud-next-spring-26-release-highlights-24c0c804b0cb) of Marketing Cloud Next Growth & Advanced Edition, accounts using **Marketing Cloud Engagement+** can now send emails stored in Content Builder of Marketing Cloud Engagement directly from a flow.

Previously, the “Send to Journey” feature was provided to trigger a journey from a flow, but going forward it is now possible to trigger and send a single email directly.

For “Send to Journey”, please refer to the article below.

[## SFMC Tips #250 : Marketing Cloud Next: Send to Journey Action

### In environments using Marketing Cloud Engagement+, it is possible to send Marketing Cloud Next contacts from a…

medium.com](/@marketingcloudtips/marketing-cloud-next-send-to-journey-action-3a0c77cc2b63?source=post_page-----450b1173ace2---------------------------------------)

> *Additionally, Salesforce CRM also had a similar feature called “Marketing Cloud Sends”, but being able to send from a flow represents the latest technology.*

In this article, I will introduce and explain this new feature.

## Setup Steps

The configuration for this feature is largely divided depending on whether personalization strings are included or not.

- **When personalization strings are included: Creation of a Triggered Data Extension is required**
- **When personalization strings are not included: Creation of a Triggered Data Extension is not required**

Let’s go through each of these settings.

## When Personalization Strings Are Not Included

1. Find and select “**Send Marketing Cloud Engagement Email**” in the flow element.

![]()

2. First, select the “Marketing Cloud Engagement Business Unit”.

3. Next, select the email.

4. This time, select an email that does not include personalization strings.

5. Next, select the “**Send Classification**” already registered in MCE.

6. Then select the “**Publication List**”. This corresponds to “Communication Subscription” in Marketing Cloud Next.

7. If you have not created a publication list, select “**All Subscribers**” under “my subscribers”.

> *\*Marketing Cloud Engagement uses implied opt-in, so it is not necessary to register consent information in advance. Upon sending, the contact is* ***automatically registered to the All Subscribers list with an Active status****.*

8. The Personalization section does not need to be configured this time.

With just these steps, sending is possible.

> *You may be wondering: for the first send, the email address from Marketing Cloud Next is used, and it is registered as the email address in All Subscribers.*
>
> *However, what happens on the second send, when the email has already been sent from MCE before? Will it use All Subscribers data or Marketing Cloud Next data?*
>
> *The answer is that it always sends using data from the Marketing Cloud Next side, and the email address in All Subscribers is overwritten with that. In other words, it behaves like journey data. This is an important point to remember.*

### **New Feature Added**

The [Summer ’26 release](/@marketingcloudtips/marketing-cloud-next-summer-26-release-highlights-04f6c5abdee6) introduces the **Retain Send Log Data** option.

With this enhancement, send log data can now be retained for emails sent through the **Send Marketing Cloud Engagement Email** element in flows. This allows organizations to leverage send log data for reporting, delivery analysis, and troubleshooting, even when emails are sent from Marketing Cloud Next flows.

![]()

## When Personalization Strings Are Included

Next, when personalization strings are included, the setup is the same up to the Personalization section.

In this example, assume the email includes “LastName” and “FirstName”.

9. When you enable “Map Personalization Data” in the Personalization section, you will be prompted to select a “**Triggered Send Data Extension**”.

10. When selecting this data extension, you must create a “Triggered Send Data Extension” in advance, considering the personalization strings and AMPscript used in the email. Start creating a new data extension and select “**Create From Template**”.

11. Select “**TriggeredSendDataExtension**”.

12. Set an easy-to-understand name so it can be easily selected later from the Marketing Cloud Next screen, and check “Is Sendable?”.

13. Create the fields used for personalization strings and save.

14. After creating it, return to the Marketing Cloud Next screen and select the newly created “Triggered Send Data Extension”.

15. When you enable data extension fields, the fields added to the data extension will be displayed.

16. Then map the data from Unified Individual fields and complete the setup.

17. When actually sending, the send data is stored in the “Triggered Send Data Extension”.

18. The name is also populated in the sent email. Success!!

## Notes

If you select an email that includes personalization strings but do not configure the Personalization section, the following error will occur and the flow cannot be activated:

- An unexpected error occurred. Please include this ErrorId if you contact support: 1787096589–44424 (-2006034501)

## Conclusion

You can see that this mechanism is essentially a version of “Send to Journey” without the journey.

Which one to choose depends on the user, but personally, I feel that “Send to Journey” is somewhat more reliable. However, for those who frequently send one-off emails in Email Studio, this new feature may also be suitable.

This ultimately comes down to preference, so please try both and choose the one that fits you best.

That’s all for this time.

Stay tuned for more Salesforce Marketing Cloud tips! 😎

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
