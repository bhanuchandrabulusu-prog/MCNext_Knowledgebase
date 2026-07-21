# SFMC Tips #192 : Marketing Cloud Next: Content Builder Agent

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-next-content-builder-agent-4c426d6dec3a

---

# SFMC Tips #192 : Marketing Cloud Next: Content Builder Agent

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--4c426d6dec3a---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--4c426d6dec3a---------------------------------------)

4 min read

·

Oct 15, 2025

--

Photo by [Jon Tyson](https://unsplash.com/@jontyson?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

In the [**Summer ’25 release**](https://help.salesforce.com/s/articleView?id=release-notes.rn_einstein_migrate_agentforce_default_aea.htm&release=256&type=5), Salesforce announced the **retirement of Agentforce (Default)**. While it continues to function for now, **no new features or updates** are being added. Organizations will need to **transition to Agentforce Employee Agent** going forward.

As part of this change, the [**Winter ’26 release**](/@marketingcloudtips/marketing-cloud-next-winter-26-release-highlights-81240775f843) introduces **new standard agent templates** designed specifically for **Marketing Cloud**.

- **Topic Name:** Campaign Planning (for campaign creation)  
   → **Agent Template Name:** Campaign Creation
- **Topic Name:** Content Creation (for content creation)  
   → **Agent Template Name:** Content Builder Agent

These agent templates are built by separating the topics that were previously bundled within **Agentforce (Default)**, making them the **successors** of the earlier model.

However, the **key enhancement** in this update is that you can now **individually configure each agent** — including company details, brand tone, and response guidelines — to ensure **brand consistency** while maintaining flexibility.

This change enables more **tailored and efficient agent operations**, aligned with each team’s role and use case.

### **Addition of the “Generate Campaign Insights” Action**

In the **Winter ’26 release**, a new action called **“Generate Campaign Insights”** has been added under the **Campaign Planning** topic.

![]()

### What is the “Generate Campaign Insights” action?

- Automatically retrieves key performance data such as **open rate**, **click rate**, and **unsubscribe rate**
- Automatically generates a **summary of major insights**

Administrators can **edit the flow** to customize this action, allowing them to focus on the metrics **most relevant to their business**.

Meanwhile, marketers can **compare high-performing and low-performing campaigns** to derive **specific improvement suggestions**, such as optimizing subject lines or adjusting email send intervals.

### **Creating and Assigning Permission Sets**

When using **Agentforce Employee Agent** for the first time, special attention is required.

This feature **cannot be used without dedicated access permissions**, and **even system administrators are not exempt**.

Currently, this access permission must be **manually created as a custom permission set**.

### Steps

1. In **Setup**, search for **Permission Sets** and click **New**.
2. Enter the following details (sample values) and click **Save**:

- **Label:** Grant Agent Access
- **API Name:** Grant\_Agent\_Access
- **Description:** This grants access to the active Agentforce for employee agents.

1. On the permission set detail page, go to the **Apps** section and scroll down to click “**Agent Access**”.
2. Click **Edit**.
3. A list of available **Agentforce Employee Agent** agents will appear.
4. Select **Campaign Creation** and **Content Builder Agent**, then click **Save**.
5. If **Agentforce Employee Agent (Default)** is listed, select and save that as well.
6. Return to the permission set detail page and click **Manage Assignments**.
7. Click **Add Assignments**, check the user(s) to grant access to (e.g., yourself), and save.

You should now have access to both the **Campaign Creation** and **Content Builder Agent**.

> *Don’t forget to* ***assign the permission set to users*** *after creating it — this step is often overlooked.*

### Notes When Starting to Use Campaign Creation

When you’re using the **Campaign Creation** feature but have **Content Builder Agent** selected, the **Generate Brief** (Confirm) button will **not appear**.

![]()

If you switch back to **Campaign Creation**, the button will reappear.

![]()

Therefore, be sure to **switch to “Campaign Creation” before starting your work**.

> *However, since this setup can be slightly inconvenient, another approach is to* ***add the “Campaign Planning” topic*** *to your* ***Content Builder Agent****, allowing you to use a* ***single agent for multiple purposes****.*

## Conclusion

This new feature isn’t an entirely new mechanism — it’s essentially a **transition measure** following the **retirement of Agentforce (Default)**.

That said, since certain setup changes are required for continued use,  
**I** **recommend preparing and transitioning early** if you’re already using Agentforce.

That’s all for now.

Stay tuned for more Salesforce Marketing Cloud tips! 😎

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
