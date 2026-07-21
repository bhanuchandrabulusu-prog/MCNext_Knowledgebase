# How to sync Pardot and Marketing Cloud Next Prospects

**Source:** https://the-agentic-marketer.com/marketing-cloud-next-deep-dives/sync-pardot-prospects

---

If you are a Pardot user and you want to use Marketing Cloud Next (Growth & Advanced) in parallel in a Converging way (if unsure, check [drop Pardot for MC Next or use both](/marketing-cloud-next-deep-dives/drop-pardot-or-use-both/)), you may wonder how to surface Pardot unassigned Prospects to  MC Next.

Pardot Prospect can be assigned, and in that case, they are in sync with either a Lead or a Contact in Salesforce. So Leads and Contacts are already handled by Marketing Cloud.

But, unassigned Prospects are “Pardot Only”, which means they exist only in Account Engagement. **In this article, we’ll leverage the new Prospect Core Object, that Marketing Cloud and Data Cloud can access, to create a new Core Prospect whenever a Pardot Prospect is created.**

Here are the ingredients we’ll use for this:

- A Dynamic List to gather new unassigned Account Engagement Prospect Prospects
- An Engagement Prospect triggered from the Dynamic List
- An Autolaunched Flow to check for duplicates and create the Core Prospect
- An External Action to call the Flow from Engagement Program

## Account Engagement Dynamic List

[![](https://the-agentic-marketer.com/wp-content/uploads/2025/09/Screenshot-2025-09-06-at-15.49.54-1024x585.png)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/Screenshot-2025-09-06-at-15.49.54-scaled.png) 

Rules matching newly created, unassigned Account Engagement Prospects

We select only Prospect created in a one day time frame, but if you handle the complete unassigned Prospect list, you may adjust this setting.

## Autolaunched Flow to create a Core Prospect

Form Salesforce Setup > Flow > New Flow we create a new Flow.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20457%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/Screenshot-2025-09-06-at-15.58.57-scaled.png) 

New Autolaunched Flow

We select the Autolaunched type.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20457%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/Screenshot-2025-09-06-at-16.00.10-scaled.png) 

Autolaunched Flow (No Trigger)

And finally, Autolaunched Flow (No Trigger) type.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20457%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/Screenshot-2025-09-06-at-16.01.46-scaled.png) 

Let's create the Autolaunched Flow

Later, we will call this Flow from an External Action in Pardot, and we will then pass parameters related to the Prospect we want to create on Core from the Pardot Prospect.

For this we will create Variables in the Flow. Open the left sidebar (upper left icon).

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20457%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/Screenshot-2025-09-06-at-16.42.57-scaled.png) 

Acessing the resources panel

We create a New Resource, a Text Variable to get the Email Address. We check Available for input.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20457%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/Screenshot-2025-09-06-at-16.45.43-scaled.png) 

Creating a variable to store the Email Adress of the Prospect to Create.

We do the same with First Name and Last Name.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20457%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/Screenshot-2025-09-06-at-16.47.58-scaled.png) 

We defined 3 inputs for our Flow

Next step is to check if a Core Prospect already exists. For this we will create a Get Record Activity.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20457%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/Screenshot-2025-09-06-at-16.51.57-scaled.png) 

Adding an Get Record activity

We select Prospects as a Salesforce Object we will query and filter the results so the found records need tot have the same Email Address, First Name and Last Name as defined in our input variables. We let the othe options as-is.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20457%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/Screenshot-2025-09-06-at-17.00.06-scaled.png) 

Trying to get similar Prospects

Next, we add a Decision Element to check if we actually found matching Prospects. We define the Label of the new created outcome as No Similar Prospect in which we check if the Prospect ID found in the previous Get Record step was null.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20457%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/Screenshot-2025-09-06-at-17.05.28-scaled.png) 

Configuring the Outcome

We rename the default outcome Similar Prospect Found, and we now have the Following result.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20457%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/Screenshot-2025-09-06-at-17.09.03-scaled.png) 

