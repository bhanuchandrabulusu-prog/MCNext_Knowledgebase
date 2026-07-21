# SFMC Tips #221 : Agentforce: How to Implement a Service Agent Using Knowledge

**Source:** https://medium.com/@marketingcloudtips/sfmc-tips-221-agentforce-how-to-implement-a-service-agent-using-knowledge-ef7a9e0cdc6b

---

# SFMC Tips #221 : Agentforce: How to Implement a Service Agent Using Knowledge

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--ef7a9e0cdc6b---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--ef7a9e0cdc6b---------------------------------------)

11 min read

·

Dec 25, 2025

--

Photo by [Priscilla Du Preez 🇨🇦](https://unsplash.com/@priscilladupreez?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

Salesforce partners implementing Marketing Cloud Next have likely noticed a growing trend: projects where Marketing Cloud Next and Agentforce Service Agent are being deployed together. We’re no longer working only within the marketing space — we now need to build knowledge across the wider Salesforce ecosystem.

Instead of staying confined to the marketing domain, let’s start learning the platform more broadly, step by step, so we don’t get left behind.

In this article, I will introduce how to implement a service agent that answers frequently asked questions (FAQ) by leveraging **Salesforce’s standard feature “Knowledge”** using an **Agentforce service agent**.

As this is a beginner-friendly introduction to Agentforce, I’ll start with a simple implementation using the **Agentforce Data Library** (ADL).

## Benefits of Using the Data Library

By using the Agentforce Data Library with Knowledge, you can build an agent that uses **RAG (Retrieval-Augmented Generation)** in just a few minutes.

For an explanation of RAG in Salesforce, please check the Matthew Wash-san’s article below.

[## Data Cloud's RAG explained ... and optimized

### Update: October 24, 2025: Data 360 (FKA Data Cloud) just announced a new feature that helps significantly with…

www.linkedin.com](https://www.linkedin.com/pulse/data-clouds-rag-explained-optimized-matthew-wash-7eqwc/?source=post_page-----ef7a9e0cdc6b---------------------------------------)

## Data Available in the Data Library

- Salesforce Knowledge articles
- PDF (up to 100 MB)
- HTML (up to 4 MB)

When you create a Data Library, the following components are automatically generated inside Data Cloud:

- Data Stream
- Data Lake Object
- Data Model Object
- Object mappings
- Search Index
- Retriever

In other words, just creating a Data Library automatically generates everything up to the retriever, enabling an extremely fast setup.

A **Search Index** vectorizes (assigns vector addresses to) text data such as Knowledge articles and stores it so it can be searched at high speed based on semantic similarity. This makes it possible to understand not just keyword matches but also semantic context and retrieve related information. In the RAG structure, this functions as the “database to search from”.

A **Retriever** identifies the most semantically similar records from the search index based on the user’s input (such as a question) and passes them to the LLM as information by inserting them into the prompt. In the RAG structure, it serves as the “component responsible for retrieving relevant data”.

For example, if a user asks, **“What is your return policy?”**, the retriever searches for records in the Knowledge articles containing semantically related concepts such as “return”, “refund”, and “order cancellation”. Because the search index is vectorized to enable semantic search, it finds contextually related results, not just keyword matches.

The retriever embeds the extracted related record content into the prompt and passes it to the LLM. This enables the AI to generate natural and contextually relevant responses based on the best matching information related to “return policy”.

## Disadvantages of the Data Library

On the other hand, when a search index is created using the Data Library, **hybrid search (vector search + keyword search)** is automatically used.

Due to this, compared to pure vector search:

1. **Costs may be higher (\*1.5 to 2 times)**
2. **Response time may be longer**

According to Salesforce, you can assume it may take **about twice as long**.

## When Hybrid Search is Effective

- Cases where product names, brand names, technical terminology, or industry terms affect search accuracy
- Cases where answers must include specific terms or model numbers

Therefore, if your Knowledge articles only contain everyday questions with no specialized terminology, setting up **manual configuration using vector search only** (without Data Library) may be more appropriate. Consider this when designing the system.

## Preparing Knowledge Articles

This article will not cover Knowledge article preparation. Please refer to Trailhead below to prepare your data.

[## Set Up Salesforce Knowledge

### Learn how to create, customize, and manage a Salesforce Knowledge base effectively for better case resolution and…

trailhead.salesforce.com](https://trailhead.salesforce.com/content/learn/projects/set-up-salesforce-knowledge?source=post_page-----ef7a9e0cdc6b---------------------------------------)

[## Ingest Knowledge Article Data for Salesforce CRM

### Discover how to utilize and ingest Knowledge article data from Salesforce CRM. Enhance your data handling skills with…

trailhead.salesforce.com](https://trailhead.salesforce.com/content/learn/projects/unstructured-data-in-data-cloud/ingest-knowledge-article-data?source=post_page-----ef7a9e0cdc6b---------------------------------------)

In the SDO environment (Simple Demo Org for partners) I am using, the following four long text fields existed on the **Knowledge object**, so I am using them as-is:

- Title
- Summary
- Question
- Detail (or Answer)

If these do not exist in your org, create custom fields for the sections corresponding to **Question** or **Detail**, and map them to the **Knowledge Article Version Data Model Object**.

\*Be careful not to select too many fields that contain the same information, as this can bias the search results.

> *This can also be tested in a publicly available* [***Developer Edition*** *org*](https://developer.salesforce.com/blogs/2025/06/new-developer-edition-signup)*.*

You can start using it once the status changes to **Ready**.

**Knowledge sample**

### Title

Changing vehicles on the day

### Summary

If there is availability, you can change vehicles on the day.

### Question

Can I change vehicles on the day?

### Detail (or Answer)

If you would like to change vehicles, please let a store staff member know. We will reserve a vehicle that is available on your desired schedule on the day.

## Creating the Service Agent

**Prerequisite:** Data Cloud must be enabled before starting.

## Preparation: Enable Einstein and Agentforce

1. Enable Einstein in “Einstein Setup”.

2. Press F5 to refresh the page, search for “Agentforce Agent,” enable Agentforce, and click **New Agent**.

3. Select **Service Agent** and click **Next**.

4. In Topic Selection, leave only “**General FAQ**” enabled and disable the rest, then click **Next**.

5. For testing, enter any text in the **Company** section. Enable **Logging** and click **Next**.

## Creating the Data Library

1. Create a new Data Library. If Data Cloud isn’t enabled, you cannot proceed.

2. Enter the Data Library name and select **Knowledge**. In this example, the name is **Knowledge Data Library**.

3. In the Field Settings tab, set **Title** and **Summary** as **Identifier Fields**.

4. In **Content Fields**, select **Question** and **Detail**. These must be **long text fields**. Only select what is necessary based on your Knowledge structure.

5. In the **Knowledge Settings** tab, filter for **Published** articles only. Add category filters if needed. Click **Create**.  
It may spin/loading for a while.

> *If a system error occurs and the status does not change from* ***Not Started*** *to* ***In Progress*** *or* ***Ready****, delete the Data Library and recreate it.*

## Confirming Data Generation

1. Once created, the following components are automatically generated (may take several minutes):

- Data Stream
- Data Lake Object and Data Model Object
- Object mappings
- Search Index
- Retriever

2. Check the Search Index. It may show no records initially; wait 5–15 minutes.

3. Once indexing is done, data will appear. At the time of writing, CRM Knowledge data syncs approximately every 15 minutes.

## Embedding the Retriever in Prompt Builder

1. Open **Prompt Builder** and select **Answer Questions with Knowledge**.

> *If prompt templates do not appear, confirm that you have the* ***Prompt Builder Manager*** *permission set.*

2. Save as a new version.

3. Remove the existing retriever in the KNOWLEDGE section and click **Add Resource**.

4. Select **Search** (or “Einstein Search” in Japanese orgs).

5. Select **Knowledge Article Version**.

6. Select the retriever created by the Data Library. Retriever names starting with **KA\_** are the Data Library versions.

7. Click the embedded retriever and open the “**Search Parameters**” section.

8. Select **Free Text** from the search box.

9. Select **Query**.

10. Ensure **Input:Query** is inserted and click **Save & Preview**.

11. Enter a question such as **“**Can I change vehicles on the day?**”** in Japanese and confirm an answer is returned.

> *Use any placeholder for Retriever ID (e.g., “a”).*

12. Activate the prompt template.

## Creating and Assigning Permission Sets

1. Go back to the agent and enter the same question:  
 **“Can I change vehicles on the day?”**  
 Set the agent’s display language if needed.

At this stage, the agent will not respond.

![]()

This is due to missing user permissions.

![]()

2. Create a new permission set. Go to Permission Sets → **New**.

3. Name the permission set.   
(Example: **Knowledge Service Agent (Custom)**)

4. Click **Manage Assignments**.

5. Assign the **EinsteinServiceAgent User**, the automatically generated user created when the service agent was built.

6. In the permission set, go to **Object Settings**.

7. Select **Knowledge (API name: Knowledge\_\_kav)**.

8. Enable **Read**, **View All**, and **View All Fields**. Save.

9. Go back to the permission set and open **App Permissions**.

10. Enable **View Knowledge** and save.

11. From the permission set home, open **Data Cloud Data Space Management**.

12. Click **Edit**.

13. Check the Data Spaces you will use and save.

## Testing

1. Return to the agent preview and ask the same question.

2. The service agent now provides the expected answer. Success!

This completes the setup of a service agent that leverages Knowledge.

## Troubleshooting Tips

When using a **Data Library** like this time, if no response is returned in the Prompt Builder preview, please check the following.

**If the Knowledge is in “Draft” status, publish it.**

> *This is because the generated retriever code contains the following condition:* `KnowledgePublicationStatus__c = 'Online'`

**The difference between**

- Publication Status (`KnowledgePublicationStatus__c`)
- Visible In Public Knowledge Base (`IsVisibleInPublicKnowledgeBase__c`)

**① What is** `KnowledgePublicationStatus__c = 'Online'`**?**

This is the condition for the **published (Publish) status**.

- **Online**: That language version is published (viewable)
- **Draft / Archived**, etc.: Unpublished or archived, and basically excluded from reference

👉 In other words, this is a filter to limit results to **only articles that are actually published**. Draft or archived articles are excluded. In Data Libraries, this is the default setting.

**② What is** `IsVisibleInPublicKnowledgeBase__c = 'true'`**?**

This is the condition for whether the article can be shown in the **Public Knowledge Base**.

- **true**: OK to expose externally (Public KB / Experience Cloud / Web)
- **false**: Internal use only (visible in the console but not exposed externally), etc.

👉 In other words, this is a filter to limit results to **only articles that are allowed to be shown externally**. This can be configured in the following location in the Data Library. When enabled via the toggle, `IsVisibleInPublicKnowledgeBase__c = 'true'` is added.

On the other hand, if a response is returned in the Prompt Builder preview, but an error occurs when testing in the agent-side preview, try the following.

- Remove the currently configured Data Library once, save, then add the same one again and save.

Or,

- Align the agent’s **Default Language** with the language specified in the **Language** field of the Knowledge Article Version DMO.

In the following case, since it is `en_US`, select **English**.

> *This is because the generated retriever code contains the following condition:* `Language__c='{!$_LANGUAGE}'`

Based on my experience, these actions should resolve the issue.  
Please use this as a reference.

## Conclusion

This time, I created a simple service agent that leverages Knowledge. These steps can also be performed in a [free Developer Edition environment](https://www.salesforce.com/form/developer-signup/), so please give it a try.

I’ve also covered how to embed the service agent you created into an external website in the article below.

[## SFMC Tips #193 : Agentforce: Deploying Service Agents on CloudPages (External Sites)

### In this article, I’ll explore how to embed the Agentforce Service Agent on an external website using CloudPages in…

medium.com](/@marketingcloudtips/agentforce-deploying-service-agents-on-cloudpages-external-sites-d4fb5edacb91?source=post_page-----ef7a9e0cdc6b---------------------------------------)

[## SFMC Tips #222 : Agentforce: Deploying Service Agents to Your Website

### Previously, I wrote an article about how to install Agentforce on an external site (CloudPages in Marketing Cloud…

medium.com](/@marketingcloudtips/sfmc-tips-222-agentforce-deploying-service-agents-to-your-website-8b5f38c6b0b9?source=post_page-----ef7a9e0cdc6b---------------------------------------)

In my case, I’m using CloudPages from Marketing Cloud Engagement, so if you have a similar environment available, you can try it out right away.

That’s all for now.

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
