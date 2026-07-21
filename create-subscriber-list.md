# 3 Ways to create a Subscriber List in Marketing Cloud Next

**Source:** https://the-agentic-marketer.com/marketing-cloud-next-deep-dives/create-subscriber-list

---

In Marketing Cloud Growth and Advanced, we have a **Subscription-based Consent model**. The Communication Subscription Consent DMO stores the Consent for a given Subscription **at the Contact Point level**. For example, that specific Email Address is OPT\_IN or OPT\_OUT for the Newsletter subscription. [Consent Management Deep Dive](/marketing-cloud-next-deep-dives/consent-management/)

But, in MCG/A, Persons are modelled as Unified Individual, and a **Unified Individual can have several Email Addresses** (more on this below). Hence, a Unified Individual is not direcly OPT\_IN our OPT\_OUT for a given Subscription. **In this article we will list (using 3 distinct methods) all Unified Individual having at least one Email Address opted in for a given Subscription**. This is just a choice (another could have been that none of the related Email Addresses should be opted out). Remember that Marketing Cloud Next is opted out by default, which means if no records are found in the Consent DMO, the Email Address is opted out, and an opted in record must be found so the Email Address is opted in (must be the most recent one in case V1 and V2 Consent models were used).

Let’s now describe 3 ways to list Susbscribed Unified Individuals for a given Subscription.

## First Method: Using Query Editor

Query Editor is a Data Cloud feature, in which you can execute SQL queries and store them in workspaces, so you can re-run them later.

Most of the time, you know your Subscription by is name (“Marketing” is the default, you may have created others like “Events” or “Newsletter”) and its Engagement Channel (Email, Phone or Whatsapp) as a Subscription may have multiple Channels.

### Get the Subscription Id from its Name and Channel

In *Data Cloud > Query Editor*, we create a new Workspace and a new Tab with the following Query (Adjust to your own Subscription Name):

```
				
					SELECT "ssot__Id__c" 
FROM "ssot__CommunicationSubscriptionChannelType__dlm" 
WHERE "ssot__CommunicationSubscriptionId__c" = (
   SELECT "ssot__Id__c"
 FROM "ssot__CommunicationSubscription__dlm" 
 WHERE "ssot__Name__c" = 'Marketing'
) 
AND 
"ssot__EngagementChannelTypeId__c" = (
 SELECT "ssot__Id__c" 
 FROM "ssot__EngagementChannelType__dlm" 
 WHERE "ssot__Name__c" = 'Email'
)
				
			
```

Which give us the Id we need to query the Communication Subscription Consent we need.

[![](https://the-agentic-marketer.com/wp-content/uploads/2025/08/009-Getting-the-Subscription-Id-from-its-Name-and-Channel-Type-1024x557.png)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/009-Getting-the-Subscription-Id-from-its-Name-and-Channel-Type.png) 

Getting the Subscription Id from its Name and Channel Type

### Get opted in Email Addresses

We will now reuse this query to get the List of Email Addresses explicitly opted in. Note: for Orgs created prior to the Summer ’25 release, there may be 2 records in the Communication Consent DMO for a given Subscription and Email Address due to the Consent evolution from V1 to V2. In this article, we deal with V2 Consent Management only.

Here is how to get all Email Addresses actually opted in from the Communication Subscription Consent DMO:

```
				
					SELECT "ssot__ContactPointValueText__c"
FROM "ssot__CommunicationSubscriptionConsent__dlm" 
WHERE "ssot__CommunicationSubscriptionChannelTypeId__c" = (
  SELECT "ssot__Id__c" 
 FROM "ssot__CommunicationSubscriptionChannelType__dlm" 
 WHERE "ssot__CommunicationSubscriptionId__c" = (
    SELECT "ssot__Id__c"
  FROM "ssot__CommunicationSubscription__dlm" 
  WHERE "ssot__Name__c" = 'Marketing'
 ) 
   AND 
   "ssot__EngagementChannelTypeId__c" = (
  SELECT "ssot__Id__c" 
  FROM "ssot__EngagementChannelType__dlm" 
  WHERE "ssot__Name__c" = 'Email'
 )
) 
AND "ssot__ConsentStatus__c" = 'OPT_IN'
				
			
```

As opted in is explicit, we simply select all email addresses with OPT\_IN value for the Consent and the Subscription id is simply the result of our previous query (we could have also just pasted the result of the previous query).

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20435%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/010-Getting-all-Subscribed-Email-Addresses-for-given-Subscription-out-of-is-name-an.png) 

Getting all Subscribed Email Addresses for given Subscription (out of is name an

### List the Subscribed Unified Individual

So now we need to go from the Email Address to the Unified Individual. For this, we will use the Unified Indv Contact Point Email DMO, which is created during the Identity Resolution, and creates all Email Contact Points related to a given Unified Individual.

Remember or definition of a Subscribed Unified Individual, it is a Unified Individual having at least one opted in Email Address for a given Subscription (identified by its Name and Channel).

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20435%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/011-The-Unified-Indv-Contact-Point-Email-DMO-ties-a-given-Unified-Individual-and-its.png) 

The Unified Indv Contact Point Email DMO ties a given Unified Individual and its

Note: you may not see the Communication Subscription Consent DMO. This is a relationship we’ll be creating in our Second Method 😎.

```
				
					SELECT "ssot__PartyId__c"
FROM "UnifiedContactPointEmail__dlm" 
WHERE "ssot__EmailAddress__c" in (
   SELECT "ssot__ContactPointValueText__c"
 FROM "ssot__CommunicationSubscriptionConsent__dlm" 
 WHERE "ssot__CommunicationSubscriptionChannelTypeId__c" = (
    SELECT "ssot__Id__c" 
  FROM "ssot__CommunicationSubscriptionChannelType__dlm" 
  WHERE "ssot__CommunicationSubscriptionId__c" = (
     SELECT "ssot__Id__c"
   FROM "ssot__CommunicationSubscription__dlm" 
   WHERE "ssot__Name__c" = 'Marketing'
  ) 
    AND 
    "ssot__EngagementChannelTypeId__c" = (
   SELECT "ssot__Id__c" 
   FROM "ssot__EngagementChannelType__dlm" 
   WHERE "ssot__Name__c" = 'Email'
  )
 ) 
 AND "ssot__ConsentStatus__c" = 'OPT_IN'
)
				
			
```

So far we have all subscribed Unified Individual Id:

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20435%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/012-A-list-of-Unified-Individual-Subscribed-to-a-given-Subscription-out-of-is-name.png) 

