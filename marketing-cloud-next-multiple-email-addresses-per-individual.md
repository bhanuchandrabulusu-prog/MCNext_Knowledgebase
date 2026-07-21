# Dealing with Multiple Email Addresses per Individual in Marketing Cloud Next

**Source:** https://the-agentic-marketer.com/marketing-cloud-next-tips-from-the-trenches/marketing-cloud-next-multiple-email-addresses-per-individual

---

There are contexts in which a given Individual may have several email addresses. Think internal / external, personal / professional, etc. By default MC Next (Growth and Advanced Editions) handles the standard Email field on Prospect, Lead and Contact objects, let’s see to add another one (or more). Refer to the Data Cloud learning path to get started with [MC Next and Data Cloud](/marketing-cloud-next-learning-path/data-cloud-foundations-value/).

## Default Behaviour

Let’s illustrate the default data model and how Identity Resolution works In MC Next, using the Lead example. The default Lead\_Home DSO/DLO is ingested by the Data Cloud – Salesforce Connector: once a record is created or modified in Salesforce, a record is created or modified in Data Cloud’s record as well.

This DSO/DLO is mapped by default with several DMO in the Data Model: the Individual one and the Contact Point Email one are the ones that we are interested in.

[![](https://the-agentic-marketer.com/wp-content/uploads/2025/09/Screenshot-2025-09-17-at-13.47.45-1024x586.png)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/Screenshot-2025-09-17-at-13.47.45-scaled.png) 

The Lead\_Home DSO/DLO is mapped to the Individual DMO.

One interesting thing is that the Individual Primary key is defined as the Lead Id value.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20458%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/Screenshot-2025-09-17-at-13.47.39-scaled.png-1.webp) 

Lead\_Home has a mapping with the Contact Point Email DMO

The Primary key used is the Lead Id, as well as for the Party Field, this means, that whenever a new Lead record is created in Salesforce, an Individual Record is created and a Contact Point Email record is also created.

This is where the relationships between those DMO come into play.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20458%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/Screenshot-2025-09-17-at-14.01.15-scaled.png) 

The Individual DMO and the Contact Point Email DMO are related

This highlighted line above, states that an Individual may have several Contact Point Email associated with it, and to find all the CPE associated with an given Individual, we’ll simply look for the CPE having the Party field value equal to the Individual Id. This is why CPE’s Party Field is set to the Lead Id in the mapping. This is another illustration of [the difference between a Mapping and a Relationship](/marketing-cloud-next-tips-from-the-trenches/data-cloud-relationship-mapping/), we already talked about.

Let’s now see how this data is used by the identity resolution.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20458%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/Screenshot-2025-09-17-at-14.14.28-scaled.png) 

Simple Matching Rules in Identity Resolution

Those matching rules simply state that two persons will be considered as the same person, when their distinct Individual DMO records do have an almost identical first name, an identical last name, and one of their related Contact Point Email DMO records do have a matching email address.

From these matching Individuals, the Identity Resolution will create a single record in the Unified Individual DMO (using Reconciliation Rules to select which values to keep) and one record in the Unified Indv Contact Point DMO per distinct email address related to the matching Individuals. Those latter records are related to the Unified Individual record using the Party Field of the Unified Indv Contact Point DMO. When sending to a Unified Individual from a Segment Triggered Flow, we actually send to all Unified Indv Contact Point (provided they are opted in for the current Subscription).

So, to our initial point: handling several email addresses for a given Individual, what do we need to do?

## Handling a second email address

It’s quite simple actually, here are the steps (adjust to Prospects or Contacts, and if more than one extra email address is needed).

### Adding a new Field on the Salesforce Lead Object

You may already have one, in which case you may skip this step. Setup > Object Manager > Lead > Fields and Relationships > New. Create a new Email Field, we’ll call it Second Email.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20458%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/Screenshot-2025-09-17-at-14.40.24-2-scaled.png) 

A second Email address is added. MC Next handles the consent ootb.

We added a Second Email address in Salesforce. It appears in the Compact layout if you use one, on the Detail component, and Marketing Cloud Next (Growth and Advanced) already manages the Consent in the Privacy Consent Status default component.

### Adding a new Field to the Lead\_Home DSO/DLO

