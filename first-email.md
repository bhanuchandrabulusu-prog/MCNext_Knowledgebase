# Marketing Cloud Next: from Zero to First Email

**Source:** https://the-agentic-marketer.com/marketing-cloud-next-tips-from-the-trenches/first-email

---

**This step-by-step guide is designed for busy marketers or consultants who want to quickly test Marketing Cloud Next (Growth & Advanced). You’ll set up the essentials, try out the platform, and send your first email, focusing only on what matters most.**

This guide was written with Partners and SDO Orgs in mind,  but you can follow the  exact same steps, if you are a regular Customer (either converging from Pardot or starting from scratch): just skip step#1 and step#2.

## Create the playground

### Step #1. Get a SDO

Partners can get a new playground environment in Partner Learning Camp, called SDO. Those are ideal for demos, so once you’ve completed this article, you’ll be able to keep using your Org, continue configuring it, and use it for demos or experiments. The playground environment gives you access to the full range of Marketing Cloud Advanced features.

From Partner Learning Camp, go to Demo Org and select SDO.

[![](https://the-agentic-marketer.com/wp-content/uploads/2025/09/001-Selecting-a-SDO-to-create-a-new-playground-in-Marketing-Cloud-Next-1024x558.png)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/001-Selecting-a-SDO-to-create-a-new-playground-in-Marketing-Cloud-Next.png) 

Selecting a SDO to create a new playground in Marketing Cloud Next

Fill the Form with the required informations, wait for an Email from Salesforce stating to change your password, and you’re good to go.

## Basic Setup

### Step #2. Activate Data Cloud

In *Setup*, search for *Marketing Cloud* in the Quick Find (do not use the orange Marketing Setup, it is Pardot setup). Click *Assistant Home*.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20436%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/002-Marketing-Cloud-Growth-Advanced-Assisted-Setup.png) 

Marketing Cloud Growth - Advanced Assisted Setup

Then, from the Basic Section of the Page, click *Go To Basic Settings* (or click *Basic Settings* in the left sidebar).

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20436%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/003-Accessing-Marketing-Cloud-Basic-Setup.png) 

Accessing Marketing Cloud Basic Setup

Click Go to *Data Cloud Setup* (as a System Administrator)

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20436%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/004-In-Data-Cloud-Setup.png) 

In Data Cloud Setup

Then *Get Started.* After some time, you are redirected to a Welcome page. Data Cloud is up and running.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20436%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/005-Data-Cloud-is-ready-to-go.png) 

Data Cloud is ready to go

### Step #3. Setting the Permissions

You can now get back to the *Basic Settings* (*Settings,* then search for *Marketing Cloud,* then click *Basic Settings* on the left sidebar). You should see something like the following. The *Install* button is grayed out, so we’ll need to adjust the Permissions.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20436%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/006-Once-Data-Cloud-is-activated-some-steps-are-automatically-taken.png) 

Once Data Cloud is activated, some steps are automatically taken

Among other steps triggered once Data Cloud was activated, the enhanced CMS used to store your assets (Emails, Landing Pages, etc) is created and a Marketing Subscription as well.

We need to add some permission sets to our current User. Go to *Settings > Users* and choose your *User.* Then hover over *Permission Set Assignments* and click *Edit Assignment:*

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20436%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/007-Editing-Assignments-for-our-current-user.png) 

Editing Assignments for our current user

Then, add Data Cloud Admin by selecting it on the left and clicking the horizontal arrow.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20436%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/008-Adding-the-Data-Cloud-Admin-Permission-Set.png) 

Adding the Data Cloud Admin Permission Set

Do the same with the Marketing Cloud Permission Set.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20436%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/009-Adding-the-Marketing-Cloud-Admin-Permission-Set.png) 

Adding the Marketing Cloud Admin Permission Set

Your Permission Set are now… set. You can go back to the basic setup and select Default for the Data Space, and then click Confirm. This will launch the Enable Marketing Cloud step whichc then creates the CMS workspace and site, configures the subscription and adds the data space access to marketing permission sets.

[Edit 03/02/2026] – If this steps errors, you may see the following:

