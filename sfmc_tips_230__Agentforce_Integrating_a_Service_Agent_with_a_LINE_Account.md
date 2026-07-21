# SFMC Tips #230 : Agentforce: Integrating a Service Agent with a LINE Account

**Source:** https://medium.com/@marketingcloudtips/sfmc-tips-229-agentforce-integrating-a-service-agent-with-a-line-account-e99698ef8d9c

---

# SFMC Tips #230 : Agentforce: Integrating a Service Agent with a LINE Account

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--e99698ef8d9c---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--e99698ef8d9c---------------------------------------)

5 min read

·

Jan 7, 2026

--

Photo by [Debby Hudson](https://unsplash.com/@hudsoncrafted?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

Agentforce can be utilized across various channels.  
In this article, I explain how to integrate Agentforce (a service agent) into a LINE account, which is the most familiar messaging app for people in Japan.

## Prerequisites

Before proceeding with this setup, the following must be completed:

- Creation of a service agent
- Creation of a flow that routes to the service agent

Please refer to the articles below to create these.

[## SFMC Tips #221 : Agentforce: How to Implement a Service Agent Using Knowledge

### Salesforce partners implementing Marketing Cloud Next have likely noticed a growing trend: projects where Marketing…

medium.com](/@marketingcloudtips/sfmc-tips-221-agentforce-how-to-implement-a-service-agent-using-knowledge-ef7a9e0cdc6b?source=post_page-----e99698ef8d9c---------------------------------------)

[## SFMC Tips #222 : Agentforce: Deploying Service Agents to Your Website

### Previously, I wrote an article about how to install Agentforce on an external site (CloudPages in Marketing Cloud…

medium.com](/@marketingcloudtips/sfmc-tips-222-agentforce-deploying-service-agents-to-your-website-8b5f38c6b0b9?source=post_page-----e99698ef8d9c---------------------------------------)

> *※ For Article #222, it is sufficient if you have completed up to* ***“7. Omni-Channel Flow Configuration”.*** *From* ***“8”****, the content branches into what is covered in this article.*

## LINE Integration Steps

### 1. Enable Messaging

Enable the messaging feature.

### 2. Select a New Channel

Select **“New Channel”.**

### 3. Select LINE

Select **LINE** from the list of channels.

![]()

### 4. Agree to the Terms

Review the displayed terms and agree to them.

![]()

### 5. Log in to the LINE Developer Console

Next, log in to the **LINE Developer Console**.

Obtain the following **four pieces of information**:

- **LINE Channel Name**  
   Example: Bells On Records Official
- **LINE Channel ID**  
   Example: 1654292823
- **LINE Channel Secret**  
   Example: e2177bdbaefd5055c5a7fed75b8971e
- **LINE Channel Access Token**  
   Example: 0eobuavCC0u2lElebASdXBEGXb+/cy5q6wz1Ye/ehZDMbSqDiP6FKjTzVxjtaq3mHO9z3sPPEBCFtzCa5Zc07ZNY8E+DL0UexbOgGZZ9HDl0Ml607Z+FYkXRHi5VmJyGy+99dvu0kIcPlADbhcdSwwdB04t89/1O/w1cDnyilF=

> *※ All of the above information can be obtained from* ***“Channel Basic Settings”*** *and* ***“Messaging API Settings”.***

### 6. Enter LINE Information

Enter the retrieved information into the Agentforce configuration screen.

![]()

### 7. Set Up Routing Later

Select **“Set up Routing Later”.**

![]()

### 8. Complete the Setup

Complete the setup.

![]()

### 9. Open the Created Configuration

At this point, it has not yet been activated.  
 Click the created configuration.

### 10. Copy the Webhook URL

In the **LINE Connection** section, copy the displayed **Webhook URL**.

### 11. Set the Webhook URL in the LINE Developer Console

Return to the LINE Developer Console and enter the Webhook URL.

Next, be sure to **execute Webhook verification** as well.

### 12. Configure Omni-Channel Routing

After completing the Webhook URL configuration, return to the Agentforce configuration screen and configure **Omni-Channel Routing**.

### 13. Select an Omni-Flow

Select the Omni-Flow.

### 14. Configure the Flow and Fallback Queue

Specify the following, which were configured in a previous article:

- Flow
- Fallback Queue

Then save the settings.

### 15. Activate

Once the configuration is complete, **activate** it.

This completes the integration setup between LINE and Agentforce (service agent).

## Testing on LINE

Now that the integration between LINE and Agentforce (service agent) is complete, let’s finally verify the operation on LINE itself.

### 1. Start a Message

From the LINE app, send a message to the target LINE account.  
 When a message is sent, the Agentforce service agent is launched and an automatic reply is returned.

### 2. Send a Question

Next, send any question.

### 3. Confirm the Response

If an appropriate response is returned from the agent, the integration is successful.

### 4. Confirm Other Actions

The service agent I created included the following actions, so I checked those as well:

- Email verification action
- Automatic case creation action

I confirmed that these actions were executed without any issues.

## Conclusion

With the messaging configuration performed this time, in addition to LINE, the following channels can also be used:

- **WhatsApp**
- **Facebook Messenger**
- **Apple Messages**

Depending on the channel, the required input items and configuration screens at the time of connection may differ slightly, but the basic setup flow is common.

Please try other channels as well.

That’s all for this time.

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
