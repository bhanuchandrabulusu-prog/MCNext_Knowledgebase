# SFMC Tips #300 : The Future of Marketing Cloud Engagement Changed by MCP Servers

**Source:** https://medium.com/@marketingcloudtips/the-future-of-marketing-cloud-engagement-changed-by-mcp-servers-e2f7f29ecd90

---

# SFMC Tips #300 : The Future of Marketing Cloud Engagement Changed by MCP Servers

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--e2f7f29ecd90---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--e2f7f29ecd90---------------------------------------)

10 min read

·

May 23, 2026

--

In the [**Summer ’26** new feature release](/@marketingcloudtips/marketing-cloud-engagement-summer-26-release-highlights-d51f444d3402) for **Marketing Cloud Engagement**, **MCP Servers have finally become available**.

- *In previous announcements, it was stated that the feature would be released sequentially to environments using a rolling deployment model after July 2026,* ***but it now appears to have already been released****.*

**MCP (Model Context Protocol)** is a common standard proposed by **Anthropic** that allows AI to safely operate external systems. Simply put, it is a mechanism that acts as a “bridge” enabling AI to directly operate external tools.

Going forward, we are entering an era where users can give natural language instructions to **Claude** or **Gemini** and operate **Marketing Cloud Engagement** through **MCP Servers**.

For example, operations such as the following:

- Create a new **Data Extension**
- Identify the journey with the highest unsubscribe rate in the past week
- Investigate journeys and email assets

