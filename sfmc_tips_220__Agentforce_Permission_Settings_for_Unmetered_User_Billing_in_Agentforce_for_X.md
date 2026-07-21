# SFMC Tips #220 : Agentforce: Permission Settings for Unmetered User Billing in Agentforce for X

**Source:** https://medium.com/@marketingcloudtips/agentforce-permission-settings-for-unmetered-user-billing-in-agentforce-for-x-6a63df2af3a9

---

# SFMC Tips #220 : Agentforce: Permission Settings for Unmetered User Billing in *Agentforce for X*

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--6a63df2af3a9---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--6a63df2af3a9---------------------------------------)

3 min read

·

Dec 22, 2025

--

Photo by [Aaron Burden](https://unsplash.com/@aaronburden?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

With the [**Agentforce Summer ’25 release**](https://help.salesforce.com/s/articleView?id=release-notes.rn_billing_a4x_pupm.htm&release=256&type=5), Salesforce introduced a new capability that allows **internal users** to use certain AI features **without consuming Generative AI credits (Flex Credits)** when specific **Agentforce add-ons** are in place.

When the conditions are met, **user-initiated** use of Agentforce AI features does **not** incur charges.

⚠️ **Important**  
This applies **only to user-initiated usage**.  
System-initiated executions (for example, LLM calls triggered from external systems) are **not** eligible for free usage.

## Eligible Usage

The following are covered under unmetered (free) usage:

- Execution of **standard (out-of-the-box) generative AI features**
- Execution of **prompt templates created in Prompt Builder**

## Supported Editions and Add-ons

This capability is available with the following **Agentforce editions and add-ons**:

- Agentforce 1 Editions
- Agentforce for Automotive
- Agentforce for Communications
- Agentforce for Consumer Goods
- Agentforce for Education
- Agentforce for Energy and Utilities
- Agentforce for Field Service
- Agentforce for Financial Services
- Agentforce for Health
- Agentforce for Life Sciences
- Agentforce for Manufacturing
- Agentforce for Media
- Agentforce for Net Zero
- Agentforce for Nonprofits
- Agentforce for Public Sector
- Agentforce for Sales
- Agentforce for Service

**Note:** Agentforce for Marketing is **not supported at this time**.

## Increasing Incidents of Unintended Flex Credit Consumption

Salesforce has recently issued warnings due to an increase in cases where **Flex Credits are consumed unintentionally**, typically caused by the following situations:

- Users have a valid user license, **but**
- Required **Permission Set Licenses (PSL)** are not assigned
- Required **system permissions** are not enabled

As a result, AI usage that should have been **unlimited for internal users** becomes **billable**.

## Background: Why Configuration Is Required

- The org must support the **Unmetered User-Based AI Permission Set License**
- Internal AI usage (Agentforce used in a **user context**) can be **unlimited**
- **However, this is NOT enabled automatically ❗**

If the correct permissions are not configured, **Flex Credits will be consumed even for internal usage**.

## Root Cause: Missing “Unlimited User” Configuration

What is commonly referred to as the **“Unlimited User”** setting actually means:

- **Unmetered User-Based AI permission**  
   (via the *Unmetered User-Based AI* Permission Set)

If a user **does not** have this configured and uses Agentforce:

- Even for internal use
- Even in a user context

👉 **Flex Credits will be consumed**

## Two Required Configuration Steps (Both Are Mandatory)

To be treated as **Unlimited (Unmetered)**, **both** steps must be completed.

⚠️ **Completing only one is not sufficient.**

### ① Assign the Permission Set License to Each Internal User

- **Unmetered User-Based AI** (PSL)

### ② Assign the System Permission to Each Internal User

- **Unmetered User Based AI**

> *⚠️* ***Note:*** *This system permission (***Unmetered User Based AI***) is only visible* ***after “Einstein Setup” is enabled*** *in the org.*

For detailed setup steps, please refer to the official Salesforce Help documentation.

[## Salesforce Help

### Edit description

help.salesforce.com](https://help.salesforce.com/s/articleView?language=en_US&id=ai.generative_ai_usage_unmetered_considerations.htm&type=5&source=post_page-----6a63df2af3a9---------------------------------------)

## Relationship with Digital Wallet

- AI usage by users **without proper Unlimited configuration**  
   👉 **will still be counted in Digital Wallet (and billed)**
- Monitoring **Digital Wallet** can help you detect anomalies  
   👉 **But be aware:** by the time you notice, credits may already have been consumed

## Summary: Mandatory Checklist

✅ Is the **Unmetered User-Based AI Permission Set License** assigned?  
✅ Is the **Unlimited User-Based AI system permission** assigned?  
✅ Is **Digital Wallet** being monitored regularly?

## Final Thoughts

Going forward, more accounts will likely rely on the **Unmetered User-Based AI Permission Set License**.

To avoid unintended charges, make sure there are **no configuration gaps**.  
If you haven’t verified this yet, I strongly recommend reviewing user permissions now.

That’s all for this time.

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
