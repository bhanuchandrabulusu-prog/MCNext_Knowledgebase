# Data Cloud survival guide for Marketing Cloud Next

**Source:** https://the-agentic-marketer.com/marketing-cloud-next-deep-dives/data-cloud-survival-guide-for-marketers

---

**Marketing Cloud Next (Growth and Advanced) heavily relies on Data Cloud. Here is what you need to know, from a Marketer perspective.**

Ready to extend the profile already? See **[Add new fields to Unified Individual](/marketing-cloud-next-deep-dives/new-fields-unified-individual-dmo)**.

## Glossary

First, let’s define some currently used terms in the Data Cloud realm.

### Data Stream Object

This is a set a records imported into Data Cloud from other systems, like a CRM or a Commerce solution. This is a very similar to Data Lake Objects, except the latter is persistent.

### Data Model Objects

Those objects constitute a standard way of storing data. You way have different Commerce solutions for example, but at the end of the day, a Case is a Case, wether it comes from Service Cloud or another system.

### Individual

This a universal DMO representing a Person.

### Unified Individual

Data Cloud aggregates all identical Individuals into a single Unified Individual, stored in the so-called DMO. Contact Points like Email Addresses or Phone numbers are also linked a Unified Individual during the Identity Resolution Process. [Add new fields to the Unified Individual DMO](/marketing-cloud-next-deep-dives/new-fields-unified-individual-dmo/).

### Data Graph

This is a customisable view of a Unified Individual. You add into it all the informations you need to personnalise your communications or take decisions inside your Flows. Data Cloud keeps it up to date for you.

### Calculated Insights

Those are measures to describe your Unified Individual. Marketing Cloud Next comes with the Scoring. Those are the main concepts we will be using in this survival guide.

## Data Model

### Person Management

In Marketing Cloud Next, you will have access to a brand-new concept of person record: meet the Unified Individuals. You may have different types of person record, for example, Contacts and Leads stored within your CRM, as well as external records, such as those in your e-commerce solution. All this information will be ingested within Data Cloud in what we call Data Stream Objects (or Data Lake Objects, similar concept).

[![](https://the-agentic-marketer.com/wp-content/uploads/2025/08/009-Profile-Ingestion-1024x699.png)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/009-Profile-Ingestion.png) 

Profile Ingestion

Data Cloud includes predefined objects called DMOs (Data Model Objects). One of these is the Individual DMO, a standardized representation of a Person. Ingested Profile into Data Streams are mapped to the Individual DMO, ensuring that all Profile records are stored in a single location, as standardised records.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20355%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/010-Profile-Ingestion-Harmonisation-in-Data-Cloud.png) 

Profile Ingestion & Harmonisation in Data Cloud

The mapping is an easy process in Data Cloud, and it is done in the setup phase, here is how it looks like. Note that the Id used to identify an Individual is its Salesforce Record Id (Lead Id for example).

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20444%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/011-Leads-are-mapped-to-the-Individual-DMO.png) 

Leads are mapped to the Individual DMO

The Identity Resolution process will then aggregate all identical Individuals into a Unified Individual by applying Match Rules — answering the question, ‘What makes two individuals identical?’ — and using Reconciliation Rules — answering, ‘If two individuals are identical and we have different informations, which should take precedence?’

A basic Identity Resolution is installed during the setup (email address based) and can modified.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20358%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/012-Identity-Resolution-creates-Unified-Individual-out-of-Individuals.png) 

Identity Resolution creates Unified Individual out of Individuals

Your person records may also be associated with Contact Points, like Email Addresses, Phone Numbers, Physical Addresses. At Ingestion time, a Lead for instance is mapped to the Contact Point Email object, a standardised representation of what an email address is.

The Identity Resolution process creates both Unified Individual and Unified Individual Contact Points which are related. So when sending an Email to a Unified Individual, the communication will actually be sent to all the associated Unified Individual Contact Point Emails.

### Customer 360 Model

So far, we have introduced the Individual, Unified Individual and Contact Points DMO. In fact, Data Cloud comes with a lot of other DMO, and their relationships. This constitutes a standardised view for all king of business needs (as well as foundation for AI efficiency), and can extended with your own.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20646%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/013-The-Individual-DMO-and-its-related-other-DMOs.png) 

The Individual DMO and its related other DMOs

## Other interesting Objects

### Engagement Data

There are 2 interesting DMOs in Data Cloud, which are filled with interactions your audience has with your brand. Email Engagement and Web Engagement. The source can be Marketing Cloud Next (Growth & Advanced) assets like Emails or Landing Pages or other tools’ assets like Account Engagement ones.

In the Email Engagement DMO, you will find Email Sends, Open, Clicks, Unsubscribe and bounces.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20444%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/014-Email-Engagement-DMO.png) 

