# Surfacing Subscription Consents on Person Accounts for Marketing Cloud Next

**Source:** https://the-agentic-marketer.com/marketing-cloud-next-deep-dives/subscription-consents-person-accounts

---

**[Edit 27/02/2026] Since Spring’26, there is a native component “Privacy Content Status” that displays and allows editing the Consents for Person Accounts. “Unified Engagement History Dashboard” gives you a detailed view of Engagement Data for Person Accounts.**

As of today, Person Accounts are not officially supported by Marketing Cloud Next. Let’s see how we can display data from Data Cloud on Salesforce layouts.

[Consent Management in Marketing Cloud Next explained](/marketing-cloud-next-deep-dives/consent-management/)

## Needed Setup

First, let’s state a Person Account in Salesforce is a merge of one Contact and one Account. They have their own Layouts, and most importantly, even if they include a reference to the associated Contact Id, their primary Record Id is an Account one (starting with “001”).

In Data Cloud, a Person Account has one Record in the Contact DLO, mapped with the Individual DMO for the Contact part, and one Record in the Account DLO, mapped to Account DMO.

There are two types of Identity Resolutions, one creates Unified Individuals by gathering similar Individuals, and the other one creates Unified Accounts out of similar Accounts. So a Person Account is both a Unified Individual and a Unified Account once the two resolution processes have run.

## Surfacing Data Cloud in Salesforce

In Salesforce, on the Leads or Contacts Lightning Pages, you can embed Data Cloud Lightning widgets : Consent, Activity, Calculated Insights or Related Records.

[![](https://the-agentic-marketer.com/wp-content/uploads/2025/08/009-1-—-Privacy-Consent-Status-2-—-Data-Cloud-Widgets-1024x558.png)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/009-1-—-Privacy-Consent-Status-2-—-Data-Cloud-Widgets.png) 

1 — Privacy Consent Status 2 — Data Cloud Widgets.

You can also, on both Leads and Contacts, add Related Lists from Data Cloud.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20436%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/010-Adding-a-Related-List-to-display-Data-Cloud-data-related-to-the-current-Indivi.png) 

Adding a Related List, to display Data Cloud data (related to the current Indivi

Unfortunately, on Accounts (and Person Accounts) there is no Data Cloud widgets as of today (and so no Subscription Consent available), only the Data Cloud Related Lists Enrichments are available.

We’ll leverage this feature to add Subscription Consent as a Related List on Person Accounts Layouts. Note that on the Privacy Consent Status available on Leads and Contact, you can modify or add Subscription Consents. By adding the Related List on Person Account, we will surface the Consent data, but we won’t be able to add or modify it (Flows or Consent Files imports need to be use for this).

## Data Cloud Related Lists Enrichments

If you create one of these on the Contact Layout for instance, you will select an Individual related DMO. Then, when displayed on a given Contact, the current Contact Id (starting with 003) will be passed to Data Cloud, which will retrieve the Unified Individual, then all its underlying Individuals (including the displayed one). Finally the Related List will be populated with a query inside the associated DMO: each record in the Individual linking Field with a value inside the underlying Individual Ids will be displayed.

A Data Cloud Related Lists Enrichment on the Person Account and Account DMO, works the same, but Account is replacing Individual. Which means, to display Subscription Consents, we need two things:

- Unified Accounts
- A Consent DMO linked with the Account DMO (with the Engagement type)

The first one is achieved by activating the Account Resolution (this is only available in the Advanced Edition, not in the Growth Edition). For the second requirement, we will create a DSO/DLO from the raw Consent DSO/DLO, using a Data Transform and map it to a new DMO.

Note, Segmentation based on Subscriptions also works on Person Accounts. See [3 ways to create a Subscriber List](/marketing-cloud-next-deep-dives/create-subscriber-list/).

## Activating Account Resolution

If not already done (requires Advanced Edition), *Data Cloud > Identity Resolution > New > Create New Ruleset > Next* and use the Following:

- Primary Data Model: Account
- Match to Data Model Object: Account
- Ruleset Id: whatever you want, here we use “A” (for Account)

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20436%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/011-Adding-an-Account-Resolution-Ruleset.png) 

Adding an Account Resolution Ruleset

*Next*. Then give your Ruleset a name, see the Objects to be created (with the suffix you added as a Ruleset Id). *Save*.

Once created, you need to create Rules, to define what “being identical for two Account Records” actually means. *Match Rules > Configure > Next.* Here we will select the first proposed rule, but it is your call.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20436%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/012-Adding-a-match-rule.png) 

Adding a match rule

Once published, *Run* the Ruleset (yes, this consumes credits).

## Creating a Consent DMO linked with the Account DMO

### Creating a Account Consent DSO/DLO and DMO

