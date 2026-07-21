# Handling sub-addressing in Marketing Cloud Next

**Source:** https://the-agentic-marketer.com/marketing-cloud-next-deep-dives/subaddressing-identity-resolution-data-cloud

---

*Sub-addressing* is supported by many providers. Let’s say you have an email address *[[email protected]](/cdn-cgi/l/email-protection)*, then, you can create as many email addresses as you wish using the format *[[email protected]](/cdn-cgi/l/email-protection)*, all receiving sent Emails to *[[email protected]](/cdn-cgi/l/email-protection).*

This is very handy, for instance you can use *[[email protected]](/cdn-cgi/l/email-protection)* every time you create a new account for a provider, and so easily identify which provider is sending you an Email (or what they do with you Email…).

But, from a Marketer perspective, all those Email Addresses are actually the same person, and one need to find a way to reconciliate them. Here is a step by step guide on how to do it in *Salesforce Data Cloud*, which you may implement to handle Sub-addressing in *Marketing Cloud Growth & Advanced (*as it relies on *Data Cloud)*.

If you haven’t prepared attributes, start with **[Enrich Unified Individuals](/marketing-cloud-next-deep-dives/enrich-unified-individual/)**

## First attempt (TL;DR not working)

At first, I have tried to extend the Contact Point Email DMO, by adding a Field to it, “Sub Addressing Safe Email”. Then, on every Datastream associated with a DLO mapped to Contact Point Email, I would add a Formula Field and map it to “Sub Addressing Safe Email”.

Then I would simply use the *DMO* Field, to identify same *Individuals* with distinct Email Address using Sub-addressing. There, I hit a snag 😉

[![](https://the-agentic-marketer.com/wp-content/uploads/2025/08/subadressing-idenity-resolution-data-cloud-10-1024x558.png)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/subadressing-idenity-resolution-data-cloud-10.png)

It appears that only the Email Address from the *Contact Point Email DMO* can be selected, not my new Field.

Plus, this method has a drawback: *Formula Fields* are not retroactive, meaning their value is calculated only for new records in their *Datastream*.

## Let’s Party 😎

*Party Identification* is a standard *DMO* whose function is to link Individuals with an *Identification Number*. You may have Driver License Number injected in a *Datastream/DLO* and wish to use this information as a matching Rule in identity Resolution. Inside the *Party Identification DMO*, an *Identification Type*and an *Identification Name* are used to specify the types of *Party* records we will use to match *Individuals.*

Eventually, the *Match Rules* in *Identity Resolution* will look like this :

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20436%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/subadressing-idenity-resolution-data-cloud-11.png) 

Match Rules based on Party Identification

## New DLO

We’ll create a new *DLO*, let’s call it “*Party* *Point Email (Sub-addressing free)”*, which will act as the standard *Contact Point Email*, and will contain a processed Email field, where the Sub-adressing part is removed, which we will use as an Identification Number. This *DLO* will be of type *Profile*.

This is how our *“Party* *Point Email (Sub-addressing free)”,* is mapped to the *Party Identification DMO* (tip, once adding a *DLO*, add it to your *Data Space* using the *Data Space tab* so you can map it to the *Party Identification DMO*) :

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20436%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/subadressing-idenity-resolution-data-cloud-12.png)

## Feed the new DLO

In Marketing Cloud Growth & Advanced, there are 3 *Datastreams* that are mapped to the *Contact Point Email DMO:* two from Salesforce *Leads, Contacts* and one from Experience Cloud (when a Prospect fills a Form).

We will create a *(batch)* *Data Transform* to write the Data from those *Datastreams* to our *“Party* *Point Email (Sub-addressing free)” DLO.* Here is the Data Transform used :

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20436%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/subadressing-idenity-resolution-data-cloud-13.png) 

Injecting 3 Datastreams to a DLO after processing their data

First, we Append *Leads* and *Contacts* records, using the Lead ID and Contact ID columns, along with the Email Addresses. Then we Append Email Addresses gathered from Marketing Cloud Growth & Advanced Forms to this. Finally, we create 2 columns with static text to be matched by the Match Rules of the Identity Resolution (*Party Identification Type = “Email Processing”*and *Party Identification Name = “Sub-address Removed”*).

Finally, before outputting in our *“Party* *Point Email (Sub-addressing free)” DLO,* we process the Email Addresses from these 3 sources to remove the Sub-addressing part.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20436%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/subadressing-idenity-resolution-data-cloud-14.png) 

Removing the Sub-addressing part of input Emails

SQL here was kinda tricky since only a subset of functions are available as of now in Data Cloud (batch) Data Transformation :

```
				
					case instr(Email__c, '+')
    when 0
        then 
            Email__c
        else
            replace(
              Email__c,
              substr(
                Email__c, 
                instr(Email__c, '+'), 
                instr(Email__c, '@')-instr(Email__c, '+')
               ), '')      
end
				
			
```

## 😎 And that’s it

There you have it, Individuals using Sub-addressing are now seen as a unique *Unified Individual*.  [Calculate Customer Lifetime Value (CLTV)](/marketing-cloud-next-deep-dives/calculated-insight-guide-customer-life-time-value/) next. In Data Cloud you can use *Profile Explorer* to watch those *Individuals* reconcilated (here is Data Cloud’s Unified Individual Lightning Layout with some Data Cloud Components added) :

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20436%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/subadressing-idenity-resolution-data-cloud-15.png) 

See the Identity Resolution handling Sub-addressing in Data Cloud

Or directly on a Lead or Contact in Salesforce (and *Marketing Cloud Growth & Advanced*)

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20436%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/subadressing-idenity-resolution-data-cloud-16.png) 

See the Identity Resolution handling Sub-addressing on Leads
