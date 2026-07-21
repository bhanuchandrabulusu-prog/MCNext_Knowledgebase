# Marketing Cloud Next: Campaign management in Segment Triggered Flows

**Source:** https://the-agentic-marketer.com/marketing-cloud-next-deep-dives/campaign-management-segment-triggered-flows

---

[**Edit 29/04/2026**: Since Spring ’26, Segment Triggered Flows have a native “Create Campaign Member” activity that can create or update Campaign Members, directly at the Unified Individual level. The rest of this article is still relevant, as it show some Flow best practices.]

**Segments are Segment Triggered Flows inputs, and they are made of Unified Individuals. Those cannot be added to Campaigns. In this article, we’ll create a reusable Sub Flow to Create or Update Campaign Members for underlying Individuals. [Send a message when something changes in Salesforce](/marketing-cloud-next-deep-dives/send-message-changes-salesforce/)**

## Creating the Sub Flow

First, we’ll create the Sub Flow. *Setup > Flows > New Flow > Start From Scratch > Autolaunched Flow (No trigger) > Create.*

This type of Flows can be launched from a caller Flow (our Segment Triggered Flow), and can be passed parameters from it. This types of Flows are standard Flows, not Marketing Flows, you may need to ask your Administrator to create it if you cannot create this type of Flow.

### Add Input Resources

Let’s create three parameters, the Id of the Unified Individual, the Campaign Id and the Campaign Member status. Open the left panel, then

- New Ressource
- **Ressource Type**: Variable
- **API Name**: UnifiedIndividualId
- **Data Type**: Text
- Available for input: **checked**

Do the same for **CampaignId** and **MemberStatus**. This is what you should have so far:

[![](https://the-agentic-marketer.com/wp-content/uploads/2025/08/009-Three-inputs-to-create-our-Campaign-Members-1024x558.png)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/009-Three-inputs-to-create-our-Campaign-Members.png) 

Three inputs to create our Campaign Members

## Retrieve the underlying Individuals

We’ve gone previously through the internals of the Identity Resolution Process. Basically a Unified Individual is a set of identical Individuals (Prospects, Leads, Contact, Visitors). What ties a Unified Individual and its underlying Individuals is a DMO called Unified Link Individual. See it as a table containing the Individual ID (*SourceRecordId\_\_c*) as a primary key (those are Salesforce Record Ids: Prospect Ids, Lead Ids and Contact Ids) along with their associated Unified Individual Ids (*UnifiedRecordId\_\_c*).

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20395%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/010-The-Unified-Link-Individual-DMO-ties-a-Unified-Individual-and-its-underlying-Ind.png) 

The Unified Link Individual DMO ties a Unified Individual and its underlying Ind

We’ll leverage this by using a Get Record Element on the Unified Link Individual Data Cloud DMO:

- Click the **circled plus** sign in the Flow
- Add a **Get Record** activity (pink)
- **Label**: Get Underlying Individuals (API name, use the default)
- **Data Source**: Data Cloud Object
- **Data Space**: Default (or whatever Data Space you use)
- **Object**: Unified Link Individual
- **Filter Conditions**: All Conditions is met
- **Field**: UnifiedRecordId\_\_c, **Operator**: Equals, **Value**: **UnifiedIndividualID**(in the Variables section)
- **How Many Records to Store**: All Records
- **How to Store Record Data**: Automatically store all fields
- Click the **cross sign** to close the right panel

So far, we created a Collection of Unified Link Individuals for every Individuals. But, our plan is to create Campaign Members, and, Campaign Members are only related to Leads or Contacts, so we need to only get those type of Individuals. On top of that, Campaign Members are related to Leads or Contacts using two distinct Fields.

For this reason, we will change our Flow to get a separate list of Contacts and Leads. Let’s remove the Get Underlying Individuals activity from the Flow add a new one to get Contacts only.

Those are the exact same step as above, but we will use Get Underlying Contacts for the Get Record activity name and we will add a new Filter Record Condition: **Field**: SourceRecordId\_\_c, **Operator**: Starts With, **Value**: 003.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20436%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/011-Get-Underlying-Contacts-by-selecting-Contacts-from-the-Unified-Link-Individual-D.png) 

Get Underlying Contacts by selecting Contacts from the Unified Link Individual D

We’ll not handle the Campaign Members creation / update actions inside this Flow, to make it more readable, we’ll create two more Flows (one for Contact Campaign Members and one for Lead Campaign Members). This Flows will receive a List of Contact Ids (and Lead Ids). Let’s start by extracting the Contact Ids from our previous Step (Get Underlying Contacts). Directly after the first activity:

