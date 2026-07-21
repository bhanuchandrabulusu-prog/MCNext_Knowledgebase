# Marketing Cloud Next: Notify the Marketing Team

**Source:** https://the-agentic-marketer.com/marketing-cloud-next-tips-from-the-trenches/notify-marketing-team

---

Marketing Teams like to be aware when something important happens. This is a handy way to ensure things work as intended, and also to live monitor what Engagement that last Campaign generated.

In Pardot, for example, we can use the Notify User or Notified Assigned User in Automation Rules or in Engagement Studio. This is basically a predefined and non-customisable Email.

How do we do the same thing in Marketing Cloud Next (Growth or Advanced Edition)?

## First Attempt

The use-case we want to handle here is to create a Notification Email when a Lead is created by submitting a Form (see [Other types of Flow](/marketing-cloud-next-learning-path/flows-automations/)). So we created a Campaign and added a Signup Form Flow type, added the Consent informations, and we’re all set to collect Leads.

[![](https://the-agentic-marketer.com/wp-content/uploads/2025/09/Screenshot-2025-09-13-at-18.10.03-1024x586.png)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/Screenshot-2025-09-13-at-18.10.03-scaled.png) 

Out of the box Signup Form Campaign

We can now add a Email Notification to the Flow by clicking the + sign before the End Element. We’ll search for Send Email, to see which choices we have.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20458%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/Screenshot-2025-09-13-at-18.14.33-scaled.png) 

Selecting the Notification Activity

Send Email Message is how we send Marketing Messages in MC Next. We cannot change the recipient which is Flow-dependent (In a such type of Flow it would use the Email Address of the first Create Element, in Segment Triggered Flow, all the Email Addresses related to the current Unified Individual would be used). So we’ll simply select the Send Email activity and we use the Email Address of the Marketing Team in Recipient Address List

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20458%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/Screenshot-2025-09-13-at-18.19.27-scaled.png) 

Configuring the Send Email Activity

Next we define the Sender. Here we will simply use our Organization-Wide Addresses Email Address. We also create the copy of the Notification, note that we added informations from the Form (Insert a Resource > Associated Form > Form Field).

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20458%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/Screenshot-2025-09-13-at-18.22.52-scaled.png) 

Setting the Sender and Notification message

We seem all set, so we save the Flow.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20458%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/Screenshot-2025-09-13-at-18.31.44-scaled.png) 

Saving the Flow with a Notification

But, then, yes, we hit a Snag… The Flow won’t save and displays “You can’t use the Send Email action type in flows with the Form-Triggered Flow trigger type.”

Don’t worry, we need to make some slight changes for the Notifications to work.

## Creating a second Flow

Yes, we’ll need a second very simple Flow. So, we start be removing the Send Message activity from the original Flow, and we create a Record Triggered Flow. Flows > New > Triggered > Record Triggered Flow. We select Lead as the Triggering object and we keep the default “A Record is created” for the Trigger.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20458%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/Screenshot-2025-09-13-at-18.39.23-scaled.png) 

Creating a Record Triggered Flow

We can now add the Send Email activity, exactly as we did before. The recipient and sender are the same. The Notification copy is a bit different, as we now have access to all the Lead Fields for personalization (Insert a Resource > Triggering Lead > Lead Field).

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20458%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/Screenshot-2025-09-13-at-18.44.17-scaled.png) 

Defining the Notification, recipient, sender and message.

You can now Save and Activate the Flow, and receive notifications when a Lead is created.

## Final Thoughts

We’re sending a Notification whenever a Lead is created, even if manually created from Salesforce. The simplest way to Notify the Marketing Team only when a Form is Submitted is to modify the Form Trigerred Flow, and create the Lead adding a specific information to the Lead Record. For example, writing the Form or Campaign Name in the Lead Source Field and then trigger the Record Triggered Flow only if the Lead has a matching value.

We can do the exact same thing using a Data Cloud Triggered Flow. For instance, when a Record is created in Website Engagement (a Form is Submitted) or Email Engagement (a Link is clicked), then we can send a Notification to the Marketing Team using the same technique as above. We’ll need some little extra-work here, as in those Engagement DMO, the related Individual must be fetched to get the First and Last Name.

We’ve notified the Marketing Team here, but we could also notify another User, like the Assigned Sales Rep. Again, we would need to get the Email Address of the Lead Owner, and dynamically define the Recipient Address from that Get Record step.
