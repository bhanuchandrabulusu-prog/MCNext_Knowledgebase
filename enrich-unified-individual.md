# Easily enrich your Unified Individuals in Marketing Cloud Next

**Source:** https://the-agentic-marketer.com/marketing-cloud-next-deep-dives/enrich-unified-individual

---

**You may want to collect and store information related to your Unified Individuals, but you are concerned about creating new fields for every new need. We’re on the same page.**

In a previous article we have seen how to enrich your Data Model by adding new Fields. Although this is a perfect solution for Fields that are mandatory to your business, some less important, yet useful data, should be easily stored and used, without modifying the Data Model.

For instance, you may want to collect feedbacks multiple times in year, or prevent a Unified Individuals to re-enter a Flow multiple times. Let’s see a way to do this.

As always, in Marketing Cloud Next, there is more than one way to do something. As an example, Campaigns and Campaigns Member may achieve the same goal in some cases.

If you haven’t extended the model yet, begin with **[Add new fields](/marketing-cloud-next-deep-dives/new-fields-unified-individual-dmo)**

## Meet “Marketing Activities”

Let’s say you are collecting information from a Form, or you created a Segment Triggered Flow to craft a special experience, and you need to store informations out of that, but without touching your Lead, Contacts, Individual or Unified Individual structure.

We’ll do something similar to Pardot’s External Activities (and, to some extend to Tags), in a very Flexible way. First, we will create a Salesforce Custom Object, so we can store every king of information for later use (*Setup > Object Manager > Create*).

We’ll keep it very basic by just storing a Label (the Activity Name) and a Text Value. But you may also add Boolean (for storing some Consent for example) or Numeric Fields (if you need some type of Counter). There is also a Individual Field, in which we will relate a Record to an Individual Record (Prospect, Lead, Contacts or Visitors).

[![](https://the-agentic-marketer.com/wp-content/uploads/2025/08/009-Marketing-Activity-store-Individual-related-informations-1024x558.png)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/009-Marketing-Activity-store-Individual-related-informations.png) 

Marketing Activity store Individual related informations.

## Create a new DSO/DLO/DMO in Data Cloud

We’ll create records in that Object from Salesforce, and we will need them in Data Cloud. Once setup, we will just use this new Objects without having to change them. Note that if do not see Marketing Activity in the following steps, you need to give the Salesforce — Data Cloud connector a view access to it, by editing its Permission Set.

For this, in *Data Cloud > Data Streams > New > Salesforce CRM > Next > All Objects*, select our new object and keep all Fields selected. Next, we’ll create an Engagement type DSO/DLO, and use the Creation Date of our Marketing Activities as the Event Time field. Finally, we’ll Deploy it.

So far, when we create new Marketing Activities, the records will automatically be added in our DSO/DLO without further steps.

Then, we want this information to be available in the Data Model so we can use it, that is we need a DMO and we need to relate it to the Individual DMO. Lets open our DSO and in the *Data Mapping section, click Start > Select Object > Custom Data Model > New Custom Object*, keep the default and save it.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20436%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/010-Our-new-Marketing-Activity-DMO.png) 

Our new Marketing Activity DMO

Finally, we’ll link that DMO to the Individual DMO. *Data Model > Marketing Activity > Relationship > New.*

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20436%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/011-Linking-Marketing-Activities-with-the-Individual-DMO.png) 

Linking Marketing Activities with the Individual DMO

## Use Marketing Activities

### For creating Segments

So far, we can access our Marketing Activity records from Segment Builder. Here, we are excluding (note the Exclude Tab, of course you can use Marketing Activities as Inclusion criteria as well) all Unified Individual, with at least one underlying Individual (Prospect, Lead, Contact or Visitors) with a Marketing Activity called “This is my Activity” with the value “And Specific Value”.

We’ll soon see how to create new Marketing Activities, but the idea is that adding a Marketing Activity to any Individual involved in a Unified Individual, makes that information available for Segmentation.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20436%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/012-Marketing-Activities-as-Segment-Critierias.png) 

Marketing Activities as Segment Critierias

### As personnalisation inputs

If we want these informations to be available as Merge Fields, Personnalisation Points (Email Variations) or as Decision Split in our Flows, we’ll simply add the records in the default Data Graph.

Follow the path *Data Graph > Edit (end of line in the list view) > Unified Individual > Unified Link Individual > Individual > Plus Sign* and select the Marketing Activity DMO, and the Fields you need (Marketing Activity and Value should never be enough)

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20436%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/013-Adding-Marketing-Activity-records-in-the-default-Data-Graph.png) 

Adding Marketing Activity records in the default Data Graph

Now, every Marketing Activities of every Individuals of a Unified Individual will be embedded in the Data Graph.

### Further ideas