- Click the **circled plus** sign in the Flow
- Add a **Transform** Element
- **Label**: Contacts Ids
- **Source Data**, click the plus sign and add the Record Collection Variable from our previous activity
- **Target Data**, click the plus sign, **Data Type**: Text. **Allow multiple values (collection)**: checked. Create.
- Click the Circle next to SourceRecordId\_\_c and the one next to Contact Ids Collections to link them.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20436%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/012-Getting-Contact-Ids-from-the-Contact-collection.png) 

Getting Contact Ids from the Contact collection.

We now have a usable collections containing the Ids of our Contacts to add (or update) as Campaign Members. Before we use it, in a new Flow, we will do the same steps for the Leads. Create a Get Underlying Leads activity, identical as Get Underlying Contacts, but using 00Q instead of 003 in the Filter Records Conditions, and extract Lead Ids using a similar Transform Element.

Let’s Save our Flow. We recommend using a consistent Prefix for all your Marketing Flows, so you can find them easily to add them (we use “MCC – “ for this). Let’s call it “MCC – Add Unified Individual to Campaign”

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20436%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/013-Contact-Ids-and-Lead-Ids-are-ready-to-be-passed-to-new-Flows-for-Campaign-Member.png) 

Contact Ids and Lead Ids are ready to be passed to new Flows for Campaign Member

### Flow Best Practice (the “No pink in loop” rule)

Before we dive into our new Flow, it’s important to have in mind, that we should use the Transform activity every time we can, specifically trying to avoid using Loops: it is more scalable and faster.

For example, in the previous example, we could have looped over the Unified Link Individual Records and for each record add a Decision Split on the record Type. In case of a Lead assign it to a predefined Collection Variable, else, in case in Contact assign it to another Collection Variable. Avoid this, as it is less performant.

And what you should avoid above everything else, is using a Get Records inside a Loop: it counts as one SOQL query, and depending on your flow, it might not take many loop iterations to reach the SOQL Query limit. Remember this as the ***“No pink in Loops”*** rule, do not use any Pink Element in your Loops (Create, Update, Get and Delete Elements are Pink Elements).

Previously, you might have used Assignment elements within the loop and Update Records elements outside the loop to update multiple record values. However, this approach alone is no longer considered best practice.

### Add/Update Contacts as Campaign Members

So let’s create a Flow that our Sub Flow “MCC — Add Unified Individual to Campaign” will call (a Sub Sub Flow 😎, but we won’t call directly). We’ll use an Autolaunched Flow as well, and recreate the exact same variables that we declared for our previous Flow: **UnifiedIndividualId**, **CampaignId** and **MemberStatus.** Plus, we will add a new variable:

- New Ressource
- **Ressource Type**: Variable
- **API Name**: Ids
- **Data Type**: Text
- Allow multiple values (collection): **checked**
- Available for input: **checked**

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20436%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/014-Adding-Contact-Ids-as-an-Input.png) 

Adding Contact Ids as an Input

Campaign Members can only have one record per Contact (or Lead) and Campaign, and so, we cannot create Campaign Members if they already exist (otherwise your Flow will error at runtime), which is why we start by getting existing Campaign Members from the Contact Id list we get as a Flow input. Add a Get Record:

- **Label**: Get existing Campaign Members
- **Data Source**: Salesforce Object
- **Object**: Campaign Member
- **Condition Requirements**: All Conditions are met (AND)
- **First Campaign Member Field**: Campaign Id, **Operator**: Equals, **Value**: Campaign Id (input parameter)
- **Second Campaign Member Field:** Contact Id, **Operator**: In, **Value**: Ids (input parameter)
- **How Many Records to Store**: All Records
- **How to Store Record Data**: Automatically store all fields

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20436%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/015-Getting-existing-Campaign-Members-from-the-Contact-Ids-inputs.png) 

Getting existing Campaign Members from the Contact Ids inputs

Next, let’s extract only the Contact Ids from this list or Campaign Member Records, using a Transform element:

- **Label**: Existing Campaign Members Ids
- **Source** **Data**: our previous activity
- **Target Data**, **Data Type**: Text, **Allow multiple values (collection)**: checked, Create.
- **Link** Contact Id Field in Source Data and the previous Field in Target Data.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20436%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/016-Extracting-Contact-Ids-which-are-Campaign-Members-already.png) 

Extracting Contact Ids which are Campaign Members already

From this, we will get non existing Campaign Members out of the input Contacts list. We’ll leverage the “IN” and “NOT IN” operators type in Get Records, which are very handy here (avoiding Loops 😎).

