# How to Build a Double Opt-In Consent Flow in Marketing Cloud Next

**Source:** https://the-agentic-marketer.com/marketing-cloud-next-deep-dives/double-opt-in-flow

---

When you’re working with Marketing Cloud Next, one of the questions that always comes up is: *do I need to implement double opt-in (DOI)?* Before wiring the flow, review the [Consent Management](/marketing-cloud-next-deep-dives/consent-management/) overview to avoid mismatches at activation.

If you’re sending emails in **Germany**, the answer is yes: Double opt-in is expected. In other countries like **Austria, Switzerland, Greece, Luxembourg, and Norway**, it’s not strictly required, but it’s often recommended as a best practice. And honestly, even outside of those markets, DOI is a great way to build trust and to ensure your subscribers really want to hear from you.

In this post, I’ll show you how to set up a **double opt-in consent flow in Marketing Cloud Next** step by step. It’s one of those things that might feel tricky at first, but once you see it broken down, it’s actually pretty straightforward.

## Step 1: Create Your Signup Form in Marketing Cloud Next

In Marketing Cloud, navigate to ‘Content’ -> open your ‘Workspace for Marketing Cloud’, and from here, click on ‘Add’ in the top right corner and choose ‘Form’ in the pop-up window. From here the form editor will open:

[![](https://the-agentic-marketer.com/wp-content/uploads/2025/09/Image-05.09.25-at-08.51-1024x772.jpeg)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/Image-05.09.25-at-08.51.jpeg) 

Create a Form in Marketing Cloud Next

For the context of this article I created a quick **newsletter sign up form** with a first name, last name, email address and checkbox to receive Marketing Communications. You might need to create the Marketing checkbox before using it in your Core environment as this is not a standard field available.

As you can see in the screenshot you are able to add a Lead or Contact Data Source f.ex. to quickly pull in your fields of these objects to build the form as well as adding a brand for the look and feel of the form. Lastly, the thank you message on the bottom right will be displayed upon submission of this form.

We will create another step by step article on how to build a Marketing Cloud Next form at a later stage.

## Step 2: Build Your Double Opt-In Email and Confirmation Landing Page

**Important: Don’t Publish Your Email Before Linking your Form as a Data Source**

After saving your form, navigate back to your Workspace and add an email by going to the blue ‘Add’ button on the top right once again and choose email this time. The email editor will open. Before you get started, the first thing you’d want to do is to choose the **Newsletter Sign Up Form** as a Data Source for this email. This is to ensure that you can send this email in the flow right after form submission, and you don’t need to wait for the Unified Individual to be created. Click next to your email which will open the side panel seen in the screenshot on the right. Choose Data Sources and complete the pop-up with the details of your form and save it.

Deep dive into how [Form Submission integrate in the the entire lifecycle](/marketing-cloud-next-deep-dives/lifecycle-walkthrough/).

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20459%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/Image-05.09.25-at-09.25.jpeg) 

MC Next: Choose a Data Source for your Email

Now, when building your email and choosing the first name, ensure that you pick ‘Event Data Provider’ -> First Name. This makes sure that the **email is using the form inputs for personalisation** rather than the Data Graph.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20776%20373%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/Image-05.09.25-at-09.38.jpeg) 

MC Next: Event Data Provider

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20743%20384%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/Image-05.09.25-at-09.40.jpeg) 

MC Next: Using the Event Data Provider for Personalisation

As for the email, build it as usual including your ‘Confirm Subscription’ button of which we will later update the link to the landing page we are building next that confirms the subscription upon clicking the link.

Don’t forget to come back to your email once the landing page is built to update the link and also update your Subject Line & Preheader. Make the email type ‘Transactional’ so you wouldn’t need a Preference or Unsubscribe page and don’t forget to save and publish the email.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20577%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/Image-05.09.25-at-09.46.jpeg) 

MC Next: Build your DOI Email

### Building the confirmation Landing Page

Once your email is saved and published, navigate once again back to your Workspace and this time, add a landing page by clicking on the blue ‘Add’ button. The landing page editor will open. In this case, we will build a simple confirmation landing page without a form.

![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20599%22%3E%3C/svg%3E)

Once you have built your landing page, don’t publish it just yet but make sure to adjust your URL Alias to something meaningful – you can only do so before publishing the landing page. Save the landing page in the builder and navigate back to the page before. Click on the URL tab and then on the pencil next to URL Alias to update it to something meaningful and save it. Go back to your content tab and publish the landing page. The Public URL will appear on the URL page once the landing page is published. This is the URL you will need to update your email with and publish it. We will also need this URL in the flow we are building now.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20355%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/Image-05.09.25-at-11.05.jpeg) 

MC Next: Update your Landing Page URL

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20730%20487%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/Image-05.09.25-at-11.10.jpeg) 

MC Next: Publish your Landing Page

Before we move into step 3 where we will build our DOI flow, just a note, that you will also be able to add in your own custom domain to host your landing pages rather than using the Salesforce enabled one, this will be shared in another article.