Using a Data Transform, you can store Marketing Activities at the Unified Individual Level. This will allow you to add a Data Cloud Profile Related Records to your Prospect, Lead and Contact Layouts in Salesforce, to display all Marketing Activities of all Individuals related to the same Unified Individual. You could also create a Calculated Insight out of these Data.

## Creating new Marketing Activities

### From a Form Triggered Flow

We will simple use a Create Record Activity in the Flow to create a new Marketing Activity. In that example the Individual Id used will be the one from the first Create Lead activity, the Value will be the feedback from the Form input and it will be a Customer Feedback.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20436%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/014-Adding-a-Marketing-Activity-from-a-Form.png) 

Adding a Marketing Activity from a Form

Note, we could have created a reusable Sub Flow to create that Marketing Activity. This is exactly what we are going to do in the next Flow type.

### From a Segment Triggered Flow

Sub Flows are very handy to create Flow components that you will be able to reuse. Let’s create one to create Marketing Activities from a Segment Triggered Flow.

This type of Flow takes a Segment as input, and injects every Unified Individual in the Segment when the Flow runs. We’ll pass the current Unified Individual Id to the Flow, along with the Marketing Activity and value. *Setup > Flows > New Flow > Start from scratch > Autolaunch Flow (No trigger) > Create.*

In the toolbox (left sidebar) we will add input variables that we will pass when call this new Flow from our Segment Triggered Flow. Let’s start by the Unified Individual Id. *New Ressource > Variable > Text type*. Lets call it UnifiedIndividualId, and click available for input.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20436%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/015-Adding-a-input-to-our-subflow.png) 

Adding a input to our subflow

Repeat these steps and create a Marketing Activity input and a Value input.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20436%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/016-Our-Sub-Flow-now-takes-three-inputs.png) 

Our Sub Flow now takes three inputs

Now, lets retrieve an Individual, the first one we meet, related to the Unified Individual Id we get. The Unified Link Individual DMO, generated by the Identity Resolution Process, is the glue we need here (basically a table with Individual Ids as primary keys and corresponding Unified Individual Ids). So we create a Get Record Activity:

- lets call it Get Any Individual
- use a Data Cloud source
- choose the Data Space (default here)
- the Unified Link Individual DMO
- use All Conditions are met
- set the matching criteria this way: UnifiedRecordId\_\_c Equals UnifiedIndividualId (the variable we created first)
- we won’t choose a Sort Order
- select Only Get the First Record
- finally let the Flow Automatically store all Fields

For email identity nuances, see **[Handling sub-addressing](/marketing-cloud-next-deep-dives/subaddressing-identity-resolution-data-cloud/)**

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20436%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/017-Getting-an-Individual-from-the-Unified-Individual-Id-parameter.png) 

Getting an Individual from the Unified Individual Id parameter

Now, we just need to create our Marketing Activity, related to the Individual from the previous step. Let’s add a Create Record.

- call it Create Marketing Activity
- we’ll Manually set the Record Fields value
- choose Marketing Activity as the Object in which we will create records into
- the Individual Id, will be the Individual Id from the previous activity
- the Marketing Activity and value, will be set the variable values we created

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20436%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/018-Creating-the-Marketing-Activity.png) 

Creating the Marketing Activity

Save the Flow, call it “MCC — New Marketing Activity”. Use a prefix of your choice, it will be handy over time to access your library of Sub Flows. Activate the Flow.

Now let’s use it! This is a very generic setup, so you can store whatever type of information you wish. I hope you will come up with innovative way of using this 😎.

As an illustration, we’ll use it to prevent a Unified Individual to go more than one time into a Reccurring Segment Triggered Flow. For this, in our Flow, we will just add a Marketing Activity “Gone through the Flow” and the Flow name as a value.

In our Segment Triggered Flow, let’s add a Sub Flow and search for our newly created one and select id. This is where a prefix comes handy.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20436%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/019-Adding-our-Subflow.png) 

Adding our Subflow

Next, let’s call it Prevent Flow Re-Entry and include the 3 input parameters so our SubFlow can create the Marketing Activity for us:

- Marketing Activity: Gone through the Flow
- Unified Individual Id: we’ll use the triggering $Record and select it Id (you need to have a Segment selected for this option to be available)
- Value: the Flow name

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20436%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/020-Calling-or-Subflow-to-create-Marketing-Activity.png) 

Calling or Subflow to create Marketing Activity

And there we have it, any time a Unified Individual enters the Flow, we store a Marketing Activity, that we will leverage to avoid a Unified Individual to re-enter the Flow (note: this option may be available directly in the Flow later). For this, we just need to add an exclusion criteria in our Segment. Next time the Flow is refreshed, any Unified Individual already gone though that Flow won’t be a Segment Member anymore.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20436%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/021-Using-a-Marketing-Activity-record-as-an-Exclusion-Criteria.png) 

Using a Marketing Activity record as an Exclusion Criteria
