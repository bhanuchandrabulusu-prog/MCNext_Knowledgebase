# SFMC Tips #193 : Agentforce: Deploying Service Agents on CloudPages (External Sites)

**Source:** https://medium.com/@marketingcloudtips/agentforce-deploying-service-agents-on-cloudpages-external-sites-d4fb5edacb91

---

# SFMC Tips #193 : Agentforce: Deploying Service Agents on CloudPages (External Sites)

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--d4fb5edacb91---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--d4fb5edacb91---------------------------------------)

5 min read

·

Oct 16, 2025

--

Photo by [COSMOH](https://unsplash.com/@cosmoh?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

In this article, I’ll explore how to **embed the Agentforce Service Agent on an external website** using **CloudPages** in Marketing Cloud Engagement.

With the recent boom in AI agents across Salesforce, many of you might be curious about how the configuration mechanism actually works.

In my previous articles, I’ve demonstrated various use cases for **CloudPages**, such as embedding a **Marketing Cloud Next** [**signup form**](/p/fe21918045e2) on an external website and testing [**form handlers**](/p/ed3e045adfad).

This time, I’ll take it a step further and deploy **Agentforce** directly onto CloudPages to see how it behaves in action.

Before diving into this experiment, I highly recommend trying the following Trailhead module first — it’ll cover about **90% of the setup work**:

[## Configure Agentforce for Exceptional Service

### Learn to set up Agentforce for Coral Cloud Resorts' service agents. Enhance customer experiences with personalized…

trailhead.salesforce.com](https://trailhead.salesforce.com/content/learn/projects/quick-start-build-your-first-agent-with-agentforce/configure-an-agentforce-service-agent?source=post_page-----d4fb5edacb91---------------------------------------)

While the Trailhead example demonstrates how to display the agent on an **Experience Cloud page**, the same principle applies to **external websites** as well.

In other words, once you understand the process, you can apply it both internally and externally — a double benefit for your learning.

Below is a simplified overview of the setup process.  
For parts that have already been configured, I encourage you to review the existing settings to understand how they’re implemented.

### **Basic Setup**

**1. Create and Activate the Agentforce Service Agent**  
 ➡ Follow the setup instructions provided in the Trailhead module.

**2. Check Omni-Channel Settings**  
 ➡ Omni-Channel is already enabled in the Playground.

**3. Check Digital Experiences Settings**  
 ➡ Digital Experiences is also already enabled in the Playground.

**4. Check Service Channel Settings**  
 ➡ Service Channel is also already enabled in the Playground.

**5. Routing Configuration**  
 ➡ The routing configuration has already been created in the Playground.

**6. Queue Configuration**  
 ➡ The necessary queues have already been created in the Playground.

**7. Omni-Channel Flow Configuration**  
 ➡ Follow the editing steps as described in the Trailhead instructions.

**8. Messaging Configuration**  
 ➡ The messaging setup has already been completed in the Playground.

**9. Embedded Service Deployment Setup**  
 ➡ The deployment configuration has already been created in the Playground.

**Note:** At this stage, the setup diverges depending on whether you’re deploying to an **internal** or **external** site. If you’re setting it up for an internal site, simply follow the Trailhead instructions as they are.

The following section explains the steps for **external site deployment**.

### **External Site Configuration**

**10. Embedding the Script into CloudPages**  
a. Open your **Embedded Service Deployment**, then select **Code Snippet**.

b. Copy the **Chat Code Snippet**.

c. Open the **Code View** in CloudPages, paste the script **just before the** `</body>` **tag**, then click **Save** and **Publish**.

**11. CORS Configuration**  
a. In **Setup**, search for **CORS**, and click **New**.

b. Enter the **CloudPages URL (origin)** — do **not** include the trailing “/”.

Example: `https://mcxkknz3m0zj3jqsxn4hm3dp3q-4.pub.sfmc-content.com`

**12. Trusted URL Configuration**  
a. In **Setup**, search for **Trusted URLs**, then click **New Trusted Domain**.

b. Enter both the **API Name** and **URL** — use the same URL as above.  
Make sure to **check “frame-src (iframe content)”**.

Example: `https://mcxkknz3m0zj3jqsxn4hm3dp3q-4.pub.sfmc-content.com`

**13. Site Settings (under User Interface)**  
a. In **Setup**, search for **Sites**, and click **Register My Salesforce Site Domain**.

b. Next, you’ll see a list of **site endpoints**. Select the one that starts with “**ESW**” **(Experience Site Workspace)**.

c. Under **Trusted Domains for Inline Frames**, click **Add Domain**.

d. Add the same CloudPages URL here as well.

Example: `https://mcxkknz3m0zj3jqsxn4hm3dp3q-4.pub.sfmc-content.com`

**14. Verify CloudPages**  
That’s it! 🎉 Your setup is complete — the Agentforce widget should now appear on your CloudPages site.

> ***Tips:*** *Steps 11–13 may look repetitive, but each one is necessary. After completing* ***Step 13****, it may take* ***1–2 minutes*** *for the changes to take effect on CloudPages. Be patient, and refresh the page until the Agentforce component appears.*

## Conclusion

As you can see, there’s not much difference between the **internal** and **external** site setup processes.

Even if certain configurations — such as **Routing**, **Queues**, **Flows**, **Messaging**, and **Embedded Service Deployment** — are already preconfigured in the Playground, you can easily recreate them by referencing the Playground setup.

If you’d like to build everything from scratch, Salesforce provides a **Developer Edition** that includes **Agentforce and Data Cloud**. You can apply for access using the link below:

[## Developer Edition with Agentforce and Data Cloud

### Build enterprise-quality apps fast and get hands-on with Agentforce and Data Cloud.

www.salesforce.com](https://www.salesforce.com/form/developer-signup/?source=post_page-----d4fb5edacb91---------------------------------------)

Also, I’ve created a separate article that walks through the process from scratch. Please feel free to create it by following the steps in the article below.

[## SFMC Tips #221 : Agentforce: How to Implement a Service Agent Using Knowledge

### Salesforce partners implementing Marketing Cloud Next have likely noticed a growing trend: projects where Marketing…

medium.com](/@marketingcloudtips/sfmc-tips-221-agentforce-how-to-implement-a-service-agent-using-knowledge-ef7a9e0cdc6b?source=post_page-----d4fb5edacb91---------------------------------------)

[## SFMC Tips #222 : Agentforce: Deploying Service Agents to Your Website

### Previously, I wrote an article about how to install Agentforce on an external site (CloudPages in Marketing Cloud…

medium.com](/@marketingcloudtips/sfmc-tips-222-agentforce-deploying-service-agents-to-your-website-8b5f38c6b0b9?source=post_page-----d4fb5edacb91---------------------------------------)

That’s all for this session! 😎

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
