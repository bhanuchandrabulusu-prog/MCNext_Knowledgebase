# SFMC Tips #261 : Marketing Cloud Next: Automatic Campaign Creation from PDF / Word

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-next-automatic-campaign-creation-from-pdf-word-136a30a73131

---

# SFMC Tips #261 : Marketing Cloud Next: Automatic Campaign Creation from PDF / Word

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--136a30a73131---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--136a30a73131---------------------------------------)

3 min read

·

Mar 1, 2026

--

Photo by [Gantas Vaičiulėnas](https://unsplash.com/@gantas?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

With the [**Spring ’26 new feature release**](/@marketingcloudtips/marketing-cloud-next-spring-26-release-highlights-24c0c804b0cb) **of Marketing Cloud Next Growth & Advanced Edition**, it is now possible to create campaigns by utilizing **PDF or Word files stored in Salesforce Files**.

This enables you, for example, to upload **campaign details that have already been approved as meeting materials** and immediately launch a campaign directly from that file.

## Setup Steps

### 1. Prepare a PDF containing campaign details

For example, assume there is a PDF that includes **campaign objectives, target audience, offer details**, and other information as shown below.

### 2. Upload the PDF to Salesforce Files

First, upload the PDF to **Salesforce Files**.

### 3. Request campaign creation from Agentforce

Next, on the **“Home” tab in Marketing Cloud**, simply ask Agentforce to create a campaign based on this PDF.

Request:  
 **“I would like to create a campaign from a file.”**

![]()

### 4. Provide the file name

Agentforce will ask for the file name, so provide the name of the uploaded file.

In this example, the file name is:  
 **“Campaign\_2026\_March”**

### 5. Campaign brief creation

After a short time, the **campaign brief is created**. Success.

![]()

### 6. Proceed with the standard Campaign Creation flow

Once the brief is generated, proceed with the **standard Campaign Creation flow**.  
([The steps are explained in this article](/@marketingcloudtips/marketing-cloud-on-core-agentforce-campaign-creation-697c992adbe6).)

![]()

### 7. Automatic generation of campaign, flow, and content

Not only the **campaign itself**, but also the **flow and content** are automatically generated.

## Summary

Even **unstructured data** that is not organized into specific fields (such as **PDF or Word files**) can now be accurately read by Agentforce.

Agentforce identifies **key content and important keywords**, and executes the creation of **campaigns, flows, and content from a single document**.

This is **only the beginning**.  
Agentforce is expected to become **even more advanced** in the future.

In this medium, I will continue to follow its evolution.

That’s all for now.

Stay tuned for more Salesforce Marketing Cloud tips! 😎

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
