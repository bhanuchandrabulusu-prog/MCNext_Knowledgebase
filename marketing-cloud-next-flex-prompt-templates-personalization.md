# Marketing Cloud Next – Use Flex Prompt Templates for 1:1 Personalization

**Source:** https://the-agentic-marketer.com/marketing-cloud-next-tips-from-the-trenches/marketing-cloud-next-flex-prompt-templates-personalization

---

We have already talked about [Campaign Creation and Content Builder Agents](https://the-agentic-marketer.com/marketing-cloud-next-deep-dives/agentforce-campaign-creation-content-builder-agents/) which are handy tools to create whole emails or refine paragraphs, but when using them, the final output often relies on traditional personalization like merge fields or repeaters, which can leave the core message looking similar for every recipient.

In this article, we’ll use **Flex Prompt Templates** from Agentforce to dynamically (that is at send time) generate email content. We’ll call the Prompt from a Flow and pass the AI generated outuput (grounded in recipient’s data) using the [Apex Personalization](https://the-agentic-marketer.com/marketing-cloud-next-tips-from-the-trenches/individual-related-record-event-apex-personalization/) we previously described to the email, which will then add it to the email as a simple Merge Field.

[![Agentforce Marketing using Flex Prompt Templates and Apex Personalization](https://the-agentic-marketer.com/wp-content/uploads/2026/01/Agentforce-Marketing-using-Flex-Prompt-Templates-and-Apex-Personalization-1024x559.png)](https://the-agentic-marketer.com/wp-content/uploads/2026/01/Agentforce-Marketing-using-Flex-Prompt-Templates-and-Apex-Personalization-scaled.png) 

Flex Prompt Templates and Apex used for 1:1 Personalization

To illustrate this technique, we’ll send a birthday email to our customers (Contacts), containing an anecdote related to the birthdate of today’s celebrants.

## Building the Segment

We’ll create a Standard Segment of Unified Individuals (as an alternative we could use a [Segment of Individuals](https://help.salesforce.com/s/articleView?id=release-notes.rn_automate_flow_marketing_cloud_segments_individuals_engagement_records.htm&release=260&type=5), which will be usable as Segment Triggered Flows in the coming Spring ’26) using the Visual Builder. We’ll keep the Publish Schedule with the default value of “Do Not Schedule” as we’ll have the Flow publish the Flow before each of its scheduled executions.

The [Unified Individual DMO mirrors the structure of the Individual DMO](https://the-agentic-marketer.com/marketing-cloud-next-deep-dives/new-fields-unified-individual-dmo/) and that latter DMO has a Birth Date Field, which type is DateTime and is mapped to the Lead, Contact and Prospect DSOs Birthdate Field. At first we thought we’d use the “Is Anniversary Of” operator in Data 360’s Segment Builder, applied to the Birth Date Field of the Unified Individual DMO. However it seems that this operator only works with Field with the Date Format, and not with the Date Time Format.

For this reason, and since we want to target only existing customers (that is Unified Individuals with at least one related Account\_Contact), we’ll simply create a new Field we’ll call Date of Birth on the Account\_Contact DMO and use it as a Segment criteria. First we create a Formula Field on the Contact\_Home DSO, with the Date type, and use a formula Field to cast the initial Field into a simple Date.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20435%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2026/01/Screenshot-2026-01-25-at-14.01.22-scaled.png) 

Adding a new Formula Field, "Date of Birth" on the Contact\_Home DSO

Then we map that new Field to a new Date Field, using the same name on the Account\_Contact DMO.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20435%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2026/01/Screenshot-2026-01-25-at-14.10.52-scaled.png) 

Our new Date of Birth Field on the Account\_Contact DMO

Next, we perform a Full Refresh on the Contact\_Home DMO, so that our Formula Field is evaluated on each Contact, and so that our Field on the Account DMO is populated with a Date. In our Segment, we now drag our new Field and apply the “Is Anniversary Of” operator.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20435%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2026/01/Screenshot-2026-01-25-at-14.22.52-scaled.png) 

Our Segment of Unified Individuals, with at least one Contact whose birthday is today, is ready

## Preparing the 1:1 Personalization

### The Apex personalization Class

We’ll use an Apex class with just a field, in which we’ll store the output of the Flex Prompt Template from the Flow and reference it in the Email as a Data Source. We’ve describe this technique applied to [Individual-related record triggered Flows](https://the-agentic-marketer.com/marketing-cloud-next-tips-from-the-trenches/individual-related-record-event-apex-personalization/) and we will use it in a Segment Triggered Flow here. Here is the Apex class (you don’t need developers skills to use this):

```
				
					public class BirthdayPersonalization {
    @AuraEnabled public String Anecdote;
}

				
			
```

The content stored in the Class, generated by the Flex Prompt, will only exist in the Flow and we won’t store in a Field in the data model, albeit this can be done, for debug reasons for example or simply to analyse what has been sent.

### Birthday Email

We’ll keep it very simple. In a Segment Triggered Flow, when the Segment is composed of Unified Individuals, we can use both the Data Graph and the Apex Class as a Source. So we’ll just a paragraph and a merge field to display the anecdote from the class, added as a data source from the Email Builder.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20435%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2026/01/Screenshot-2026-01-25-at-14.45.40-scaled.png) 

Our Birthday Email

### The Flex Prompt Template

From Setup, we open Einstein > Einstein Generative AI > Prompt Builder, then +New Prompt Template.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20435%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2026/01/Screenshot-2026-01-25-at-14.55.01-scaled.png) 

We'll use Flex as a Prompt Template Type

Then give it a name, here Birthday Anecdote, and under Inputs (optional) we click +Add and add a Free Text and check Require when the Template runs. We could add much more input data, or even retrieve data directly from the Flex Prompt to ground the Prompt to the recipient’s data. For our example, we’ll just use the Contact’s birth date from the Flow.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20435%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2026/01/Screenshot-2026-01-25-at-14.58.51-scaled.png) 

Defining a text variable used a Prompt input

+Next. We then select the LLM model we want to use Gemini 2.5 and add the Following Prompt:

```
				
					You want to please your customer by telling them a funny anecdote that happened on the day of their birth.
You will receive a text input, which is the date your customer was born: {!$Input:Bithdate}

Instructions:
"""
Generate a text message, minimum 50 words, with emojis. 

Use a funny tone.

Add the following information to the text message: a funny anecdote that happened at the day of their birth. If you can't find any anecdote that happened the exact day, try to find one the same day but the year before or after.
If still nothing create a generic birthday email.
Do not add any signature or reference any dates.
"""

Now generate the text message to your customer.
				
			
```

The birth date is added using +Insert Ressource .

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20435%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2026/01/Screenshot-2026-01-25-at-15.07.25-scaled.png) 

Grounding the Prompt with the input text

You can then test the Flex Prompt Template by clicking +Preview and manually add a birthdate.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20435%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2026/01/Screenshot-2026-01-25-at-15.11.10-scaled.png) 

