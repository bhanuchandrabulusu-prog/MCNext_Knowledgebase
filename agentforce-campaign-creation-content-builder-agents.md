# Marketing Cloud Next: Campaign Creation and  Content Builder Agents

**Source:** https://the-agentic-marketer.com/marketing-cloud-next-deep-dives/agentforce-campaign-creation-content-builder-agents

---

In this article we will see **how to activate and use Agentforce Generative AI in Marketing Cloud Next** (Growth and Advanced). You may already have set the Agentforce (Default) agent (fka Copilot or In-Org Assistant) and in that case you’ll have to **migrate**, which we cover in here as well.

## Setup

### Activate Einstein

If not already done, go to **Setup > Einstein > Einstein Generative AI > Einstein Setup** and Turn On Einstein. Leave other elements on the page as-is.

[![](https://the-agentic-marketer.com/wp-content/uploads/2025/11/Screenshot-2025-11-24-at-15.32.14-1024x559.png)](https://the-agentic-marketer.com/wp-content/uploads/2025/11/Screenshot-2025-11-24-at-15.32.14-scaled.png) 

Turning On Einstein Generative AI features

### Activate Agentforce

From **Setup > Einstein > Einstein Generative AI > Agentforce Studio > Agentforce Agents** and Turn Agentforce On.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20437%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/11/Screenshot-2025-11-24-at-15.54.38-scaled.png) 

Enabling Agentforce and Agents

### Migration from Agentforce (default) – Optional

If you previously activated Einstein Copilot, and added the Campaign Creation and Content Creation to it, along with their related actions, you should be prompted to migrate to Agentforce employee agent. You simply **trigger the migration using the Get Started Button**.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20436%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/11/Screenshot-2025-11-20-at-16.09.12.png) 

Agentforce (Default) in-org assistant must be upgraded to Agentforce Employee Agent

This will create a new **Agentforce Employee Agent**, embedding the same Topics. You can now remove those Topics from the newly created Agent, and follow the steps to create the new agents below. You may then deactivate Copilot by changing **Enable the Agentforce (Default) Agent to Off**. You should see “Your Agentforce (Default) Agent is Now an Employee Agent”.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20437%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/11/Screenshot-2025-11-24-at-16.14.43-scaled.png) 

Agentforce Employee Agents is now turned On and Copilot turned Off

Note, to see the Get Started button mentioned above, you may need to provision some **Flex Credits** ([source](https://help.salesforce.com/s/articleView?id=ai.agent_setup_explore_types.htm&type=5))

### Create the Campaign Creation Agent

We will create this Agent, and the following one (Content Craetion),  using  using an **Agent Template**, based on **Agentforce Employee Agents**. To be available, those templates **require Salesforce Foundations** (See Set up AI in Marketing Cloud Next [in the Implementation Guide](https://resources.docs.salesforce.com/rel1/doc/en-us/static/pdf/mktg_implementation_guide.pdf)) and **Flex Credits** (see this Employee Agent in [Agent Types and Considerations](https://help.salesforce.com/s/articleView?id=ai.agent_setup_explore_types.htm&type=5)). From Agentforce in Setup, Click New Agent.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20437%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/11/Screenshot-2025-11-24-at-16.33.56-scaled.png) 

Selecting the Campaign Creation Agent Template

Next. This Agent contains the **“Marketing Cloud: Campaign Planning” Topics** and its relations action. This Agent template is for “Users who want to generate, make, create, summarize, or bootstrap their marketing campaigns or briefs should use this topic.”.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20437%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/11/Screenshot-2025-11-24-at-16.37.34-scaled.png) 

The "Marketing Cloud: Campaign Planning" Topic is added by default

[**Edit** 11/03/2026] – Since Spring ’26 new Topics must be added to the Campaign Creation Agent. First the Content Creation Topic (same as below, containing the following actions: “Marketing Cloud: Create Section with Content”, “Marketing Cloud: Draft Content” and “Marketing Cloud: Create Section”) and **the new Marketing Cloud: Campaign Preview Refinement Topic** (containing the following actions: “Marketing Cloud: Refine Campaign Preview”, “Get Record Details”, “Update Record” and “Query Records”). This latter Agentforce Topic enables conversational refinement of campaign drafts, allowing marketers to adjust structure, content, and channels before final deployment.

Next. In this Page, give some Context of **which Company the Agent is working for**, in the Company input, and check “Keep a record of conversations with enhanced event logs to review agent behavior” to analyse how this Agent is used. Next.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20437%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/11/Screenshot-2025-11-24-at-16.43.06-scaled.png) 

Defining the Language and Tone of the Agent

Then, select **which languages** your Agent can handle and the **default Tone** to use. Create. You agent is now Created and you are redirected to Agent Builder. Click Activate (you don’t need to add a knowledge library to this type of agent) so your Agent can be used. Before it is available, we’ll need to allow its use using a Permission Set in a following step.

### Create the Content Creation Agent

The procedure to install this Agent is similar to the previous one, we just select another Agent Template as a starting point: the **Content Builder Agent**. From Agentforce Page, New Agent.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20437%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/11/Screenshot-2025-11-24-at-16.49.47-scaled.png) 

Content Creation Agent Template.

Then Next (notice the Topic in this template id now **Content Creation**). Next, add your Company info. Next. Create.

### Giving Access to our new Agents

One of the main difference between the previous version of in-org Agents (Copilot) and Agentforce Employee Agent is that you **define who can access them thanks to a Permission Set** (preferred method to the Profile based one). We’ll create one Permission Set to give access to the two new agents, but you could create one Permission Set for each Agent to have a more granular control.

**Setup > Permission Sets > New** (or use an exisinting one), and give a name to it, like “Marketing Agents Access”, then Save.

Once you Saved, Select the **new Agent Access permission.**

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20437%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/11/Screenshot-2025-11-24-at-18.15.41-scaled.png) 