## Step 3: Create an Event-Triggered Automation Flow

You might have picked up already, that when building your form it asks for a flow, and you are also unable to publish your form without a flow. We didn’t publish the form on purpose when we built it, but only saved it. Every form needs a flow to tell it what should happen with the form submissions. You cannot publish a form without a flow. We are now creating the accompanying flow for it and when publishing the flow, the form will be automatically published at the same time.

Once you have published your form once, and you are making changes to it later on, be alert that you will need to create an accompanying new flow version with it for every change.

In Marketing Cloud, navigate to ”Flows” and click “New” in the top right corner. On the next page, type “automation” in the top right box and click on “Automation Event-Triggered Flow”.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20772%20293%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/Image-05.09.25-at-11.21.jpeg) 

MC Next: Create a Flow

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20272%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/Image-05.09.25-at-11.22.jpeg) 

MC Next: Create an Automation Event - Triggered Flow

Select form submission on the next page as your event from the event library. Then select the newsletter form we have built before from the opening content library. Save your flow by clicking on the top right “Save” button, give it a name in the pop-up and click save.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20362%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/Image-05.09.25-at-11.28.jpeg) 

MC Next: Chose your Form as Event Trigger

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20377%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/Image-05.09.25-at-11.29.jpeg) 

MC Next: Name your Flow

## Step 4: Update or Create (Upsert) the Subscriber Record from the Form Submission

The first step we want to add in our flow is a create record element to ensure that the form submission will be captured inside Salesforce. I’m using a Lead record in this example, however pending on your business setup, this might be a different object. Since we can check in the same step if there is already an existing Lead with the same email address, we are calling this step ‘Upsert Lead’ which stands for create and update at the same time.

1. Click on the plus icon and choose the “Create Records’ element
2. Give it a name and choose “Manually” where it says “How to set record field values”
3. Choose the object: Here I choose Lead
4. Map the Lead fields from the left to the form fields on the right by choosing “Associated Form -> Respective Field Name”
5. Toggle “Check for Matching Records”on
6. For conditions, add “Email equals Associated Form -> Email”
7. Save the flow

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20557%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/Image-05.09.25-at-13.03.jpeg) 

MC Next: Upsert Lead

## Step 5: Send the Double Opt-In Email

As a next step, we are sending the Double Opt In Email we have built in Step 2.

1. Click on the plus icon and choose the “Send Email Message” element
2. Give it name
3. Choose the DOI emai by clicking on “Select Email” from your content library
4. Choose a “From Name and Address”
5. Save the flow

For this one, we do not need to choose a communication subscricption since we have classified this email as a transactional one.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20979%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/Image-05.09.25-at-13.14.jpeg) 

MC Next: Add the DOI Email to the Flow

## Step 6: Add a Wait Step Before Checking for the DOI Click

Next, we are adding a wait step into the flow to give the person who just received the email time to click on the double opt-in link in the email.

In my example below I’m adding a wait step for 20 minutes since I do expect people to react fairly quickly and click the link. However, wait for the backup option in case they don’t further down the article.

1. Click on the plus icon and choose the “Wait for Amount of Time” element
2. Give it a name , i.e. how long your wait period is
3. Add a wait period of your choice
4. Save the flow

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20536%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/Image-05.09.25-at-13.24.jpeg) 

MC Next: Add a Wait Step to a Flow

## Step 7: Query the Email Engagement DMO for DOI Link Clicks

As a next step, we now need to find out if the DOI link click has happenend. For this, we are querying the Email Engagement Data Cloud DMO by adding in a “Get Records” element to the flow. All Email Engagement for Marketing Cloud Next are stored in this Email Engagement DMO.

1. Click on the plus icon and choose the “Get Records” element
2. Give it a name, i.e. Get DOI link clicks
3. Choose the Data Cloud object
4. Choose the default Data Space and the object Email Engagement
5. For the conditions choose
   1. Sendtime Email Address equals Associated Form -> Email Address
   2. Resolved URL equals -> put in the URL from the landing page we created earlier
6. Save the flow

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20596%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/Image-05.09.25-at-15.17.jpeg) 

MC Next: Query the Email Engagement DMO

## Step 8: Add a Decision Split Based on the Link Click

Now that we have collected the DOI link clicks in the previous step, we need a decision split to find out if the previous step found any link clicks.

1. Click on the plus icon and choose the “Decision” element
2. Give it a name, i.e. Was the Double Opt in link clicked?
3. Rename the “New Outcome” into “DOI link clicked”
4. As conditions add the same as we did in the get records step
   1. Click into Resource -> Record Lookup -> Email Engagement from Get DOI link clicks -> Sendtime Email Address equals Associated Form -> Email Address
   2. Click into Resource -> Record Lookup -> Email Engagement from Get DOI link clicks -> Resolved URL equals -> put in the URL from the landing page we created earlier
