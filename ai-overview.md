# AI Overview in Agentforce Marketing

**Source:** https://the-agentic-marketer.com/marketing-cloud-next-deep-dives/ai-overview

---

There are several main areas where Agentforce and Einstein can be leveraged in Marketing Cloud Growth & Advanced.

## Einstein Send Time Optimisation

When sending Emails to you Audience, their actual engagement with your content like Open or Clicks are a solid data fundation, which can be used to train an Einstein Model (data is anonymised and the 90 previous days of engagement are used).

It becomes then possible to Send an Email, not at a given predefined time, but at a time Einstein AI chooses for you, so the Engagement rate is maximized for each Individual.

Setup, is really easy, search for Marketing Cloud in Setup (the global one), then go to Custom Setting, Einstein AI and finally “Configure Einstein Settings” button.

[![](https://the-agentic-marketer.com/wp-content/uploads/2025/08/009-Once-activated-Einstein-STO-needs-at-least-72-to-train-the-model-1024x559.png)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/009-Once-activated-Einstein-STO-needs-at-least-72-to-train-the-model.png) 

Once activated Einstein STO needs at least 72 to train the model.

Once Activated (at least 72 hours, but can be more depending on you engagement data), you can select to send an Email in the Flow associated with the Campaign at a the best time chosen by Einstein STO.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20437%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/010-Select-in-a-Flow-to-send-your-Email-at-the-best-time-once-Einstein-STO-is-activ.png) 

Select in a Flow to send your Email at the best time (once Einstein STO is actived)

As of now, Einstein STO can be used in Email Sending, but not for SMS sending.

## Einstein Decision

Use AI inside a Flow to check each recipient’s email fatigue and engagement score, take the [right decision based on Eisntein Engagement Frequency and Einstein Scoring](https://the-agentic-marketer.com/marketing-cloud-next-deep-dives/agentforce-marketing-einstein-decision-engagement-frequency-scoring/).

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20437%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2024/04/Screenshot-2025-11-27-at-00.27.24-scaled.png) 

Einstein AI Engagement Frequency and Scoring

## Content Co-Creation

[**Edit 24/11/2025**, this feature is now an [Agentforce Employee Agent](https://the-agentic-marketer.com/marketing-cloud-next-deep-dives/agentforce-campaign-creation-content-builder-agents/)]

When creating an Email by adding Email type Content from the linked Enhanced Workspace, you are offered the possibility to draft your Pre-header, your message Body or your Subject Line with Einstein AI.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20437%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/011-Email-Co-Creation-when-creating-an-Email-Content-from-scratch.png) 

Email Co-Creation when creating an Email Content from scratch.

One can ask for a longer or shorter, adjust the style, whatever you can think of, can be achieved by a Prompt. If satisfied by the generated content, copy it and paste it in your Email.

When Creating an Email Send, using a Marketing Cloud Growth & Advanced Campaign (Single Email with Einstein), the entire creation process is handled by AI. You simply specify in a Prompt what you want to achieve, and a Campaign brief, containing an Audience along with an Email asset is automatically generated for you. Of course, you can refine the proposittion by further prompting.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20437%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/012-A-single-Prompt-to-generate-a-commplete-Email-and-an-Audience.png) 

A single Prompt to generate a complete Email and an Audience.

Clicking “Looks Good” once satisfied triggers the creation of all what’s need for you Email Campaign. As Einstein puts it:

> I’ve created campaign assets for you based on the campaign brief details. Next, review the segment and finalize the email subject, preheader, and body.

This is really impressive, especially if you consider that the generated Contents are actually safely grounded in your own data, thanks to the Trust Layer and Data Cloud.

As of now, SMS or Landing Page can not be created by Einstein Co-create.

To activate this feature (and I can’t see any reason you wouldn’t 😎), search for “Generative AI” in the Quick find of the overall Setup, and click Einstein Setup, and finally “Turn on Einstein”:

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20437%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/013-Activating-Generative-AI-for-Email-and-Campaign-Co-Creation.png) 

Activating Generative AI for Email and Campaign Co-Creation

Finally, don’t forget to Click Go To Einstein Data Collection and turn on Collect and Store Einstein Generative AI Audit Data, this is how your data will be used to train models, enhancing the Co-Creation process with knowledge on gained from your own data:

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20437%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/014-Allow-Data-Cloud-to-access-your-data-so-your-Prompts-get-contextual-answers.png) 

Allow Data Cloud to access your data so your Prompts get contextual answers

## AI Segment Builder

We’ve seen a Campaign can create a Segment, from a single Prompt, but you can also use Einstein to create Segment for a Single Prompt. Then use this Segment in Marketing Cloud Growth & Advanced or send it to another Cloud by activating it in a Data Action Target.

To activate this feature, simply search for Feature Manager in global setup and Enable Einstein Segment Creation:

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20437%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/015-Enabling-Segment-Co-Creation-from-setup.png) 

Enabling Segment Co-Creation from setup

Et voilà, when creating a new Segment in Data Cloud, you can now choose a standard creation by selecting your criteria or let Einstein do this for you (note that only Unified Profiles can be segmented this way, which is convenient since Marketing cloud Growth & Advanced only take this type of audience as an input):

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20437%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/016-Create-a-Segment-old-fashion-or-AI-based.png) 

Create a Segment old-fashion or AI based

Then, once accepted the warning related to AI generated content (which applies also to content Co-Creation), you access a prompt to build your Audience:

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20437%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/017-Suggested-segment-rules-out-of-a-single-Prompt.png) 

Suggested segment rules out of a single Prompt

The assisted Segment Co-Creation process proposes a set of Rules, which you can accept to actually create the Segment for use or refine to better suit you needs.

## Agentforce Sales Agents

With Marketing Cloud Next, you can activate:

- The [Inbound Lead Generation](https://the-agentic-marketer.com/marketing-cloud-next-deep-dives/agentforce-marketing-inbound-lead-generation/) Agent from a template to qualify your inbound Leads and scedule meetings from yor website via a chat.
- The [Lead Nurturing Agent (fka SDR Agent)](https://the-agentic-marketer.com/marketing-cloud-next-deep-dives/agentforce-marketing-lead-nurturing-agent/)to send a first outreach email and a sequence of nurturing contents and handle answers

Both Agent can take advantage of your company knowledge to ground and personalise their responses into knowledge files and descriptions (Value proposition and Key achievements).

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20437%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2024/04/Screenshot-2025-11-27-at-00.51.54-scaled.png) 

Sales Agents in Agentforce marketing

Exciting times ahead!
