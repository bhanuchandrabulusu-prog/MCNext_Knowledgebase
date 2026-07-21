# SFMC Tips #15 : Batch Event API Allows Entry of up to 100 Contacts in Journey Builder with a Single…

**Source:** https://medium.com/@marketingcloudtips/batch-event-api-allows-entry-of-up-to-100-contacts-in-journey-builder-with-a-single-request-9655b12b72dd

---

# SFMC Tips #15 : Batch Event API Allows Entry of up to 100 Contacts in Journey Builder with a Single Request

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--9655b12b72dd---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--9655b12b72dd---------------------------------------)

2 min read

·

Dec 28, 2023

--

Photo by [Yurii Khomitskyi](https://unsplash.com/@ykhomi?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

In Salesforce Marketing Cloud’s Journey Builder, when entering contacts via API in commercial emails, previously, only one contact could be included per request. However, with the **Winter ’24 release**, a new Batch Event API has been introduced, enabling the entry of up to **100 contacts per request**.

**▶ Interaction: Enter Contacts into a Journey in Batches**

[## Salesforce Developers

### Create an entry event that asynchronously inserts a batch of subscribers into a journey.

developer.salesforce.com](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/enterContactsIntoJourneyInBatches.html?source=post_page-----9655b12b72dd---------------------------------------)

Please enter the information as follows. This sample serves as an example of entering three contacts with a single request.

```
--- Method  
POST  
  
--- Headers  
Content-Type: application/json  
Authorization: Bearer [Access Token]  
  
--- Endpoint  
[REST Base URL].rest.marketingcloudapis.com/interaction/v1/async/events  
  
--- Body (Sample)  
{  
  "eventDefinitionKey": "[Event Definition Key]",  
  "members": [  
    {  
      "contactKey": "[Subscriber Key 1]",  
      "data": {  
        "id": "[Subscriber Key 1]",  
        "email": "[Email Address 1]",  
        "firstName": "[First Name 1]",  
        "lastName": "[Last Name 1]"  
      }  
    },  
    {  
      "contactKey": "[Subscriber Key 2]",  
      "data": {  
        "id": "[Subscriber Key 2]",  
        "email": "[Email Address 2]",  
        "firstName": "[First Name 2]",  
        "lastName": "[Last Name 2]"  
      }  
    },  
    {  
      "contactKey": "[Subscriber Key 3]",  
      "data": {  
        "id": "[Subscriber Key 3]",  
        "email": "[Email Address 3]",  
        "firstName": "[First Name 3]",  
        "lastName": "[Last Name 3]"  
      }  
    }  
  ]  
}
```

As a result, multiple contacts are stored in the data extension with just one request, as depicted in the image.

Thank you for reading.

Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