A list of Unified Individual Subscribed to a given Subscription (out of is name

Let’s make it more easy to read by adding the First and Last Name of the Unified Individual:

```
				
					SELECT "ssot__Id__c",
    "ssot__FirstName__c",
    "ssot__LastName__c"
FROM "UnifiedIndividual__dlm" 
WHERE "ssot__Id__c" in (
 SELECT "ssot__PartyId__c"
 FROM "UnifiedContactPointEmail__dlm" 
 WHERE "ssot__EmailAddress__c" in (
  SELECT "ssot__ContactPointValueText__c"
  FROM "ssot__CommunicationSubscriptionConsent__dlm" 
  WHERE "ssot__CommunicationSubscriptionChannelTypeId__c" = (
   SELECT "ssot__Id__c" 
   FROM "ssot__CommunicationSubscriptionChannelType__dlm" 
   WHERE "ssot__CommunicationSubscriptionId__c" = (
    SELECT "ssot__Id__c"
    FROM "ssot__CommunicationSubscription__dlm" 
    WHERE "ssot__Name__c" = 'Marketing'
   ) 
   AND 
   "ssot__EngagementChannelTypeId__c" = (
    SELECT "ssot__Id__c" 
    FROM "ssot__EngagementChannelType__dlm" 
    WHERE "ssot__Name__c" = 'Email'
   )
  ) 
  AND "ssot__ConsentStatus__c" = 'OPT_IN'
 )
)
				
			
```

There we have it, the Subscriber List query for a given Subscription (just replace the Subscription Name and Channel, and if using a different Channel, adjust the Contact points accordingly).

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20435%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/013-Subscriber-List-using-Query-Editor.png) 

Subscriber List using Query Editor.

## Second Method: Creating a Segment

### Linking the Unified Individual DMO and the Consent in Data Cloud

By default, the Communication Subscription Consent is indirectly linked to the Unified Individual DMO using the Individual DMO. We will deactivate this relationship, as it relies on a joining field which the Consent system does not fill.

As we already mentioned it above, we will rather create an extra relationship between the Unified Indv Contact Point Email DMO and the Communication Subscription Consent DMO. We will do this by editing its Relationship tab as follow:

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20435%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/014-Disabling-the-Individual-DMO-relationship-and-creating-a-new-one-with-the-Unifie.png) 

Disabling the Individual DMO relationship and creating a new one with the Unifie

### Creating a Segment of Subscribers, the Subscription Criteria

We create a new Segment, and in the Related Attributes, we open the Communication Subscription Consent DMO.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20435%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/015-Creating-a-new-Segment.png) 

Creating a new Segment

We then drag the Communication Subscription Channel Type to the Canvas (this is the first field, hover over a field for some time to get its complete name).

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20435%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/016-Setting-the-Subscription-Criteria.png) 

Setting the Subscription Criteria

The Value can be found using the query in the first method. We keep the Measurement, operator and value to the default: we are looking for Unified Individuals having at least one opted in email address (we’ll add this as our next criteria).