- Add a Get Record (pink) activity, **Label**: Get non existing Campaign Members
- **Data Source**: Salesforce Object, **Object**: Contact
- **Condition** **Requirements**: All Conditions Are Met
- **First Contact Field**: Id, **Operator**: In, **Value**: Ids (input parameter)
- **Second Contact Field**: Id, **Operator**: Not In, **Value**: Existing Campaign Member Ids (output of our previous Transform activity)
- **How Many Records to Store**: All records
- **How to Store Record Data**: Automatically store all fields

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20436%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/017-Campaign-Members-to-Create-are-Contacts-in-the-input-list-underlying-the-Unified.png) 

Campaign Members to Create are Contacts in the input list underlying the Unified Individual and not in the list of already existing Campaign Members

Before we create the Campaign Members to create or update, we need to extract a Collection of non existing Campaign Members. Create a Transform:

- **Label**: Non Existing Campaign Member Ids
- **Source Data**: our previous Get Records activity (“Get non existing Campaign Members”)
- **Target Data**, **Data Type**: Text, **Allow multiple values (collection)**: checked, Create.
- **Link** Id Field in Source Data and the previous Field in Target Data.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20436%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/018-campaign-management-segment-triggered-flows.png)

Let’s create a Collection of Campaign Members, with the correct Member Status (which may already be the case), so we can update them. Let’s add a new Transform Activity. For this, we will use a Transform activity again, but instead of using a Collection as a target, we will use Campaign members. In the target, we will add the Member Status and the Campaign Member Id (so the update activity knows where to apply the new Member Status).

- New Transfrom, **Label**: Campaign Members to update
- Source Data: **Get existing Campaign Members**
- **Target Data**, **Data Type**: Records, **Allow multiple values (collection)**: checked, **Object**: Campaign Member, Create
- Link the Id Field in Source Data, and the Id Field in Target Data
- Click next to the Status Field in the Target Data so the “fx” (formula) tag appears

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20436%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/019-Well-define-the-Member-Status-using-our-input-parameter.png) 

We’ll define the Member Status using our input parameter

Click formula, and select out Member Status input parameter

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20436%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/020-Setting-the-new-Member-Status-to-the-value-defined-as-a-Flow-input-parameter.png) 

Setting the new Member Status to the value defined as a Flow input parameter

Here is the final Transform “Campaign Members to update” activity:

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20436%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/021-Campaign-Members-records-to-update.png) 

Campaign Members records to update

We can now update our existing Campaign Members, by using the previous Transform output in an Update Records (pink) activity.

- Add an Update Record Element, **Label**: Update Campaign Members
- **How to Find Records to Update and Set Their Values**: Use the IDs and all field values from a record or record collection
- **Record or Record Collection**: Campaign Members from Campaign Members to Update

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20436%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/022-Using-our-previously-created-Collection-in-the-previous-Transform-Activity.png) 

Using our previously created Collection in the previous Transform Activity

Next, we will create the Campaign Members with another Transform Element:

- **Label**: Campaign Members to create
- **Source** **Data**: **Contacts from Get non existing Campaign Members**

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20436%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/023-Selecting-Contacts-to-create-as-Campaign-Members.png) 

Selecting Contacts to create as Campaign Members

- **Target Data**, **Data Type**: Records, **Allow multiple values (collection)**: checked, **Object**: Campaign Member, Create
- Link the Id Field in Source Data (Contacts), and the Contact Id Field in Target Data (Campaign Member)
- Click next to the Status Field in the Target Data so the “fx” (formula) tag appears, Click formula, and select out Member Status input parameter
- Click next to the Campaign Id Field in the Target Data so the “fx” (formula) tag appears, Click formula, and select out CampaignId input parameter

We now have our Campaign Members ready to be created, let’s add a (pink) Create Records Element:

- **Label**: Create Campaign Members
- **How to set record field values**: From a Record Variable
- **How Many Records to Create**: Multiple
- **Record Collection**: Campaign Members from Campaign Members to Create
- **Update Existing Records**: unchecked

There we have it, a Sub Flow, getting the Campaign Id, the Member Status and a List of Contacts Id, creating non existing Member Campaigns and updating existing.

Let’s **Save** it and call it “MCC – Add Contacts to Campaign”, and then let’s **Activate** it.

### Add/Update Leads as Campaign Members

We could go through the exact same steps we took for the previous section to create “MCC — Add Contacts to Campaign”, but, as the structure is the same, we’ll copy and edit the Flow we just created so it handles Leads.

From “MCC — Add Contacts to Campaign”, click the arrow next to “Save as New Version” so you can click on “Save as new Flow”.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20436%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/024-Reusing-our-Flow-by-adapting-it-for-Leads.png) 

Reusing our Flow by adapting it for Leads

By reviewing how activities should be modified to handle Leads instead of Contacts, you’ll see which need modifications and which don’t, and you may be able to apply them, as the logic is exactly the one we’ve just gone through.