Our first step is to create a DSO/DLO. *Data Cloud > Data Lake Object > New > New > Next.* We’ll select Engagement as a Category, name it Account Consent, and add the following fields (don’t forget to select an Event Time Field, required for Engagements DSO/DLO).

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20457%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/013-Preparing-our-DSODLO-which-will-receive-Consent-Data-for-our-Accounts-and-Person.png) 

Preparing our DSO/DLO which will receive Consent Data for our Accounts and Person

*Save*. We’ll need to Map this DSO/DLO to a new DMO, and for this, we must add the DSO/DLO we just created into our Data Space: *Data Cloud > Data Space > Choose you Data Space > Add Data Lake Object* and select Account Consent, with without filtering it (up to you).

From the DSO/DLO page, *Data Mapping > Start > Select Objects > Custom Data Model > New Custom Object > Save.*

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20457%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/014-Creating-a-DMO-and-mapping-it-in-the-same-move.png) 

Creating a DMO, and mapping it in the same move

Our new DSO/DLO is now mapped to a DMO. Before feeding it with Consent Data using a Data Transform, let’s relate it to the Account DMO. Open the newly created DMO, and *Relationship > New > +New Relationship*, and select the Fields as below:

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20436%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/015-Creating-a-relationship-between-the-Account-Consent-DMO-and-the-Account-DMO.png) 

Creating a relationship between the Account Consent DMO and the Account DMO

*Save*.

### Feeding the DSO/DLO (and hence the DMO) with Consent Data

The MessagingConsent-MessagingConsent DSO is the DSO/DLO where Consents are stored, it is mapped to the Communication Subscription Consent DMO. Let’s create a Data Transform out of it: *Data Cloud > Data Transform > New > Batch Data Transform > Next > Data Lake Object > Add Input Data.* Then select MessagingConsent-MessagingConsent, and select the following fields.

[EDIT 2025/09/20] – Since Consent Management in Marketing Cloud Next (Growth or Advanced) has switched to V2, the Ingestion API now writes Consent records into the **MessagingConsentV2-MessagingConsent**which is the one to use.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20436%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/016-Adding-the-Consent-Data-to-the-Data-Transform.png) 

Adding the Consent Data to the Data Transform

The Contact Point Value contains the Email Address of the related Subscription Consent, and we selected other informations as the Consent itself (opt\_in or opt-out), etc.

Then we join this Data with the Contact DSO/DLO, so we get the Contact related to this Email Address, and then access the related Account from it. As a Join Key, we will use the follwing and keep the default Join Type.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20436%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/017-Joining-the-raw-consent-and-the-contacts.png) 

Joining the raw consent and the contacts

Notice the preview, we have Consent values along with their corresponding Account.

We now need to add an output to the canvas. We select the previously created Account Consent DSO/DLO, and map it that way:

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20436%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/018-Mapping-the-outputs-of-the-Data-Transform-to-the-Account-Consent-DSODLO-we-creat.png) 

Mapping the outputs of the Data Transform to the Account Consent DSODLO we creat

*Apply* and *Save* with whatever name you wish. You can now open the Data Transform, *Schedule* it, and *Run* it.

From now on, whenever a Consent is added or edited, our Data Transform will mirror those changes, as records related to the Account. We now just need to display this information 😎.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20436%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/019-Data-is-there-lets-display-it.png) 

Data is there, let’s display it.

## Adding Data Cloud Related Lists Enrichments

*Setup > Object Manager > Account > Data Cloud Related List > New*. Select Account Consent for the Data Cloud Object.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20436%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/020-Adding-the-Account-Consent-DMO-as-a-data-source-for-our-related-list.png) 

Adding the Account Consent DMO as a data source for our related list.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20436%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/021-Subscription-Consents-displayed-on-a-Person-Account-Layout.png) 

Subscription Consents displayed on a Person Account Layout.

*Next*, *Next*. Then you select the Layouts this Related List should be added to, notice you have Person Account Layouts along with standard Business Accounts Layouts (Thank Claudia Hoops for this tip 👍).

Finally, go to any Person Account record, *Setup > Edit Page.* Add a Dynamic Related List Single (in case you wonder why, this type of Related List displays only a 7 days history if displayed as a standard Related List — see screenshot above).

There we have it!

## Final Thoughts

You’ll notice the Consent Id is in fact a concatenation of the Email Address and the Subscription Id. You can modify our Data Transform, to include the   
CommSubscription\_Home DSO/DLO which contains the name of Subscription, and create a new field with the Subscription name.

We can only see subscriptions, not add or edit them. To do so, this would require a dedicated Lightning Web Component.

You can create other Related List to display data from Data Cloud. For example, you may emulate the Activity widget, which display Engagement data (from Email and Web Engagement DSO/DLO).