Note on the Container Path, which is a way of going from on DMO to another by using the Relationships between them. By default Data Cloud selects the shortest. Here we use the default *Communication Subscription Consent.Contact Point Value > Unified Indv Contact Point Email.Party > Unified Individual.Unified Individual Id.* This means: select all the records in the Communication Subscription DMO matching the criteria on the canvas. Get all related Unified Indv Contact Point Email (this is the relationship we created earlier) using the Contact Point Value field. Then using the Party Field of that latter DMO get the Unified Individual Ids and add them in the Segment. The joining field is only specified for the left DMO for example *Communication Subscription Consent.Contact Point Value* is defined using the *Unified Indv Contact Point Email.Email Address* but only the *Unified Indv Contact Point Email.Party* is displayed in the Container.

### Creating a Segment of Subscribers, the Consent Criteria

Then we add the Consent Status, by draging it to the canvas using the Add related Attribute here (we want two critreria in one container, not two containers with one criteria, this may lead to a different result). We’ll use OPT\_IN for the value.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20435%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/017-2-Segment-criteria.png) 

2 Segment criteria

And there we have it, if we scheduled this Segment to be refreshed, then we have a list of subscribed Unified Individual which can be used to be segmented further (used as Segment criteria) or simply to send an Email using a Segment Trigger Flow.

We coud get the list of non-subscribed Unified Individual by creating another list and use our Segment as an Exclude criteria.

You can use one of the two techniques described if you to view the [list of actual Segment Members](/marketing-cloud-next-deep-dives/list-your-segment-members/).

## Creating a Segment of Subscribers using a Calculated Insight

Using this method, we will streamline the creation of a Segment, but we will also be a able to display the number of opted in Email Addresses at the Lead or Contact level.

### Creating a Calculated Insight

In *Data Cloud > Calculated Insight > +New* and use the following options.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20435%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/018-A-new-Calculated-Insight-created-with-the-visual-builder.png) 

A new Calculated Insight created with the visual builder.

We use the visual builder (we could have used a Streaming Calculated Insight, as we already did the SQL design the first method above), and use the Unified Indv Contact Point Email DMO as the Input Data.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20435%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/019-Unified-Indv-Contact-Point-Email-used-as-Input-Data.png) 

Unified Indv Contact Point Email used as Input Data

Then we add a Join Element to join our Unified Indv Contact Point Email DMO with the Communication Subscription Consent DMO: here we leverage the relationship we created in the previous method. We use the *Unified Indv Contact Point Email.Email Address* and *Communication Subscription Consent.Contact Point Value* in a *LEFT JOIN* statement.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20435%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/020-Getting-all-Consent-Records-for-every-Email-Addresses-of-the-Unified-Indv-Contac.png) 

Getting all Consent Records for every Email Addresses of the Unified Indv Contact

We then get all the associated Unified Individuals linked with the Unified Indv Contact Point Email records by using the following joining fields *Unified Individuals.Id = Unified Indv Contact Point Email.Party* in an *INNER JOIN.*

It may sound familiar, if you read the First Method in this article: we are leveraging the Builder but actually using the same logic we used previously.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20435%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/021-Getting-all-Unified-Individual-Ids.png) 

Getting all Unified Individual Ids

Then we’ll filter the results to keep only OPT\_IN records regarding the specific Subscription (Marketing here, identified by its Id).

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20435%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/022-Filtering-the-results-by-Subscription-and-Consent.png) 

Filtering the results by Subscription and Consent

Finally we group the resulting Unified Individual, which is needed in an Calculated Insight that can be displayed on Leads and Contacts. We do this by adding an Aggregate element, counting the disctinct subscribed Email Addresses (Count used as a Measure) for a given Unified individual (Id used as Dimension).

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20435%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/023-Finally-aggregating-the-counting-COUNT-by-Unified-Individual-GROUP-BY.png) 

Finally, aggregating the counting (COUNT) by Unified Individual (GROUP BY)

*+Save and Run* and Schedule when you want your Calculated Insight to be refreshed. And finally *Publish* your Calculated Insight.

There you have it, a Calculated Insight which can be used to display the Subscriber List for a given Subscription and Channel, but not only.

### Viewing the Subscriber List from Data Explorer

Once your Calculated Insight has run, you can display its content in Data Explorer. You may also filter the results if you need it.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20435%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/024-Subscriber-List-by-displaying-a-Calculated-Insight.png) 

Subscriber List by displaying a Calculated Insight

### Creating a Segment using the Calculated Insight as a criteria

Every Calculated Insight can be used as Segmenting criteria. They are available as a direct Attribute of the Unified Individual DMO. Drag our measure name, and specify it must be at least one (a Unified Individual is defined as a Person with at one Email Address in this article).

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20435%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/025-A-Calculated-insight-based-Segment.png) 

A Calculated insight based Segment

### Displaying the number of Subscribed Email Addresses on Leads and Contacts

On Prospect, Leads and Contacts, Calculated can displayed using the *Data Cloud Profile Insight Component.*

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20435%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/026-Adding-the-Calculated-Insight-to-the-Lead-Layout.png) 

Adding the Calculated Insight to the Lead Layout

We define the component parameter as show: in the Default Data Space, display the Calculated Insight related to the Unified Individual linked to the Current Individual (Lead) using the Unified Individual Link junction object.
