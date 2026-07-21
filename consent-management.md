# Consent Management in Marketing Cloud Next explained

**Source:** https://the-agentic-marketer.com/marketing-cloud-next-deep-dives/consent-management

---

In this article we will dive deep into how the Consent is handled in Marketing Cloud Growth and Advanced. It is a Subscription-based model and it is managed at the Contact Point level (Email Address, WhatsApp or Phone number for SMS). Everything is stored in Data Cloud.

## A Subscription Model

Subscriptions can be declared in the Consent tab of the Marketing App. When defining a new Subscription, you need to relate it to one or more **Engagement Channel**. The available Channels are Email, SMS and WhatsApp. Each Engagement Channel has its own settings (Authenticated Domain for Email, Short or Long Code for SMS, etc.) which must be configured during the setup phase, and a default Preference Center. **Subscriptions are stored in the Communication Subscription DMO** (which is mapped to the CommSubscription\_Home DSO which MCG/A writes into thanks to the Salesforce Connector).

[![](https://the-agentic-marketer.com/wp-content/uploads/2025/08/009-3-Subscriptions-defined-in-MCGA-Consent-tab-stored-in-Data-Cloud-1024x557.png)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/009-3-Subscriptions-defined-in-MCGA-Consent-tab-stored-in-Data-Cloud.png) 

3 Subscriptions defined in MCGA Consent tab, stored in Data Cloud

Each Subscription is tied to one or more Engagement Channel. **The Communication Subscription Channel Type DMO** (mapped to the CommSubscriptionChannelType\_Home DSO which MCG/A writes into thanks to the Salesforce Connector) stores all the informations the Subscriptions and all their associated Engagement Channel as separate records.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20435%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/010-Subscriptions-and-Engagement-Channels-definition.png) 

Subscriptions and Engagement Channels definition

In our example, the Events Subscription (0XlbF00000001ybSAA) has two Engagement Channel Types (0eFbF000000009iUAA and 0eFbF000000009hUAA). Those Channel Types (starting with 0eF) are defined in the **Engagement Channel Type DMO** (mapped to the EngagementChannelType\_Home DSO).

In the Communication Subscription Channel Type DMO (starting with OeB), the Comm Subscription Channel Type Id **uniquely identifies a given combination of subscription and engagement channel**.

## Consent storage

The Consent Management defines, for a given Contact Point and a given Comm Subscription Channel Type if the a **permission has been given (Opt In) or not (Opt Out) to receive the communications of a given type, and related to a given subscription**.

These informations are stored in the **Communication Subscription Consent DMO**. One important information is that MCG/A is based on **an implicit Opt Out**, this means, **if no information is given, a given recipient is assumed Opt Out**.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20435%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/011-Communication-Subscription-Consent-DMO.png) 

Communication Subscription Consent DMO

The **Consent Status** is what defines if a permission has been given by a recipient. It may be OPT\_IN or OPT\_OUT, and if no record is found, Marketing Cloud Growth and Advanced will assume an OPT\_OUT.

For a given Contact Point, you should see one record for a given Subscription and Engagement Channel. But, there has been changes introduced since Summer ’25 and the Communication Subscription Consent DMO might be mapped to both **MessagingConsent-MessagingConsent** and **MessagingConsentV2-MessagingConsent****DSOs**. Since the Summer ’25 release, only the V2 DSOs is written into, but if your instance was created before, you may see 2 records for a given Contact Point and a given Subscription and Engagement Channel (each with a distinct Data Source).

When a Consent Status is modified (see below, *How to Modify the Consent Status?*), MCG/A first checks if a record exists. If yes, then the record is updated by changing the Consent Status into OPT\_IN or OPT\_OUT (unless it was created using the V1 system, in that case a new record is created, with V2 as the Data Source).

**Marketing Cloud Next always uses the latest record as the current Consent Status.**

You may have noticed on the previous screenshot a **dummyCsctToken** Comm Subscription Channel Type. This is used when **Unsubscribing from a Test Email**.