[![Agentforce Marketing setup errors on "Create CMS Workspace and CMS Site" and "Configure Communication Subscription and Preference Page" steps](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20170%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/Screenshot-2026-03-03-at-12.04.34.png) 

Errors on "Create CMS Workspace and CMS Site" and "Configure Communication Subscription and Preference Page" steps

In that case, here are the steps you need to follow to fix the issue. Basically you’ll need to create the workspace manually with the Default\_Content\_Workspace API name.

1. Open the App Launcher and select the Digital Experiences app.
2. Navigate to CMS Workspaces. If the tab is hidden, find it in the “More” dropdown menu.
3. Start a new workspace by clicking Add Workspace.
4. Define the purpose by selecting Marketing and clicking Next.
5. Enter the workspace details (note: If these names are taken, you may use alternatives; the system will attempt to recreate the default later if needed):
   - Name: Content Workspace for Marketing Cloud.
   - API Name: Default\_Content\_Workspace.
   - Description: Content for your marketing campaigns.
6. Set the Language: Choose your Org Default or English if the default is unavailable.
7. Finish and Confirm: Click Finish. If it fails, try the process one more time.
8. Final Step: System Processing. Wait up to 24 hours: Once created, do not make further changes. The system needs to run a job to complete the provisioning.

### Step #4. Setting the Company address

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20436%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/010-Adding-a-physical-address-to-the-Org.png) 

Adding a physical address to the Org

Enter the details of your Company in the Fields Street, City, State, Zip/Poste Code and Country (All fields must have a value).

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20436%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/011-Filling-the-Fields-to-define-a-physical-address.png) 

Filling the Fields to define a physical address

*Save*.

### Step #5. Deploying the Data Kits

By deploying the Data Kits, we are installing Data Streams and their Connectors so the data flows from Marketing Cloud Growth/Advanced and the Salesforce Platform into Data Cloud (more on this later).

Go back to Basic Settings (you should know how to do that by now 😎), and click the *Install* button, which should now be available.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20436%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/012-Lets-install-the-Data-Kits.png) 

Let's install the Data Kits

The Data Kits are being installed one after the other. Every time an installation is completed, you should receive an Email.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20198%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/013-Email-received-a-new-Data-Kit-is-installed.png) 

Email received, a new Data Kit is installed

It can take some time to complete all the Data Kits.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20436%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/014-Data-Kits-are-being-installed.png) 

Data Kits are being installed

You should see something like this by now:

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20436%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/015-Data-Kits-are-installed.png) 

Data Kits are installed

Note: from time to time this process fails, for different types of reason, but we’ve always managed to fix it. So, if it is happening to you, comment this article, we’re here to help. Start by simply retrying.

### Step #6. Create an Identity Resolution

By staying on the Basic Setting page, we are now going to setup the process of identifying identical person records and reconciling them. This is called Identity Resolution in Data Cloud and this process creates the Unified Individuals records which we will be using soon. Click *Generate Ruleset* in the last section

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20436%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/016-Generating-an-Identity-Resolution-Ruleset.png) 

Generating an Identity Resolution Ruleset

Then click *Generate.*

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20436%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/017-Let-the-setup-create-a-basic-Identity-Resolution-Ruleset-for-us.png) 

Let the setup create a basic Identity Resolution Ruleset for us

Note: the matching generated is very simple, two Individuals are considered identical as long as their Email Addresses are matching (when they have one in common to be precise). We won’t generate a Unified Account Rule Set in this quick setup.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20436%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/018-The-Identity-Resolution-is-set-and-the-Unified-Individual-is-selected.png) 

The Identity Resolution is set and the Unified Individual is selected

### Step #7. Create a Sender Domain

In the past, we could use the sender address [[email protected]](/cdn-cgi/l/email-protection), as it was an Organisation-Wide already verified address. But, Marketing Cloud Next (Growth/Advanced) now needs an Authenticated Domain. First we will need to trigger a migration to Authenticated Domains. *Setup* and search for *Migration* open it (under Unified Messaging Email)

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20435%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/Screenshot-2025-09-03-at-21.38.06-scaled.png) 

The Migration tool, mandatory to create an Authenticate Domain

*Transfer*. If you have running Campaigns, you are asked to stop/pause them before proceeding. Check *I’m ready*.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20435%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/Screenshot-2025-09-03-at-21.39.17-scaled.png) 

When Campaigns are paused, you can Transfer the Domain Management to Marketing Cloud

*Transfer*

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20435%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/Screenshot-2025-09-03-at-21.41.36-scaled.png) 

Marketing Cloud Next (Growth / Advanced) now handles the Sending Domains

