# SFMC Tips #226 : Agentforce: Escalating from an AI Agent to a Live Chat Agent

**Source:** https://medium.com/@marketingcloudtips/sfmc-tips-226-agentforce-escalating-from-an-ai-agent-to-a-live-chat-agent-0450bbb09115

---

# SFMC Tips #226 : Agentforce: Escalating from an AI Agent to a Live Chat Agent

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--0450bbb09115---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--0450bbb09115---------------------------------------)

7 min read

·

Jan 1, 2026

--

Photo by [Justin Luebke](https://unsplash.com/@jluebke?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

In the previous article, I explained the mechanism for connecting to a live human agent at the start of a chat.

[## SFMC Tips #225 : Agentforce: How to Set Up Live Human Chat

### In the previous article, at the start of the chat, I introduced a configuration where users can select which path to…

medium.com](/@marketingcloudtips/sfmc-tips-225-agentforce-how-to-set-up-live-human-chat-7e09f6ae051b?source=post_page-----0450bbb09115---------------------------------------)

In this article, as a continuation, I will introduce how to switch to a live human agent during a conversation with an AI agent.

This switching mechanism is generally called “Escalation”.

For example, the following role division is possible:

- Frequently asked questions and simple inquiries → Automatically handled by the AI agent
- Questions that are difficult for AI to handle or complex consultations → Escalated to a human agent for response

By switching between AI and human agents depending on the situation, smooth and appropriate support can be achieved.

> ***Important:*** *In this article, we will continue to use the live chat settings created in the previous article. If the setup is not yet complete, please follow the steps in the previous article and prepare the environment so that live chat can be called (able to respond in the Service Console).*

## Overview of the Settings to Be Implemented

This configuration will proceed in the following steps:

1. **Checking the Service Channel**
2. **Creating a Sending Omni-Channel Flow**
3. **Connecting the Sending Omni-Channel Flow and the Agent**
4. **Adding a Topic for Escalation**
5. **Operation check during conversation with the AI agent**

## 1. Checking the Service Channel

1. Open **[Setup] > [Service Channels]** and check the list.  
In SDO environments or free developer environments, a service channel for “Messaging Session” may already be created.  
 (Examples: Messaging, LiveMessage, etc.)

> *Note: Only one service channel can be created per object.*

2. On the service channel detail screen, check that the target object is set to **“Messaging Session”**.  
If there are no issues, make a note of the service channel name to be used later when creating the flow.

- Free developer environment: Messaging (\*this time)
- Example for partner-only SDO: LiveMessage

## 2. Creating a Sending Omni-Channel Flow

1. Search for **Flow** from Setup and create a new flow.

2. Select **Omni-Channel Flow**.

3. Add an element and select **Route Work**.

![]()

4. After determining the element name and API reference name, click + **New Resource** in the “Record ID Variable”.

5. Select **Variable**.

6. On the next screen, input or select the following and save:

- API Reference Name: `recordId`
- Data Type: Text
- Availability Outside the Flow: Check “Available for input”

7. When `recordId` is entered in the Record ID Variable, select “**Messaging**” from the service channels.  
\*This “Messaging” targets the “Messaging Session” object.

8. In **Route To**, select **Queue**.

![]()

9. For the Queue ID, select the queue created in the previous article (in this example: Live Agent Queue).  
Customer service agents are assigned to this queue, and they will be called.

![]()

10. Save the flow.

11. Activate the flow.

![]()

## 3. Connecting the Sending Omni-Channel Flow and the Agent

1. Move to the **Agentforce Builder** of the previously created Service Agent, disable it once, then click **Add from Asset Library** from a new topic.

2. Add the **Escalation** topic.

> ***Tips:*** *The Escalation topic is slightly unique in that no actions are linked to it.*

3. Click **Connections**.

4. If the newly released Summer ’25 **Enhanced Connection Panel** is not enabled, please enable it.

5. Click **Enhanced Chat V2**.

6. In the **Escalations** section, select the (**Outbound) Omni-Channel Flow** created earlier.

7. Enter the message to be displayed when transferring and save.

- example: *One moment, I’m transferring our conversation to get you more help.*

8. Next, click **Messaging** and perform the same settings.

> *Currently, if you are using the traditional* ***Enhanced Chat V1****, the processing will occur on the “Messaging” side.  
> On the other hand,* ***Enhanced Chat V2*** *is an item exclusively for Enhanced Chat V2.*
>
> *Therefore, to avoid omissions regardless of which version is being used, it is recommended to configure both.*

## 4. Changing Instructions for the General FAQ Topic

1. Change the content of the General FAQ topic to the following. Items **②③④** are especially important.

**Classification Description**  
This topic is intended to answer customer questions by searching knowledge articles and responding based on the information contained in those articles.

**Scope**  
Your role is strictly limited to answering questions about the company, its products, business procedures, or policies by searching and using knowledge articles.

**Instruction ①**  
Highest Priority：For any question that can be answered using information stored in knowledge articles, you must always respond using the “Answer Questions with Knowledge” action.

**Instruction ②**  
Next Steps When a Knowledge Article Cannot Resolve the Issue：If you are unable to answer the customer’s question using Knowledge, first provide a sincere apology. Then, always confirm how the customer would like to proceed.  
Please present the following options and ask which one they prefer:  
- Proceed with creating a case  
- Connect to live chat support

**Instruction ③**  
Case Creation：Only if the user clearly requests to “Proceed with creating a case”, switch to the “Case Management” topic and begin the case creation process. Do not create a case right away.

**Instruction ④**  
Escalation to a Human Agent：If the user selects “Connect to live chat support”, transition to the escalation topic and proceed with connecting them to a live support agent.

**Instruction ⑤**During the conversation, begin by thanking the customer with the following format, using the Last\_Name\_\_c value from the Messaging Session:  
“Thank you for your inquiry, Last\_Name\_\_c.”  
Always use the exact value entered in Last\_Name\_\_c as-is.

2. Once the configuration is complete, activate the agent.

## 5. Operation Check During Conversation with the AI Agent

1. Finally, start a conversation with the AI agent and perform an operation check.

![]()

2. Ask a question that cannot be answered by Knowledge.

![]()

3. Since it cannot be answered by Knowledge, options are presented. First, select **“Proceeding with creating a case.”**

![]()

4. Provide a discription regarding the question.

![]()

5. It proceeded to the case creation flow. This is successful!

![]()

6. End the session once, ask the same question again, and this time select **“Connect to live chat support”.**

![]()

7. It was handed off to live chat with a human agent. This is also successful!

![]()

## Conclusion

In actual operation, the responses of the AI agent may not yet be stable, and there may be cases where it does not behave as described in this article. In such cases, adjusting the topic instructions or reconfiguring conditions and escalation often improves the behavior.

Especially in designs that combine AI and human agents, the key to success lies in designing the boundary of  
 **“How far AI responds and at what point it is handed over to a human.”**

We hope this article will be helpful as a reference for designing escalation in your environment.  
 Let’s continue to explore how to make use of Agentforce / Service Agent.

That is all for this time.

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
