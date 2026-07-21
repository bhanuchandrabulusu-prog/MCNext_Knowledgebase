# SFMC Tips #139 : Marketing Cloud Next: Addition of “Never” Option for Recurring Flows

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-next-addition-of-never-option-for-recurring-flows-54a38c91c733

---

# SFMC Tips #139 : Marketing Cloud Next: Addition of “Never” Option for Recurring Flows

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--54a38c91c733---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--54a38c91c733---------------------------------------)

4 min read

·

Jun 13, 2025

--

Photo by [Florian Klauer](https://unsplash.com/@florianklauer?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

As part of the **Summer ’25 new feature release** for **Marketing Cloud Next** (Marketing Cloud Growth & Advanced Edition), a new option called **“Never”** has been added to the rejoin mode settings for recurring flows.

[## SFMC Tips #106 : Marketing Cloud Next : Summer ’25 Release Highlights

### Exciting updates for Marketing Cloud Next (Marketing Cloud Growth & Advanced Edition) have been unveiled. For the first…

medium.com](/@marketingcloudtips/marketing-cloud-on-core-summer-25-release-highlights-4ad6f39c5d6d?source=post_page-----54a38c91c733---------------------------------------)

### Alignment with Marketing Cloud Engagement

This “Rejoin Mode” corresponds to the **“Re-entry Mode”** in Journey Builder within Marketing Cloud Engagement. With this addition, the rejoin mode functionality now matches the specifications of Marketing Cloud Engagement.

**Before Summer ‘25:**

![]()

**After Summer ‘25:**

![]()

### What is Rejoin Mode?

Rejoin mode allows you to configure conditions for re-entry into the same flow. It is particularly useful for preventing repeated entries of the same recipient, such as when recipients meet segment criteria daily. This feature helps avoid inappropriate multiple entries into a flow.

### Current Rejoin Mode Options

1. **Always (Re-enter anytime)**  
   Recipients can re-enter the flow any number of times, even if they are already active within the flow.
2. **After Completion (Re-entry only after exiting)**  
   Recipients can re-enter the flow only if they are no longer active in the flow.
3. **Never (No Re-entry)**  
   Once a recipient has entered the flow, they cannot re-enter the same flow again. *(New feature introduced in the Summer ’25 release)*

### Frequently Asked Questions

**Q:** If I select the “After Completion” or “Never” options, will recipients also be prevented from re-entering new versions of the same flow?  
**A:** Yes, re-entry into new versions of the same flow is also restricted. However, for the “After Completion” option, recipients can re-enter the new version once their participation in the previous version is complete.

## cf. Flow Deactivation and Version Management

Following the discussion on **Rejoin Mode**, this section briefly explains the behavior of **flow deactivation** in Marketing Cloud Next.

### 1. Types of Deactivation

Flow deactivation refers to the process of stopping a flow. While Marketing Cloud Engagement equates its “Stop” process to the second option described below, Marketing Cloud Next provides **two deactivation options**:

### **①** Deactivate and Complete Work

- The flow’s status changes to **“Completed”**.
- New entries are no longer accepted after deactivation.
- Existing recipients already in the flow will not be stopped; they will continue to progress along their paths.
- This behavior is similar to the **“Finishing”** state in Marketing Cloud Engagement.

### **②** Deactivate and Cancel Work

- The flow’s status changes to **“Canceled”**.
- New entries are no longer accepted after deactivation.
- Existing recipients’ actions are halted immediately, and those currently on the path will stop progressing at that point.
- While this is close to the **“Stop”** behavior in Marketing Cloud Engagement, it differs in one critical way: **Recipients are not forcibly removed from the flow; they remain on the path**.

This distinction impacts flows using the **“After Completion”** rejoin mode. Since there is no method to forcibly remove recipients from the flow, those remaining on the path cannot re-enter or progress. To ensure that they can re-enter, you need to choose **“Deactivate and Complete Work”** to allow the flow to complete fully.

This behavior differs from the “Stop” functionality in Marketing Cloud Engagement, where recipients are forcibly removed upon stopping, enabling re-entry even when “After Completion” is selected.

### Important Notes

- Once you confirm either option (① or ②), you cannot switch to the other.

### 2. Activating a New Version

When a new version of the flow is activated, the old version is automatically set to **“Deactivate and Complete Work”** (Status: Completed).

### **Important Notes**

- Recipients already in the old version remain on their paths, and their progress is not halted.
- If you need to stop the old version forcibly, you cannot switch to **“Deactivate and Cancel Work”** after the fact. However, you can return to the old version and use the “**Pause”** feature to stop the recipients from progressing further.

## Conclusion

Previously, achieving the **“Never” (No Re-entry)** option required some creative workarounds. However, with this new official support, the configuration process has been greatly simplified.

One practical use case for this feature is scenarios like a **Welcome Journey**, where you want to deliver content to recipients **only once**. In such cases, the **“Never” (No Re-entry)** rejoin mode can be applied effectively.

By leveraging **Rejoin Mode** appropriately, you can further enhance the precision of your flows.

That’s all for now.

Stay tuned for more Salesforce Marketing Cloud tips! 😊

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
