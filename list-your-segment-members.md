# 2 Methods to list your Segment members in Marketing Cloud Next

**Source:** https://the-agentic-marketer.com/marketing-cloud-next-deep-dives/list-your-segment-members

---

[EDIT 29/09/2025] **Data Cloud now has a “Preview” feature**, which can be activated in  Data Cloud Setup > Feature Manager > Segment Preview > Enable. The methods described in this article still work.

Marketing Cloud Growth and Advanced uses Unified Individuals as Segment Members. A Segment is a List of Persons you want to communicate to. Once you have created your Segment, it may be a good idea to preview which Unified Individual are actually inluded. If you haven’t assembled a reusable audience yet, start with [3 Ways to create a Subscriber List.](/marketing-cloud-next-deep-dives/create-subscriber-list/)

In this article you’ll discover 2 ways of doing this. The first one is based on a native preview in Campaign and the second one relies on Query Editor.

## Seeing the Segment Members from a Campaign

When you create a Segment Triggered Flow in a MCG/A Campaign (Single Email, Blank Email or Message Series), you are presented different options to create a new Segment, or use an existing one.

[![](https://the-agentic-marketer.com/wp-content/uploads/2025/08/009-Selecting-a-Segment-in-a-Segment-Triggered-Flow-1024x557.png)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/009-Selecting-a-Segment-in-a-Segment-Triggered-Flow.png) 

Selecting a Segment in a Segment Triggered Flow

Whatever the way you created it, once the Segment is published and you select it as Segment Trigger Flow trigger, there is a Preview button.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20435%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/010-Preview-Button-from-a-Campaign.png) 

Preview Button from a Campaign

Once you open it, your Campain Members are revealed, with their Unified Individual Ids, along with their First and Last Name. You can even search inside your member lists by one of the criteria displayed.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20435%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/011-Segment-Members-Preview.png) 

Segment Members Preview

There you have it. You can create a dummy Campaign and a Blank Email Flow, which you will use to inspect your Segment. [Waterfall Segmentation in Marketing Cloud Next explained](/marketing-cloud-next-deep-dives/waterfall-segmentation/).

## Using Query Editor to display your Segment Members

Query Editor is a handy way to write and store you SQL queries. We create a new Workspace and a first tab to start inspecting the Market Segment DMO.

```
				
					SELECT 
 "ssot__CreatedDate__c",
 "ssot__Id__c",
 "ssot__Name__c"
FROM "ssot__MarketSegment__dlm" 
ORDER BY "ssot__CreatedDate__c" DESC
				
			
```

This DMO lists all your Segment and provide the Id, along with their name and other informations. We can use it to find the Id of a given Segment knowing its name (the query is case sensitive):

```
				
					SELECT "ssot__Id__c"
FROM "ssot__MarketSegment__dlm" 
WHERE "ssot__Name__c" = 'Bamsoo staff'
				
			
```

And here is what you get.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20435%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/012-Getting-a-Segment-Id-out-of-it-name.png) 

Getting a Segment Id out of it name

We now how to get our Segment Id using Query Editor (you can also find in the URL of a Segment). We’ll be specifically interested in the Unified Individual – Latest DMO which is where the Segment Members are stored (Unified Individual – History DMO is used to handle old Members). Let’s explore it.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20435%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/013-Creating-a-tab-in-Query-Editor-to-inspect-the-Unified-Individual-Latest-DMO.png) 

Creating a tab in Query Editor to inspect the Unified Individual - Latest DMO

By removing empty columns from the query created, we land on something like:

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20435%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/014-The-content-of-theUnified-Individual-—-Latest-DMO.png) 

The content of the Unified Individual — Latest DMO

The second column is a Unified Individual Id and the Segment Id starts the same as the one we previously retrieved, unless it is 15 digits whereas the previous one was 18 digits long. By further inspecting the DMO, it looks like the Unified Individual — History DMO stores a truncated Segment Id, so we get all Unified Individual Ids of a given Segment by issuing the following SQL query which we save in a Query Editor Tab of our current Workspace.

```
				
					SELECT "Individual_Unified_SM_1730503232302__dlm"."Id__c" as "UUID"
FROM 
 "Individual_Unified_SM_1730503232302__dlm", 
 "ssot__MarketSegment__dlm"
WHERE 
 "Individual_Unified_SM_1730503232302__dlm"."Segment_Id__c"=SUBSTRING("ssot__MarketSegment__dlm"."ssot__Id__c",1,15)
 AND 
 "ssot__MarketSegment__dlm"."ssot__Name__c" = 'Bamsoo staff'
				
			
```

This gives the expected List. Note Unified Individual — History DMO has a different name when used in Query Editor (Individual\_Unified\_SM\_1730503232302\_\_dlm in our example, just drag the DMO from the left sidebar to get the actual name for your Data Cloud instance). Don’t worry, if you just drag the DMO into the Query Canvas, the correct name will be used in the resulting query.

Finally, let’s get the First and Last Name of the Segment Members so we have a similar rendering as the one from the previous method.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20435%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/015-Segment-Members-their-Id-First-Name-and-Last-Name-in-Query-Editor.png) 

Segment Members, their Id, First Name and Last Name in Query Editor

There you have it a, a reusable query to list your Segment Members (just type in your actual Segment name).

```
				
					SELECT 
     "ssot__Id__c",
     "ssot__FirstName__c",
     "ssot__LastName__c"
FROM "UnifiedIndividual__dlm" 
WHERE "ssot__Id__c" IN (
   SELECT "Individual_Unified_SM_1730503232302__dlm"."Id__c" as "UUID"
   FROM 
    "Individual_Unified_SM_1730503232302__dlm", 
    "ssot__MarketSegment__dlm"
   WHERE 
    "Individual_Unified_SM_1730503232302__dlm"."Segment_Id__c"=SUBSTRING("ssot__MarketSegment__dlm"."ssot__Id__c",1,15)
   AND 
    "ssot__MarketSegment__dlm"."ssot__Name__c" = 'YOUR SEGMENT NAME HERE'
)
				
			
```

## Final Thoughts

You can also inspect the Unified Individual Latest DMO an filter it by Segment Id in Data Explorer. This will give you the list of Unified Individual Ids, but not their First and Last Name.

Also, you may want to give a try to the beta Segment Member Verification action, that can be embedded in an Agent to verify if a given Unified Individual is in a given Segment. [See here for more details](https://medium.com/@marketingcloudtips/marketing-cloud-next-segment-member-verification-agent-18f64f4f22ba).
