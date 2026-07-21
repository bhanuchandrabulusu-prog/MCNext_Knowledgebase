# SFMC Tips #311 : Marketing Cloud Next: Setting Up Consent Synchronization with MC Engagement

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-next-setting-up-consent-synchronization-with-mc-engagement-33b4cba94f47

---

# SFMC Tips #311 : Marketing Cloud Next: Setting Up Consent Synchronization with MC Engagement

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--33b4cba94f47---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--33b4cba94f47---------------------------------------)

8 min read

·

Jun 17, 2026

--

Photo by [Ryoji Iwata](https://unsplash.com/@ryoji__iwata?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

With the [Summer ’26 new feature release](/@marketingcloudtips/marketing-cloud-next-summer-26-release-highlights-04f6c5abdee6) for Marketing Cloud Next Growth & Advanced Editions, **it is now possible to map consent information from Marketing Cloud Engagement standard lists and publication lists to Communication Subscriptions in Marketing Cloud Next**.

When a Marketing Cloud Engagement standard list or publication list is mapped, statuses are automatically synchronized between both systems whenever a subscriber updates their consent.

Although standard lists can also be used in this feature, it is difficult to imagine practical use cases for them, so this article uses publication lists as an example.

## Configuration Steps

1. Normally, when implementing Marketing Cloud Next, there are many cases where a Marketing Cloud Engagement organization is already in operation, and publication lists may be managed as shown below.

*\*If publication lists do not exist in Marketing Cloud Engagement, it may be a good idea to create a* ***general publication list*** *such as “All Subscribers (Publication Lists)” within Marketing Cloud Engagement and utilize that.* 💡

2. As data, email addresses and statuses are managed based on Subscriber Key.

![]()

3. With the Summer ’26 new feature release, Consent Mapping is now displayed under the Consent tab. You can start creating a Communication Subscription that will be consent-mapped by clicking the Map Consent button.

4. Select a standard list or publication list in Marketing Cloud Engagement. Not all subscriber lists can be selected.

5. After deciding the name of the new Communication Subscription that will be created on the Marketing Cloud Next side, click Map Consent to start the creation process.

*The Communication Subscription name can be changed later.*

6. Mapping starts and the status becomes Syncing.

7. After waiting 10 to 20 minutes, the status becomes Active and you can start using it.

## Considerations

At first glance, this appears to be a simple synchronization feature. However, after actual testing, there turned out to be many important behaviors that should be understood due to the differences in design philosophy between the two products.

This article summarizes the results of the actual testing.

## Existing Communication Subscriptions Cannot Be Used

The first thing I wanted to confirm was whether existing Communication Subscriptions could be linked to standard lists or publication lists.

The conclusion is that this is not possible.

When synchronization is enabled, **a new Communication Subscription is automatically created for each standard list or publication list**.

In addition to existing subscriptions, a new Communication Subscription configured for synchronization is created.

At first glance this behavior may seem inconvenient, but it is actually reasonable.

If mapping to an existing Communication Subscription were allowed, the following question would arise:

- Should the historical subscription state on the list side be treated as the source of truth?
- Should the historical subscription state on the Communication Subscription side be treated as the source of truth?

To avoid this conflict, it appears that the design intentionally creates a new Communication Subscription.

*Therefore, environments that have already started operating Communication Subscriptions will need to implement some type of workaround.*

## Synchronization Is Extremely Fast

Synchronization itself is performed through APIs.

When the state of a standard list or publication list changes, it was reflected on the Marketing Cloud Next side within a few seconds.

However, there is a delay before Communication Subscription Consent DMO is updated, and it takes approximately 5–10 minutes before it can actually be confirmed.

## Data Stream Integration Is Not Involved

Before testing, I assumed that it might be necessary to wait for data stream synchronization, but that was not the case.

Email addresses and subscription statuses are referenced directly through APIs and do not depend on:

- Data Streams
- Subsequent DLO / DMO processing

## Behavior During Initial Synchronization

After synchronization completed, an interesting behavior could be observed in the Communication Subscription Consent DMO.

Only subscribers with Active, Bounced, or Held statuses in the standard list or publication list had OPT\_IN records created in Communication Subscription Consent. No records were created for Unsubscribed subscribers.

This appears to be because Marketing Cloud Next adopts the concept of Implicit Opt-Out.

In other words, the idea is:

“**For the initial load, only keep people who have consented, and do not create unnecessary records for people who have not consented.**”

## Publication List Update Behavior

When the Communication Subscription status is changed on the Marketing Cloud Next side, the change is also reflected in Marketing Cloud Engagement.

For example, when changing from OPT\_OUT to OPT\_IN:

- If the subscriber does not exist, it is added to the publication list.
- If the subscriber already exists, the publication list status is updated.

In other words, consent status in Marketing Cloud Next is synchronized back to Marketing Cloud Engagement.

***Note:******If an email address cannot be found among all subscribers, a subscriber whose Subscriber Key is the email address will be automatically created****. Therefore, if consent is imported into Marketing Cloud Next before importing subscriber data into All Subscribers, unnecessary billable contacts may be created. The order of processing should therefore be carefully considered.*

![]()

## Important Assumption: MCE and MCN Use Different Identifiers

This is the most important point for understanding this feature.

- Marketing Cloud Engagement is managed based on Subscriber Key.
- Marketing Cloud Next is managed based on email address.

Therefore, a conversion process between the two always occurs during synchronization.

This design difference is the cause of the behaviors described below.

## What Happens During MCN → MCE Synchronization

Marketing Cloud Next manages consent at the email address level.

Therefore, when a Communication Subscription is updated, subscribers with that email address are reflected in the publication list.

The problem arises when multiple Subscriber Keys exist for the same email address.

**The result is that only one subscriber is selected for addition or update**.

I investigated which subscriber is selected, and based on observed behavior, it appears that:

- **Only the subscriber most recently added to the publication list**

is selected, although there is no official documentation confirming this.

*Therefore, environments that manage the same email address under multiple Subscriber Keys within Marketing Cloud Engagement should conduct thorough testing.*

## What Happens During MCE → MCN Synchronization

During MCE → MCN synchronization, Subscriber Key is not used. Only the email address is used.

When a change occurs in the publication list, Marketing Cloud Next is updated based on the email address held by that subscriber.

A similar issue can occur here as well.

In this case, everyone using that email address may become unable to receive emails, so caution is required.

## All Subscribers Takes Priority

In Marketing Cloud Engagement, the status of All Subscribers takes precedence over publication lists.

Therefore, even if Marketing Cloud Next changes a record from OPT\_OUT to OPT\_IN and attempts to set the publication list status to Active, the update will not be processed if the All Subscribers status is Unsubscribed.

## The Most Dangerous Behavior

This was the most surprising result during testing.

What happens when the status in All Subscribers is changed from Active to Unsubscribed?

As a result, all Communication Subscriptions associated with that email address in Marketing Cloud Next became OPT\_OUT.

This part is understandable.

However, further investigation showed that not only the Communication Subscriptions created through publication list synchronization became OPT\_OUT, **but also Communication Subscriptions that were not synchronized with Marketing Cloud Engagement**.

In other words, a universal unsubscribe performed in MCE can potentially affect all Communication Subscriptions in MCN.

This is an extremely important point.

**Once this feature is enabled, it may impact Communication Subscriptions that have no direct relationship with MCE**.

This must be considered during operational design.

## Why Does This Happen?

This is not a bug.

**Changing All Subscribers from Active to Unsubscribed represents a Universal Unsubscribe**.

In other words, it means:

“**Do not send emails to this email address going forward.**”

Therefore, it is logically correct that all Communication Subscriptions in Marketing Cloud Next become OPT\_OUT.

## The Reverse Direction Does Not Restore Consent

What happens if the All Subscribers status is changed back from Unsubscribed to Active?

This was also tested.

As a result, nothing happens.

- Communication Subscriptions do not automatically return to OPT\_IN.
- Publication list statuses do not automatically return to Active.

This is because Salesforce’s design philosophy is that:

- **A Universal Unsubscribe feature exists.**
- **A Universal Resubscribe feature does not exist.**

Simply changing the All Subscribers status back to Active is not considered consent to receive emails again.

Publication lists must be reactivated separately.

***Note:*** *Due to the way publication lists work, to reactivate a publication list, the All Subscribers status must first be changed from Unsubscribed back to Active.*

## Conclusion

What did you think?

There is no doubt that this consent synchronization feature has been highly anticipated by many users. The configuration itself is very simple, but actual testing revealed that there are far more operational considerations than one might initially expect.

**Particular caution is required in environments where the same email address is managed under multiple Subscriber Keys**. Because Marketing Cloud Next and Marketing Cloud Engagement use different identification models, synchronization may not behave as expected. Thorough testing is recommended before implementation.

Another especially important finding from this testing was the scope of impact when changing the All Subscribers status. **Because it is treated as a Universal Unsubscribe, it can affect Communication Subscriptions that are not directly synchronized with Marketing Cloud Engagement**.

That said, the value of being able to unify consent management between Marketing Cloud Next and Marketing Cloud Engagement is extremely significant, and this will likely become one of the standard operating models going forward.

If you are considering centralized consent management, be sure to thoroughly validate the behavior in a test environment first, and then take advantage of this feature.

That’s all for this time.

Stay tuned for more Salesforce Marketing Cloud tips! 😎

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
