# Agentforce Marketing: go headless, today

**Source:** https://the-agentic-marketer.com/marketing-cloud-next-tips-from-the-trenches/headless-marketing

---

At TDX ’26 conference, Salesforce announced “**Headless 360**” which simply means you’ll be doing your marketing job from Claude, ChatGPT or Slack, in plain language (and very soon, voice), without ever opening a Salesforce tab.

## Headless 360: When You Stop Working Inside Salesforce

So far, when using an Agent in Marketing Cloud Next, you type a prompt inside Salesforce. The agent is made of Topics and Actions, and a reasoning engine decides which ones to trigger, and in what order, to complete the task (think [Campaign or Content Creation Agents](https://the-agentic-marketer.com/marketing-cloud-next-deep-dives/agentforce-campaign-creation-content-builder-agents/))

Now imagine that same reasoning engine is no longer locked inside Salesforce. Instead, it lives in Claude or ChatGPT, and every possible Salesforce action is available to it. You describe what you want, in plain language (text or voice), from wherever you already work. The AI selects the right actions, in the right order, and gets it done, an on-the-fly agent, if you will.

That is headless marketing. **Salesforce hosted MCP servers** expose the actions. The **Agentforce Experience Layer** (AXL) brings the results back to you. No browser required.

[![](https://the-agentic-marketer.com/wp-content/uploads/2026/04/headless_marketing_updated-1024x762.png)](https://the-agentic-marketer.com/wp-content/uploads/2026/04/headless_marketing_updated.png) 

The headless marketing loop: your AI assistant selects the right Salesforce MCP servers, executes the task, and displays the result, without you ever opening a browser.

Two pieces make this possible. Salesforce hosted MCP servers are the bridge: they expose Salesforce capabilities, querying Data Cloud, reading records, triggering Flows, as actions that any compatible AI assistant can discover and call. Think of them as a menu of everything Salesforce can do, written in a language Claude or ChatGPT can read.

The Agentforce Experience Layer is the return path: once Salesforce has done the work, AXL formats the result as a card, a summary, or a decision tile, and renders it back inside the AI interface you started from. You never left. You never opened a tab.

Together, MCP and AXL close the loop: in through the AI, out through the AI.

## What's available today

There are two types of MCP servers. The **DX MCP Servers** are for developers, they are installed locally and are used to create new things inside Salesforce. But when **Parker Harris asked “*Why should you ever log into Salesforce again?*“**, a few days before TDX ’26, he was primarily talking about the **Salesforce Hosted MCP servers**, that AIs can use to discover, select, call Salesforce actions and format the results.

### Existing hosted MCP servers

The [list of supported hosted MCP servers](https://developer.salesforce.com/docs/platform/hosted-mcp-servers/guide/products-supporting-mcp.html), does not cover the whole Salesforce platform as of today, but you can expect more servers to come very soon (including a dedicated **marketing/** endpoint covering Agentforce Marketing capabilities to handle segment queries, campaign actions, consent management, etc.). Here is what is available so far (may be different in your Org):

- **platform/sobject-all:** full read, create, update, delete on any Salesforce object
- **platform/sobject-reads:** read-only access, safe for broad use
- **sobject-mutations:** create and update, no delete
- **data-cloud-sql:** query Data Cloud entities using SQL
- **analytics/tableau-next:** dashboards, semantic models, KPIs
- **invocable\_actions:** discover and trigger any Flow or Apex action in your org

In the next section, we will connect Claude to your Salesforce org and walk through a concrete headless marketing use case, querying Data Cloud and checking consent, using what is available today. Not everything is there yet, but enough to make it real and useful.

### A word on AXL (Agentforce Experience Layer)

The Agentforce Experience Layer is what formats the result on the Salesforce side before sending it back to your interface. Think of it as the presentation layer: it can wrap a raw query result into an approval card, a decision tile, or a structured summary, without you ever touching the Salesforce UI.

AXL supports many surfaces: Slack, Teams, Mobile, Gemini, WhatsApp. But here is the important nuance for today: **only Claude and ChatGPT currently support both sides of the loop** (they can call MCP servers to trigger actions *and* receive AXL-formatted results natively). Slack and Teams can receive AXL outputs, but rely on a pre-built Agentforce agent to do the reasoning: they cannot initiate MCP calls on their own yet.

In other words, if you want the full headless experience today, plain language in, structured result out, no browser, Claude and ChatGPT are your interfaces. In the following we’ll use Claude.

## Connect Claude to Salesforce

Before we can start using Salesforce from Claude, we need to connect them.

### Step 1 - Create an External Client App

Setup > External Client App Manager > +New External Client App.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20438%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2026/04/Screenshot-2026-04-24-at-01.49.51-scaled.png) 

Fill the Basic Information section of the External Client App

in the OAuth Settings section > +Enable OAuth. In Callback URL use *https://claude.ai/api/mcp/auth\_callback* (see [here if you use another MCP client](https://developer.salesforce.com/docs/platform/hosted-mcp-servers/guide/create-external-client-app.html)). Add the following OAuth scopes: *Access Salesforce Hosted MCP servers* and *Perform requests at any time*.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20438%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2026/04/Screenshot-2026-04-24-at-01.58.42-scaled.png) 

Defining the OAuth setttings of the External App

Finally, in the Security section, uncheck everything except *Require Proof Key for Code Exchange (PKCE) extension for Supported Authorization Flows* and *Issue JSON Web Token (JWT)-based access tokens for named users*

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20438%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2026/04/Screenshot-2026-04-24-at-02.02.07-scaled.png) 

Definig the security settings of the External App

+Create (it may take up to 30 minutes before the App is actually available). In Settings > App Settings access and store the Consumer Key and Secret.

### Step 2 - Activate MCP Servers

MCP servers are disabled by default and must be enabled by an admin, a security measure to control access to org data.

Setup > MCP Servers. You will see the list of MCP servers, you can open them to better understand what they do, in a human readable format. In the Tools section, you’ll see the possible actions they offer, their URL, and in Prompts, examples of how to call them.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20438%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2026/04/Screenshot-2026-04-24-at-02.12.08-scaled.png) 

The List of available MCP Servers

You can select which hosted MCP Server you want to activate, so Claude has access to these only through the External App. Note that you also can create your own MCP servers.

### Step 3 - Adding MCP Servers to Claude

First ensure you are connected to the Org in which you created the External App and activated the MCP Servers in your default browser. Then, in Claude, Customize (left sidebar) > Connectors > +Add Custom Connector

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20502%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2026/04/Screenshot-2026-04-24-at-02.33.02-scaled.png) 

Creating a Custom Connector in Claude

You’ll need to add a name, an MCP Server URL (found in detail tab of the server you want to add), and the App credentials (Consumer Key and Secret) in Advanced Settings.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20502%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2026/04/Screenshot-2026-04-24-at-02.46.23-scaled.png) 

