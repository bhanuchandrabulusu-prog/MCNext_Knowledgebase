# SFMC Tips #224 : Agentforce: How to Set Up a Pre-Chat Form and How to Utilize It Afterwards

**Source:** https://medium.com/@marketingcloudtips/sfmc-tips-224-agentforce-how-to-set-up-a-pre-chat-form-and-how-to-utilize-it-afterwards-6626d3d7907b

---

# SFMC Tips #224 : Agentforce: How to Set Up a Pre-Chat Form and How to Utilize It Afterwards

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--6626d3d7907b---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--6626d3d7907b---------------------------------------)

12 min read

·

Dec 29, 2025

--

Photo by [Ibrahim Shabil](https://unsplash.com/@shabilphotos?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

When installing Agentforce (Service Agent) on an external site, you can configure a “pre-chat form” that asks users to enter information such as their name or email address before the conversation begins.

![]()

However, this mechanism comes with both advantages and disadvantages.

### ✅ Advantages

**1. Eliminates the need for identity confirmation, enabling smoother conversations**  
Since the name and email address are obtained in advance, the agent does not need to ask “What is your name or email?” during the conversation, preventing interruptions in the conversation flow.

**2. Helps deter malicious usage**  
By providing a minimum input process, spam, pranks, or misuse can be filtered to a certain extent, making it easier to maintain a healthy usage environment.

### ⚠️ Disadvantages

**1. May increase abandonment rate**  
Some users may feel that input is troublesome and leave the page.  
Particularly for users who “just want to casually ask something first”, this can become a psychological barrier.

**2. Makes anonymous consultations more difficult**  
Users who are reluctant to provide personal information or are sensitive about privacy may refrain from using the service.

**3. The reliability of the entered information cannot be guaranteed**  
The input information is not necessarily accurate, and there may be cases where false names or fake email addresses are registered.  
 In such cases, additional confirmation may be required later anyway.

**4. Possible involvement with privacy or legal compliance**  
Since the entered information constitutes personal information, you may need to comply with personal information protection laws such as GDPR and the Act on the Protection of Personal Information, update privacy policies, or obtain consent.

Of course, the points mentioned above do not cover all advantages and disadvantages.  
However, in reality, the negative impacts tend to be more significant, so it is necessary to be aware of this in advance.

Even so, there is no problem if you still wish to utilize this pre-chat input function.  
The configuration itself can be used immediately, so this article will explain the specific setup procedures.

## Prerequisite: Installing Agentforce (Service Agent) on an external site

Before proceeding with the contents of this article, you must first install Agentforce on your external site. If installation has not yet been completed, please refer to the following three articles for configuration.

[## SFMC Tips #221 : Agentforce: How to Implement a Service Agent Using Knowledge

### Salesforce partners implementing Marketing Cloud Next have likely noticed a growing trend: projects where Marketing…

medium.com](/@marketingcloudtips/sfmc-tips-221-agentforce-how-to-implement-a-service-agent-using-knowledge-ef7a9e0cdc6b?source=post_page-----6626d3d7907b---------------------------------------)

[## SFMC Tips #222 : Agentforce: Deploying Service Agents to Your Website

### Previously, I wrote an article about how to install Agentforce on an external site (CloudPages in Marketing Cloud…

medium.com](/@marketingcloudtips/sfmc-tips-222-agentforce-deploying-service-agents-to-your-website-8b5f38c6b0b9?source=post_page-----6626d3d7907b---------------------------------------)

[## SFMC Tips #193 : Agentforce: Deploying Service Agents on CloudPages (External Sites)

### In this article, I’ll explore how to embed the Agentforce Service Agent on an external website using CloudPages in…

medium.com](/@marketingcloudtips/agentforce-deploying-service-agents-on-cloudpages-external-sites-d4fb5edacb91?source=post_page-----6626d3d7907b---------------------------------------)

Once you have completed the above settings, the agent should already be displayed on the external site.

At this stage, the agent is configured only for simple FAQ responses based on Knowledge.

![]()

## Here is where we begin the setup procedure

First, let’s take a step back and look at the overall flow of the setup. We’ll proceed through the following steps. This process is almost identical to the sequence outlined in the [Help page](https://help.salesforce.com/s/articleView?id=service.reimagine_miaw.htm&type=5).

1. **Create pre-chat input fields**
2. **Enable the pre-chat feature**
3. **Create Custom Labels for the dropdown values**
4. **Add fields to Messaging Session**
5. **Configure the Omni-Channel Flow**
6. **Configure settings on the Agentforce side**
7. **Publish the pre-chat feature**
8. **Launch the agent and test behavior**

## 1. Create Pre-Chat Input Fields

In this scenario, we will not handle email addresses, since we assume that email addresses will be obtained later using an authentication flow **during the conversation**.

> *Personally, I also recommend obtaining it through an authentication flow, as this ensures data reliability.*

Therefore, the fields obtained in the pre-chat will be limited to the following three:

- Last Name
- First Name
- Connect with AI Agent or Connect with a Human Agent (selection / dropdown)

※ This time, we will not configure the functionality for “Connect with a Human Agent”, and will only create it as a selectable option.

**1.** In Setup, search for “**Messaging Settings**” to create the pre-chat input fields.  
This “Messaging Settings” should have been created as part of the steps to display the agent on an external site, so select the channel you previously created.

**2.** Scroll down to find the “**Custom Parameters**” section.

If there are custom parameters, it means standard parameters exist as well.  
There are four standard parameters:

- Last Name
- First Name
- Email
- Subject

**3.** In this case, we will use the standard parameters “First Name” and “Last Name”, so only create the dropdown “Connect with AI Agent or Connect with a Human Agent” as a custom parameter, and save it.

- Parameter Name: **Support Method**
- Parameter API Reference Name: **Support\_Method**
- Channel Variable Name: **Select Support Method** (※ displayed on pre-chat)
- Data Type: **String**
- Maximum Length: **100**

**4.** Next, create a new “**Parameter Mapping**” right below.

**5.** Here, create mappings to send the values obtained to the Omni-Channel Flow later.  
Standard parameters can be used without having to create them.

**6.** Create and save the following mappings. (Three fields)

> *Naming of flow variable names can be anything, but you will need to assign the same names to variables created later in the Omni-Channel Flow.*

( Parameter Name ⇔ Flow Variable Name )

- First Name ⇔ firstName
- Last Name ⇔ lastName
- Support Method ⇔ supportMethod

## 2. Enable the Pre-Chat Feature

**1.** Next, in Setup, search for “**Embedded Service Deployments**”.  
This should also have been created when installing the agent on the external site, so select the existing embedded service.

**2.** Click “**Edit Pre-Chat**”.

**3.** From here, specify the order of display. First, select “First Name” under “**Visible Pre-Chat Fields**”.

**4.** Next, select “Last Name”.

**5.** Finally, select “Custom”.

**6.** Since custom fields require configuration, define as follows and click Next:

- Field Data Type: **Dropdown**
- Channel Variable Name: **Select Support Method**
- Dropdown Name: **Support Method**
- Dropdown API Reference Name: **Support\_Method**
- Dropdown API Values:  
  **Connect\_with\_AI\_Agent** (displayed on pre-chat)  
  **Connect\_with\_a\_Human** (displayed on pre-chat)

**7.** Set the display order and save.

**8.** All three items are now configured.  
The items will be displayed on the pre-chat screen by the names on the left side.  
You can also mark them as required or fine-tune the order if needed.

**9.** Check the box for “**Activate the pre-chat feature**”.

> *Why check it at the last stage?  
> → Because this checkbox may automatically become unchecked during the configuration process.  
> So please make sure it is checked at the end.*
>
> *Also, even if you check it and save, it will not be reflected immediately.  
> In order to apply it, you need to “****Publish****” the Embedded Service.*

**10.** Lastly, if you are obtaining names, scroll to the bottom and change “**Visitor Name**” from Guest to First Name + Last Name before saving.

> *By doing this, the red text in the preview (Visitor Name) will change from Guest to full name, and a Messaging Session record will be created each time a chat starts.  
> The “****Messaging User****” field of that record will also change from Guest to full name, making it clear who the inquiry is from.*

## 3. Create Custom Labels for the dropdown values

The API values configured for the dropdown above will appear as-is in the pre-chat interface.  
Because the accepted values can only contain **English characters and underscores**, it is recommended to prepare custom display labels. This step is **optional**.

- Connect\_with\_AI\_Agent
- Connect\_with\_a\_Human

You will need to create display labels for each language you intend to use.  
 Configure them as follows:

1. In **Setup**, search for “**Translation Language Settings**” and select it.  
Click **Edit** for **English**, which should already be enabled.

2. Assign the currently logged-in user as the translator and save.

3. Configure **Japanese** in the same way.

4. If the language is currently disabled, enable it first, assign the translator, then save.

5. Return to “**Embedded Service Deployments**” from Setup, and click “**Set Custom Labels**”.

6. You can configure the settings for each language that you previously enabled.

7. Under **Chat Group**, select **Pre-Chat**.

8. Under **Label Group**, select **Dropdown Values**.

9. In **Label Type**, select **Standard**.  
The dropdown API values you configured earlier will appear.  
Enter the custom display labels and click **Save**.

10. Next, configure the same settings for **Japanese**.

11. Enter the custom display labels in Japanese and click **Save**, then **Done**.  
※ Make sure to click **Save** before clicking **Done**.

> *You can also modify the display labels for standard fields such as* ***Last Name*** *and* ***First Name*** *within this Custom Display Label editor.*

## 3. Add Fields to Messaging Session

The pre-chat fields configured this time can be used immediately by simply publishing them.  
For example, if your objective is to “deter malicious usage”, this alone is sufficient.

However, now that we have obtained the first and last names, we want to utilize them contextually in the agent afterwards.

To do this, follow these steps:

Open Messaging Session and create the following fields:

- First Name (Text: Length 100)
- Last Name (Text: Length 100)

**2.** Save and add them to the page layout.

**3.** The fields are now created.  
Next, we will update these fields through the Omni-Channel Flow.

## 4. Configure the Omni-Channel Flow

**1.** Open the existing Omni-Channel Flow that was created for displaying the agent on the external site.  
\*Do **not** create a new one.

**2.** In this flow, we will do the following two things:

- Store “First Name” and “Last Name” in the Messaging Session object
- Branch the flow based on “Connect with AI Agent or Connect with a Human Agent”

To accomplish this, create the following three variables:

- **firstName** (Text) → Available for input
- **lastName** (Text) → Available for input
- **supportMethod** (Text) → Available for input

**3.** These variable names must match the names configured in Messaging Settings.  
These are already mapped.

![]()

> *The previously created variable* `recordId` *will receive the Messaging Session ID from the chat screen when the session begins.*

**4.** Next, place an “**Update Records**” element.  
Select the Messaging Session object and choose the “**Messaging Session ID**” field.

For the value, select the variable `recordId`, which stores the Messaging Session ID.

5. Configure the fields to update:

- Messaging Session > First Name ← firstName
- Messaging Session > Last Name ← lastName

6. Next, place a “**Decision**” element.  
Select the item “supportMethod” on the left, and type “Connect\_with\_AI\_Agent” directly on the right — the dropdown value we defined earlier.

7. Place the “**Route Work**” element in the left-side branch path.  
Save as a new version and activate.

## 5. Configure Settings in Agentforce

**1.** Move to Agentforce Builder and configure “**Context**” so that the agent can use the first and last name values stored in the Messaging Session.

**2.** From Context Variables, select Messaging Session.

**3.** If the agent is in Draft or Inactive state, the Edit button will appear. Click it.

**4.** Add the newly created name fields and save.

**5.** Next, open the “**General FAQ**” topic to modify instructions.

**6.** Add the following to the instructions and save:

> *During the conversation, begin by thanking the customer with the following format, using the Last\_Name\_\_c value from the Messaging Session:  
> “****Thank you for your inquiry, Last\_Name\_\_c.****”  
> Always use the exact value entered in Last\_Name\_\_c as-is.*

**7.** Save and activate the agent.

> *Pre-chat runs before the agent executes, so it cannot be tested within Agent Builder.*

## 6. Publish the Pre-Chat Feature

Once the agent is activated, return to the “**Embedded Service Deployments**” screen.  
Confirm that pre-chat is enabled, then click “**Publish**”.

## 7. Launch the Agent and Verify Operation

**1.** All steps are now complete.  
Opening the chat should display the pre-chat form.

![]()

**2.** Enter values and start the conversation.

![]()

**3.** The conversation starts, so ask a question:

*“Can I change or cancel my rental reservation after booking?”*

![]()

**4.** You can confirm that the response begins by using the last name.

![]()

**5.** End the session and select “Connect with a Human” from the pre-chat dropdown.

![]()

**6.** It will state that no agent exists, confirming the branching logic works correctly.

![]()

**7.** Finally, check the Messaging Session record and confirm that the names are stored.  
Success!!

## Conclusion

The configuration method for Agentforce introduced this time is just **one example**.  
Agentforce requirements vary greatly depending on each company, so the optimal setup always depends on the situation.  
Please consider this article **not as the only correct answer**, but as **one idea or hint** for implementation.

Also, since this article is structured for **Agentforce beginners**, please note that actual production usage may require additional improvements and considerations.  
The structure here is quite simplified.

That’s all for now.

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
