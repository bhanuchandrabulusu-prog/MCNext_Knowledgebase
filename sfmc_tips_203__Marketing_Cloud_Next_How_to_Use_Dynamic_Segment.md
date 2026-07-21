# SFMC Tips #203 : Marketing Cloud Next: How to Use Dynamic Segment

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-next-how-to-use-dynamic-segments-06ee41977c2a

---

# SFMC Tips #203 : Marketing Cloud Next: How to Use Dynamic Segment

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--06ee41977c2a---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--06ee41977c2a---------------------------------------)

7 min read

·

Nov 16, 2025

--

Photo by [Wren Meinberg](https://unsplash.com/@wrenaylameinberg?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

In the October 2025 Data Cloud update, two major features were introduced: **Dynamic Segments** and **Broadcast Flows**.

### Data Cloud Segment Features Covered in This Article:

1. ✖️ [Standard Segment](/p/d240bb357d3d)
2. ✖️ [Waterfall Segment](/@marketingcloudtips/marketing-cloud-on-core-waterfall-segment-fbe99d4af303)
3. ️✖️ [Real-Time Segment](/@marketingcloudtips/marketing-cloud-next-leveraging-real-time-segments-868c0f591205)
4. ⭕ [**Dynamic Segment**](/@marketingcloudtips/marketing-cloud-next-how-to-use-dynamic-segments-06ee41977c2a)
5. ✖️ Einstein Segment Creation (AI-Driven segments)

In particular, Dynamic Segments suddenly appeared in the new segment creation screen, leaving many users wondering:

- “How do I use this?”
- “What’s different from a traditional segment?”

This article explains, as simply as possible, **how these new features work**, **when to use them**, and **how to configure them step by step**.

## How the Two Features Relate

First, an important point:

💡 **Dynamic Segments can currently be used *only* in Broadcast Flows.**  
They are not supported in any other flow type.

## What Is a Dynamic Segment?

### Static Conditions vs. Dynamic Conditions

Dynamic Segments allow you to combine traditional **static conditions** with **dynamic conditions** that change depending on the timing of the send.

**Examples of Static Conditions**

- Example: Gender = Female  
   → At API execution time, the condition is fixed as “send to all females”.

**Examples of Dynamic Conditions**

- Example: Values passed from the API determine whether the condition becomes A, B, or C at send time.  
   → The extracted segment changes based on parameters inserted right before execution.

Values used for dynamic conditions are specified **as parameters when the API is executed**.

Example request body:

```
{  
  "inputs": [  
    {  
      "ticketIdVariable": "TID01359"  
    }  
  ]  
}
```

This allows you to dynamically send to all customers who purchased the ticket with ID “TID01359”.

👉 In other words:

- **Static conditions** = fixed filtering criteria
- **Dynamic conditions** = filtering criteria that change every execution based on parameters

### No “Published” Status for Dynamic Segments

Traditional segments have statuses such as Draft or Published.  
Dynamic Segments do **not** have a “Published” status.

They **always use the latest saved configuration**, so no publishing task is required.

### Large-Scale Sending: Up to 100,000 Records

Dynamic Segments can send messages to large audiences.  
 Currently, **up to 100,000 records** can be processed at one time.

### Important Notes When Using Count / Preview

You can still use **Count** and **Preview** with Dynamic Segments.

However, because dynamic parameters cannot be counted directly:

**You must temporarily replace dynamic parameters with static values to run Count / Preview.**

1. Temporarily change the dynamic field into a static value
2. Check Count / Preview
3. If correct, switch it back to the parameterized filter

This ensures safe verification before activating your flow.

## What Is a Broadcast Flow?

A Broadcast Flow is essentially the **segment-based version** of an On-Demand Flow.

- **On-Demand Flow:** triggered per individual
- **Broadcast Flow:** triggered per segment

It enables real-time bulk messaging to all individuals within a segment.

### Current limitations

- Only **ad-hoc API-triggered execution** (no schedules)
- **Debug** is not supported
- **Wait elements** are not supported

\*Both features (Debug and Wait elements) are on the roadmap.

## How to Configure Dynamic Segments

Now, let’s walk through the configuration steps that many of you have been curious about.

1. First, on the **New Segment** screen, select **Dynamic Segment**.

2. Under **Segment On**, select **Individual**.

3. As mentioned earlier, there is no “Publish” concept for Dynamic Segments, so you cannot set a publish schedule. Only configure the **lookback period** for the engagement data.

4. Next, as a static condition, create a segment that counts people who have purchased the ticket whose Ticket ID is `TID01359`.

5. Confirm that this count matches the number you expect. If the flow runs with this number of records, you can consider it a success.

6. Once you’ve confirmed the count, open the filter screen again and check “**Enable Parameterized Values”**.

7. For the value, enter a variable name related to the Ticket ID, such as `ticketIdVariable`. This is just a variable name, so you can use any label you like.

8. You’ll see that the value is replaced with `Variable: {!ticketIdVariable}`, and the segment can no longer be counted. Click **Done** and save the configuration.

The Dynamic Segment configuration is now complete.

## Broadcast Flow Configuration

Next, configure the Broadcast Flow.

1. In **Flow Builder**, search for **Broadcast Flow** and select it.

2. In the start element of this flow, the only thing you can select is a **Dynamic Segment**.

3. Next, specify the **API name** of the Data Model Object that stores the email address.

4. Then, at the bottom, specify the value that will be inserted into the **parameterized filter** of the Dynamic Segment. In this example, I want to use a value coming from the API execution, so I’ll provide it as a variable. Click **New Resource**.

5. Select **Variable**.

6. Give the variable an appropriate name (here, I’ll use the same name as in the segment configuration, `ticketIdVariable`), set the **Data Type** to **Text**, and check **Available for input**. This allows the API to pass a value into this variable. Then complete the setup.

7. Next, click **Add Element**. From here, you can configure a **Marketing Cloud Next Send** or **send customers into a** **Marketing Cloud Engagement Journey**. More channels are planned to be added in the future.

8. In this example, I’ll configure a **Marketing Cloud Next Send**. After you finish the settings, save the Broadcast Flow and activate it.

The Broadcast Flow configuration is now complete.

## Executing the REST API

Executing the REST API involves two steps:

1. **Obtaining an access token**
2. **Making the request to the resource server**

For instructions on how to obtain the access token, please refer to the article below.

[## SFMC Tips #181 : Marketing Cloud Next: Obtaining an Access Token for the REST API

### Previously, I wrote an article on how to obtain an access token when using the REST API in Marketing Cloud Engagement.

medium.com](/@marketingcloudtips/marketing-cloud-next-obtaining-an-access-token-for-the-rest-api-156eca392584?source=post_page-----06ee41977c2a---------------------------------------)

Once you have retrieved the access token, proceed with the request to the resource server.

1. Prepare the following three items in advance:

- **Access Token**
- **Flow API Name**
- **My Domain name** (Go to Setup → “My Domain” to confirm)

2. Open a new request in Talend API Tester and configure it as follows.

```
-- Method  
POST  
-- Endpoint  
https://[My Domain Name].my.salesforce.com/services/data/v65.0/actions/custom/flow/[Flow API Name]  
-- Headers  
Content-Type: application/json  
Authorization: Bearer [Access Token]
```

> *Note: There must be a space between “Bearer” and the access token.*

3. Use the following as a sample body. `ticketIdVariable` is the variable name you configured as a new resource in the flow. By replacing `TID01359` on demand, you can target different ticket IDs.

```
{   
"inputs" : [ {  
   "ticketIdVariable" : "TID01359"  
   } ]   
}
```

4. Once everything is configured, it should look like this. The areas highlighted in red are the key points.

5. If there are no issues, click **Send**.

6. Confirm that you receive a `200` (success) response.

7. When you check the sends in the flow, you should see that the number of messages sent matches the count you saw when using the static condition in the segment. That means it worked correctly!!

## Value Created by These Features

By combining Dynamic Segments and Broadcast Flows, companies can:

- ✔ Deliver operational and service notifications in near real time
- ✔ Improve customer satisfaction
- ✔ Strengthen brand trust
- ✔ Reduce unnecessary inquiries and service cases

## Use Case Examples

### 1. Operational Notifications

- Immediate gate-change alerts for airline passengers
- Weather-related emergency announcements to all guests in a theme park

### 2. Service Notifications

- Notify affected postal codes before a network outage occurs
- Pre-notify households in scheduled inspection zones

## Conclusion

If your organization frequently needs fast, large-scale, real-time messaging, these are truly game-changing features.

- **Dynamic conditions can be replaced at send time**
- **Entire segments can be notified in real time**
- **Perfect for operational and service notifications**
- **Significant improvements to CX and operational efficiency**

While debugging and wait elements aren’t yet supported, the feature set is already powerful.

Also, remember that Broadcast Flows can be triggered as **subflows**, allowing parent flows to initiate them.

Try incorporating them into your operations.

That’s all for now.

Stay tuned for more Salesforce Marketing Cloud tips! 😎

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
