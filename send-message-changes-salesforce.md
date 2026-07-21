# Send a message from Marketing Cloud Next upon changes in Salesforce

**Source:** https://the-agentic-marketer.com/marketing-cloud-next-deep-dives/send-message-changes-salesforce

---

## Context

By S*omething happens in Salesforce* we mean a change occurs in a Salesforce standard or Custom Object Record (update or create). By *Send a Message*, we refer to a specific activity in a Flow, but we’ll basically be triggering an Automation Event Triggered Flow where you can craft whatever experience you wish. [Overview of 5 Flow templates](/marketing-cloud-next-deep-dives/5-flow-templates/).

As an example, let’s say you work in a boat renting company (Ursa Boat Rental), and you are tasked to set up an acknowledgement process: every time a new boat reservation is created in Salesforce, send an email message. Without the solution provided below, you would be left with the following options:

- Real Time Datagraph (which requires Sub-Second Real-Time Profiles & Entities add-on license) and an Automation Triggered Flow. You would then be able to send a message from the Flow, provided the changes you are reacting to are ingested in Data Cloud using the Ingestion API or a web or mobile app data stream.
- Create a Segment of reservations and use that Segment in a Segment Triggered Flow.

Both solutions may work, but the first is not that easy to setup and leads to extra costs, the latter introduces a latency (standard Segments are refresh every 12 hours and Flows are running on a daily basis).

## Enter Engagement Signals

Engagement Signals are used to create Custom Events, which can then trigger Automation Triggered Flows. They just require an Engagement type DMO, and **they are available only in the Marketing Cloud Advanced Edition, not in Growth Edition**.

In our boat renting example, we have the Boat Reservation custom Object in Salesforce, which is where new reservations are stored, and its DSO/DLO counterpart, mapped to the Boat Reservation DMO in Data Cloud.

[![](https://the-agentic-marketer.com/wp-content/uploads/2025/08/009-The-Boat-Reservation-DSO-mapped-to-the-Boat-Reservation-DMO-1024x557.png)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/009-The-Boat-Reservation-DSO-mapped-to-the-Boat-Reservation-DMO.png) 

The Boat Reservation DSO mapped to the Boat Reservation DMO.

So let’s create a Boat Reservation Engagement Signal. Depending on your Salesforce configuration, you may need to create a Tab and add it to an App or give access to it to your profile (or via a Permission Set). Then you should be able to see a list of existing Engagement Signals (may be empty).

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20435%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/010-Existing-Engagement-Signals-in-our-test-Org.png) 

Existing Engagement Signals in our test Org

Click *New* and check *Exclude related objects so that this engagement signal is available for flows* (more about this later)*.* All your Engagement DMOs are listed, we’ll use our Boat Reservation in our example.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20435%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/011-Creating-a-Boat-Reservation-Engagement-Signal.png) 

Creating a Boat Reservation Engagement Signal

Click *Next,* and use the following values:

- *User Identifier*: this is where your Individual Id (Lead, Contact, Prospect or external Customer Id) is stored in your DMO
- *Timestamp Identifier*: select the creation date of your event
- *Item Identifier*: Select a DMO field that identifies what’s being engaged with, like a product or article. We’ll leave that empty but we could add the Boat type for example
- *Event Identifier*: Select a DMO Field that identifies a unique event. We’ll select the unique Record Id of our Boat Reservation Record in the Salesforce Custom Object

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20435%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/012-Specifying-how-our-Engagement-Signals-relates-to-the-Data-Model.png) 

Specifying how our Engagement Signals relates to the Data Model

Click *Next*. Select if you want every Record to trigger an Event or if you to gather similar records. We’ll stick with the defaults there.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20435%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/013-Count-each-event-as-a-discrete-engagement-signal.png) 

Count each event as a discrete engagement signal

Click *Next.* Here, we can define extra criteria that need to be satisfied to actually trigger an event. For example, we may only acknowledge certain types of Boats Reservations (you may also think Closed Cases or Opportunities entering specific a Stage as other examples of Engagement Signals). We’ll stick with the defaults there too.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20435%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/014-We-could-add-extra-triggering-criteria.png) 

