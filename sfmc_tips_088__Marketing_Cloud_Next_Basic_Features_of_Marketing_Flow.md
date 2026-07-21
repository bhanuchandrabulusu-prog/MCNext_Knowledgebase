# SFMC Tips #88 : Marketing Cloud Next: Basic Features of Marketing Flow

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-on-core-introduction-to-flow-builder-features-fd65d9ea0b97

---

# SFMC Tips #88 : Marketing Cloud Next: Basic Features of Marketing Flow

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--fd65d9ea0b97---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--fd65d9ea0b97---------------------------------------)

7 min read

·

Mar 13, 2025

--

Photo by [Maksym Tymchyk 🇺🇦](https://unsplash.com/@maksym_tymchyk?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

In Marketing Cloud Next (Marketing Cloud Growth Edition/Advanced Edition), you can use Flow Builder to execute marketing scenarios. Flow Builder serves a similar purpose to Journey Builder in Marketing Cloud Engagement (MCE), but it comes with distinct features and specifications. This article explains the basic functions and key considerations when working with Flow Builder.

## Core Features of Flow Builder

### Basic Elements in Flow Builder

The structure and user experience of Flow Builder closely resemble those of Journey Builder. You can build flows by combining the following elements:

- **Place Segments and Schedules**
- **Add Email (SMS, WhatsApp) or Wait Elements**
- **Set Decision Splits and Send Time Optimization (STO)**
- **Define Exit Criteria**
- **Determine Rejoin mode (Re-Entry mode)**

While the basic operations are nearly identical to Journey Builder, there are some key differences in specifications.

## Key Specifications and Behavioral Differences

### 1. Segment Behavior and Actual Delivery Count

Flow Builder does not use the term “Entry Source”. Even if you edit and refine a segment just before delivery, the segment that was last published will be used for the flow execution.

**For example:**  
If you narrow a segment down to 3 contacts just before delivery, but the segment had 6 contacts when last published, the flow will target all 6 contacts.

Interestingly, Flow Builder provides an option to automatically publish the latest segment before flow execution — something not available in MCE.

**Note:**  
This automatic publication can require up to two hours of preparation, potentially delaying the start of the flow. For instance, even if you schedule an email for 2 PM, the email might be sent at 3 PM if the segment isn’t published in advance. This is critical for time-sensitive campaigns.

**\*Supplement: An Easy-to-Understand Explanation of the Concept of “Publish”**

### For Journey Builder

- Creating a data extension is essentially the same as “creating and publishing a segment”.
- In other words, **there is no need to perform a separate “Publish” task**.
- Practically speaking, you can think of the data extension as being in a “Published” state the moment it is created.

### For Flow Builder

- When you create a segment, it is still in a **provisional state**.
- At this stage, you can think of the segment as incomplete.
- **Only after “Publishing” does the segment become finalized as a distribution list**.
- Keep in mind that immediately after creating a segment, it remains in a “**floating provisional state**”.
- Segments in this provisional state will not be used for sending. Instead, only the “**final published segment**” is used for sending.

### 2. Schedule Types

Flow Builder allows you to select from two schedule types:

- **Run Once**
- **Recurring**

### 3. Start Time Precision

You can set the flow start time in **one-minute increments** when configuring the schedule.

### 4. Recurring Schedule Limitations

Currently, recurring schedules are limited to “**Daily**” or “**Weekly**”. More flexible options like “Hourly” or “Monthly” schedules are unavailable. Future updates may bring enhancements to this feature.

### 5. Rejoin Mode (Re-Entry Mode)

Flow Builder’s equivalent of MCE’s Re-Entry mode is called “Rejoin mode”, with the following options:

- **Always (Re-enter anytime)**
- **After completion (Re-entry only after exiting)**

![]()

**Important:**  
Unlike MCE, Flow Builder does not have a “**No Re-entry**” option. To prevent a contact from entering a flow more than once, you’ll need to employ creative solutions, such as:

- **Exclusion Conditions in Segments**  
   Save contacts that entered the flow into a Data Model Object (DMO) and use this data for exclusion in segments, mimicking MCE’s “Update Contact” activity.
- **Using a “Wait Until Date” element**  
   Place this element at the end of the flow and set a far-off future date (e.g., December 31, 2040). If combined with the “**After Completion**” rejoin mode, this prevents contacts from re-entering the flow.

### 6. Single Execution

Like MCE, Flow Builder offers the options to:

- Start at Specific Date and Time
- Start Immediately after Activation

**Note:**  
When using the automatic segment publication feature, selecting “Start Immediately after Activation” might not result in instant delivery due to the preparation time required for segment publishing.

## Activating and Managing Versions in Flow

### 1. Types of Deactivation

When deactivating a flow, you have two options:

**“Deactivate and complete work”** (Status: Complete)

- Processing will not stop, and contacts currently in the flow will continue to progress.
- This is equivalent to “Finishing” in Marketing Cloud Engagement (MCE).

**“Deactivate and cancel work”** (Status: Canceled)

- Processing stops entirely, and contacts currently in the flow will no longer progress.
- Similar to “Stopped” in MCE, but with a difference: contacts remain on the path and are not forcibly marked as completed.

This distinction affects flows set to Rejoin mode: After Completion (allowing reentry only after completion).

- **Because contacts are not forcibly removed from the flow**, in the case of a new flow version set to “Rejoin mode: After Completion,” any contacts left on the previous path will not receive messages in the new version.
- To ensure those contacts are processed fully, you must select “**Deactivate and complete work**”, allowing them to move to the end of the flow.

This key difference separates this option from MCE’s “Stopped” action.

- In MCE, the “Stopped” action forcibly removes contacts from the path, enabling them to reenter and receive messages in a new version even when “Re-Entry mode: **Re-entry only after exiting**” is set.

**Important:**

- Once you choose an option, it cannot be changed later.
- Even if you select “Deactivate and complete work”, you can use the pause functionality to effectively halt the flow, preventing contacts from progressing along the path — similar to “Deactivate and cancel work”.

### 2. Creating a New Version

When a new version of the flow is created, the previous version is automatically set to “Deactivate and complete work” (Status: Complete).

**Key Points to Note:**

- Contacts already entered into the previous version will remain on their respective paths and continue to progress.
- You can pause the previous version to prevent further progression if needed.

## Key Features and Considerations

### 1. Behavior of Wait Elements

In Flow Builder, **the wait period continues to progress** even if the flow is paused. Unlike MCE, there is no option to extend the wait period during a pause.

- If the wait period expires while the flow is paused, emails may be sent immediately upon resuming the flow.

### 2. Scheduling Flexibility for Recurring Flows

Flow Builder allows scheduling with past dates if the schedule is recurring. For example, if you set a start date of March 10, 2020, at 3:00 PM, the flow will still run starting at the current 3:00 PM. This level of flexibility is not available in MCE.

### 3. Editing After Activation

If a flow has been activated but no contacts have yet entered the flow (i.e., the flow is scheduled but not yet running), you can deactivate it and make edits. However, once contacts start entering the flow, you’ll need to create a new version to make changes.

### 4. Updating Email Content

According to the help documentation, editing and saving content followed by Re-“Publish” should ensure the latest version is reflected.

[## Help And Training Community

### Edit description

help.salesforce.com](https://help.salesforce.com/s/articleView?language=en_US&id=mktg.mktg_content_status_ref.htm&type=5&source=post_page-----fd65d9ea0b97---------------------------------------)

However, when I tested this in my environment, I occasionally encountered cases where the old version was sent instead. Given this inconsistent behavior, I plan to investigate the root cause further. To ensure the updated email content is reliably reflected, it seems effective to create a new version of the flow and reconfigure the email element after deleting it once.

## Exit Criteria

In Flow Builder, you can configure **Exit Criteria**, similar to Marketing Cloud Engagement.

- Exit criteria are evaluated at the **start (entry point)** and again **after a wait element completes**.
- You can define up to **10 conditions**.

The following can be used as conditions:

- Global attributes
- Direct attributes from the data graph
- Related attributes linked to the data graph
- Attributes from calculated insights linked to the data graph

By leveraging these exit criteria, contacts who no longer meet the conditions can be **automatically removed from the flow**.

[## SFMC Tips #287 : Marketing Cloud Next: Behavior of Exit Criteria

### In this article, I summarize the behavior of Exit Criteria in Marketing Cloud Next Growth & Advanced Edition.

medium.com](/@marketingcloudtips/marketing-cloud-next-behavior-of-exit-criteria-7f55f708ecea?source=post_page-----fd65d9ea0b97---------------------------------------)

Flow Builder shares a similar interface with Journey Builder in MCE while offering unique specifications and constraints. By understanding these differences and leveraging their features, you can design more efficient and flexible marketing scenarios.

That’s it for now!

Stay tuned for more Marketing Cloud Growth & Advanced Edition tips! 😊

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
