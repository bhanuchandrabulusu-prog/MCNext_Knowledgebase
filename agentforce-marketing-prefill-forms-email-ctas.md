# Agentforce Marketing: How to Prefill Forms from Email CTAs

**Source:** https://the-agentic-marketer.com/marketing-cloud-next-tips-from-the-trenches/agentforce-marketing-prefill-forms-email-ctas

---

So far, Form prefilling isn’t supported in Marketing Cloud Next. This means that when a known visitor lands on a page containing a form, it won’t automatically populate with the prospect’s information, even if the visitor is already identified by a cookie.

We’ll leverage the **URL Parameter Field Default Value** a new feature (winter ’26) of MC Next, to add the informations we know when a Prospect opens a Landing Page from an Email Call to Action.

## Default Values on a Form

We’ll prefill the Form with the First Name and Last name of the recipient, and will also use the hidden Field feature, a new Form feature in winter ’26 to pass both the Unified Individual Id, and a Campaing name, using UTMs for that latter field

### Creating the Form

We’ll create a Form directly from CMS: Add Content then select Form and give it a title. In this example we won’t use a Data Source. On the left sidebar, we add a **Plain Text Input** for the First Name. We give it a **Label**, displayed on the Form and a **Unique Name**, needed to reference the field value in the Flow handing the Form Submission. We also unfold the Field Default Value section. A **Static Value** can be used as an option, but what we are interested here is to **define the default value dynamically**, from the URL used as a CTA in an Email. So we select **URL Parameter as a Value Type**, and add an **URL Parameter** name. We can also add a **Fallback Value** in case the URL parameter is empty ot not present in the calling URL.

[![](https://the-agentic-marketer.com/wp-content/uploads/2025/11/Screenshot-2025-11-15-at-16.46.39-1024x558.png)](https://the-agentic-marketer.com/wp-content/uploads/2025/11/Screenshot-2025-11-15-at-16.46.39-scaled.png) 

Giving a name to the URL Parameter in the Form Field Default Value

We do the exact same thing for the Last Name field.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20436%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/11/Screenshot-2025-11-15-at-17.25.03-scaled.png) 

Creating the Last Name Field in an identical way

We’ll now add hidden fields in the Form to receive the Unified Individual Id and the UTM parameter. We’ll pass them to the Form using parameters in the hosting Landing Page URL, from the Email CTA, as the First Name and Last Name, but we’ll declare them hidden, so that they are not diplayed when the Form is viewed in its hosting Landing Page.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20436%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/11/Screenshot-2025-11-15-at-17.31.13-scaled.png) 

Declaring a hidden form field and set an URL Parameter default value

Finally, whe declare a Campaign hidden field. For this field, we’ll define Fallback value, so that thiz field also has a value, even if we don’t specify one on the calling URL from the email.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20436%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/11/Screenshot-2025-11-15-at-19.02.15-scaled.png) 

A Fallback Value is a default value for a dynamic field

We save our work and we will now create a Flow associated with that Form, that will handle Form submissions. **We don’t publish the Form, this needs to be performed by the Flow Activation.**

### The submission handling Flow

From a Campaign, a Signup Form Flow type, creates a Landing Page, including a Form and a Flow (related to the hosting Campaign) for use. In this article, we show the manual approach, and so we’ll create a Flow from the Form, using the New Flow button from the right sidebar.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20436%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/11/Screenshot-2025-11-15-at-18.37.51-scaled.png) 

A new Flow to handle the Form submission