We could add extra triggering criteria

Click *Next* and give your Signal a name.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20435%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/015-Naming-and-Saving-our-Signal.png) 

Naming and Saving our Signal

Click *Save.*

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20435%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/016-Engagement-Signal-Created.png) 

Engagement Signal Created

## Handling the Resulting Event in a Flow

**This is where the magic happens**: every time a record is created as an Engagement Signal, a Custom Event with the same name is triggered in an Automation Event Triggered Flow.

So we create a Campaign, and a Blank Event Flow (you can create an Automation Event Triggered Flow directly if you prefer). [Campaign management in Segment Triggered Flows](/marketing-cloud-next-deep-dives/campaign-management-segment-triggered-flows/). We then open the Flow and click *Select Event* to select what we just created 😎.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20435%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/017-Selecting-our-brand-new-Custom-Event-Boat-Reservation.png) 

Selecting our brand new Custom Event “Boat Reservation”

We stick with the *Every time an event meets entry conditions* option, but could also select *If the current event meets entry conditions and the previous event didn’t meet entry conditions.* This helps defining further the triggering context.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20435%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/018-Selecting-the-triggering-options.png) 

Selecting the triggering options

We can now do whatever we want in the Flow, adding Decisions for example, calling an MCE journey, or, as we’ll do it here, add a Send Email Activity.

First we go to the CMS and create an Email, and edit it in the Builder. Before we do anything, we add the Boat Reservation Data Source to our Email, so we can access every field in the triggering record to Personnalise our Email. How cool is that?

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20435%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/019-Adding-our-triggering-Record-as-a-Data-Source.png) 

Adding our triggering Record as a Data Source

You may have errors popups, but don’t worry, the Data Source is added. You can then build your Email and use the Event Data Provider to pick the merge Field from the triggering record.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20435%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/020-Adding-the-Thumbnail-of-the-reserved-Boat.png) 

Adding the Thumbnail of the reserved Boat

*Publish* the Email, add a *Send Email Activity* and set the options (Sender, etc) then *Activate* the Flow.

You’re done setting the Boat Reservation acknowledgment process. This is just an example of how you can leverage Engagement Signals. This is very Transactional, but you can use it for whatever Marketing needs you have.

## From the trenches

Here are some of our findings.

### Custom DMO are now supported

Until the 256.12 release, only Standard DMO were supported (think Case for Example). The Flow would not activate if the Engagement Signal was created out of a Custom DMO. This should be no longer the case.

### Emails are not sent

Your Flow, may fails upon reacting to an Engagement Signal, with this error in your Flow Run DMO, *Unable to resolve psr for known-to-known event triggered flow with non-crm individual: flow is missing datagraph.* In that case, a workaround is to deactivate the Flow, suppress the Datagraph from the Advanced Settings Flow, Save the Flow, re-add the Datagraph, Save and Activate the Flow. See the [related known issue](https://help.salesforce.com/s/issue?id=a02Ka00000gZBzN).

### Don’t use the Data Graph to personnalise your emails

Or you’ll get the following error *“This action is missing the following dependencies: Add a Wait for Amount of Time element immediately before this element. Set the Amount of Time field to 24 hours or more..*” Embed every information needed in your Engagement Signal if needed.

### Not Real Time

It takes between 10 to 15 minutes from the moment the record is created / updated in Salesforce for the Flow to be triggered.

### Only for Engagement DMOs so far

Engagement Signals can only be triggered by Engagement type DMOs. But what is you want trigger a Custom Event when a Lead Record changes. Leads are ingested as Profiles, not Engagement. In that case you can create a Data Transform to create a Lead Changes Engagement DSO and map it to an Engagement DMO. In that case, you would need to wait for the Data Transform to run so the changes trigger a Custom Event (1h the max refresh frequency). Another solution could be to create a Custom Salesforce object which you would feed with a Flow and create a Engagement DSO out of it.