Finally, the primary Id used for the Communication Subscription Consent DMO is **forged from the Contact Point and the Comm Subscription Channel Type**. Like [[email protected]](/cdn-cgi/l/email-protection)#0eBbF00000000HlUAI in the first line of the previous screenshot.

## Where to display the Consent Status?

The Consent Status can be added on Prospect, Lead and Contact Layout. This is done by using the **Privacy Consent Status** component. This component displays the Consent Status of the Email Address (Contact Point Email) field of the current Prospect, Lead or Contact, of each Subscription. For Person Accounts, see [Surfacing Subscription Consents on Person Accounts](/marketing-cloud-next-deep-dives/subscription-consents-person-accounts/)

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20435%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/012-Subscription-Consent-Status-of-the-current-Lead-Email-Address.png) 

Subscription Consent Status of the current Lead Email Address

This component works as follows, for each Subscriptionn does a related record (same Email Address and same Subscription) exist in the Communication Subscription Consent DMO for the Email Engagement Channel (0eB…)? If so, display the Consent of the latest record (Opted In or Opted Out), else, display Opted Out (implicit Opted Out).

## How to modify the Consent Status?

The Consent Status can be modified in the following ways:

- **Manually**: from the Privacy Consent Status component (there is a dropdown at the end of each Subscription line)
- **Unsubscribe link in an Email**: One like of this type is required (alternatively a Preference Center link) in every Promotional Email. By clicking this link, a recipient immediately unsubscribes from the given Subscription selected at send time (no two-click unsubscribe so far).
- **Preference Center in an Email**: You can add a Preference Center in you Emails, where a recipient can choose which Subscriptions she/he wants to be active and can also Unsubscribe them all.
- **Import**: Marketing Cloud Next has a Consent menu item, where a file containing the Contact Points to modify (along with the Consent change date) the Consent Status (select Opt In or Opt Out) of can be uploaded for bulk changes.
- **Flow**: both Segment Triggered Flows and Automation Triggered Flows can be used to change the Consent Status. To be compliant with local rules, you may setup a [2 steps Flow (DOI)](/marketing-cloud-next-deep-dives/double-opt-in-flow/).

## Final Thoughts

A given Unified Individual can be linked to several Email Adresses. In that case, how to determine the Consent Status of a Unified Individual for a given Subscription? Should all Email Adresses be OPT\_IN or OPT\_OUT, is only one of them enough? There is no correct answer (at least one being the most common), it is a matter of choice.

One thing which brings clarity in that case is (multiple Email Adresses related to a given Unified Individual) is to create a new DMO, related to Unified Individual DMO, and fill with every email address (Unified Indv Contact Point Email) along with their current Consent Status for each available Subscriptions. Then you can add a Data Cloud Profile Related Records to display them on Lead and Contact Layouts.

Also, a DLO called ConsentAuditTrailV2-ConsentAuditTrail (there is also a ConsentAuditTrail-ConsentAuditTrail, no longer used since Summer ’25), which is not mapped to any DMO, acts as an history tracking by storing changes (whereas Communication Subscription Consent works in an upsert mode)

[Edit 31/01/2026], at send time, the **source of truth of Consent is actually a cache**. When an email is sent, Marketing Cloud Next checks the cache for a Consent Record related to the current recipient’s email address. If a record exists in the cache, that consent is used. if not, the Communication Subscription Consent is queried and the cache populated. The cache value is used for 90 days, unless it is updated, but not every way of updating the consent actually updates the cache. From the previous section list of possible ways to update the Consent, the following ones actually handle the cache for you: manual update from Lead and Contact layouts, Unsubscribe link/Preference Center, CSV import. In Flows, only the Create Consent activity officially does. The MessagingConsentV2.MessagingConsent activity seems to work, but there is no official guarantee of this. Write in the Communication Subscription Consent DMO (for example by importing data into a DLO mapped to it) does not update the cache.
