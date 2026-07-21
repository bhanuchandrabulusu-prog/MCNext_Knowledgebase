# SFMC Tips #281 : Marketing Cloud Next: How to Set Up Conversational Email

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-next-how-to-set-up-conversational-email-0ef29d7fd113

---

# SFMC Tips #281 : Marketing Cloud Next: How to Set Up Conversational Email

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--0ef29d7fd113---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--0ef29d7fd113---------------------------------------)

16 min read

·

Apr 24, 2026

--

Photo by [Tim Mossholder](https://unsplash.com/@timmossholder?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

**Conversational Email** has been introduced as a [Spring ’26 new feature](/@marketingcloudtips/marketing-cloud-next-spring-26-release-highlights-24c0c804b0cb) of **Marketing Cloud Next Advanced Edition** (\*this time, Growth Edition is not included).

This is the mechanism that Salesforce frequently announces as “**two-way email**”, and simply put, it is a function in which the Agentforce service agent automatically generates responses using generative AI to customer replies to emails.

Interactions with AI have already become common in chat and similar channels, but the fact that this can be realized via email can be considered a very new experience.

In my previous articles, I have introduced methods for embedding chat into [websites](/@marketingcloudtips/sfmc-tips-222-agentforce-deploying-service-agents-to-your-website-8b5f38c6b0b9) and [LINE](/p/e99698ef8d9c), but in this article, I will explain how to embed this mechanism into email.

## Main Use Cases of Conversational Email

Conversational Email can be utilized throughout the entire customer lifecycle and evolves traditional one-way notifications into interactive experiences.

The main use cases illustrated by Salesforce are as follows:

- **Promote event participation:** Easily respond with attendance status or preferences via reply
- **Cart abandonment measures:** Resolve pre-purchase questions via reply and prevent drop-off
- **Post-purchase follow-up:** Support initial usage and personalize experiences
- E**nhancement of transactional emails:** Request support by replying to delivery or billing notifications
- **Service reservations:** Easily select date and time via reply
- **Order management:** Handle return requests and check delivery status via reply
- **Loyalty improvement:** Provide benefits and offers through conversations
- **Product recommendations:** Personalized suggestions based on purchase history
- **Account linkage:** Improve efficiency for replenishment and inventory management via email replies

Indeed, it would be helpful if generative AI could handle all of these use cases.

I also recommend watching the following webinar.

[## The Future of Email is a Conversation

### Learn how to transform your emails from "no-reply" messages to two-way conversations that are interactive and…

www.salesforce.com](https://www.salesforce.com/events/webinars/the-future-of-email-is-a-conversation/?driverid=701ed000013ddaNAAQ&source=post_page-----0ef29d7fd113---------------------------------------)

## Overview of Conversational Email Implementation

For implementing Conversational Email, the following actions are required:

1. **Mechanism to escalate inquiries that Agentforce cannot handle**
2. **Basic configuration of the service agent**
3. **Enable conversation functionality for each sender address**
4. **Creation of conversational campaigns and flows**

In this article, I will explain this entire flow as carefully as possible. It will be a slightly long article, but I will not split it midway and will compile it as a single article. If you are interested, please read through to the end.

## 1. Escalation Mechanism

Now, the reason why we start with this configuration is that in the service agent settings, if there is no escalation flow, the agent cannot be activated. Even for those who think “escalation is unnecessary”, this is a required task.

Since this section is a bit long, I will summarize the flow:

1. **Enable Omni-Channel settings**
2. **Enable Messaging settings**
3. **Confirm Service Channels**
4. **Configure Routing**
5. **Configure Queue**
6. **Configure Presence Status**
7. **Configure and assign Presence Status Permission Sets**
8. **Configure Omni-Channel Flow**
9. **Configure Omni-Channel in Service Console**
10. **Confirm Service Console**

Now, let’s proceed.

## 1. Enable Omni-Channel Settings

Open “**Omni-Channel Settings**” from Setup and check “**Enable Omni-Channel**”.

## 2. Enable Messaging Settings

Open “Messaging Settings” from Setup and check Enable “**Messaging**”.

## 3. Confirm Service Channel

1. Open [**Setup**] > [**Service Channels**] and check the list.

In SDO or free developer orgs, a service channel for “**Messaging Session**” with a specific name is created, so confirm that name.

- In a free developer org: **Messaging**
- In a partner demo org (SDO): **LiveMessage**

If there is no service channel for the “**Messaging Session**” object, create a new one.

*※ Only one service channel can be created per object.*

## 4. Configure Routing

1. Select **Routing Configulations** from Setup and click New.

2. In the next screen, define **Routing Name** (e.g., **Escalation Routing**) and **API Name**, then input or select the following and save:

- **Routing Priority: 1**
- **Routing Model: Most Available**
- **Work Item Size: Inherited**
- **Units of Capacity: 1**

> Important: The above settings are just an example. In production, configure routing according to your Service Cloud admin and company requirements.

## 5. Configure Queue

1. Select “**Queues**” from Setup and click New.

2. In the next screen, define **Label** (e.g., **Escalation Queue**) and **Queue Name**, then input or select the following and save:

- **Routing Configuration: set “Escalation Routing”**
- **Supported Objects: Messaging Session**

3. Scroll down and select users (mainly **customer service agents**) as queue members, then save.

## 6. Configure Presence Status

1. Open [Setup] > [Presence Status] and prepare the following three statuses:

- **Available for Escalations … Online**  
   ⇒ Set Service Channel to “Case”
- **Busy … Busy**
- **Unavailable … Busy**

*※ In my SDO environment, many statuses are already prepared.*

2. Configure as follows:  
*\*Select* ***Cases*** *and* ***LiveMessage****.*

*※ Presence Status indicates whether an agent is available. Omni-Channel routes work based on this status.*

## 7. Presence Status Permission Set and Assignment

1. Create a new permission set to access Presence Status.

- Name: **Service Presence Statuses Access (Custom)**

2. In App Settings, select “**Service Presence Statuses Access**”.

3. Enable the three created Presence Statuses.

4. After creating the permission set, assign it to users.

5. Assign it to customer service agents responsible for escalation.

6. Also confirm that “**Service Cloud User**” is enabled for the user.

## 8. Add Access Permissions for Service Agents

1. Create another permission set.

- Name: **Messaging Permissions (Custom)**

Open the permission set and select App Permissions.

2. Click Edit and select:

- **Agent Initiated Outbound Messaging**
- **Configure Messaging**
- **Messaging Agent**

3. Assign this permission set to escalation users.

4. Also assign the “**Messaging User**” permission set license (not the permission set itself).

## 9. Configure Omni-Channel Flow

1. Create a “**New Flow**” from Setup.

2. Select “**Omni-Channel Flow**”.

3. Add element → “**Route Work**”.

![]()

4. Define **Label** and **API name**, and create a “**new resource**” for Record ID.

5. Select “**Variable**”.

6. Configure:

- **API Name: recordId**
- **Data Type: Text**
- **Available for Input: Checked**

7. Select “**LiveMessage**” service channel.

8. Routing Type: **Queue (default)**

9. Queue ID: select “**Escalation Queue**”.

10. Save and activate the flow (**Escalation Flow**).

![]()

## 10. Configure Omni-Channel in Service Console

1. Open “**App Manager**” from Setup.

2. Find “**Service Console**” → Edit.

3. Add Cases to “**Navigation Items**”.

4. Add “**Utility Items (Desktop Only)**”.

5. Select “**Omni-Channel**”.

6. Save.

## 11. Confirm Service Console

1. Confirm “**Omni-Channel**” appears in the “**utility bar**”.  
This enables escalation agents to receive escalated emails.

### Considerations

- When a conversation is escalated, agents can view the entire history and reply within the same thread.
- Replies received within 30 days from the last sent email continue to be routed based on rules.
- Agents cannot initiate new outbound conversations. They can only respond to assigned/escalated ones.

### Extended Conversation Component

2. Open “**Edit Page**” from “Service Console” settings.

3. Remove the standard “**Conversation**” component.

4. Add “**Enhanced Conversation**” component and save.

5. Agents can now respond to escalated emails from this screen.

How was it?

That concludes the section on building the escalation mechanism. It was quite long.

Next, we will proceed with the configuration of the service agent.

## 2. Basic Configuration of the Service Agent

1. Enable “**Einstein**” from “**Einstein Settings**”.

2. Next, refresh the screen once by pressing “**F5**”, then enable Agentforce from Setup > “**Agentforce Agents**”. After that, move to the new Agentforce Builder that was officially released in February 2026.

3. Click “**New Agent**”.

4. Select “**Agentforce Service Agent**”.

5. This time, I named it “**Agentforce Conversational Email Agent**”. Also create a user for Agentforce.

6. When the agent is created, the Agentforce Builder configuration screen will be displayed. This time, for topic selection, keep the default topics for the service agent. Do not change anything.

Next, click the plus mark for “**Connections**” from the menu and click “**Add Connections**”.

7. Select “**Marketing Email**” and add it to the agent.

8. As you can see in the “**Behavior**” menu, at this time, the agent supports **only plain text responses**.

9. Select the “**Routing**” menu. In the Escalation Flow section, select the **Omni-Channel Flow (Escalation Flow)** created in Section 1.

10. Move to the “**System**” menu and **delete the default Welcome Message**. There is no delete button, so remove the existing text. (※ This is currently a required step.)

11. Save and Commit Version.

12. Finally, activate the agent.

## 3. Enable Conversation Function for Sender Address

1. Select Setup > “**Authenticated Domains**” and add a domain.

*※ If there is already an authenticated domain in use in production, you can use that as is.*

2. Follow the appropriate steps to add the sending domain.

*※ For details on setting up a sending domain, refer to the following article.*

[## SFMC Tips #140 : Marketing Cloud Next: Steps for Email Domain Authentication

### For instructions on Email Domain Authentication, which is part of the basic setup in Marketing Cloud Next (Marketing…

medium.com](/@marketingcloudtips/marketing-cloud-next-email-authentication-steps-424e9cbbf76d?source=post_page-----0ef29d7fd113---------------------------------------)

3. When the domain status becomes “**Active**”, click “**View Details**”.

4. Move to the “**Reply Mail Management (RMM)**” tab and configure reply mail management as usual.

> *You may wonder whether RMM configuration is required for Agentforce to reply to emails, but this is used to process normal incoming messages that are not consent requests, not part of ongoing conversations, or not part of a conversational campaign flow.*

*※ For RMM configuration, refer to the following article.*

[## SFMC Tips #163 : Marketing Cloud Next: Adding From Addresses & Reply Mail Management (RMM)

### Marketing Cloud Next (Marketing Cloud Growth & Advanced Edition) does not provide an SAP (Sender Authentication…

medium.com](/@marketingcloudtips/marketing-cloud-next-adding-from-addresses-reply-mail-management-8cc7bd2ce258?source=post_page-----0ef29d7fd113---------------------------------------)

5. Next, move to the “**From Addresses**” tab displayed on the same screen and select the sender address to be used for this Conversational Email.

*Note: Conversational Email configuration must be set for each From address. The “Sender Display Name” and “Sender Address” selected here will be used in future conversations with the agent.*

6. Next, click the “**Configure**” button for “**Agent Conversational Messaging**” in the “**Capabilities**” section.

7. Select the “**Routing Type**”.

- **Agentforce Service Agent:** Routes the conversation directly to a specific configured service agent
- **Omni Flow:** Uses flows to route messages based on complex business logic
- **Omni Queue:** Routes the conversation directly to a specific queue

![]()

8. This time, select “**Agentforce Service Agent**” for the simplest routing. Select the service agent created earlier.

*※* ***Only agents that are “activated” in Agentforce Builder*** *will be displayed here. If the agent is not displayed, activate it and try again.*

9. For the Fallback Queue, select the **Escalation Queue** created in the previous section. After setting, click “Save”.

10. Activate the configuration.

11. Next, configure the **Resolve Remaining Incoming Messages** section. This setting determines how replies that **aren’t part of an active campaign or an ongoing conversation** should be handled. For this example, leave it set to **Use Default Domain Settings**.

- **Use Default Domain Settings**  
  Uses the existing **Reply Mail Management (RMM)** settings configured for the domain.
- **Use Custom Settings**  
  Temporarily overrides the domain’s Reply Mail Management (RMM) settings for this sender address and applies a dedicated set of reply handling rules.
- **Use Agent Conversational Settings**  
  Routes replies that aren’t associated with an active campaign or ongoing conversation to the conversational routing logic, where they are handled as a new conversation with the configured service agent.

**Note:** *Salesforce provides a detailed explanation of these options in the following Help documentation. Review it to determine which option best fits your use case.*

[## Salesforce Help

### Edit description

help.salesforce.com](https://help.salesforce.com/s/articleView?language=en_US&id=mktg.um_channel_email_routing_scenarios_examples.htm&type=5&source=post_page-----0ef29d7fd113---------------------------------------)

12. After saving the settings, return to the **Routing** block in **Agentforce Builder** (renamed to **Settings** in recent releases). You’ll see that your **Service Agent** has been registered as the **Marketing Email** channel.

In the **Summer** ’26 release, Salesforce introduced the ability to configure organization-specific **email signatures** and **disclaimers** directly in the **Settings** block. For more information, refer to the following article.

[## SFMC Tips #319 : Marketing Cloud Next: Custom Signatures and Legal Disclosures for Conversational…

### With the Agentforce June 2026 release, the Inputs feature has been added to the Agentforce Builder configuration for…

medium.com](/@marketingcloudtips/marketing-cloud-next-custom-signatures-and-legal-disclosures-for-conversational-email-90d6d09bf5ea?source=post_page-----0ef29d7fd113---------------------------------------)

With that, the configuration of **Conversational Email** is complete.

The final step is to configure the **Campaign** and **Flow**. While these can be created manually, we’ll take advantage of the **Campaign Creation Agent** to generate them instead.

## 4. Create Campaign and Flow

1. Finally, create a campaign and flow using Agentforce. This feature is explained in the following article, so first configure the Agentforce Employee Agent so that it works.

[## SFMC Tips #117 : Marketing Cloud Next: Agentforce Campaign Creation

### Notice: This article is being updated in accordance with the Spring ’26 new feature release.

medium.com](/@marketingcloudtips/marketing-cloud-on-core-agentforce-campaign-creation-697c992adbe6?source=post_page-----0ef29d7fd113---------------------------------------)

2. Open the agent from the marketing app “Home” screen.

3. Enter the following text and send it. You will be asked whether to create a **two-way email campaign**, so request creation as a two-way campaign.

> Build me a campaign targeting all individuals with an appointment coming up in 2 days. Assume the email includes a CTA prompting recipients to reply to the email if they would like to reschedule their appointment.

4. A brief will be proposed, so save it as is once.

5. Then, the brief should have “**Conversational Campaign**” checked. If it is not checked, request “Please check Conversational Campaign”.  
Next, click a “**Generate Campaign Preview**”.

6. Review the created “**Preview**”.

7. You should see that the final step includes a “**Forward to Agent**” element.

8. The “Wait” element is a standard time-based wait, but ignore it, “save the campaign preview”, and create the campaign.

9. This will automatically generate both the **campaign** and **flow**. In Flow Builder, it should include a “**Wait Until Event**” element and a “**Forward to Agent**” element.

*Tips: The “Wait Until Event” element is configured to wait until an email reply is received. This is also a new feature in Spring ’26, and it can be used even in flows that are not conversational email.*

10. After that, set the segment, configure the published email, activate the flow, and send it.

Now, all that remains is to try replying to the sent email.  
Let’s reply to the email that was actually sent.

## 5. Reply to the Sent Email

1. The email has arrived, so reply to it.

*Google has a thread display feature, so by using* ***thread view****, you can feel like you are chatting. Of course, even in mailers without thread display, you can perform conversational email as a normal email exchange.*

2. State that you want to create a case. (Example: **Create a case.**)

3. After several tens of seconds, a reply email is received. The first time, since the campaign flow with the wait event created earlier is triggered, and compared to chat, there is a sense that email sending processing takes time.

4. If you move to the flow, you can confirm that the flow is running.

5. For identity verification, you are asked for the registered email address, but since it is unclear which one, notify “**Escalation**”.

6. Then it is transferred to a human agent.

7. Now move to the “**Service Console**” and click “**Omni-Channel**” in the utility bar.

8. From Presence Status, select the green “**Available for Escalations**”.

(※ Be careful as a loud sound will play.) 🔊🔊🔊

![]()

9. Then, you should find a “**Support Email Conversation**” sent earlier, so select it.

- The **green icon** is the “**Messaging Session**” record.
- If you are testing in an SDO, please be aware that various other test data may be automatically generated as well.

![]()

10. This allows you to interact with the customer via email from this screen.

Success!!

## Conclusion

How was it?

Although it was a very long setup, for those familiar with Agentforce service agents, it is simply a reuse of existing mechanisms, so it may have felt like a simple setup.

Operationally, since service agents are required as handlers for escalation, please design while considering staffing in addition to the basic setup.

That’s all for this time.

Stay tuned for more Salesforce Marketing Cloud tips! 😎

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