Email Engagement DMO

In the Web Engagement DMO, you will find Page views (with UTMs), Form Submitted, etc.

### Consent

You define if a Person is Optin or Optout for a given Subscription Channel. For example you may have a Newsletter and Generic Announcement Email Channels. You can define Consent from a Lead or Contact, by Importing a file or using a Flow.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20232%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/015-DMOs-involved-in-Consent-Management-in-Data-Cloud.png) 

DMOs involved in Consent Management in Data Cloud.

Note: that creating a N:1 Relationship between the Communication Subscription Consent DMO and the Contact Point Email DMO allows for any Segmentation based on Consent.

### Other DMOs

You may find Email Engagement Frequency and Email Engagement Score useful. They are filled by AI to give you insight regarding Email fatigue and Score.

In fact, everything Marketing Cloud Next related is stored in Data Cloud, we’ve just seen the most important ones, but of course, depending on your use-cases, others may come useful (Prospect, Campaigns, etc).

## Using this Data

### Viewing Unified Individual data

Even though you can access the Unified Individual directly inside Data Cloud, the common way of displaying data is to add Data Cloud informations on the Lead and Contact Layouts. This is done a setup time.

For example, the activity Widget gives you a view on a time lime of Engagements Data. This is not only related the Current Contact Points the specific Individual is linked with, but to all Contact Points of the Unified Individual this specific Individual belongs to.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20448%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/016-1-Viewing-Activity-2-Calculated-Insights-more-coming-3-Consent-Management.png) 

1- Viewing Activity, 2- Calculated Insights (more coming), 3- Consent Management

### Calculated Insights (ex. scoring)

Data Cloud gives you a handy way to create metrics out of your Unified Individual and Individual data. Overall Marketing is an example of pre-created Calculated Insights, brought to you by Marketing Cloud Next and calculated based on the Engagemeny Data stored in Email and Web Engagement DMOs. You can also create your own, build a [Customer Lifetime Value (CLTV) metric](/marketing-cloud-next-deep-dives/calculated-insight-guide-customer-life-time-value/)

### Data Graphs

You can create a representation of your Unified Individuals using one or more Data Graph. Those informations will be made available as Merge Fields inside the Email Builder, to create Email Personnalisation or take actions based on their value in your Marketing Flows.

There is a default Data Graph used by Marketing Cloud Next (Growth and Advanced) in the Email Builder and Flows (you can choose another Data Graph for each Flow if you wish).

Calculated Insights can also be added in a Data Graph.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20444%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/017-A-Datagraph-represents-your-Unified-Individuals.png) 

A Datagraph represents your Unified Individuals

### Segments

A Segment is a list of Unified Individual with the same Criteria. You can create them directly from a Marketing Cloud Next Campaign.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20556%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/018-Create-a-Segment-directly-from-a-Marketing-Cloud-Next-Campaign.png) 

Create a Segment directly from a Marketing Cloud Next Campaign

You can also create them in Data Cloud, either using a handy builder on simply by using an AI prompt.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20444%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/019-A-segment-in-Data-Cloud.png) 

A segment in Data Cloud

Segments needs to be published and regularly refreshed, so they are up to date as it pertains to matching Unified Individual.

## Credits

There are different types of credits consumed depending on the type of operations you are doing.

Per million rows processed :

- Ingestion: Batch: 2000 credits / Streaming: 5000 credits
- Profile Unification: 100000 credits
- Calculated Insights: Batch: 15 credits / Streaming: 800 credits
- AI Prompts: on the prompt length, …

Email, SMS, WA messages are unit-based.

Marketing Cloud Next (Growth & Advanced) already comes with credits, and you can buy more if you need:

```
				
					+------------------------------------+------------------------------------+
|           Growth Edition           |          Advanced Edition          |
+------------------------------------+------------------------------------+
| 180K Email Credits/yr              | 360K Email Credits/yr              |
| 20K AI Request Credits             | 100K AI Request Credits            |
| 240K Data Cloud Service credits    | 480K Data Cloud Service credits    |
| 10K Segment and Activation credits | 20K Segment and Activation credits |
| 1 TB Data Cloud storage credits    | 1 TB Data Cloud storage credits    |
| 500 Active Flows                   | 750 Active Flows                   |
+------------------------------------+------------------------------------+
				
			
```

The best way to monitor your credit consumption is to use the Digital Wallet (aka Consumption Cards).

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20444%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/020-Digital-Wallet-to-keep-an-eye-on-your-credits-consumption.png) 

Digital Wallet to keep an eye on your credits consumption

The best way to monitor your credit consumption is to use the Digital Wallet (aka Consumption Cards).
