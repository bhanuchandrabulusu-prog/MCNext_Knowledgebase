# Agentforce Marketing: Audience Flows unify Data Cloud and CRM Audiences

**Source:** https://the-agentic-marketer.com/marketing-cloud-next-tips-from-the-trenches/agentforce-marketing-audience-flows-unify-data-cloud-and-crm-audiences

---

In Summer ’26, the Campaign creation experience and available Flow types in Agentforce Marketing were significantly revamped. Segment Triggered Flows are now part of a broader orchestration model called Audience Flows.

**Audience Flows unify multiple audience entry models, including both Data Cloud audiences and CRM-based audiences, under a single orchestration framework.**

**Note**: this article is based on current Summer ’26 release notes and Sandbox Preview environments. Features may still evolve before GA.

[![](https://the-agentic-marketer.com/wp-content/uploads/2026/05/Screenshot-2026-05-16-at-14.20.24-1024x528.png)](https://the-agentic-marketer.com/wp-content/uploads/2026/05/Screenshot-2026-05-16-at-14.20.24-scaled.png) 

Audience Flows now unify Data Cloud and CRM-based audience orchestration in Agentforce Marketing.

## A new Campaign experience

### Segment, List or Event

When creating an Agentforce Marketing Campaign, users are now presented with streamlined audience orchestration choices directly from the Campaign interface: Segment, List, or Event.

Segment refers to the existing Segment Triggered Flow model based on Data Cloud audiences. List introduces a new CRM record-based orchestration model, while Event supports Automation Event Triggered Flows based on interactions such as email link clicks or Form submissions.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20413%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2026/05/Screenshot-2026-05-16-at-17.54.35-scaled.png) 

Campaign creation now centralizes multiple audience orchestration models

### Previous Flow templates moved

Previously available Flow templates can now be found in the **Quick Start** tab, while **Build Your Own** is selected by default. The Signup Form experience has also been redesigned as a guided wizard.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20413%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2026/05/Screenshot-2026-05-16-at-18.07.14-scaled.png) 

The new Campaign experience separates guided templates from custom orchestration setup

### Creating an Audience Flow from a Campaign

If you select either Segment or List from the Build Your Own tab, an Audience Flow is created, so you can select the entry population, define when the Flow executes and open it directly in Flow Builder

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20413%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2026/05/Screenshot-2026-05-16-at-18.32.57-scaled.png) 

A new Audience Flow (Segment or List type)

Audience Flows can also be created directly from the Flow list and related to a Campaign (by simply setting the Associated Record field). We’ll present this method below.

## Audience Flows: Two Audience Models, One Flow Framework

From the Flow list, click New. Search for Audience and select the Audience Flow type. Select the Data Space and a Data Graph (if you plan to use a Segment of Unified Individuals and want another Data Graph as the default one). Next.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20413%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2026/05/Screenshot-2026-05-16-at-18.43.32-scaled.png) 

The new Audience Flow is now a set of 4 Flow types.

Before we describe each of these Flow types, let’s state that Segment is for Data Cloud audiences and the other three types are new and are used with CRM records.

All four Audience Flow types share the same scheduling and execution framework.

### Unified Starting options

Audience Flows are **time triggered**, and when they run, the eligible records in the selected population type (Segment, Record, List or Campaign) join the Flow interview.

Audience Flows can be **one shot** flows, in that case you define when the Flow should be triggered: immediately upon activation or scheduled to a future time.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20413%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2026/05/Screenshot-2026-05-16-at-18.58.39-scaled.png) 

One-time Audience Flow

They can also be declared as **Recurring**. The **frequency** can be set from 1 hour to 1 year and week-end days can be excluded.  How record **re-entry** should be handled is governed by the Can Rejoin Flow? parameter (Always, After Completion, Never). If needed, these settings are detailed in [Start Option Decoded article](https://the-agentic-marketer.com/marketing-cloud-next-tips-from-the-trenches/recurring-segment-triggered-flows-start-options/) (originally written for Segment Triggered Flows).

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20413%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2026/05/Screenshot-2026-05-16-at-19.08.45-scaled.png)