New Flow, then from the drop down, we select Open in Flow Builder (the Flow is in invalid state since it is empty). We could do whatever types of actions we want here, like sending an email (in that case a Create Record first element would be need or a [use a subflow to do so](https://the-agentic-marketer.com/marketing-cloud-next-tips-from-the-trenches/agentforce-marketing-upsert-record-person/).). Here, we’ll just log the values of the inputs’ form in a custom object (Marketing Activity).

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20436%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/11/Screenshot-2025-11-15-at-18.51.58-scaled.png) 

Storing the First Name by acessing the Associated Form field list from Global Variables

We do the same for the other three (Last Name, Unified Individual Id and Campaign) inputs from the Field, and then Activate the Flow, which, in turn will Publish the Form. This can take some time, so check the Publication tab from the Form record, you will also receive an email once the Form is published. **Note, if you make changes to the Form later on, you’ll need to create a new version of the Flow and Activate that one to Publish the Form again.**

Also, as we created the Form from the CMS and a Flow from the Form, that latter is not related to a Campaign. **You can relate a Flow to an existing Campaign from the Flow Record, by editing the Flow’s Associated Record Field, which is actually the Flow’s Campaign.**

## Embedding the Form in a Landing Page

### Creating the Landing Page

Again, we’ll create a Landing Page directly from the CMS, Add Content > Landing Page. We select the Use Components (the other option is to use an existing Landing Page as a starting point). We build our landing page, and insert a From Component form the Layout section in the left sidebar of Marketing Cloud Next Landing Page editor.

[![Adding a Form Component to our Landing Page in Agentforce Marketing](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20436%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/11/Screenshot-2025-11-16-at-13.35.50-scaled.png) 

Adding a Form Component to our Landing Page

Use then select our Form in the CMS by clicling the Add Form button.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20436%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/11/Screenshot-2025-11-16-at-13.37.53-scaled.png) 

Our Form ins now included in the Landing Page

The hidden fields are not displayed when the Form is used. We can now give a the Page a Public Title and a Title, Save it, and then Publish it.

### Prefilling the From in the Landing page

Once the Landing Page is published we jump to the URL Tab of the Landing Page record to get its public URL. We open it in a navigator and append the parameters at the end of the URL:

```
				
					?first_name=&lt;Your first name&gt;&amp;last_name=&lt;Your last name&gt;&amp;uiid=&lt;Unified Individual Id&gt;&amp;utm_campaign=&lt;Your Campaign Name&gt;
				
			
```

As expected, the visible Fields are prefilled with the values from the URL Parameters.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20436%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/11/Screenshot-2025-11-15-at-19.40.29-scaled.png) 

Our Form is prefilled thanks to the URL parameters we appended

Let’s now Submit the Form. As we stored the hidden fields values as as well in our Marketing Activity Log object, we can see in a report that this fields are also filled with the passed values from the parameters once the Form was submitted.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20436%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/11/Screenshot-2025-11-15-at-19.53.40-scaled.png) 

The values passed from the URL populated the Form and where stored upon submission

## Creating a dynamic Email CTA

We now need to create inside an email the same URL, with the parameters so that when a recipient clicks on it, the Landing Page is prefilled with the related informations.

We create our Email from ths CMS, Add Content > Email > Use Component, and define a Subject line for our email. We add a paragraph with our company address and an unsubscribe link. Then we add a Button component.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20436%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/11/Screenshot-2025-11-15-at-20.14.33-scaled.png) 

Creating the Dynamic CTA in the email

We’ll then click Configure Action and select Link to Dynamic URL

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20436%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/11/Screenshot-2025-11-15-at-20.17.07-scaled.png) 

Link to Dynamic URL CTA

In the Dynamic URL, we paste the public URL of the Landing Page (URL tal on the Landing Page record). Then we add at the end of the URL:

```
				
					?first_name=
				
			
```

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20436%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/11/Screenshot-2025-11-15-at-20.35.28-scaled.png) 

Adding the First Name Parameter to the Landing Page URL

The values of the parameters in the URL will be sourced from the Data Graph. It can be any value directly or indirectly related to the Unified Individual, as long as it its avaliable in the default Data Graph defined for Agentforce Marketing. Here we will add the First Name value. Click Add Merge Field > Select Data Graph attribute> Primary Object > First Name.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20436%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/11/Screenshot-2025-11-15-at-20.32.25-scaled.png) 

Adding the First Name value from the Data Graph

Click Done. We’ll then do the same First Name. At the end of the URL, add:

```
				
					&amp;last_name=
				
			
```

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20436%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/11/Screenshot-2025-11-15-at-20.38.52-scaled.png) 

Adding the Last Name in the Dyamic URL.

Then insert the Merge Field for the Last Name. We do the same for the Unified Individual Id. Finally, we add a parameter for the Campaign name, which is a static string here. You should see somthing like this in your Dynamic URL:

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20436%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/11/Screenshot-2025-11-15-at-20.43.13-scaled.png) 

Our dynamic is Complete and so is our dynamic CTA

Save the Email. In Preview, you can select a Unified Individual from a published and click the CTA to check the Fields are prefilled. You can also send the email to a test List and clicking the dynamic CTA.

## Final Thoughts

The Default Value feature in Agentforce Marketing Forms are only available for the following components:

- Checkbox
- Dropdown
- Number
- Plain Text (the one we used here)
- Text Area

So you cannot use this to prefill  Form with the Recipient Email address for example. Maybe this has to do with a coming ootb prefilling solution.

You may encounter issues with merge fields being url-encoded prior to sending.

We have been able to dynamically pass the hosting URL to a field, for example to reuse a given Form in different internal or external landing pages, and be able to distinguish from the one associated flow which page was the submission made form. This implies making some adjustments to the From code itself.