One interesting point is that Converted Leads cannot be updated or created as Campaign Members. Although invisible from Salesforce, they are ingested by Data Cloud and so you need to remove them from “MCC — Add Leads to Campaign”. Add a Get Record using all passed as the Ids Collection Lead Ids, but with an extra criteria IsConverted must be false. Create a Transform to get only Ids and use that latter output where we previously used Ids.

### Edit “MCC — Add Unified Individual to Campaign”

We now just need to edit our main Sub Flow, so that it calls the two Flows we just created, with correct parameters, and it will be ready for use in a Segment Triggered Flow. If closed, reopen “MCC — Add Unified Individual to Campaign”.

After the last activity, add a Sub Flow, search “MCC – Add Contacts to Campaign” and select it, use Add Contacts to Campaign as a Label.

We now need to set the input values. For Campaign Id, we’ll just get the one from the Current Flow. Click on the toggle “Included” next to CampaignId so it is checked, click the input next to CampaignId and select the current Flow parameter for CampaignId:

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20436%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/025-Passing-Campaign-Id-from-the-Sub-Flow-to-the-Sub-Sub-Flow.png) 

Passing Campaign Id from the (Sub) Flow to the (Sub) Sub Flow

Do the Same for Member Status and for Unified Individual Ids. Last, for Ids add the Contact Ids Collection from the Contact Ids Transform previous activity.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20436%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/026-Passing-all-Contact-Id-to-the-Sub-Flow-to-handle-Campaign-Member.png) 

Passing all Contact Id to the Sub Flow to handle Campaign Member

Do the same thing by adding the “MCC — Add Leads to Campaign” Flow, calling it “Add Leads to Campaign” and passing Leads Ids instead of Contact Ids.

Save and Activate the Flow. The hard work is now complete, we now have a reusable Flow “MCC – Add Unified Individual to Campaign”, that we will use right now in an actual Segment Triggered Flow.

### Calling the Sub Flow from a Segment Triggered Flow

We’ll use a standard “Single Email” Segment Trigerred Flow created from a Campaign, add a Wait for Event (Click activity) and use our new Flow to add/update the current Unified Individual to a Campaign, with a Status of Sent, then Clicked or Not Clicked.

By default, Marketing Cloud Next (Growth & Advanced), simply creates a Flow with only one activity, a “Send Email Message”.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20436%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/027-A-simple-Segment-Triggered-Flow.png) 

A simple Segment Triggered Flow

We’ll add a Sub Flow, to add the Individuals of the current Unified Individual as a Campaign Member. We need to get the Campaign Id (starts with 701, you can find it in the URL when the Campaign is displayed) and the Member Statuses. In Marketing Cloud Next, the Campaign Member section is very handy to get all Campaing Members displayed and add / view Member Statuses.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20436%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/028-Viewing-Campaign-members-and-Status.png) 

Viewing Campaign members and Status.

Add a Sub Flow element before the Send Email Message activity (we’ll use a Wait for Event activity, and this latter element must be just after the Send Message). Choose “MCC – Add Unified Individual to Campaign” as a Sub Flow, activate the inputs toggles, add the Campaign Id, the Member Status, and in UnifiedIndividualId, for this one, we’ll select Triggering UnifiedIndividial\_\_dlm > Unified Individual Id.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20436%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/029-Adding-Unified-Individual-to-the-Campaign-with-a-Sent-Status.png) 

Adding Unified Individual to the Campaign with a Sent Status

Finally, we add a Wait for Event activity, specifying a timeout and the link to track, and two “MCC — Add Unified Individual to Campaign” to change the status accordingly. [Trigger a reaction on click or open event](/marketing-cloud-next-deep-dives/trigger-flow-click-open-event/).

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20436%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/030-Our-final-Flow-using-our-new-Sub-Flow-to-manage-Campaigns-in-Segment-Triggered.png) 

Our final Flow, using our new Sub Flow to manage Campaigns in Segment Triggered

## Final Toughts

As Campaign Id and Member Status are parameters we add as Flow inputs, we may verify the Campaign actually exists, and that the Member Status is correct as well.

In this article we have gone through the steps to add a “Unified Individual to a Campaign”. To do this, we add or update *all its underlying Individuals*(Contacts and Non Converted Leads) as Campaign Member. You may find it more convenient, depending on your use case to add *only one Lead or Contact as a Campaign Member, and not all*. We recommend adding a boolean parameter to “MCC — Add Unified Individual to Campaign”, called “All”, if All is set to True, then do what we described in this article. If not, Use a Collection Sort to get only the first Lead or Contact.

If you want to store and use informations that the Campaign and Campaign Status cannot handle, then you might find useful our deep dive article on how to enrich your Unified Individual DMO.
