# SFMC Tips #318 : Agentforce: Easily Switch LLM Models for Each Subagent with Model Override

**Source:** https://medium.com/@marketingcloudtips/agentforce-easily-switch-llm-models-for-each-subagent-with-model-override-fc83493ee86b

---

# SFMC Tips #318 : Agentforce: Easily Switch LLM Models for Each Subagent with Model Override

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--fc83493ee86b---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--fc83493ee86b---------------------------------------)

6 min read

·

Jul 5, 2026

--

Photo by [Zoltan Tasi](https://unsplash.com/@zoltantasi?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

Agentforce Builder continues to evolve. In the May 2026 release, it became possible to specify a different LLM model for each subagent by using Agent Script.

At that time, however, you had to specify the model API name directly in the Agent Script. As a result, every time you wanted to change the model, you had to look up the available model API name and edit the script, making it difficult to quickly compare and evaluate different models.

For example, you specified the model directly in `model_config` as shown below.

Example: `model://sfdc_ai__DefaultBedrockAnthropicClaude46Sonnet`

```
subagent GeneralWebSearch:  
    label: "General Web Search"  
    description: "Searches public information and provides concise answers, including Google Maps search URLs or driving route URLs when appropriate."  
    model_config:  
        model: "model://sfdc_ai__DefaultBedrockAnthropicClaude46Sonnet"  
    reasoning:  
        instructions: ->
```

This has now been improved. In the June 2026 feature release, this configuration became even easier to use.

You can now change the model directly from the Agentforce Builder canvas using the GUI. This allows you to switch LLMs based on your use case without directly editing the YAML.

## How to Configure Model Override

The configuration process is very simple.

1. Select a subagent and click the **+** button that appears.

2. Click **Model Override**.

3. Select the model you want to use from the drop-down menu in the upper-right corner.

> ***Note:*** *Some models may not appear in the list. If that happens, switch to Script Mode and enter the* [*API Name*](https://developer.salesforce.com/docs/ai/agentforce/guide/supported-models.html) *directly.*

## Available Models (As of July 2026)

Agentforce supports a wide range of generative AI models from OpenAI, Anthropic, Google, Amazon, NVIDIA, and others.

For the latest list of supported models, see the following official documentation.

**Available Models:** [Supported Models for Agentforce](https://developer.salesforce.com/docs/ai/agentforce/guide/supported-models.html)

## OpenAI

- **GPT-5:** High-performance model in the GPT series. Suitable for a wide range of business tasks and advanced agents.
- **GPT-5 Mini:** Lightweight version of GPT-5. Designed for general-purpose use requiring fast responses.
- **GPT-5.1:** Improved version of GPT-5 with higher quality and stability.
- **GPT-5.2:** Successor to GPT-5.1. Suitable for advanced reasoning and complex tasks.
- **GPT-5.4:** High-performance model with a good balance of quality and usability.
- **GPT-5.4 Mini (Beta):** Lightweight version of GPT-5.4 for simple tasks such as FAQs and summarization.
- **GPT-5.5 (Beta):** OpenAI’s highest-performance class model. Ideal for advanced reasoning and long-form generation.
- **GPT-4.1:** Well-balanced model with stable performance. Suitable for Agentforce, Web Search, and many other use cases.
- **GPT-4.1 Mini:** Lightweight version of GPT-4.1. Suitable for Router Agents and FAQs.
- **GPT-4 Omni (GPT-4o):** General-purpose multimodal model. Also used as a standard Agentforce model.
- **GPT-4 Omni Mini (GPT-4o Mini):** Lightweight version of GPT-4o. Suitable for lightweight chat and FAQ scenarios.
- **O3:** Reasoning-focused model. Excels at analysis and complex decision-making.
- **O4 Mini:** Lightweight reasoning model with a good balance between reasoning capability and response speed.
- **OpenAI Ada 002:** Embedding model used for search and RAG.
- **Azure OpenAI Ada 002:** Azure version of the embedding model, available through the Models API.

## Anthropic Claude

- **Claude Haiku 4.5:** Lightweight Claude model for FAQs, classification, and routing.
- **Claude Sonnet 4.5:** Balanced model suitable for general business tasks and Agentforce use cases.
- **Claude Sonnet 4.6:** Latest Sonnet model with a good balance of performance and quality.
- **Claude Opus 4.5:** High-performance model for advanced reasoning and long-form generation.
- **Claude Opus 4.6:** Improved version of the Opus series.
- **Claude Opus 4.7:** Further enhanced high-performance model.
- **Claude Opus 4.8:** Anthropic’s highest-performance class model for complex tasks and advanced reasoning.

## Google Gemini

- **Gemini 2.5 Flash:** Fast-response model optimized for chat and search.
- **Gemini 2.5 Flash Lite:** Lightweight version of Gemini 2.5 Flash for low-overhead use cases.
- **Gemini 2.5 Pro:** High-performance model in the Gemini 2.5 series.
- **Gemini 3 Flash:** High-speed model in the Gemini 3 generation.
- **Gemini 3 Pro (Beta):** High-performance Gemini 3 model. *Scheduled for retirement.*
- **Gemini 3.1 Flash Lite:** Ultra-lightweight model in the Gemini 3.1 series.
- **Gemini 3.1 Pro (Beta):** High-performance model in the Gemini 3.1 series.
- **Gemini 3.5 Flash:** Google’s latest high-speed model for chat, search, summarization, and many other use cases.

## Amazon Nova

- **Amazon Nova Lite:** Lightweight model provided through Amazon Bedrock. Suitable for FAQs and simple agents.
- **Amazon Nova Pro:** Higher-end model in the Nova series for general business tasks and text generation.

## NVIDIA Nemotron

- **Nemotron 3 Nano 30B (Beta):** Lightweight reasoning model for classification, summarization, and lightweight agents.
- **Nemotron 3 Super 120B (Beta):** High-performance reasoning model for analysis and research.

## Responses Can Vary Significantly Depending on the Model

You might think, “Is there really much difference between the models?”

In reality, there are greater differences than you might expect in response content, writing style, and the way suggestions are presented.

For example, ask a service agent the following question:

**“**Please recommend sightseeing spots in Kyoto for a first-time visitor.**”**

### ⭐ GPT-5.4

![]()

### ⭐ Claude Sonnet 4.6

![]()

### ⭐ Gemini 3.5 Flash

![]()

When you compare the results, it is clear that the responses are almost as if they were written by different people.

Even though the same question is asked, the recommended locations, level of detail, writing style, and overall tone differ depending on the model.

Ultimately, the choice may come down to personal preference, but it is very important to compare and evaluate which model is best suited for your service agent.

With this update, you can now perform those comparisons directly in Agentforce Builder, which is a significant advantage.

> ***Note:*** *Response quality, strengths, cost, and response speed (latency) vary by model. Even with the same prompt, generated results and action execution behavior may differ. Before deploying to production, thoroughly compare and evaluate models based on your own use case.*

If you use Beta models, Salesforce recommends evaluating them in a Sandbox or development environment before deploying them to production.

## Which Model Is Used by Default?

You may be wondering, “Which model is used if I don’t configure Model Override?”

You can check the default model under **Setup > Einstein Audit, Analytics, and Monitoring Setup**.

One of the following providers should be selected:

- Salesforce Default
- AWS Hosted
- Gemini (available starting in June 2026)

As of July 2026, selecting **Gemini** uses **Gemini 3.5 Flash**.

For **AWS Hosted**, **Claude Haiku 4.5 on Amazon Bedrock** is currently used.

On the other hand, **Salesforce Default** is the default configuration that combines multiple trusted models managed by Salesforce. It currently includes GPT-4o among its model portfolio, but because Salesforce optimizes and manages this configuration, the underlying models may change in the future.

For the latest Agentforce models, refer to **here**.

## Conclusion

Until now, when release notes announced that “new LLM models have been added”, many people probably wondered, “Where would I actually use them?”

With this update, the answer finally seems much clearer.

The addition of **Model Override** makes it easy to switch to the most appropriate model for each subagent, making model selection, comparison, and evaluation much easier than before.

New LLM models will likely continue to be added in the future. The ability to switch models directly within Agentforce Builder without editing Agent Script is a major improvement that significantly increases the efficiency of agent development.

Whenever a new model is released, be sure to test it with your own use cases and compare its characteristics and behavior. Doing so will help improve the quality of your agents.

That’s all for this time.

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
