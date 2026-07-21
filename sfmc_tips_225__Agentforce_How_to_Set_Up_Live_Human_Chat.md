# SFMC Tips #225 : Agentforce: How to Set Up Live Human Chat

**Source:** https://medium.com/@marketingcloudtips/sfmc-tips-225-agentforce-how-to-set-up-live-human-chat-7e09f6ae051b

---

# SFMC Tips #225 : Agentforce: How to Set Up Live Chat Agent

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--7e09f6ae051b---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--7e09f6ae051b---------------------------------------)

8 min read

·

Dec 31, 2025

--

Photo by [Vidar Nordli-Mathisen](https://unsplash.com/@vidarnm?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

In the previous article, at the start of the chat, I introduced a configuration where users can select which path to proceed on:  
 “**Connect with AI Agent**” / “**Connect with a Human (Live Agent)**”.

[## SFMC Tips #224 : Agentforce: How to Set Up a Pre-Chat Form and How to Utilize It Afterwards

### When installing Agentforce (Service Agent) on an external site, you can configure a “pre-chat form” that asks users to…

medium.com](/@marketingcloudtips/sfmc-tips-224-agentforce-how-to-set-up-a-pre-chat-form-and-how-to-utilize-it-afterwards-6626d3d7907b?source=post_page-----7e09f6ae051b---------------------------------------)

![]()

However, at that time, I did not mention the configuration steps for human chat (Consult a Support Representative).  
This time, as a continuation, I will explain the configuration method to implement live human chat.

In the previous article, I explained the configuration where the “AI path” / “Human path” selected by the customer in the pre-chat is branched using a Flow.  
Based on that premise, this time I will proceed with the configuration of human chat using the Human path (the path on the right).   
Please understand this in advance.

However, please rest assured that the basic configuration does not change significantly.

## **Flow of the configuration this time**

To implement live human chat, proceed with the configuration in the following order.  
Even if you have not read the previously mentioned article, you can build the configuration by following this order.

1. **Confirm Omni-Channel settings are enabled**
2. **Confirm Service Channel**
3. **Configure Routing**
4. **Configure Queue**
5. **Configure Presence Status**
6. **Configure Permission Set for Presence Status and assign it**
7. **Configure Omni-Channel Flow**
8. **Configure Omni-Channel for the Service Console**
9. **Verify in the Service Console**
10. **Verify the flow from chat**

By completing these settings,  
basically, routing to a human representative will occur and they will be ready to respond.

## 1. Confirm Omni-Channel settings are enabled

1. Open Omni-Channel Settings from Setup and configure the following three items, then save:

- Check **Enable Omni-Channel**
- Turn on **Enable Enhanced Omni-Channel Routing**
- Select **Automatically log agents in to Omni-Channel in the new window or tab**

## 2. Confirm the Service Channel

1. Open **Setup > Service Channels** and check the list.  
In demo environments or free developer orgs, a Service Channel for “Messaging Session” may already exist.  
(Examples: Messaging, LiveMessage)

> *※ Only* ***one service channel can be created per object****.*

2. On the service channel detail page, confirm that the target object is set to “Messaging Session”.  
If there are no issues, note the service channel name to use later in the Flow configuration.

- Free developer org: **Messaging** (used this time)
- Example in a partner-only SDO: **LiveMessage**

If a Service Channel for the “Messaging Session” object does not exist, please create one.

Example in a partner-only SDO

## 3. Configure Routing

1. From Setup, select **Routing Configurations** and click **New**.

2. On the next settings page, decide the **Routing Configuration Name** and **Developer Name**, then enter or select the following and save.  
Even if these settings differ, the agent will not fail to function.

- Routing Priority: **1**
- Routing Model: **Most Available**
- Capacity Type: **Inherited**
- Units of Capacity: **1**

## 4. Configure Queue

1. From Setup, select **Queues** and click **New**.

2. On the next screen, decide the **Label** and **Queue Name**, then enter or select the following and save:

- Routing Configuration: search and select the configuration created earlier
- Supported Object: select **Messaging Session**

3. Scroll down, and as queue members, select the people who will act as agents (typically customer service representatives), then save.

## 5. Configure Presence Status

1. Next, open **Setup > Presence Statuses** and create the following three statuses:

- **Available** … Online / Messaging
- **Away — On Break** … Busy
- **Away — Missed Call** … Busy

2. Configure referring to the following:

**◆ What is Presence Status?**  
Presence Status indicates whether representatives are available to respond. Omni-Channel uses this status to route messages to representatives who can respond.

- Available: Accepting work (online)
- Away types: temporarily unavailable
- Offline (default): No need to create (already available)

## 6. Configure Permission Set for Presence Status and assign

1. Next, create a permission set to access this Presence Status.  
Prepare a new permission set.  
In my case, I named it **“Service Presence Statuses Access (Custom)”**.

2. In the permission set, go to “App Settings” and select **Service Presence Statuses Access**.

3. Make the three created Service Presence Statuses available.

4. After creating the permission set, assign it to users.

5. Assign it to users who handle live chat (customer service representatives).

6. After that, go to the user’s edit page and enable **Service Cloud User** for that user. (← Do not forget)

## 7. Configure the Omni-Channel Flow

1. Search for **Flows** in Setup and open the existing Omni-Channel Flow created in the previous article.

2. On the right side branch after the decision, add an element and select **Route Work**.

3. After deciding the element name and API reference name, select the variable **recordId** (already created).

This **recordId** receives the Messaging Session ID when a conversation with the agent begins. For reference, it is configured as follows:

- API Reference Name: **recordId**
- Data Type: **Text**
- Availability Outside the Flow: Checked for “**Available for Input**”

4. After the recordId variable is entered, select “**Messaging**” from the Service Channels.  
\*This “Messaging” targets the **Messaging Session** object.

5. Select “**Queue**” for the Route To.

6. For the Queue ID, select the queue created earlier.

7. Once the configuration is complete, save the flow as a **new version**.

8. Activate the flow.

## 8. Configure Omni-Channel for the Service Console

1. From Setup, open **App Manager**.

2. Find **Service Console** from the list and select **Edit** from the action menu.

3. From **Utility Items (Desktop Only)**, click **Add Utility Item**.

4. Select **Omni-Channel**.

5. Save the configuration.

## 9. Verify the Service Console

1. Next, verify in the Service Console.  
Click **Omni-Channel** displayed in the utility bar as shown below.

2. It is currently “Offline”, so change it to “Available”.

![]()

3. Confirm that it has switched to “Available”.

![]()

4. Then, in Object Manager, search for **Messaging Session**.

5. From the Lightning Record Page, select **Messaging Session Record Page** and click Edit.

6. Delete the default **Conversation** component.

7. Drag and drop the **Enhanced Conversation** component where the removed component was.

8. Save and activate.

> ***Important Note:*** *Enhanced Chat conversations can only be displayed in the* ***Enhanced Conversation*** *component.*

## 10. Verify flow from chat

1. Select **“Connect with a Human”** and start the chat.

![]()

2. Immediately, the call will come through to the Service Console. Click the checkmark.

![]()

3. The conversation starts with the person whose name was entered in the pre-chat form.

4. Confirm that both sides are able to converse. Success.

## **Conclusion**

In the configuration steps introduced this time, I did not handle representative workload (capacity) or detailed routing conditions.  
Therefore, for actual full-scale operation in business, more detailed tuning is required depending on the environment and service structure.

However, I believe that you were able to grasp the overall flow up to the point where you can receive human chat.  
First, use the procedures here as a base and develop according to your environment.

I hope this article will be helpful as the first step in utilizing Agentforce.

That is all for this time.

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
