# SFMC Tips #122 : Marketing Cloud Next: How to Leverage Event Data

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-on-core-personalization-part-2-8d0efb6402af

---

# SFMC Tips #122 : Marketing Cloud Next: How to Leverage Event Data

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--8d0efb6402af---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--8d0efb6402af---------------------------------------)

5 min read

·

May 27, 2025

--

Photo by [Rick Gebhardt](https://unsplash.com/@rick_gebhardt?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

In a previous article, I explained how to deliver personalized messages to individual contacts in **Marketing Cloud Next** (Marketing Cloud Growth & Advanced Editions) by utilizing “**Dynamic Content**” and “**Merge Fields**” when creating content, as well as “**Decision Elements**” in Flow Builder.

[## SFMC Tips #96 : Marketing Cloud on Core: Personalization Part.1

### In Marketing Cloud on Core (Marketing Cloud Growth & Advanced Editions), you can deliver personalized messages to…

medium.com](/@marketingcloudtips/marketing-cloud-on-core-personalization-1af8d9aa9026?source=post_page-----8d0efb6402af---------------------------------------)

In this article, I’ll expand on that by introducing an example of leveraging “**Event Data**” to personalize email messages.

### Types Covered in This Article (Part.2)

- ✖️ Unified Individual Data Model Object (Direct Attributes)
- ✖️ [Data Graph](/@marketingcloudtips/marketing-cloud-on-core-personalization-1af8d9aa9026) (Direct & Related Attributes)
- ⭕ **Event Data**
- ️✖️ [Personalization Recommender](/@marketingcloudtips/marketing-cloud-next-repeater-component-and-recommender-fb41b9c72ad0) (Salesforce Personalization)

### What is Event Data?

Event data refers to information collected at the time an event occurs — such as the name entered in a registration form. A typical scenario is sending an immediate follow-up email containing the registrant’s name right after they submit the form.

In such scenarios, the reason why the direct attribute **“Name”** of the Unified Individual data model object cannot be used is that the data immediately after registration has not yet completed the **ID resolution process**, and therefore, **data graph attributes** such as **“Name”** for the Unified Individual do not exist.

> ***Important:*** *To utilize data graph attributes, a wait element of at least* ***24 hours*** *is required before the Send Email Message element.*

To address this limitation, **“Event Data”**, which allows the **immediate use of data captured in the form**, can be effectively utilized. By leveraging event data, it becomes possible to deliver **flexible messaging** based on information available at the time of registration.

## How to Set Up Event Data

### 1. Verify and Select the Data Source

Open your email content, go to the “**Data Source**” tab in the property panel, and select the pre-created registration form as the data source.

### 2. Add Merge Fields

Click on “**Add Merge Field**”, then select “**Select an Event**” from the options.

### 3. Map Registration Form Fields

Choose fields like “**Name**” and “**Email Address**” from the registration form as the merge fields.

### 4. Publish the Email

Review the content and “**Publish**” the email after completing the configuration.

## **Key Points When Working with Event Data**

When handling an event data source within email content, keep the following in mind:

**1. There is a limit to the number of event data sources**  
Each email can include only **one** event data source.

**2. Not supported in repeatable components**  
Repeatable components do **not** support event data sources.

**3. Cannot replace or remove after publishing** 🚨  
Once an email has been published, even if you revert it to draft status, you **cannot** update the data source content.

**New in Winter ’26**  
 Starting with the Winter ’26 release, you can freely replace or remove event data sources **as long as the email remains in draft status** before it’s published.

![]()

## How to Configure the Flow

### 1. Setting Up the Signup Form

Next, configure the flow. For details on how to set up the signup form, please refer to the following article.

[## SFMC Tips #104 : Marketing Cloud on Core: Creating a Signup Form

### With Marketing Cloud on Core (Marketing Cloud Growth & Advanced Edition), you can easily create a “Signup Form” on a…

medium.com](/@marketingcloudtips/marketing-cloud-on-core-creating-a-signup-form-dcb43bbe9fea?source=post_page-----8d0efb6402af---------------------------------------)

### 2. Configuring the Thank You Email and Activating the Flow

Before activating the flow, configure the pre-created thank you email as follows. Once the email setup is complete, activate the flow.

> *At this stage,* ***it is not necessary to set a wait time of 24 hours or more between the consent request element and the thank you email.*** *(Note: If you use the “Name” attribute from the data graph instead of the event data attribute “Name”, a wait time of 24 hours or more is required.)*

### 3. Activating the Landing Page and Submitting the Form

After activating the landing page, open its URL. Enter your name and email address in the form, then click the submit button.

### 4. Verifying the Process

After submitting the form, check whether the personalized thank you email has been sent successfully. As shown below, the success was confirmed without using the unified individual data model object.

![]()

## Conclusion

Event data is not something that must be utilized at all costs. In situations like this example, where the unified individual “Name” data has not yet been generated, it is helpful to recall that “event data might be usable here”.

[In my earlier article on configuring data graphs](/@marketingcloudtips/marketing-cloud-on-core-personalization-1af8d9aa9026), I mentioned that personalization features leveraging **Unified Individual Data Model objects** are available not only in Marketing Cloud Growth & Advanced Edition but also in Salesforce Starter & Pro Suite. However, personalization powered by data graphs is **not supported** in Salesforce Starter & Pro Suite.

By contrast, event data **is available** in Salesforce Starter & Pro Suite as well.

## Personalization Features by Edition

**Personalization using Unified Individual (direct attributes only)**= **Unified Individual Data Provider**✅ Available: Marketing Cloud Growth & Advanced Edition  
✅ Available: Salesforce Starter & Pro Suite

**Personalization using Data Graph (direct and related attributes)**= **Data Graph Data Provider**✅ Available: Marketing Cloud Growth & Advanced Edition  
❌ Not available: Salesforce Starter & Pro Suite

**Personalization using Event Data**= **Event Data Provider**✅ Available: Marketing Cloud Growth & Advanced Edition  
✅ Available: Salesforce Starter & Pro Suite

**Personalization using Personalization Recommenders**= **Personalization Recommendations Data Provider**✅ Available: Marketing Cloud Advanced Edition  
❌ Not available: Salesforce Starter & Pro Suite, Growth Edition

That’s all for this time.

Stay tuned for more Salesforce Marketing Cloud tips! 😊

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