You can now reload the Setup and search for Authenticated.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20435%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/Screenshot-2025-09-03-at-21.43.36-scaled.png) 

We can now create an Authenticated Domain

*+Add Domain.*

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20435%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/Screenshot-2025-09-03-at-21.45.15-scaled.png) 

Adding a Custom Domain

Enter a Sub-Domain of your main Domain and *Submit* (you can also use your root Domain)

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20435%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/Screenshot-2025-09-03-at-21.47.11-scaled.png) 

The Domain is ready to be setup

We will then need to Create 8 DNS entries, so Marketing Cloud Next can send Emails using our Sending Domain. To display the new entries to create, click *Manual DNS Record Information*.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20435%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/Screenshot-2025-09-03-at-21.49.42-scaled.png) 

The DNS CNAME records we need to create.

The way you create those Records depends on how your DNS is managed. Once the records are created and propagated (this may take some time depending on different factors, TTL, etc.), you can proceed to the activation of the Sending Domain.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20435%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/Screenshot-2025-09-03-at-21.51.12-scaled.png) 

Creating the Domain

Check *I completed my changes with my DNS provider*and *Activate my Domain*.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20435%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/Screenshot-2025-09-03-at-21.53.01-scaled.png) 

Activating the Domain

Check *Notify me when complete* and add your Email Address to be informed when the Domain is Activated. *Finish*. The status is now Pending.

Next, we will create a Sender Address, used to send our first Email. Click the *From Addresses* Tab.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20435%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/Screenshot-2025-09-03-at-21.58.43-scaled.png) 

Adding a new Sender Email Address

+ *Add From Addresses*

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20435%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/Screenshot-2025-09-03-at-22.00.09-scaled.png) 

Declaring the Sender Address

*Save*. An email should be received when the Domain is activated and the Sender Address will then be usable.

### Step #8. Creating a Default Data Graph.

A Data Graph is a set of data tied to a Unified Individual. It is used to personalize the Emails for example, or in Flow Decisions. We need a default one to send Emails, even though we wont personalize the first Email we’ll send. Go to *Data Cloud > Data Graph > New*

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20435%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/Screenshot-2025-09-03-at-22.07.15-scaled.png) 

Creating a default Data Graph

Select *Start From Scratch*. *Next.*

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20435%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/Screenshot-2025-09-03-at-22.10.16-scaled.png) 

We'll create a Standard Data Graph

*Next*. Give the Data Graph a Name and select the Unified Individual DMO for *Primary Data Model Object.*

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20435%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/Screenshot-2025-09-03-at-22.11.14-scaled.png) 

Defining a Data Grapg tied to the Unified Individual DMO

*Next*.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20435%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/Screenshot-2025-09-03-at-22.13.33-scaled.png) 

The Data Graph is created

We could add other DMOs, but for this Quick Start we will just add the First Name and Last Name fields of the Unified Individual DMO. *Save and Build*

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20435%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/Screenshot-2025-09-03-at-22.16.06-scaled.png) 

Choosing when to refresh the Data Graph

Let’s keep a daily refresh. *Save and Build*. Then we need to declare this Data Graph as the default one for Marketing Cloud Next (Growth/Advanced). *Setup > Customer Engagement.*

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20435%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/Screenshot-2025-09-03-at-22.21.52-scaled.png) 

Setting the default Data Graph for Marketing Cloud Next.

Select the Data Graph you created above, in the *Configure Basic Personalization* section.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20435%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/Screenshot-2025-09-03-at-22.24.36-scaled.png) 

Defining the Default Data Graph

*Update*.

**And, that’s it. Our Marketing Cloud Next (Growth/Advanced) instance is ready to send emails.** Of course, in this quick setup we have only configured the features we need to send an email, more on this in the Final Thoughts section.

**We can now…**

## Use Marketing Cloud Next

### Step #9. Creating a recipient

We are going to send an email to a new Lead, with an Email Address we have access to.

So go to Marketing Cloud by clicking the App Launcher (aka the waffle) and searching for *Marketing*, then selecting the purple icon, not the orange one (which is a legacy App you may remove).

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20436%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/1BAgVjwjJeuFNLiyONLVNnw.png) 

Opening Marketing Cloud Advanced

Then select *Leads > New* (use the first record type) and create a new *Lead*, by specifying a known Email Address.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20436%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/1jGeQa4kFKdtVUqUoZWfQcA.png) 