*The full list of what AI can do through the MCP Server is available* [***here***](https://developer.salesforce.com/docs/marketing/mce-mcp/references/mce-mcp-tools/mce-mcp-tools.html)*.*

*In particular, Tools marked as “****Destructive****” may modify or overwrite items such as journeys, automations, and SQL query definitions. Depending on how they are used, they could impact existing configurations or production operations, so please use them with extreme caution.*

*The official documentation also lists the* ***required scopes*** *(permission ranges) for each Tool. It is strongly recommended to* ***grant only the minimum scopes necessary****.*

**Marketing Cloud Engagement** did not have an **Agentforce** running on the core platform like **Marketing Cloud Next**.

However, by connecting **Claude** or **Gemini** through **MCP Servers**, there is a possibility that we are entering an era where external AI can be used like an “operator for Marketing Cloud Engagement”.

In this article, I will actually configure the **MCP Server** and review the flow up to the start of usage.

## Prerequisites

Before starting the steps in this article, install and configure AI assistants that support **MCP**, such as the following.

- **Claude Code**
- **Gemini CLI**

Claude Code is basically a paid feature.  
Therefore, this time **I am implementing it using Gemini CLI**, **which is available for free**.

*If you’re using* ***Claude Code****, please refer to the* [*following link*](/@roybablu164/how-to-connect-claude-to-salesforce-marketing-cloud-via-mcp-server-71a76f4fc97b)*.*

[## How to Connect Claude to Salesforce Marketing Cloud via MCP Server

### A complete step-by-step setup guide for Windows. Written for people who have never used a CLI before. Every error you…

medium.com](/@roybablu164/how-to-connect-claude-to-salesforce-marketing-cloud-via-mcp-server-71a76f4fc97b?source=post_page-----e2f7f29ecd90---------------------------------------)

## Create an Installed Package

To use **MCP Servers**, create an **Installed Package** on the **Marketing Cloud Engagement** side so that AI assistants can connect to it.

1. From the “Setup” screen in **Marketing Cloud Engagement**, navigate to the following.

Platform Tools ＞ Apps ＞ **Installed Packages**

2. Click “New”.

3. Enter a package name (example: **Marketing Cloud MCP for Gemini**) and save it.

![]()

*\*The help documentation instructs you to select “****Other****” for the category,* ***but currently category selection is not available****.*

## Create an API Integration Component

1. Scroll down within the created **Installed Package** and click “**Add Component**”.

2. Select **“API Integration”** as the component type.

![]()

3. Select **“Public App”** as the integration type and proceed to the next step.

![]()

## Configure Public App Properties

1. Next, a **Redirect URI** is required, but it cannot yet be finalized at this stage, so temporarily enter the following value. It will later be replaced with the official URI.

```
https://salesforce.com
```

![]()

2. Next, configure the permission scopes that will be granted to AI through the **MCP Server**.

⚠️ **Warning:** *Do not grant more permissions to AI than necessary.*

For example, if you want to allow the creation and modification of **Data Extensions**, grant scopes such as the following.

- Data ｜ Data Extensions ｜ Read
- Data ｜ Data Extensions ｜ Write

![]()

## Check the Client ID and Tenant ID

1. After creating the **Installed Package**, confirm and make note of the following.

- **Client ID**This is the displayed **24-character alphanumeric string**.
- **Tenant ID**This is the **28-character alphanumeric string** included in the **Authentication Base URI** and similar values.

For example, if the **Authentication Base URI** is as follows:

```
https://mcphchq9d5b8mlzeyc2v1example.auth.marketingcloudapis.com/
```

Then the **Tenant ID** is the following value.

```
mcphchq9d5b8mlzeyc2v1example
```

## Configure the Official Redirect URI

1. Next, click the **“Edit”** button in the **API Integration** section.

2. Using the **Client ID** and **Tenant ID** you noted earlier, configure the following official **Redirect URI**.

![]()

- Replace the previously entered “https://salesforce.com” value.
- Replace `{tenantId}` and `{clientId}` with your own values.

**① When using the US-hosted MCP Server**

```
https://mai-mce-mcp-cdp1.sfdc-yfeipo.svc.sfdcfc.net/t/{tenantId}/c/{clientId}/api/mcp/oauth/callback
```

**② When using the EU-hosted MCP Server**

```
https://mai-mce-mcp-cdp1.sfdc-yzvdd4.svc.sfdcfc.net/t/{tenantId}/c/{clientId}/api/mcp/oauth/callback
```

***\*In the case of Japan****, it is likely acceptable to use the* ***US-hosted MCP Server*** *from a distance perspective. This difference mainly affects* ***connection latency****.*

## Grant Access Permissions

1. Next, grant the required permissions from the **Access** tab.

**Note:** *It may take several minutes for newly registered or updated Installed Package settings to take effect. If you encounter authentication or connection issues, please wait a few minutes after making the changes and then try again.*

## Use MCP Servers with Gemini CLI

1. Add the MCP server in Gemini CLI by entering the following command:

```
gemini mcp add mce -t http https://xxxxx.svc.sfdcfc.net/t/{tenantId}/c/{clientId}/api/mcp
```

**① When using the US-hosted MCP Server**

```
https://mai-mce-mcp-cdp1.sfdc-yfeipo.svc.sfdcfc.net/t/{tenantId}/c/{clientId}/api/mcp
```

**② When using the EU-hosted MCP Server**

```
https://mai-mce-mcp-cdp1.sfdc-yzvdd4.svc.sfdcfc.net/t/{tenantId}/c/{clientId}/api/mcp
```

- Replace `{tenantId}` and `{clientId}` with your own values.
- Command to check whether it has already been registered: `gemini mcp list`
- If you want to remove it first: `gemini mcp remove mce`

2. After the configuration is complete, run MCP authentication in Gemini CLI. This will open the Marketing Cloud Engagement login screen in your browser.

- Method: Enter `/mcp auth mce`.

Note: *The slash (*`/`*) is required here because these are treated* ***as internal Gemini CLI commands****. Without the slash, the input will be treated as a normal prompt.*

3. Once authentication is completed, the following message will be displayed, and Gemini CLI will be able to access Marketing Cloud Engagement through the MCP server.

![]()

4. As a result, you can operate Marketing Cloud Engagement by giving natural language instructions directly to Gemini CLI.

↓ ↓ ↓

## Verification with Gemini

1. I requested the creation of a Data Extension using natural language, like the following:

> *Please create a Data Extension named* ***TestSubscribers*** *in Marketing Cloud Engagement.*
>
> *Please create the following fields.*
>
> *SubscriberKey  
> Text  
> Length 100  
> Primary Key*
>
> *EmailAddress  
> EmailAddress  
> Length 254*
>
> *FirstName  
> Text  
> Length 50*
>
> *LastName  
> Text  
> Length 50*
>
> *CreatedDate  
> Date*
>
> *Please configure it as a* ***Sendable Data Extension****.  
> Please map* ***SubscriberKey*** *to* ***Subscriber Key****.*

2. Gemini clearly displayed which [Tool](https://developer.salesforce.com/docs/marketing/mce-mcp/references/mce-mcp-tools/mce-mcp-tools.html) was being used during execution.

3. After execution, the result was displayed along with a link to the Data Extension inside Contact Builder.

### Gemini CLI MCP Tool Execution Permission Options

When executing an MCP tool in Gemini CLI, the following options are displayed:

- **① Allow once**  
  Allows the tool to run only this time. The next time the same tool is used, Gemini CLI will ask for confirmation again.
- **② Allow tool for this session**  
  Allows this specific tool to run without confirmation for the duration of the current session. Other tools will still require confirmation.
- **③ Allow all server tools for this session**  
  Allows all tools registered on the selected MCP server to run without confirmation for the duration of the current session. This is the most convenient option if you plan to work extensively with Marketing Cloud Engagement.
- **④ No, suggest changes (Esc)**  
  Rejects execution of the tool.

4. When navigating to the link, I was able to confirm that the Data Extension had been created successfully without any issues. Success!!

## Considerations

### About Usage Fees

- The **MCP Server** itself for **Marketing Cloud Engagement** can be used free of charge.
- However, when using **MCP Servers**, tokens are consumed on the AI assistant side, such as **Claude** or **Gemini**. Usage fees associated with token consumption vary depending on the type of AI being used and the contract between the organization and the AI provider.
- In addition, **MCP Servers** internally operate by calling **Marketing Cloud Engagement APIs**. Therefore, the number of **API calls** on the **Marketing Cloud Engagement** side is also consumed.

*Marketing Cloud Engagement has annual limits on the number of API calls that can be executed, and those limits vary depending on the contracted Edition.*

- *Pro Edition: 2 million API calls per year*
- *Corporate Edition: 6 million API calls per year*
- *Enterprise Edition: 200 million API calls per year*

*\*At this time, there is no provided method to check the cumulative API call consumption.*

How was it?

With this **MCP Server** support, **Marketing Cloud Engagement** may be entering an era where it can be operated while directly conversing with AI.

In particular, areas that **Marketing Cloud Engagement** previously lacked, such as:

- Natural language operations
- SQL validation and updates
- Automation of administrative tasks
- Acceleration of analysis

will likely be supplemented by **Claude** or **Gemini**.

This may be considered the beginning of an era where AI works “side by side” with **Marketing Cloud Engagement administrators and operators**.

I believe this update has the potential to significantly change the operational methods of **Marketing Cloud Engagement** itself going forward.

It may be interesting to start experimenting with small use cases first and explore what kinds of things become possible.

That is all for this time.

Salesforce also announced the following use cases at **Connections 2026**.

## 1. Create and Update Journeys

With MCP, Journey Builder journeys can be created and modified entirely through conversation.

Traditionally, marketers needed to open Journey Builder and manually:

- Configure the Entry Source
- Add Email Activities
- Add Wait Activities
- Save and publish the journey

With MCP, you can simply say:

> *“Create a three-email welcome journey. Send Email 1 immediately after registration, Email 2 three days later, and Email 3 seven days later.”*

The agent can automatically:

- Create the journey
- Add and configure the required activities
- Save the configuration

## 2. Data Extension Management

Creating and maintaining Data Extensions can also be done using natural language.

For example:

> *“Create a Data Extension for Holiday Shoppers. Include Email, First Name, Last Name, and Purchase Date fields, and make Subscriber Key the Primary Key.”*

The agent can automatically:

- Create the Data Extension
- Create the fields
- Configure the data types
- Set the Primary Key

Tasks that previously required manual configuration in Contact Builder can now be completed through conversation alone.

## 3. SQL and Automation Studio Operations

MCP is also well suited for maintaining Automation Studio assets.

For example:

> *“A new field called Propensity Score has been added to the Customer\_Signals Data Extension. Update all SQL queries that use this Data Extension to include the new field. First generate an impact analysis report, then apply the changes.”*

The agent can:

- Locate relevant SQL Query Activities
- Analyze dependencies
- Update the SQL queries
- Update Automation Studio assets

For Marketing Cloud Engagement administrators, SQL maintenance is likely one of the most valuable MCP use cases.

## 4. Subscriber and Contact Management

Subscriber and contact information can also be searched and updated through conversation.

For example:

> *“Check the subscription status of john@example.com. If the contact has opted out of the Marketing List, update the First Name to Jonathan.”*

The agent can:

- Search for the contact
- Check All Subscribers status
- Review List Memberships
- Update the contact profile

Tasks that previously required switching between Contact Builder, Email Studio, and All Subscribers can now be completed in a single conversation.

## 5. SMS and Push Notification Management

MCP can also assist with MobileConnect and MobilePush administration.

For example:

> *“Create a keyword called SAVE20. Create an SMS Definition and send a transactional SMS to the Summer Promo list.”*

The agent can:

- Create the MobileConnect keyword
- Create the SMS Definition
- Send the SMS message

In addition, MCP can support the management of push notifications through MobilePush.

That’s all for this article.

Stay tuned for more Salesforce Marketing Cloud tips! 😎

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
