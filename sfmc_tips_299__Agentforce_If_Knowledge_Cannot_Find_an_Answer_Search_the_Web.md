# SFMC Tips #299 : Agentforce: If Knowledge Cannot Find an Answer ⇒ Search the Web

**Source:** https://medium.com/@marketingcloudtips/agentforce-if-knowledge-cannot-find-an-answer-search-the-web-34b70e7a965e

---

# SFMC Tips #299 : Agentforce: If Knowledge Cannot Find an Answer ⇒ Search the Web

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--34b70e7a965e---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--34b70e7a965e---------------------------------------)

11 min read

·

May 22, 2026

--

Photo by [amir rostami](https://unsplash.com/@rosstmi?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

**In Agentforce Service Agent, there may be cases where you want the agent to search your company website as well when knowledge articles alone cannot answer the question**.

This article explains, in as simple a way as possible, how to configure that behavior.

## Creating the Service Agent

1. First, open the “**New Agentforce Builder**” and start creating a new agent.

2. Select “**Agentforce Service Agent**”.

3. Decide the agent name and begin the creation process.

4. To make the work easier, close the chat panel on the right side.

5. If necessary, change the “**System Settings**” and “**Language Settings**”.

6. Next, for the subagents, select “**Add from Asset Library**”.  
 (\**Topics have now been renamed to subagents.*)

7. Here, add “**General Web Search**”.

8. When changes are made to the configuration, a dot will appear in the menu. It is recommended to save frequently while working.

*For reference, the* ***Agent Router*** *plays a role similar to* ***a company receptionist****. It first receives the user’s statement and then routes the request to the appropriate agent (more precisely, subagent) depending on the content.*

*This time, because a new subagent was added, the available routing destinations increased, which means the contents of the Agent Router were also updated automatically.*

9. After clicking Agent Router, switch from “Canvas” to “**Script**”.

*The “Script” view is convenient because you can review all configuration contents together.*

10. The following is the configuration content.  
You can see that the Agent Router routes requests to the appropriate subagent according to the user’s statement.

```
start_agent agent_router:  
    label: "Agent Router"  
    description: "Welcome the user and determine the appropriate subagent based on user input"  
    model_config:  
        model: "model://sfdc_ai__DefaultEinsteinHyperClassifier"  
    reasoning:  
        instructions: ->  
            | Select the best tool to call based on conversation history and user's intent.  
        actions:  
            go_to_ServiceCustomerVerification: @utils.transition to @subagent.ServiceCustomerVerification  
                available when @variables.isVerified == False  
            go_to_CaseManagement: @utils.transition to @subagent.CaseManagement  
                available when @variables.isVerified == True  
            go_to_AccountManagement: @utils.transition to @subagent.AccountManagement  
                available when @variables.isVerified == True  
            go_to_ReservationManagement: @utils.transition to @subagent.ReservationManagement  
                available when @variables.isVerified == True  
            go_to_DeliveryIssues: @utils.transition to @subagent.DeliveryIssues  
                available when @variables.isVerified == True  
            go_to_OrderInquiries: @utils.transition to @subagent.OrderInquiries  
                available when @variables.isVerified == True  
            go_to_GeneralFAQ: @utils.transition to @subagent.GeneralFAQ  
            go_to_escalation: @utils.transition to @subagent.escalation  
            go_to_off_topic: @utils.transition to @subagent.off_topic  
            go_to_ambiguous_question: @utils.transition to @subagent.ambiguous_question  
            go_to_GeneralWebSearch: @utils.transition to @subagent.GeneralWebSearch
```

This time, by adding “General Web Search”, the following configuration was added.

```
go_to_GeneralWebSearch: @utils.transition to @subagent.GeneralWebSearch
```

This line is important. In other words, when General FAQ cannot provide an answer, it becomes possible to explicitly transition to GeneralWebSearch using this code.

*For reference,* `@variables.isVerified == True` *means “prior identity verification is required”. Since General FAQ and General Web Search do not have this condition attached, they can be executed even without identity verification.*

*In addition, the Salesforce proprietary model “****HyperClassifier****”, which can be confirmed in the model section and is used for subagent classification, is a model with excellent processing speed and classification accuracy. This model has been introduced since around April 2026.*

*For newly created agents like this example, the model is automatically applied. However, older agents created previously may still be using the legacy model. Therefore, if possible, replacing it with HyperClassifier is recommended.*

## Subagent: General FAQ

1. Next, open the “**General FAQ**” subagent in **Script view** as well.

2. The **“Instructions” inside the Reasoning block** were changed as follows.

```
| Your job is solely to help with issues and answer questions about the company, its products, procedures, or policies by searching knowledge articles.  
| ALWAYS call AnswerQuestionsWithKnowledge first before considering any other action.  
| Never provide generic information, advice, or troubleshooting steps unless retrieved from knowledge articles or web search results.  
| If the customer's question is too vague or general, ask for more details and clarification to give a better answer.  
| If AnswerQuestionsWithKnowledge returns no relevant results or cannot provide sufficient information, do not immediately ask for escalation.  
| Instead, transition to GeneralWebSearch.  
| Do not transition to GeneralWebSearch before attempting AnswerQuestionsWithKnowledge.  
| Only ask if they want to escalate to a live agent when the question cannot be answered by either knowledge articles or web search.  
| Include sources in your response when available from the knowledge articles or web search results, otherwise proceed without them.
```

With this, the following flow becomes much more stable:

- First, **Knowledge**
- If it cannot answer, **Web Search**
- Finally, **Escalation**

*\*Please note that this does not guarantee the flow will always behave exactly this way.*

3. Next, also modify the **“Actions” inside the Reasoning block**.  
 By default, it likely looks like the following.

```
actions:  
    AnswerQuestionsWithKnowledge: @actions.AnswerQuestionsWithKnowledge  
        with query = ...  
        with citationsUrl = ...  
        with ragFeatureConfigId = ...  
        with citationsEnabled = ...
```

4. Add the final line here.

```
actions:  
    AnswerQuestionsWithKnowledge: @actions.AnswerQuestionsWithKnowledge  
        with query = ...  
        with citationsUrl = ...  
        with ragFeatureConfigId = ...  
        with citationsEnabled = ...  
  
    go_to_GeneralWebSearch: @utils.transition to @subagent.GeneralWebSearch
```

The addition of this explicit transition instruction is the **key point** this time.

## Subagent: General Web Search

1. Next, open “**General Web Search**” in **Script view**.

2. Regarding the “Instructions” here, the default settings are generally sufficient. Adjust them if necessary.

If you scroll down a little further, the **“Actions” inside the Reasoning block** will be displayed.

```
actions:  
    WebSearch: @actions.WebSearch  
        with searchQuery=...  
        with searchProvider=...  
        with siteFilter=...
```

For `searchQuery`, search keywords are automatically extracted from the text entered by the user.

Regarding `searchProvider`, as of May 2026 when this article was written, the following three search providers are available.

- BrightData
- OpenAI
- You.com

For `siteFilter`, you can specify up to 10 target site domains separated by commas. By specifying your company’s domain here, it can effectively function as a “company site search”.

For example, change it as follows.

```
actions:  
    WebSearch: @actions.WebSearch  
        with searchQuery = ...  
        with searchProvider = "openai"  
        with siteFilter = "nac-plus.co.jp"
```

## Creating a Data Library for Knowledge

1. Next, from the menu, select “Data” → “**Data Library**”, and switch the display back from “Script” to “**Canvas**”.

If a knowledge data library does not yet exist, click the “**Agentforce Data Library**” **link** as shown below.

2. After navigating, create a new data library.

3. Enter a name (example: `Knowledge Data Library`) and save it.

4. Select “**Knowledge**” as the data type.

5. Next, select two “**Identifying Fields**”.

There are no strict rules for this selection, but in this example, **Title** and **Summary** are selected.

6. Next, select the “**Content Fields**”.

There are also no fixed rules here, but this time **Question** and **Details** were selected as the fields corresponding to questions and answers.

When you save the configuration, the generation process will automatically begin.

7. After about 15 minutes, it should become “**Ready**”, and then it will be available for use.

8. Return to the Agentforce Builder screen and click the refresh button. The created data library will then become selectable.

9. Select it and save.

10. At this point, prepare at least one knowledge article for later testing.

The following type of content is sufficient.

- **Title**  
  Custom Preference Center cannot update CRM Email Opt Out field
- **Summary**  
  Explains the limitation of the MCA Custom Preference Center regarding the standard CRM Email Opt Out field.
- **Question**  
  Can the MCA Custom Preference Center update the standard CRM Email Opt Out field?
- **Detail (Answer)**  
  The MCA Custom Preference Center is designed to manage consent for Data 360 (Marketing Cloud Next).  
  If you are referring to the standard CRM Email Opt Out field as “CRM consent”, the value of that field cannot currently be processed or updated by the Custom Preference Center.  
  If synchronization with CRM consent fields is required, consider implementing a custom solution using a custom form, Flow, or other automation approach.

## Prompt Template Adjustment

1. Next, adjust the prompt template “**Answer Questions with Knowledge**” to match the data library.

Open this from **Prompt Builder**.

*To edit Prompt Builder, the “****Prompt Template Manager****” permission set is required. Assign it to the target user if necessary.*

2. This time, the prompt body itself will not be changed.

However, remove the Retriever configured by default and replace it with the Retriever for the data library created this time.

First, give it a name and save it to **create a new version**.

3. Once Version 1 is created, it becomes editable. Delete the existing Retriever and click “**Insert Resource**”.

4. Select “**Retriever**”.

5. Next, configure the Retriever.

6. The Retriever beginning with `KA_` is the Retriever derived from the data library, so select that one.

7. If you scroll slightly downward, there is a “**Search Parameters**” section.

When you click “**Search Text**”, fields that can be used as input will appear, so select Query.

8. After confirming that `Input:Query` is displayed, insert it into the screen.

9. Once the Retriever insertion is complete, save and activate the configuration.

## Knowledge Access Permissions

Finally, the current Service Agent user does not have access permission to Knowledge. Therefore, create a permission set for knowledge access and assign it to the user.

In Agentforce, one user is assigned to each agent. In other words, even though it is Agentforce, internally it operates as a “user”.

This user is actually created automatically at the time the agent is first created. It is the following screen.

Therefore, the permission set will be assigned to the user created here.

1. First, begin creating a permission set.  
Example: `Knowledge Access (Custom)`

2. Open “**Object Settings**”.

3. Select “**Knowledge**”.  
*Choose Kav (Knowledge Article Version).*

4. Check the following permissions and save.

- **View All Records**
- **View All Fields**

5. Next, return to the top of the permission set and click “**App Permissions**”.

6. Check “**Allow View Knowledge**” and save.

7. Furthermore, return again to the top of the permission set and click “**Data Cloud Data Space Management**”.

8. Click “Edit”.

9. Check the data spaces you will use and save.

At this point, the following three settings are completed.

- **Object Settings**
- **Application Permissions**
- **Data Space Permissions**

10. After completing the settings up to this point, click “**Manage Assignments**”.

11. If you search using the string “Einstein”, the user created earlier will appear, so assign the permission set to that user.

## Operation Check

1. Now that all settings are complete, finally perform an operation check.  
 Click “**Preview**” at the top of the screen.

2. First, try asking a question using the knowledge article created earlier.

Question:  
`Can the MCA Custom Preference Center update the standard CRM Email Opt Out field?`

3. Then, a response was returned using only the knowledge article.

4. Next, check Web Search.

This time, in each of your environments, you have probably configured some site domain in `siteFilter`, so try asking about content that exists within that site. This content has not been registered in knowledge.

Question:  
`Please tell me about your Salesforce implementation and operational support services.`

5. Then, it first searched the knowledge articles, and because no answer was found, it automatically proceeded to search the specified website afterward. Success!!

How was it?

Flows like the following are extremely important in actual service agents:

- First check Knowledge
- If it cannot answer, perform Web Search
- Finally, perform Escalation if necessary

In the traditional Agentforce Builder, there were situations where finely adjusting this type of control was difficult. However, with the new script-based Agentforce Builder, it has become possible to control behavior much more flexibly.

Also, the key point is not simply adding Web Search, but controlling:

“in what order decisions should be made”

through the combination of Reasoning and Actions.

At first it may feel slightly difficult, but once you actually run it, it becomes much easier to understand, so please give it a try.

That is all for this time.

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