A new Lead is created. We'll use it as a recipient

Before we leave this page, we are going to edit it to add the *Privacy Consent Status* component, so we can opt in this new email address to our default Marketing *Subscription* created during setup for us. *Settings > Edit Page*

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20436%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/1ik40k0IKMBWxSfU2DXz8AQ.png) 

Adding the Consent Component to the Lead Layout

Search for *Privacy* and drag the *Privacy Consent Status* in the canvas, in the Marketing Tab.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20436%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/1najq-SAIgxdzw16bjPSi3Q.png) 

Adding the manual Consent Management component.

*Save*. Back to our Lead page, we click the arrow at the end of the line corresponding to our Email Address, and set the *Consent Status* to *Opted In*.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20436%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/1HViEeUCiaUq_bbO9jVtY5g.png) 

Updating the Consent Status

*Save*

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20436%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/1NR9wem4k35dX5Msz0CegdA.png) 

We now have a Lead who can receive our Emails.

### Step #10. Let’s Synchronise Data Cloud

That *Lead* would eventually be created in the *Lead\_Home DSO* and hence be created as an *Individual*, but we’ll speed up the process here. Go to Data Cloud (App Launcher and search for it), in the menu select *Data Stream*, then access the *All Data Streams* list view and search for *Lead*. Then, using the arrow at the end of the line, select *Refresh* and then open the Data Stream.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20436%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/14oUN4_cRVl0oV-9QHfSe6g.png) 

Refreshing the Lead Data Stream

When the *Last Run Status* changes from Pending to Success (and we should have 1 Last Processed Record: our new *Lead*).

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20436%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/1phNyV63qIN8RXTlxOmgW3g.png) 

Our Lead DSO is in sync with the Lead Object in Salesforce.

### Step #11. Running the Identity Resolution

In the setup process, we created in an earlier step an *Identity Resolution Ruleset*, but we did not schedule it. So we’ll run it now. Go to the *Identity Resolution* in the Data Cloud menu, select the Individual Identity Resolution record and then click *Run Ruleset*.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20436%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/14NnjoY9DdjUUwAfJkoo1VQ.png) 

Performing a manual Identity Resolution

After some time, *Last Run Status* changes from empty to Succeeded.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20436%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/1j1SAr48DSClD1wG2avtu0w.png) 

Our Unified Individuals are created

### Step #12. Update the Data Graph

As we just created our Unified Individuals, we need to run the Data Graph, to be built a Data Graph for each of them. *Data Cloud > Default Data Graph  > Refresh Now.*

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20435%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/Screenshot-2025-09-03-at-22.39.16-scaled.png) 

Refreshing the default Data Graph

After some time, the Data Graph is updated.

### Step #13. Create a Segment

In Marketing Cloud Next, Emails Campaigns are sent to Segments, made of Unified Individual. Let’s create a Segment in Data Cloud with just our new Lead. Go to the Segment Menu item in Data Cloud and click *New*. Leave the selected choices as-is an then click *Next*.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20436%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/16Z_sPGUp_gR9KDe0HajMSQ.png) 

Launching the Segment creation

Then select Unified Individual for Segment On and a name for the Segment.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20436%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/1bhL52pmRKusnvaER8Y4dVg.png) 

defining the Segment On and the Segment Name

*Next*. We’ll keep the default *Standard Publish* for the *Publish Type* and *Run Mode* to *Do Not Schedule*.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20436%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/16YxVZRRVMEtojCziRKq7CA.png) 

Default Publish Type and Schedule

*Save*. Great, we are now in Segment Builder, exposing Data Cloud DMOs.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20436%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/1LCybwsr3EU-SSC8VaOB2Dg.png) 

Segment created. So far all Unified Individuals are included

Let’s filter the Segment, so we only have our test Recipient. *Related Attributes > Contact Point Email,* then Drag the Email Address Field in the canvas of the Segment Builder.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20436%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/1f2BrnriPvdwey4aHOnfftQ.png) 

Adding Segment criteria

In the value, add the Email address of the Lead we created earlier. *Done*. *Save*.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20436%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/1lpRyb2GxC7wS4CS-58Etmg.png) 

The Segment has now only one Unified Individual

*Done*. We’ll now *Publish* the Segment, so we can use it. Click *Publish.*

