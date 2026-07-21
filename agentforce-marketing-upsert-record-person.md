# Agentforce Marketing: leverage Upsert a Record for a Person

**Source:** https://the-agentic-marketer.com/marketing-cloud-next-tips-from-the-trenches/agentforce-marketing-upsert-record-person

---

## Create Record first Activity

When sending an Email in a Form Triggered Flow you need to add a Create Record as a First Element in the canvas, otherwise, you won’t be able to save it.

[![](https://the-agentic-marketer.com/wp-content/uploads/2025/11/Screenshot-2025-11-03-at-17.14.24-1024x557.png)](https://the-agentic-marketer.com/wp-content/uploads/2025/11/Screenshot-2025-11-03-at-17.14.24-scaled.png) 

Form Trigerred Flows sending Emails need a Create Record as first Element

The message you get is:

*This action is missing the following dependencies: The first element of the flow must either be a Create Records element or a Subflow element. If the element is a Create Records element, it must create a contact, lead, or prospect. If the element is a Subflow element, the referenced flow must have a “recordId” output..*

The reason we get this message is that the Send Message Activity needs to ensure there is a Record in the Flow with an Email Address Field.

To get rid of that error, we can add a Create Record: Prospect, Lead or Contact as the first activity of the Flow.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20435%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/11/Screenshot-2025-11-03-at-17.42.48-scaled.png) 

Addind a Create Record (Lead) with the Matching option

We can now save the Flow. As we don’t want to create a new Lead if one already exists, we activated the *Check for Matching Records* option. You can specify any Matching Rules you like.

However, what if we want to create a Contact, if a Lead does not exist, for example? Using this architecture, we cannot do this. We’ll use a Subflow for this, and make sure to comply with the statement we gor earlier: *If the element is a Subflow element, the referenced flow must have a “recordId” output.*

The good news here, is that since the Winter ’26 Release, Agentforce Marketing (Marketing Cloud Next) offers us a predefined Subflow for this.

## Upsert a Record for a Person

Not only will we be able to introduce a more elaborated logic to check for existing Records, but also, we will build a reusable subflow. Flows > New and *search for Upsert a Record for a Person.*

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20435%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/11/Screenshot-2025-11-03-at-18.04.03-scaled.png) 

Creting a Upsert a Record for a Person Subflow Template

We select the Subflow template, and the Next, give it a name, then Save, and we have a starting point to handle the creation / matching of Prospect, Leads and Contacts.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20435%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/11/Screenshot-2025-11-03-at-18.10.11-scaled.png) 

Regular Upsert a Record for a Person Flow Template

The logic is very simple, and yet already powerful. First, let’s inspect the Variables of the created Flow.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20435%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/11/Screenshot-2025-11-03-at-18.13.19-scaled.png) 

Flow Variables: 2 inputs, 1 output

The Flow takes the *Company* and the *Last Name* as inputs and use these informations to check for existing Records. We will pass this informations when calling the Flow from our Form Trigerred Flow. The Flow returns a *RecordId*, which is what will be returned to and used by the calling Flow.

The logic is simple: update an existing Contact, if none is found, update an existing lead, if none exist, create or update an existing Prospect.

See this as starting point, for your own logic, and maybe add more input variables, like an Email Adress from the Form, etc.

Once you are done, Activate the Flow.

## Using Upsert a Record for a Person

In our Form Triggered Flow, we will replace the first Create Record Element, and replace it with a our Subflow, so we remove it, and add a Subflow element and select the Flow you create above from the template.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20435%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/11/Screenshot-2025-11-03-at-18.30.57-scaled.png) 

Replacing the Create Record with our Flow created from the Template

Next we just need to pass the parameters the Subflow is expecting, we get their value from the Form which triggered the Flow (if you created more Variables above, define them too). Click the toggle next to Company, and then select *Associated Form* under *Global Variables* and select the Form Field containing the Company value. Do the same for *lastName* and the other Fields you may ave created.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20435%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/11/Screenshot-2025-11-03-at-18.38.09-scaled.png) 

Defining the Subflow input parameters from the posted Form Fields

There we have it, a custom logic to create or update Records using the Upsert a Record for a Person template to create a custom Subflow.