From the Lead DSO > Add Source Field and select the new Field.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20458%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/Screenshot-2025-09-17-at-14.49.02-scaled.png) 

Adding our new Field nto the DSO so that it is ingested

If you can’t see the Field, you need to give access to it to the Connector using the Data Cloud – Salesforce Connector Permission Set (see [add a new field](/marketing-cloud-next-deep-dives/new-fields-unified-individual-dmo/) article). We now have a new field in the DMO and we want to create a new record in the Contact Point Email DMO, which is almost the only thing we need to do.

The simplest idea that comes to mind for this is to open the Lead\_Home mapping, and create a mapping between Second Email and the Contact Point email DMO. But, as there is already a mapping between the standard Lead Email field and that DMO, this will fail. We do not want to replace the existing mapping.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20458%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/Screenshot-2025-09-17-at-14.57.22-scaled.png) 

We don't save the replacement, the existing mapping must remain

### Let’s create a new DLO

If we do so, and map that new DLO to the Contact Point Email DMO, then we’ll just need to fill it with the Lead’s Second Email informations, and we’ll have 2 Contact Point Email records, that the Identity Resolution will then use. We’ll define the Fields as follow.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20458%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/Screenshot-2025-09-17-at-15.06.58-scaled.png) 

Creating a new DLO to host the second Email Address

Once created, we map it that way to the Contact Point Email DMO. You may need to add that new DLO to the current Data Space if the Start button to define the mappings is not available. First we add the Contact Point Email on the right.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20458%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/Screenshot-2025-09-17-at-15.12.19-scaled.png) 

Adding the Contact Point Email DMO so we can map it.

Then we simply map our fields as follows.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20458%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/Screenshot-2025-09-17-at-15.13.59-scaled.png) 

Mappings between the new DLO and the target DMO

### Filling the new DLO

Our final step is to store the Second Email records from the Lead\_Home as records in our new DLO. We’ll use a Data Transform for this. We’ll create a Streaming one in that example, but you may use a Batch one as well (with a visual Builder).

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20458%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/Screenshot-2025-09-17-at-15.18.35-scaled.png) 

Creating a new Streaming Data Transform in Data Cloud

Give a name and define the Lead Second Email DLO we just created.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20458%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/Screenshot-2025-09-17-at-15.19.49-scaled.png) 

Defining the Data Transform target

Next we need to define the SQL query from the Lead\_Home DSO/DLO, the resulting fields of the query must match the API name of the DLO fields. We create a fake Id for the Contact Point Email Id (Primary Key) as the Lead Id is already used in the standard mapping (just appending a ‘-2’) and we only add non-empty second email addresses.

```
				
					SELECT 
Lead_Home__dll.Second_Email_c__c AS Second_Email__c,  
Lead_Home__dll.Id__c AS Party__c, 
CONCAT(Lead_Home__dll.Id__c , '-2') AS Id__c
FROM Lead_Home__dll
WHERE Lead_Home__dll.Second_Email_c__c != ''
				
			
```

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20458%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/Screenshot-2025-09-17-at-15.32.18-scaled.png) 

SQL Query for the Streaming Transform

Finally we confirm the Stream Source (in the FROM clause) is the Lead\_Home DSO/DLO, and we’re all set. We validate that the Second emails where ingested in the Lead Second Email DLO using Data Explorer (or Query Editor).

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20458%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/Screenshot-2025-09-17-at-15.36.01-scaled.png) 

Confirming the Streaming Data Transform works.

Finally, let’s open a Unified Individual, made of a Lead containing two email addresses and see if the Unified Indv Contact Point Email records were created after we manually triggered the Identity Resolution process.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20458%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/Screenshot-2025-09-17-at-15.43.42-scaled.png) 

Our Unified Individual has 2 Email Adresses.

## Final Thoughts

There we have it, we can add a second (or more) email address to the Lead object in Salesforce (and/or Prospect, Contact). When Marketing Cloud Next (Growth and Advanced Editions) performs an Email sending to a Segment, every Email Addresses will receive the Email. If you want to select which email address will receive a given communication then you can create specific Subscriptions for this, for example if you have a personal and a professional email address, then you can create a Personal and Professional Subscription, adjust the consent per Email Address type (Flows may help to automate this) and then simply choose the correct Subscription in your Flow.
