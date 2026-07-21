# Agentforce Marketing: use Data 360 Segments in Account Engagement

**Source:** https://the-agentic-marketer.com/marketing-cloud-next-deep-dives/agentforce-marketing-data-360-segments-account-engagement

---

If you installed the standard Sales Data Kit in Data 360 (fka Data Cloud) your Leads and Contacts (Account Engagement assigned Prospects) are already ingested. You can thus use the power of Data 360 and use all your data, without having to create Custom Objects or Custom Fields in Pardot, to create Segments in **Data 360 and use them as Account Engagement Dynamic List**.

## Account Engagement Prerequisites

**Account Engagement must be connected to Data 360**. This must done for each Pardot’s Business Unit. If you have followed the Account Engagement – Marketing Cloud Next Convergence Learning Path, **the Data Cloud – Account Engagement Connector is already created and activated**. If not, find the procedure in the [Prospect Activity Ingestion part of the Engagement ingestion guide](https://the-agentic-marketer.com/marketing-cloud-next-deep-dives/pardot-engagement-data-agentforce-marketing/).

## Data 360 new mappings

We need to make some  changes in how Leads and Contacts DSO/DLO are mapped to their DMO Counter Part. **This is mandatory for Account Engagement’s Dynamic List to be able to fetch those records**.

From Data Cloud > Data Streams, open the Lead\_home DSO, and then click Review inside the Data Mapping right section.

[![](https://the-agentic-marketer.com/wp-content/uploads/2025/11/Screenshot-2025-11-11-at-13.45.56-1024x558.png)](https://the-agentic-marketer.com/wp-content/uploads/2025/11/Screenshot-2025-11-11-at-13.45.56-scaled.png) 

The Lead Home DSO, we'll add mapping to

Then scroll until you see the Individual DMO on the right sidebar. Just after the mapped fields, unfold the Unmapped section, and click Add New Field. **Then use Account Engagement Integration ID as a Field Label, use the predefined API name Account\_Engagement\_Integration\_ID and Text as the Data Type**.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20436%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/11/Screenshot-2025-11-11-at-13.49.54-scaled.png) 

Adding the required Account Engagement Integration ID Text field

Save. Again, unfold the Unmapped Field section and click on Lead Id from the left sidebar, finally hover over the newley created field and click it.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20436%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/11/Screenshot-2025-11-11-at-13.53.59-scaled.png) 

Mapping Lead Id to Account Engagement Integration ID

Now the Account Engagement Integration ID field is no longer in the Unmapped section. Click Save. Finally, let’s verify in the Individual DMO, using Data Explorer that our new field is correctly filled, by checking if there is a value, and that it is equal to the Lead Id.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20436%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/11/Screenshot-2025-11-11-at-17.00.26-scaled.png) 

Using Data Explorer to check the value in our new field

**Then, redo the exact same steps, but with the Contact\_Home DSO/DLO (create one field on the Individual DMO – if you haven’t already – and map it with the Contact Id).**

The setup is now complete. Run the Indentity Resolution to have fresh Unified Individual Records.

## Use Data 360’s Segment in Account Engagement

### Create a Data 360 Segment

From Data Cloud > Segment, click New. Keep with the defaults (Visual Builder and Standard Segment). Next. For regular Marketing Cloud Next Segments, we need to choose Unified Individual, but for Segments created to be used in Pardot, we can use Individuals, Leads, or Contacts as well (you would then need to map Lead Id and Contact Id to an new Account Engagement Integration ID field on Lead and Account Contact resp.). We recommend using Unified Individual for consistency.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20436%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/11/Screenshot-2025-11-11-at-14.36.24-scaled.png) 

Creating a Segment of Unified Individuals in Data 360

Then use a Standard Publish and select the Publish Schedule (how often will the Segment will be updated) and Loopback window (the data recency). Save.

### Defining the Segment Criteria

If not already done, let’s activate the streamlined criteria definition and members preview, in **Data Cloud Setup > Feature Manager and enable Navigate the Attribute Library More Intuitively and Segment Preview.**

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20436%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/11/Screenshot-2025-11-11-at-14.47.45-scaled.png) 

Activating the Preview and Field picker enhancement

By default, when no criteria are defined, the Segment is made of all unified Individuals. You should see something similar to this (with the actual number of Unified Individual in your instance).

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20436%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/11/Screenshot-2025-11-11-at-14.52.27-scaled.png) 

Let's define the Segment critieria

As an example we will create a Segment of Competitor, which we may use as an exclusion list in Pardot. But, of course, you have all your data at your finger tips, so you can acheive any segmentation you want. In the Search Attibutes, input Email Address and drag the one from Unified Indv Contact Point Email DMO.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20436%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/11/Screenshot-2025-11-11-at-15.01.10-scaled.png) 

Using our Competitor Email Address as a Criteria

Then use Contains as the Operator and input your first competitor name. You can add other competitors in the same container, just drag the Email Adress in the Add related Attribute there zone. Use the Or Operator between the two competitors.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20436%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/11/Screenshot-2025-11-11-at-15.06.54-scaled.png) 

Defining our Competitor by the email address domain

Add your other Competitors or other criteria you wish. You can use the Preview button to see the Unified Individuals matching members. You can also define criteria that the members must not match (Exclude) and perform sort and group operations (Rank and Limit). **Once satisfied, Save and Publish Now your Segment.**

Don’t worry about the “This segment is scheduled to publish without an activation. To start sending this segment to an activation target, add an activation” message, we’re not using activations here.

### Using the Segment in Account Engagement

Once the Segment is Published (Publish Status is Success), go to Account Engagement > Prospects > Segmentation > Segmentation Lists. Click +Add List. Give it a name and check the Dynamic List checkbox.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20436%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/11/Screenshot-2025-11-11-at-15.19.41-scaled.png) 

Creating a Dynamic List form a Data Cloud Segment

**In Dynamic List Type select Data Cloud Segment**. Account Engagement Rules are the standard Dynamic Lists we’ve been using for years. Data Cloud Segment is a new Dynamic List type, not created from Pardot Criteria, but from the Unified Individuals inside a Data 360 Segment.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20436%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/11/Screenshot-2025-11-11-at-15.25.47-scaled.png) 

Let's select the Data Cloud Segment to create our new Dynamic List

Our published segments are displayed. Let’s choose the one we created previsouly containing our Competitors. Click +Create List.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20436%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/11/Screenshot-2025-11-11-at-17.04.30-scaled.png) 

Our list is created, and it is empty for now

### Notes on Data Cloud Segment Dynamic List type

It can take **up to 3 hours** for the Dynamic list to be initially populated. Then, your Dynamic List will be refreshed when the associated Data 360 Segment is published (either manually or from a schedule): it can take **up to 1 hour** after the Segment refresh for the list to be refreshed as well.

**The number of records in your Segment will not be the same as the one in your Dynamic List.** This is because a Unified Individual may be tied to multiple Leads and Contacts and also to records without the required Account Engagement Integration ID field (think Prospect). Prospect in the Recycle bin but in the Segment won’t show in the List neither.

You  can create up to **100 Data Cloud Segment Dynamic List** type per Pardot Business Units. Each List can have **at most 1 million records**.

**Finally a given Segment can only be used once to create a Dynamic List**. In our previous example we would not be able to select the Competitor’s Segment to create another Data Cloud Segment Dynamic List. This is not really a big deal as you can create another regular Dynamic List, and use the membership to the Data Cloud Segment Dynamic List as a first crtieria, and then add a country criteria for example.

This is very flexible: create Segment in Data 360 using all your data and then segment further in Account Engagement using Data Cloud Segment Dynamic List as master lists.