The Decision to check for existing Prospect id setup

We could the same check for existing Leads or Contacts. In the No Similar Prospect Found, we add a Create Record Element and define the Prospect Email Address, First Name and Last Name from the input variables.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20457%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/Screenshot-2025-09-06-at-17.13.14-scaled.png) 

Creating a new Prospect.

Note, there is a Check for Matching Record: we could have used it as a first step for this Flow as an alternate design. We leave it disabled here.

Before we save the Flow, we open its Settings (gear) and in Show advanced we select System Context without Sharing – Access All Data as an option for How to Run the Flow?

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20457%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/Screenshot-2025-09-06-at-18.08.37-scaled.png)

This is just a quick fix. As an alternative you may also allow change the permissions of the Integration user so it can see and execute Flow. Save the Flow.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20457%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/Screenshot-2025-09-06-at-17.17.33-scaled.png) 

Naming and saving the Flow

And finally, we activate the Flow

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20457%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/Screenshot-2025-09-06-at-17.19.18-scaled.png) 

The Flow is activated and ready to be used.

## External Action to call the Flow

External Actions are easy to setup in Account Engagement (they require the Advanced licence or higher). They are stored inside Marketing App Extensions, so we create one: Marketing Setup > Marketing App Extension > New.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20457%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/Screenshot-2025-09-06-at-17.22.43-scaled.png) 

Creating a Marketing App Extension

We give it a name and check Activate in Automation so we can use them in Engagement Studio.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20457%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/Screenshot-2025-09-06-at-17.25.08-scaled.png) 

Linking the App Extension with the current Business Unit in Pardot

Next to Business Unit ASsignements, we select New and the Account Engagement Business Units we want to use this extension in. Then we create an External Action, by clicking New next to Action Types.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20457%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/Screenshot-2025-09-06-at-17.29.39-scaled.png) 

Let's create a new External Action

We give it name, and as an invocable action we select our Flow. Notice the Invocable Action Schema is filled, we could edit it, for example to define default values for the Flow inputs. Check Active in Automation so we can use this External Action.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20457%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/Screenshot-2025-09-06-at-17.31.48-scaled.png) 

Creating the External Action out of our Autolaunched Flow

Now we can create the Engagement Program, triggered by our Dynamic List and calling the Flow to create the Core Prospect, via an External Action.

It may a good time to check how [Pardot Concepts and Marketing Cloud Next concepts can converge](/marketing-cloud-next-deep-dives/translating-pardot-concepts/).

## The Engagement Program

From Automations, we Add and Engagement Program, and in Engagement Studio, we give it a name and select our Dynamic List as Recipient List.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20457%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/Screenshot-2025-09-06-at-17.36.54-scaled.png) 

Creating the Engagement Program

We Safe the Engagement Program and now, and add an our External Action, by searching for its name.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20457%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/Screenshot-2025-09-06-at-17.49.53-scaled.png) 

Adding the External Action.

Then we need the values of the Fields we declared as inputs from the Flow. The syntax is the same as the one used for Merge Fields, relying on handlebar.

- EmailAddress: {{Recipient.Email}}
- FirstName: {{Recipient.FirstName}}
- LastName: {{Recipient.LastName}}

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20457%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/Screenshot-2025-09-06-at-17.55.47-scaled.png) 

Defining the External Actions

We can then Save and Start the Flow. Every new unassigned Pardot Prospect will be created as Marketing Cloud Next Prospect from now on.

## Final thoughts

There is a handy way to troubleshoot External Actions related issues. In Account Engagement Settings, there is an External Actions Error left menu entry, which gives informations on why an External Action call failed.

This is a first step to convergence. We could also have passed the Opt In Pardot Status of the Account Engagement Prospect, so that we add a Marketing Cloud Next Consent from the Flow we created. Engagement data can also be pulled from Pardot to Marketing Cloud Next (Growth and Advanced).