5. Rename the “Default Outcome” into DOI link not clicked
6. Save the flow

Now we can differentiate between the people who have clicked the link and didn’t click the link.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20477%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/Image-05.09.25-at-15.29.jpeg) 

MC Next: Add a Decision Split to see if the DOI Link was Clicked

### Step 8a: The DOI Link was Clicked

If the DOI link was clicked, we are now able to set the consent for the newsletter as well as setting our DOI checkbox to “true” and capturing the date and time when it happened.

1. Click on the plus icon and choose the “Consent Request” element
2. Give it a name, i.e. “Setting newsletter consent”
3. Set the Consent Status to “Opt In”
4. Set the Contact Point to Associated Form -> Email
5. Set the Channel to Email
6. Choose the respective communication subscription(s) you’d like the record to opt in for, here Newsletter
7. Save the flow

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20636%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/Image-05.09.25-at-15.43.jpeg) 

MC Next: Set Newsletter Consent

Secondly, we are updating our DOI checkbox and Date & Time field on the Lead object.

1. Click on the plus icon and choose the “Update Records” element
2. Give it a name, i.e. “Set DOI to true”
3. For the step “How to find records to update and set their values” choose “Specifiy conditions to identify records, and set the fields individually”
4. Choose the Lead object under object
5. As conditions choose Lead ID equals Create Records -> Lead from upsert leads -> Lead Id
6. Set field values
   1. DOI = True
   2. DOI Date and Time = Running Flow Interview -> CurrentDateTime

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20593%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/Image-05.09.25-at-15.43-1.jpeg) 

MC Next: Set DOI to True & add Date

## Step 9: Repeat Step 6, 7 and 8 to give People more Time for the Link Click

On the side of the node where the DOI link was not clicked, you could now consider to repeat the steps 6 by adding another longer wait step, followed by step 7 and query them Email Engagement DMO once again and step 8, add the Decision split. You might be able to get more opt-ins of those people who didn’t click after 20 minutes.

Alternatively, you could also make the first wait step longer.

The screenshots below show how you could copy and paste steps as well as then connect the flow up on the DOI clicked path to the already existing consent steps so you don’t have to repeat those.

First, click on the three dots on an element and “copy element”, followed by clicking on the plus sign where you’d like to element to paste it to. Make sure to tidy up the name of the step once pasted.

Secondly, click on the plus sign once again where you’d like to connect the flow up to a different path and click “connect to element”. You will see that the elements will get little plus signs on them and you can click on the element you’d like the flow to be connected up to from here.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20573%20568%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/Image-05.09.25-at-19.15.jpeg) 

MC Next: Copy Flow Steps

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20586%20568%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/Image-05.09.25-at-19.15-1.jpeg) 

MC Next: Paste Flow Steps

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20745%20520%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/Image-05.09.25-at-19.16.jpeg) 

MC Next: Connect a Flow Step

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20399%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/Image-05.09.25-at-19.17.jpeg) 

MC Next: Connect a Flow

### Here’s how the final flow will look like:

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20989%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/Image-05.09.25-at-19.17-1.jpeg) 

MC Next: Final DOI Flow

## Alternative Step: Use the ‘Wait Until Event’ element

If you can wait for 24 hours before finding out who has clicked on your DOI link, you could use the “Wait Until Event” element. This element needs the Unified Individual to work, hence the 24 hour wait step as the Identity Rules run once daily by default.

1. Click on the plus icon and choose “Wait Until Event”
2. Choose from the Event Library “Email Link Click”
3. Give it a name, i.e. “DOI link clicked?”
4. For Flow Action to Monitor choose the “Send DOI Email”
5. For the Link choose the URL of the landing page that was added to the email
6. For the timeout path, choose 24 Hours

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20476%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/Image-05.09.25-at-20.03.jpeg) 

MC Next: Wait Until Event Step

From here, move the “setting newsletter consent” element and  “set DOI to true” element into the Event Occurs path and you will be done.

Of course, once again you could consider here too repeating the wait until step to see if anyone clicks later than 24 hours.

Lastly, you could add a welcome email to the Event Occurs path after setting consent. This would of course work also with the other version of the flow.

Once you are all done, don’t forget to save your flow, activate and test it.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20632%201008%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/Image-05.09.25-at-20.09.jpeg) 

MC Next: Final DOI Flow with Wait Until Event Step

## Final Words

So that’s it. Here are two different options on how you can build a Double Opt In flow. If you’d like to associate it with a Campaign, you could do so by filling the ‘Associated Record’ field on the flow record page.

An alternative version could be, that you’d be looking to first of all check if you do have an existing lead or contact before creating or updating the respective record. Since the flow currently forces you to add a create record step at the start when sending an email (as this is where the email will be sent to), you could get around that by creating a prospect record f.ex. and later deleting that again.   
  
Since all engagement is linked to the email address, which would then be owned by either the already existing or newly created lead or contact, the flow would still work the same way.