Creating a Permission Set to Access the Agentforce Marketing Agents

Then Click Edit, and Add the Agent/s you want to give access to thanks to this Permission Set.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20437%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/11/Screenshot-2025-11-24-at-18.25.07-scaled.png) 

Select which Agent this Permission Set will give access to

Then click Save, **Manage Assignement > Add Assignement**, to add the users you want to give access to the new Agents, then Next and Assign. The Agent Access Tab, when editing an Agentforce Employee Agent displays the Permission Set/s that can be added to a User to grant access to it.

**And that’s it, you can new use Agentforce to create Campaigns and Content.**

## Using Agentforce Agents in Marketing Cloud Next

We now have the Campaign Creation Agent and the Content Creation Agent (these are the default names). **From the Homepage of the Marketing App**, you can click on the Agentforce icon and you will be  presented the option to select the Agent you want to use.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20437%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/11/Screenshot-2025-11-24-at-18.39.17-scaled.png) 

Agentforce Agents from the Marketing App homepage

### Campaign Creation

**Only Campaign Creation** should be selected from the Marketing App Homepage, **Content Builder Agent is meant to be used in the Content Editor only.**

With Campaign Creation selected (you may need to accept to use Agentforce the first time the Agent launches) click Select.

Then you can input a Campaign Brief and follow the steps, which will create **an entire Campaign**:

- Campaign and Brief records
- Contents
- Flow
- Segment (using Einstein Segment Builder)

Troughout the process, you can accept or refine the proposed items.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20437%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/11/Screenshot-2025-11-24-at-18.50.40-scaled.png) 

Agenforce Campaign Creation creates an entire Campaign in 3 simple steps.

### Content Creation Agent

That Agent is to be used **within the Content Editor** (Email, Landing Page, WhatsApp messages, etc.). The Campaign Creation should not be used from within the Builder. **From the Builder select the Agentforce icon on the top left**, which opens a new window, where you can add content from a prompt. Previously, a sparkling icon on a Canvas component was to be used. Click Content Builder Agent and then Select.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20437%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/11/Screenshot-2025-11-24-at-19.25.45-scaled.png) 

Content Creation Agent from the Builder

You can then ask the Agent to generate Content: paragraphs, Column, for you from a Prompt.

## Create Custom Agents

You might want to create your own Agents from the Agentforce Employee Agent template to generate your own Content or Assets. For this, inspecting how the two previous Agents work in Agent Builder, and see how the reasoning engine orchestrates the Actions in their Topic is really insightful.

However, reusing the Actions, is not that easy. For example, in the Content Creation Agent, the  Create Section with Content Action ([reference](https://help.salesforce.com/s/articleView?id=ai.copilot_actions_ref_mc_create_section_with_content.htm&type=5)) does actually generate and write content in an Email (or other type of content), but cannot be used to write content generated from another action (for example, a new action getting the last 3 articles of the TAM website). As the reference puts it “This action calls an internal invocable action, which uses internal-only prompt templates to create and revise sections with content in landing pages and emails in the content builder.”

The Same is true for the Save Campaign Action, found in the Marketing Cloud: Campaign Planning Topic. The Action is actually a Flow, calling a Invokable Action to create a Flow and Emails, but this cannot be used out of this Context.

However, you may create a Data Library (ex. infos on your services) and make it available in a new Prompt Template, that you then wrap in a new Action and embed in the default Content Creation Agent. Finally add instructions on how to use/prioritise this Action (something like “Use in priority the Service Detail Action when the input Prompt references a given Product or Service). [See this Trailhead module](https://trailhead.salesforce.com/content/learn/modules/ai-in-marketing-cloud-next/create-and-customize-a-marketing-campaign-with-agentforce) for more info.