Adding one Salesforce hosted MCP Server to Claude

In this example we first add the *marketing/data-cloud-queries* MCP server. Basically, we are giving Claude the power to query, reason over, and act on your Salesforce data, directly from a conversation, in plain language, with no code and no browser

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20502%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2026/04/Screenshot-2026-04-24-at-02.49.45-scaled.png) 

Click Connect to be directed to Salesforce

Then click Allow on the next screen.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20455%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2026/04/Screenshot-2026-04-24-at-02.50.12-scaled.png) 

Allowing Claude the access to the External App

Claude should now be connected to the MCP server you added.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20455%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2026/04/Screenshot-2026-04-24-at-02.50.36-scaled.png) 

The connection was successful

Back to Claude settings, we can see our new connector, along with the MCP server URL and the available actions.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20502%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2026/04/Screenshot-2026-04-24-at-02.51.01-scaled.png) 

Displaying the connection detail to our first hosted MCP server

You can then add other actions, depending on what you want Claude to do. For our Marketing use-case, we’ll also add the sobject-reads MCP server, using the same steps (execpt allowing access to the External App, which was already granted).

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20502%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2026/04/Screenshot-2026-04-24-at-03.11.57-scaled.png) 

A second MCP Server was added to extend how Claude can interact with Salesforce

## Let's go headless!

We can now simply ask Claude to perform task, using natural language, and it will select the appropriate MCP server, and which action inside them to trigger, in the relevant order (on the fly agent). Here is prompt we’ll use:

```
				
					Query my Data Cloud subscription records and find all contacts who are 
opted in to the Newsletter subscription, then cross-check them in Salesforce 
to show me those whose Contact record has not been modified in the last 6 months. 
Give me a table with their name, email, opt-in date, and last modified date.
				
			
```

And voilà, see our first headless use of Salesforce in action.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20562%201024%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2026/04/first-headless-flow-scaled.png) 

Our prompt was executed and calls to 2 different MCP servers were performed before displaying the final result.

## Final thoughts

What we just did is more powerful than it looks. One plain-English sentence. Two MCP servers selected on the fly. A real Data Cloud schema explored autonomously, a consent table queried, results cross-referenced in Salesforce Core, filtered by date, and returned as a clean table. No browser. No clicks. No SQL.

And this is just the beginning. The *marketing/* MCP endpoint, covering segments, campaign actions, flows, and consent, is already on Salesforce’s roadmap. When it lands, the way every marketer interacts with Salesforce changes for good.

I cannot wait.