Audience Flow is a unified experience (Start options and Flow design). It can take 4 types of populations (corresponding to the Flow types), and they can be composed of records from either Data Cloud or CRM.

### Audience Flows with a Data Cloud Records source

When you select Segment for the Audience Source, you can define which Data Cloud’s Segment records will be injected.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20413%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2026/05/Screenshot-2026-05-16-at-19.30.26-scaled.png) 

Audience Flow using a Data Cloud Segment

Segments of Individuals can be used here (you need an [Activation Template](https://the-agentic-marketer.com/marketing-cloud-next-deep-dives/prioritize-contact-points-activation-templates/) to send messages in that case), but using Unified Individuals is what makes this Audience type really powerful. You then benefit from the Identity Resolution for population cleaning along with cross-channel behavior, and Data Graph for personalisation. **You use this when audience intelligence lives in Data Cloud.**

### Audience Flows with a CRM Records source

The other 3 options are based on CRM records populations. You use these for CRM-native simplicity, operational orchestration, Salesforce object-centric activation or if you see no need for Data Cloud. **Use them when the operational truth already lives in CRM.**

#### Record Query Flow

When you select the Record option, you actually define a new **Record Query Flow**. You then need to select the triggering object: either a Salesforce person object (Prospect, Lead, Contact, Person Account) or any Salesforce object with a relationship (lookup) to one or more person object (like Task or Case). You then define which criteria (field based) a record of the triggering Object need to match.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20413%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2026/05/Screenshot-2026-05-16-at-19.52.16-scaled.png) 

Record Query Flow, Object and Field criteria

#### List Flow

Summer ’26 also introduces **Actionable Lists**. Leads or Contacts can be added to these static Lists, either by importing a CSV file (ex. Tradeshow attendees), or from a Flow (new Add to Actionable List Flow action). Unlike Record Query Flows, the audience is pre-defined rather than dynamically computed from object criteria, and you just need to select an Actionable List to define a **List Flow**.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20413%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2026/05/Screenshot-2026-05-16-at-20.12.10-scaled.png) 

List Flow, a group of static Lead or Contact records

#### Campaign Flow

With a **Campaign Flow**, you select which Campaign Members (Leads and Contacts, Prospects cannot be Campaign Members) will be injected in the Flow, by simply choosing a Campaign

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20413%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2026/05/Screenshot-2026-05-16-at-20.56.49-scaled.png) 

Campaign List Flow injecting Campaign Member

Note: in the previous Campaign experience, prior to Summer ’26, there is an option to select Campaign Members. This options is still available (Select Segment) along with Quick Filters. However, these two options are creating a Segment of Unified Individuals, and hence cannot be used in the Audience Flow of Campaign Flow type.

## Key Takeaways

With **Audience Flows**, Salesforce is standardizing orchestration around a common execution framework. Start options, scheduling logic and Flow design are now unified, while only the source of injected records differs between Data Cloud audiences and CRM records.

Audience Flow is no longer defined by where the audience originates, but by how Salesforce orchestrates it.

However, if sending messages, Data Graph personalization can only be used in Segment Flows using Segments of Unified Individuals. For the other Flow types (or when using Segments of Individuals), you can instead use Apex Personalization or the no-code Content Variables introduced in Summer ’26. In that case, the Content Variable is defined in the Email Builder and its value is injected directly from the Flow through the Send Email Settings.

What makes this evolution particularly interesting is that Salesforce now gives marketers a real architectural choice between Data Cloud audiences and CRM-native audiences, while keeping the same orchestration experience.

**Data Cloud audiences are especially powerful when**:

- Identity Resolution matters
- audiences combine multiple data sources
- cross-channel behavior is important
- audience intelligence lives in Data Cloud

**CRM audiences remain highly relevant when**:

- the operational truth already lives in CRM
- simplicity matters
- the use case is object-centric
- orchestration is tightly coupled to Salesforce operational processes

Data Cloud audiences are about audience intelligence. CRM audiences are about operational truth.

The important shift is that marketers no longer need to adopt a single audience model for every use case. Both approaches can now coexist under the same Audience Flow framework depending on the business need.

This feels like another step toward Flow becoming the universal orchestration layer of Agentforce Marketing.
