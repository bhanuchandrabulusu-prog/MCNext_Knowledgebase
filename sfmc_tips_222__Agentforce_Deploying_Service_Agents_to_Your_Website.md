# SFMC Tips #222 : Agentforce: Deploying Service Agents to Your Website

**Source:** https://medium.com/@marketingcloudtips/sfmc-tips-222-agentforce-deploying-service-agents-to-your-website-8b5f38c6b0b9

---

# SFMC Tips #222 : Agentforce: Deploying Service Agents to Your Website

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--8b5f38c6b0b9---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--8b5f38c6b0b9---------------------------------------)

7 min read

·

Dec 25, 2025

--

Photo by [Ahmad Dirini](https://unsplash.com/@ahmadirini?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

Previously, I wrote an article about how to install Agentforce on an external site (CloudPages in Marketing Cloud Engagement).

[## SFMC Tips #193 : Agentforce: Deploying Service Agents on CloudPages (External Sites)

### In this article, I’ll explore how to embed the Agentforce Service Agent on an external website using CloudPages in…

medium.com](/@marketingcloudtips/agentforce-deploying-service-agents-on-cloudpages-external-sites-d4fb5edacb91?source=post_page-----8b5f38c6b0b9---------------------------------------)

At that time, I received feedback such as “**I want to know a little more about the steps in the middle**”, so this time I would like to supplement the “**parts that were omitted**”.

## Which parts were omitted

The settings omitted in the previous article were the following items. The reasons for omission are also described. At the time of that article, I used a Trailhead Playground, so I omitted them.

**① Creating and activating an Agentforce Service Agent**  
 ➡ Omitted because it can be configured by following Trailhead instructions

**② Confirm activation of Omni-Channel settings**  
 ➡ Enabled by default in the Playground environment.

**③ Confirm activation of Digital Experiences settings**  
 ➡ Enabled by default in the Playground environment.

**④ Confirm Service Channel**  
 ➡ Already created in the Playground environment.

**⑤ Routing settings**  
 ➡ Already created in the Playground environment.

**⑥ Queue settings**  
 ➡ Already created in the Playground environment.

**⑦ Omni-Channel Flow settings**  
 ➡ Editable by following Trailhead instructions.

**⑧ Messaging settings**  
 ➡ Already created in the Playground environment.

**⑨ Embedded Service Deployment settings**  
 ➡ Already created in the Playground environment.

By the way, among these, [**① Creating and activating an Agentforce Service Agent**](/@marketingcloudtips/sfmc-tips-221-agentforce-how-to-implement-a-service-agent-using-knowledge-ef7a9e0cdc6b) corresponds to the article I wrote last time, so in this article I will cover ② to ⑨ except for ①.

And by continuing from here and proceeding with the previous article (installation on CloudPages), you will be able to complete the entire workflow.

Now, let’s move on to the setup flow!!

## Setup Procedure

## 1. Creating and activating an Agentforce Service Agent

This step has already been explained in the previous article.  
Please refer to the following article to create a Service Agent that utilizes Knowledge.

[## SFMC Tips #221 : Agentforce: How to Implement a Service Agent Using Knowledge

### Salesforce partners implementing Marketing Cloud Next have likely noticed a growing trend: projects where Marketing…

medium.com](/@marketingcloudtips/sfmc-tips-221-agentforce-how-to-implement-a-service-agent-using-knowledge-ef7a9e0cdc6b?source=post_page-----8b5f38c6b0b9---------------------------------------)

## 2. Confirm activation of Omni-Channel in Omni-Channel Settings

Open Omni-Channel Settings from Setup and configure the following three items and save.

- Check “**Enable Omni-Channel**”
- Turn on “**Enhanced Omni-Channel Routing**”
- Select “**Automatically log agents into Omni-Channel in the new window or tab**”

## 3. Confirm activation of Digital Experiences in Digital Experiences settings

Select **“Settings” under Digital Experiences** from Setup and confirm whether Digital Experiences is activated. If it is not activated, please activate it.

## 4. Confirm Service Channel

Next, open **Setup > Service Channels**.  
In a demo environment, a Service Channel for Messaging Sessions may already be created with a name containing “**Message**”. In that case, click the appropriate Service Channel.

> ***\*Only one Service Channel can be created per object.***

On the Service Channel detail screen, confirm that the object “**Messaging Session**” is selected, and make note of the Service Channel name. You will use it later when creating the Flow.

- In this example (SDO), the Service Channel name is **“LiveMessage”**.
- In free development environments, it is often **“Messaging”.**

If there is no Service Channel for the “Messaging Session” object, please refer to the following example and create a new one.

## 5. Routing Settings

Select **Routing Configurations** from Setup and click “New”.

On the next screen, decide the Routing Configurations Name and API Reference Name, and enter or select the following and save.  
Note: The agent will not fail to work if you do not use these exact settings.

- **Routing Priority: 1**
- **Routing Model: Most Available**
- **Work Item Type: Inherited**
- **Unit of Work Item Size: 1 (or Many samples set this to 2)**

## 6. Queue Settings

Select **Queues** from Setup and click “New”.

On the next screen, decide the Label and Queue Name, and enter or select the following and save:

- Routing Configuration: Search and select **the Routing Setting configured above ↑**
- Supported Objects: Select “**Messaging Session**”

## 7. Omni-Channel Flow Settings

Select “Flows” from Setup and create a new Flow.

Select **Omni-Channel Flow**.

Add an element and select **Route Work**.

![]()

Decide the Element Name and API Reference Name, then select “New Resource” for the Record ID variable.

Select **Variable**.

Enter or select the following on the next screen and save:

- **API Reference Name: recordId**
- **Data Type: Text**
- **Availability Outside the Flow: Check “Available for input”**

Once “recordId” has been entered in the Record ID Variable field, select “LiveMessage” from Service Channel.

> *This “LiveMessage” targets the “Messaging Session” object.*

![]()

For Routing To, select **Agentforce Service Agent**.

Select the Service Agent that has already been created.  
“Only **activated** agents” can be selected here, so if nothing appears, please confirm whether it is activated.

For Fallback Queue ID, select the queue created earlier.

![]()

Once configuration is complete, name the Flow, save it, and activate it.

## 8. Messaging Settings

Select **Messaging Settings** from Setup and create a new channel.  
Note: The Messaging toggle does not need to be enabled here.

Select **Enhanced Chat**.

![]()

Enter the Channel Name and API Reference Name, set Release Type to “Web”, and enter the domain where you plan to place the agent.

![]()

For Channel Routing, select **Omni-Flow**.

![]()

Select the Flow definition.

> *This screen is a bit unusual —* ***the suggestion list will not appear unless you type characters****.  
> For example, if the Flow Name is “Service Agent Route Work”, typing “Service” will show the suggestion.*

Next, select the queue created earlier.

> *Again, you must type to show suggestions.  
> If the queue name is “Service Agent”, type “Service”.*

Save after entering.

This step automatically forms the “Embedded Service Deployment” and “Site Endpoint” in the background using this Messaging Setting name, so the process may take some time.

## 9. Embedded Service Deployment Settings

Next, select **Embedded Service Deployments** from Setup.  
As mentioned above, the Embedded Service Deployment using the Messaging Setting name will have been automatically generated, so select it.

Click **Publish** once here.

> ***Important Note****: If the agent does not appear properly on your site, returning to this screen and clicking “****Publish****” may cause the agent to appear.*

That is all.

## How was it?

Once the configuration up to this point is complete, please continue with the next steps in the following article:

[## SFMC Tips #193 : Agentforce: Deploying Service Agents on CloudPages (External Sites)

### In this article, I’ll explore how to embed the Agentforce Service Agent on an external website using CloudPages in…

medium.com](/@marketingcloudtips/agentforce-deploying-service-agents-on-cloudpages-external-sites-d4fb5edacb91?source=post_page-----8b5f38c6b0b9---------------------------------------)

Remaining tasks are as follows:

1. **Paste the script into the external website**
2. **CORS settings**
3. **Trusted URL settings**
4. **Site settings (under User Interface)**
5. **Confirm display on the external website**

In this article, assuming that many readers on my note are Marketing Cloud Engagement users, I introduced **CloudPages** as an example that is easy to try.

However, if you have your own **external website** that you can freely use, you may install it not only on CloudPages but also on any other website.

> ***Tips:*** *If the “Domain” in Messaging Settings (8) is set somewhat correctly, the agent may appear on the website even without performing steps 11–13. However, from the perspective of stable operation and preventing issues, performing all settings is best practice.*

That’s all for now.

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
