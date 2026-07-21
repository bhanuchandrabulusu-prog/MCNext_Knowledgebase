# SFMC Tips #238 : Marketing Cloud Next: Personalization × Agentforce

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-next-personalization-agentforce-1741523f070f

---

# SFMC Tips #238 : Marketing Cloud Next: Personalization × Agentforce

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--1741523f070f---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--1741523f070f---------------------------------------)

5 min read

·

Jan 21, 2026

--

Photo by [Branden Skeli](https://unsplash.com/@branden_skeli?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

There is a reason why I have recently been writing a series of articles focused on Agentforce.  
It is because I ultimately wanted to arrive at *this point*.  
In this article, I would like to tie together what the previous efforts were aiming toward.

Although I personally do not consider this to be a completed form yet, I was able to successfully display the results shown in **Personalization Points** in Salesforce Personalization on a service agent.

These Personalization Points are deeply connected to the personalization recommender mechanism used in **repeater components** in Marketing Cloud Next.

Therefore, in this article, I am challenging an implementation in which the *exact same recommendation results* displayed in repeater components are returned when a customer asks the service agent,  
 “What products do you recommend?”

For details on the personalization recommender mechanism itself, please refer to the article below.  
The content of this article is verified using an SDO environment where that mechanism has already been implemented.

[## SFMC Tips #177 : Marketing Cloud Next: Repeater Component and Recommender

### In Marketing Cloud Next (Marketing Cloud Growth & Advanced Edition), you can take advantage of the Recommender feature…

medium.com](/@marketingcloudtips/marketing-cloud-next-repeater-component-and-recommender-fb41b9c72ad0?source=post_page-----1741523f070f---------------------------------------)

## Verifying the Displayed Results

Now, let’s look at the actual behavior (display results).

Person A has an attribute indicating a preference for **Rock**, so Rock-genre products are delivered as an email with repeater components using personalization recommender technology.

On the other hand, in the Agentforce chat, a carousel display using **Adaptive Response Formats** is used in Enhanced Chat v1.  
You can also confirm that the products returned in response to the question “**What products do you recommend?**” are in the same order as in the email.

![]()

Next is the case of Person B.  
Person B has an attribute indicating a preference for **Jazz**, so Jazz-genre products are sent by email.

Likewise, in the Agentforce chat, it was confirmed that the products are displayed in exactly the same order as the email version.

![]()

## Implementation Key Points

During this implementation, several important points became clear.  
Here, I will focus on sharing those points.

First, **dataspace** and **IndividualId** are required.

- dataspace can basically be a fixed value (for example: `default`)
- IndividualId must retrieve customer information depending on whether it is during a conversation or pre-chat, and pass a Salesforce ID (such as ContactId)

```
Map<String, Object> context = new Map<String, Object>();  
context.put('dataspace', 'default');  
context.put('individualId', contactId);  
  
Map<String, Object> body = new Map<String, Object>();  
body.put('context', context);  
body.put(  
     'personalizationPoints',  
     new List<Object>{  
         new Map<String, Object>{  
             'name' => 'PersonalizationRecommendations_9a7f'  
         }  
     }  
);
```

In addition, **personalization points** must be explicitly specified.  
In this case, to match the email conditions exactly, the personalization point configured in the email with repeater components was reused as is.

What is specified here is the **API reference name**.  
In this example, it is `PersonalizationRecommendations_9a7f`.

![]()

Next is the creation of a **Named Credential**.  
In the External Credential settings, you can choose between “Authentication Required” and “No Authentication”, but please follow the Authentication Required configuration as shown in the diagram above.  
In this case, I configured it as **No Authentication**.

At the same time, create a permission set, and for **External Credential Principal Access**, it is recommended to grant access to both:

- the execution user
- the agent user

The Data Cloud tenant endpoint can be found in the following location.  
This is what you configure in the Named Credential.

When actually retrieving content, use the following endpoint:

- [personalization/v1/decisions](https://developer.salesforce.com/docs/marketing/einstein-personalization/guide/decisioning-api-request-personalization.html)

```
HttpRequest req = new HttpRequest();  
req.setMethod('POST');  
req.setHeader('Content-Type', 'application/json');  
req.setHeader('Accept', 'application/json');  
req.setEndpoint('callout:Personalization/personalization/v1/decisions');  
req.setBody(JSON.serialize(body));
```

In this display, Product information is specified using the API reference names of each field in the **Goods Product DMO**.  
These are configured in the “**Item Data Graph**” and are linked on the “**Recommenders**” side.

```
ChoiceItem c = new ChoiceItem();  
c.name        = asString(item.get('ssot__Name__c'));  
c.imageUrl    = asString(item.get('Image_URL__c'));  
c.linkUrl     = asString(item.get('Link_URL__c'));  
c.mimeType    = asString(item.get('MIME_Type__c'));  
c.description = asString(item.get('ssot__Description__c'));  
c.price = formatPriceYen(item.get('Price_Text__c'));
```

> *If you understand how the personalization recommender mechanism works, this part should be relatively easy to grasp. (*[*more info*](/p/fb41b9c72ad0)*)*

From a design perspective, the key point is to design the response with the assumption that it will ultimately be returned using “**Adaptive Response Formats**”. For details, please refer to the article below.

[## SFMC Tips #236 : Agentforce: Adaptive Response Formats with Flow

### In the previous article, we verified the display of Adaptive Response Formats using Salesforce Apex sample code.

medium.com](/@marketingcloudtips/agentforce-adaptive-response-formats-with-flow-2a0cb5012f16?source=post_page-----1741523f070f---------------------------------------)

In addition, when returning six or more items in Adaptive Response Formats, responses become unstable, so it is mandatory to limit the maximum to five items.

```
Integer maxItems =  
    (inRec != null && inRec.maxItems != null && inRec.maxItems > 0)  
        ? inRec.maxItems  
        : 5;
```

> ***Note:*** *After saving the Apex class settings, do not forget to grant* ***Apex Class Access*** *to the service agent.  
> If you forget this, the agent will not be able to use the Apex class.*

## Conclusion

Although this has turned into a rough report consisting mostly of excerpts, I believe I was able to convey the overall picture and the key points.  
Even if I were to publish the complete version of the code, it would only work in my own environment, so this time I limited the explanation to the essentials.

I believe that **service agents are part of marketing tools**.  
By marketers themselves stepping into this area, they can add even greater value to Marketing Cloud Next.  
I encourage you to research and experiment with it.

Articles related to Agentforce are summarized below:

[## List: Agentforce | Curated by Nobuyuki Watanabe @marketingcloudtips | Medium

### Agentforce · 22 stories on Medium

medium.com](/@marketingcloudtips/list/agentforce-bd934e94ef20?source=post_page-----1741523f070f---------------------------------------)

That’s all for this time.

Stay tuned for more Salesforce Marketing Cloud tips! 😎

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