![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20436%22%3E%3C/svg%3E)

Don’t worry about the warning, we will use the Segment soon. We wait some time for the Segment to be published: *Publish Status* changes from nothing to *Success*.

### Step #14. Creating a Campaign

Get back to Marketing Cloud by using the App Launcher (purple icon), and select Campaign in the Menu. Click *New*. Use the first *Record Type*, *Next*. Give your Campaign a name:

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20435%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/Screenshot-2025-09-03-at-22.54.55-scaled.png) 

Creating our Campaign

*Save*.

### Step #15. Creating the Flow and Email

Marketing Cloud Next (Growth and Advanced) uses Flows for almost every action/automation. There are good starting points already created. Using those templates, we create complete starting points.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20435%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/Screenshot-2025-09-03-at-22.55.58-scaled.png) 

Available Flow Templates in a Campaign

Click *Select* to create a *Single Email* Flow.

Note: we have not activated Agentforce in this Quickstart, but if we had, you could also create a Campaign, its Flow and Asset out of a single prompt.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20435%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/Screenshot-2025-09-03-at-22.58.54-scaled.png) 

Our first Flow is created. It is a Segment Triggered Flow

For this Flow, we will need to configure some elements. Click *Open Flow*.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20435%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/Screenshot-2025-09-03-at-22.59.56-scaled.png) 

The Flow we just created. Let's configure it.

*Click +Set Schedule. Keep Run Once and select* Start Immediately after Activation

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20435%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/Screenshot-2025-09-03-at-23.01.10-scaled.png) 

Running the Flow once: when we activate it

Close the right panel using the cross button (or *Save*). Click on *Segment Triggered Flow* (first element) and then click *Select Segment.* For the Segment, we select the Segment we create earlier.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20435%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/Screenshot-2025-09-03-at-23.02.21-scaled.png) 

Selecting the Recipient Segment

Next, we click on the Send Email Message element (the second one).

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20435%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/Screenshot-2025-09-03-at-23.04.31-scaled.png) 

Editing the Email

Next to the Email name, we use the dropdown and click *Edit*.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20435%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/Screenshot-2025-09-03-at-23.05.18-scaled.png) 

Opening the Email for edition

We are directed to the Email Builder. We won’t make any changes, but this where you could choose your Brand for styling, add or remove parts, personalise the copy using Merge Fields (for this you will need a Data Graph to expose Data Cloud to the Builder), etc. Click *Publish*.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20435%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/Screenshot-2025-09-03-at-23.06.28-scaled.png) 

The publishing interface of an Email

Then *Next* and *Publish Now.* Our Email is now published, let’s go back to the Flow. We will select the *From Address*, using the Adress of the Sending Domain we declared earlier. If not Available, the Domain has not been activated yet (activation email not received yet), and you’ll need to wait for this.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20435%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/Screenshot-2025-09-03-at-23.28.47-scaled.png) 

Adding our Sender

We’ll now select the Subscription to use in the Marketing Email (the one we declared our *Lead* opted in: Marketing, created for us during the setup).

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20435%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/Screenshot-2025-09-03-at-23.29.36-scaled.png) 

Setting the Subscription

*Save* the Flow. If the previous editing steps of the Flow were correct, Schedule, Segment, Publishing the Email, defining a Sender and a Subscription, then there should be no more error on the left sidebar.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20435%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/Screenshot-2025-09-03-at-23.30.49-scaled.png) 

The Flow is ready to activated

### Step #16. Sending the Email

You’re all set 😎. *Activate*, and your first Email will be sent.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20435%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/Screenshot-2025-09-03-at-23.32.52-scaled.png) 

Activating the Flow

You should receive quickly an Email in your inbox 🎉.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20613%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/Screenshot-2025-09-03-at-23.33.58.png) 

You've sent and hopefully received your first Email!

## Final thoughts

From there, there are a lot of things you can do, like:

- Enhancing the Data Graph for personalization
- Changing default images
- Activating Marketing Performance
- Adding Data Cloud Components in Lead and Contacts
- Preparing SMS and WhatsApp channels
- Adding Predictive AI (Einstein)
- Activating Agentforce
- Testing Designer Beta
- Creating your first Landing Pages and Form
- Configuring Internal and External Tracking
- Experiment Flows, Repeaters
- Try a etter Identity resolution
- Using RMM
- Understanding Consent Management
- …

A lot to come.
