# SFMC Tips #182 : Marketing Cloud Next: On-Demand Flows with REST API

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-next-on-demand-flows-with-rest-api-fbef5c58804e

---

# SFMC Tips #182 : **Marketing Cloud Next: On-Demand Flows with REST API**

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--fbef5c58804e---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--fbef5c58804e---------------------------------------)

5 min read

·

Oct 5, 2025

--

Photo by [hesam Link](https://unsplash.com/@hesamjr?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

In the [Winter ’26 release](/@marketingcloudtips/marketing-cloud-next-winter-26-release-highlights-81240775f843) of Marketing Cloud Next Growth & Advanced Edition, a new type of **On-Demand Flow** has been introduced, enabling you to instantly trigger contacts and deliver messages through the **REST API**.

With this enhancement, **messages can now be delivered within about 30 seconds after an event occurs**, significantly reducing the time lag that had previously been an issue.

When creating a new flow, you can also assign a **Data Graph**, which can be used in decision splits and exit conditions, making personalization possible.

> *At the time of Winter ’26,* ***personalization using Data Graphs*** *was already possible, but there was a limitation:****you could not directly pass arbitrary additional information from the API****.*
>
> *However, in the* [***Spring ’26 release***](/@marketingcloudtips/marketing-cloud-next-spring-26-release-highlights-24c0c804b0cb)*, this limitation has been removed.  
> You can now* ***pass additional data from the REST API and dynamically generate personalized messages****. This is explained in the following article.*

[## SFMC Tips #244 : Marketing Cloud Next: Personalizing On-Demand Flows Using Apex

### With the Winter ’26 new feature release of Marketing Cloud Next Growth & Advanced Edition, a new flow type called…

medium.com](/@marketingcloudtips/marketing-cloud-next-personalizing-on-demand-flows-using-apex-366692c7ce6a?source=post_page-----fbef5c58804e---------------------------------------)

In this article, I’ll walk you through how to actually trigger this **On-Demand Flow** using “Talend API Tester”. Of course, the same process can also be carried out with “Postman” or similar tools.

> *To follow along, you’ll need to obtain an* ***access token*** *available on the Salesforce Platform. I’ve outlined the detailed steps in the following article, so please check that out.*

[## SFMC Tips #181 : Marketing Cloud Next: Obtaining an Access Token for the REST API

### Previously, I wrote an article on how to obtain an access token when using the REST API in Marketing Cloud Engagement.

medium.com](/@marketingcloudtips/marketing-cloud-next-obtaining-an-access-token-for-the-rest-api-156eca392584?source=post_page-----fbef5c58804e---------------------------------------)

## **Steps to Configure an On-Demand Flow**

1. Open a new flow and search for **On-Demand Flow**.

2. Select a **Data Space** and a **Data Graph**. In this example, I’ll trigger based on an Individual ID, but you can also use your existing Data Graphs built on Unified Individual IDs.

3. A simple flow like the one below will open. Start configuring it.

4. Once you’ve set up the canvas and named the flow, save it and click the gear icon.

5. Copy and make a note of the **Flow API Name** shown here, as you’ll need it later.

6. Finally, activate the flow.

## **Steps to Configure Talend API Tester**

1. Now let’s run the REST API!!  
Before you start, make sure you have the following three items prepared:

- **Access Token** (If you haven’t obtained one yet, see [here](/@marketingcloudtips/marketing-cloud-next-obtaining-an-access-token-for-the-rest-api-156eca392584))
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

3. Next, here’s a sample request body:

```
{   
"inputs" : [ {  
   "EmailAddress" : "XXXXXXXXXXXXXXX@XXXXXXXX",  
   "IndividualId" : "XXXXXXXXXXXXXXXXXX"  
   } ]   
}
```

> *Note: Use an 18-digit Salesforce ID for the* ***IndividualId****.  
>  If you enter an ID that does not correspond to an existing CRM record, an error will occur during flow execution.*
>
> *Also, the email will be sent to the address specified here, so even if the CRM record does not have an email address, the send itself is still possible.  
>  However, this email address follows the consent management settings — if the recipient has opted out through communication subscriptions, the email will not be sent.*

4. Once your setup is complete, it should look like the example below. The red box highlights the key areas.

5. If everything looks good, click **Send**.

6. Confirm that you receive a **200 (Success)** response.

7. Within about 30 seconds, the email will be delivered. As long as the conditions are correctly configured, “repeater components” will also execute as expected.

## Conclusion

This really is a **game-changing feature!** For Marketing Cloud Engagement users, it may remind you of the **API Event entry source** in Journey Builder.

It can be used for both **promotional emails** and **transactional emails**. However, note that transactional emails are **not delivered faster** just because they’re transactional.

From an analytics perspective, **flow canvas reporting** works as usual, and the data is also stored in the **Email Engagement DMO**. You can use it just like any other feature — rest assured.

That’s it for this article.

Stay tuned for more Salesforce Marketing Cloud tips! 😎

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
