# SFMC Tips #231 : Agentforce: Automatically Generating Summaries with a Record-Triggered Flow

**Source:** https://medium.com/@marketingcloudtips/sfmc-tips-231-agentforce-automatically-generating-summaries-with-a-record-triggered-flow-7b30a8b15635

---

# SFMC Tips #231 : Agentforce: Automatically Generating Summaries with a Record-Triggered Flow

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--7b30a8b15635---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--7b30a8b15635---------------------------------------)

5 min read

·

Jan 8, 2026

--

Photo by [Patrick Fore](https://unsplash.com/@patrickian4?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

For example, in Knowledge records referenced as FAQs by Agentforce service agents, there may be cases where the “Title”, “Question”, and “Answer” are filled in, but the “Summary” (overview/description) field remains empty.

If you feel that creating this summary manually every time is time-consuming, it is possible to automatically generate it using generative AI.

In this article, I explain the steps to automatically create Knowledge summaries using generative AI in Agentforce.

This approach is not limited to Knowledge and can also be applied to other objects. For example, it can be used to automatically generate an overview for Accounts or a summary of the current status of Opportunities.

## Prerequisites

1. Confirm that the user who will run the process has the **Prompt Template Manager** permission set.

2. Confirm that the user who will run the process is a **Knowledge User**.

## Creating a Record Summary Template

### 1. Create a Prompt Template

In Setup, search for **Prompt Builder** and create a new prompt template.

Select **Record Summary** as the template type.

Enter the following information:

- **Prompt Template Type**: Record Summary
- **Prompt Template Name**: Knowledge Summary
- **API Reference Name**: Knowledge\_Summary
- **Template Description**: One-sentence summary integrating title, question, and answer for an article.
- **Object Type**: Knowledge (Knowledge\_\_kav)

### 2. Configure the Prompt Template Draft

Next, enter the template draft. The following is an example; feel free to modify it according to your use case.

Please integrate the following three pieces of information and summarize this knowledge article.

- Title  
   Insert the “Title” here
- Question  
   Insert the “Question” here
- Answer  
   Insert the “Answer” here

The summary will be used as a summary field and should accurately capture the key points of the knowledge article.  
Avoid subjective or conversational expressions, and write in a professional and objective tone so that a third party can clearly understand the content.

Please strictly follow the constraints below:

- Within 80 characters
- Summarize concisely in a single sentence
- Do not include https:// links

### 3. Insert Resources

Delete placeholders such as “Insert ‘Title’ here” in the template and click **Insert Resource**.

Select **Knowledge**.

Select **Title**.

Using the same procedure, insert resources for **Question** and **Answer** as well.

After completing the settings, save and activate the template.

## Creating a Record-Triggered Flow

### 1. Create a New Flow

In Setup, search for **Flows** and create a new flow.

Select **Record-Triggered Flow** as the flow type.

### 2. Configure Trigger Conditions

In the Start element, select the **Knowledge** object and configure the flow to trigger when a record is created or updated.

As trigger conditions, configure the flow to run only when the Title, Question, or Answer is changed.

Select **Is Changed** as the operator and **True** as the value.

## 3. Add a Prompt Template Action

Add an Action element and search for **Prompt Template**.

Select the previously created **Knowledge Summary**.

Set the label and API reference name.  
On the input side, specify **Triggering Knowledge\_\_kav** for **objectToSummarize**.

Select **Entire Resource**.

On the output side, **Prompt Response** is automatically generated, so no additional configuration is required.

### 4. Configure Record Update

Next, add an **Update Records** element.  
Set the label and API reference name, and select **Summary** as the field to update.

For the value, specify the output result from the Prompt Template action.

Select **Prompt Response**.

After completing the settings, save and activate the flow.

## Verify on a Knowledge Record

### 1. Verify Automatic Generation

Prepare a Knowledge record with an empty Summary field and open the edit screen.

Edit part of the title and save.  
Only when the Title, Question, or Answer is changed will the summary be automatically generated based on the latest content.

As shown below, the summary has been automatically generated. Success.

## Conclusion

As shown, automatic summary generation can be implemented relatively easily by combining a record summary template and a record-triggered flow.

The generated Knowledge summaries are also extremely useful information when introducing a RAG mechanism into Agentforce. Please consider adopting this approach.

That’s all for this time.

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