Previewing the Flex Prompt Template output

Once the Prompt outputs the expected results in Preview, we can +Activate it.

## Let’s Build the Flow

### Triggering Conditions

We’ll use a recurring Segment Triggered Flow. We define the Start Date and Time. As a Repeat Schedule, we’ll use Daily (Note, since Spring ’26 we can schedule hourly Flows), run it every day and select Never for Can Rejoin Flow as we want to send the anecdote only one time to our customers.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20435%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2026/01/Screenshot-2026-01-25-at-15.22.33-scaled.png) 

Setting the recurring Segment Triggered Flow

Then in +Select Segment, choose the Segment we created earlier and select “Immediately before running this flow” as we want the Flow to refresh the Segment prior to each execution.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20435%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2026/01/Screenshot-2026-01-25-at-15.24.44-scaled.png) 

Defining the Segment and have the Flow refresh it.

### Accessing the Contact

By design our Segment has at least one Contact whose birthday is today. We’ll get it by adding a [Determine CRM Record](https://the-agentic-marketer.com/marketing-cloud-next-tips-from-the-trenches/agentforce-marketing-determine-crm-record-individual/) for individual element in the Flow. We will only keep a Contact branch.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20435%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2026/01/Screenshot-2026-01-25-at-15.33.19-scaled.png) 

Getting the Contact from the Unified Individual

In the Contact Branch, we’ll store the birthday in a new Text Variable, using an Assignement Activity.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20435%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2026/01/Screenshot-2026-01-25-at-15.36.54-scaled.png) 

Storing the Contact's Birthday

### Calling the Flex Prompt Template

The beauty of Flex Prompt Templates is that once activated, they are made available to Flow builder as a simple Action Element.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20435%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2026/01/Screenshot-2026-01-25-at-15.43.09-scaled.png) 

Flex Prompt Templates are called from the Flow with a simple Action element

We just need to specify the actual birthdate by defining the Prompt’s input with our previous Text Variable.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20435%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2026/01/Screenshot-2026-01-25-at-15.44.52-scaled.png) 

Calling the Prompt template and defining its input

### Sending the Email

#### Loading the Apex Class

Before sending the email we previously built, we need to assing the anecdote from the previous step to the field in our class. For this we create a new Ressource, a Variable with the Data Type Apex-Defined.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20435%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2026/01/Screenshot-2026-01-25-at-15.49.46-scaled.png) 

Instanciating the Apex Class as a Variable

We now add a new Assignement activity in the Flow to load the value in class, so that the Email can use it. The value is the Prompt Response of the output of the previous Flex Prompt Template.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20435%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2026/01/Screenshot-2026-01-25-at-15.54.05-scaled.png) 

Loading the LLM generated anecdote in the Apex variable

#### Sending the Email

Our final step is to add a Send Message Activity to the Flow, defining the Sender and the Communication Subscription to use.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20435%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2026/01/Screenshot-2026-01-25-at-15.57.24-scaled.png) 

Our Flow is complete with the final Send Email Message

And that’s it, our Flow is finished, we just need to activate it.

## Final thoughts

We presented a simple use case, but, this is a very powerful technique. You can change it to pass the Birth Place to the Flow, so the anecdote is more personal.

We can pass more data from the Flow to the Flex Prompt Template, up to 5 sources, not just simple text variables, but complete records as well. Flex Prompts can themselves call Flows, and so the possibilities are endless.

We can also tell our Prompt to generate HTML, not just text, to create complex layouts. A kinf of grounded, email vibe-coding.

Finally, keep in mind that Prompt Template execution consumes Data 360 credits. One parameter used to compte the credit consumption is the Prompt length. So keep an eye on your consumption cards and perform small batches to start.
