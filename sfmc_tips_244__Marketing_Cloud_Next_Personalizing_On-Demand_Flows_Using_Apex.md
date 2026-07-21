# SFMC Tips #244 : Marketing Cloud Next: Personalizing On-Demand Flows Using Apex

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-next-personalizing-on-demand-flows-using-apex-366692c7ce6a

---

# SFMC Tips #244 : Marketing Cloud Next: Personalizing On-Demand Flows Using Apex

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--366692c7ce6a---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--366692c7ce6a---------------------------------------)

8 min read

·

Feb 5, 2026

--

Photo by [Jonathan Castañeda](https://unsplash.com/@jonathecreator?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

With the **Winter ’26 new feature release** of **Marketing Cloud Next Growth & Advanced Edition**, a new flow type called **“On-Demand Flow”** was added.  
In a previous article, I introduced that this enables you to **instantly trigger contacts via REST API and send promotional/transactional messages**.

[## SFMC Tips #182 : Marketing Cloud Next: On-Demand Flows with REST API

### Photo by hesam Link on Unsplash

medium.com](/@marketingcloudtips/marketing-cloud-next-on-demand-flows-with-rest-api-fbef5c58804e?source=post_page-----366692c7ce6a---------------------------------------)

At the time of Winter ’26, **personalization using Data Graphs** was already possible, but there was a limitation:  
**you could not directly pass arbitrary additional information from the API**.

However, in the [**Spring ’26 release**](/@marketingcloudtips/marketing-cloud-next-spring-26-release-highlights-24c0c804b0cb), this limitation has been removed.  
You can now **pass additional data from the REST API and dynamically generate personalized messages**.

In this article, I would like to **pass personalized values to an On-Demand Flow**.

For example, suppose you have an order completion email like the following:

```
Subject: Your Order Confirmation  
  
Dear {{FirstName}} {{LastName}},  
Thank you very much for your order.  
  
We're pleased to confirm that your order has been successfully received.  
  
=============================  
  
Order Number  
{{OrderNumber}}  
  
Order Date  
{{OrderDate}}  
  
Item Details  
Item: {{ItemName}}  
Quantity: {{ItemQuantity}}  
Price: {{ItemPrice}} Yen  
  
Payment Method  
{{PaymentMethod}}  
  
Total Amount  
{{TotalAmount}} Yen  
  
==============================  
  
Your order will be shipped as soon as it is ready.  
We will notify you once it has been dispatched.  
  
If you have any questions, please feel free to reply to this email or contact our support team.  
  
Thank you for shopping with us.  
We look forward to serving you again.  
  
Best regards,  
Customer Support Team
```

For this implementation, we will **use Apex technology**, so we use an Apex class like the following.

- **Example Apex Class: OrderConfirmationContactService**

```
public without sharing class OrderConfirmationContactService {  
  
    @AuraEnabled public String LastName { get; set; }  
    @AuraEnabled public String FirstName { get; set; }  
    @AuraEnabled public String OrderNumber { get; set; }  
  
    @AuraEnabled public String ItemName { get; set; }  
    @AuraEnabled public String ItemQuantity { get; set; }  
    @AuraEnabled public String PaymentMethod { get; set; }  
  
    @AuraEnabled public String OrderDateYmdJp { get; set; }  
    @AuraEnabled public String OrderDateYmdSlash { get; set; }  
    @AuraEnabled public String ItemPriceFormatted { get; set; }  
    @AuraEnabled public String TotalAmountFormatted { get; set; }  
  
    private String orderDateRaw;  
    private String itemPriceRaw;  
    private String totalAmountRaw;  
  
    @AuraEnabled  
    public String OrderDate {  
        get { return orderDateRaw; }  
        set {  
            orderDateRaw = value;  
  
            OrderDateYmdJp = null;  
            OrderDateYmdSlash = null;  
  
            if (String.isBlank(orderDateRaw)) return;  
  
            Date d = Date.valueOf(orderDateRaw.substring(0,10));  
            DateTime dt = DateTime.newInstance(d, Time.newInstance(0,0,0,0));  
            OrderDateYmdJp = dt.format('yyyy年MM月dd日');  
            OrderDateYmdSlash = dt.format('yyyy/MM/dd');  
        }  
    }  
  
    @AuraEnabled  
    public String ItemPrice {  
        get { return itemPriceRaw; }  
        set {  
            itemPriceRaw = value;  
  
            ItemPriceFormatted = null;  
  
            if (String.isBlank(itemPriceRaw)) return;  
  
            ItemPriceFormatted = Decimal.valueOf(itemPriceRaw.replace(',', '')).format();  
        }  
    }  
  
    @AuraEnabled  
    public String TotalAmount {  
        get { return totalAmountRaw; }  
        set {  
            totalAmountRaw = value;  
  
            TotalAmountFormatted = null;  
  
            if (String.isBlank(totalAmountRaw)) return;  
  
            TotalAmountFormatted = Decimal.valueOf(totalAmountRaw.replace(',', '')).format();  
        }  
    }  
}
```

> ***Tip:*** *Dates and numbers must be processed in advance inside Apex, rather than formatting them in the email.*

- **Example Apex Test Class: OrderConfirmationContactServiceTest**

```
@IsTest  
private class OrderConfirmationContactServiceTest {  
  
    @IsTest  
    static void testFormatting() {  
        OrderConfirmationContactService s = new OrderConfirmationContactService();  
  
        s.OrderDate = '2026-02-05';  
        s.ItemPrice = '2000';  
        s.TotalAmount = '22000';  
  
        System.assertEquals('2026年02月05日', s.OrderDateYmdJp);  
        System.assertEquals('2026/02/05', s.OrderDateYmdSlash);  
        System.assertEquals('2,000', s.ItemPriceFormatted);  
        System.assertEquals('22,000', s.TotalAmountFormatted);  
    }  
}
```

> *Since many* ***Marketing Cloud Engagement users*** *may read this article, I will also explain the Apex class setup.*

## Steps to deploy an Apex class to Production

✅ Create in Sandbox and manually test for errors  
✅ Add both Apex class and Test class to a Change Set  
✅ Validate → Deploy in Production

```
Sandbox  
↓  
Create Change Set (Apex + Test)  
↓  
Production Validate  
↓  
Deploy
```

For creating a Marketing Cloud Next Sandbox and sending change sets, please refer to the following article if needed.

[## SFMC Tips #196 : Marketing Cloud Next: Testing with Sandbox

### With the Winter ’26 release of Marketing Cloud Next Growth & Advanced Edition, Salesforce introduced Sandbox…

medium.com](/@marketingcloudtips/marketing-cloud-next-testing-with-sandbox-22f23d92eef0?source=post_page-----366692c7ce6a---------------------------------------)

Below are the detailed steps.

## Apex Class Setup Procedure

### STEP 1: Sandbox (Development & Preparation)

First, open the Sandbox, go to Setup → **Apex Classes**, and click **New**.

Be sure to register the Production Apex class first.

> *If you try to register the test first, you will get an error saying the Production Apex class does not exist.*

Next, register the test class as well.

### STEP 2: Send from Sandbox → Production

Go to Setup → **Outbound Change Sets**, create a new change set, and add:

- Apex class
- Test Apex class

Upload it to the Production organization.

### STEP 3: Validate in Production

Log in to Production → Setup → **Inbound Change Sets**, open the target change set, and click **Validate**.

Run local tests.

### STEP 4: Deploy in Production

Once validation succeeds, click **Deploy**.

Run local tests again.

Deployment is complete.

This explanation was a bit long, but now the Apex class has been successfully registered in Production.

## Creating Email Content

Paste the email template above into a **Paragraph** block.

This time, we will use the newly introduced **“Apex Class Data Provider”** (available from Spring ’26 onward) as the data source, so add a new data source.

Select the Apex class created earlier.

Next, replace the placeholders in the email with fields from the **Apex Class Data Provider**.

The fields defined in the Apex class will be displayed.

After setting all merge fields, save and publish the email.

> *Before publishing, change it to “Transactional Email”.*

## Create an On-Demand Flow

Create an **On-Demand Flow** from a new flow.

After opening the flow:

First, add a **Variable** resource. You can leave it as is.

- The API Name will be used later in the REST API body
- Data Type: Apex-Defined
- Apex Class: select the class created earlier
- Check “Available for input”

Next, configure the email, then save and activate the flow.

> *The Flow API Name is used in the REST API endpoint.*

After configuring the flow, open Properties → **Edit Access**.

Grant flow access permissions to the profile that executes the REST API.

## Executing the REST API

Finally, execute the REST API.  
Please refer to the following article for details.

[## SFMC Tips #181 : Marketing Cloud Next: Obtaining an Access Token for the REST API

### Previously, I wrote an article on how to obtain an access token when using the REST API in Marketing Cloud Engagement.

medium.com](/@marketingcloudtips/marketing-cloud-next-obtaining-an-access-token-for-the-rest-api-156eca392584?source=post_page-----366692c7ce6a---------------------------------------)

[## SFMC Tips #182 : Marketing Cloud Next: On-Demand Flows with REST API

### Photo by hesam Link on Unsplash

medium.com](/@marketingcloudtips/marketing-cloud-next-on-demand-flows-with-rest-api-fbef5c58804e?source=post_page-----366692c7ce6a---------------------------------------)

① Obtain an access token  
② Execute the REST API below

> *“OrderInfo” corresponds to the Variable API Name created in the flow.*

```
--- Method  
POST  
  
--- Endpoint  
[MyDomain].my.salesforce.com/services/data/v65.0/actions/custom/flow/[Flow API Name]  
  
--- Headers  
Content-Type: application/json  
Authorization: Bearer [Access Token]  
  
--- Body (Sample)  
{  
  "inputs": [  
    {  
      "EmailAddress": "xxxxxxxxxxxxxxxxxxx@gmail.com",  
      "IndividualId": "003A800000ODmp1IAD",  
      "OrderInfo": {  
        "LastName": "Takahashi",  
        "FirstName": "Miyu",  
        "OrderNumber": "ORD-0001",  
        "OrderDate": "2026-02-05",  
        "ItemName": "Sample Item",  
        "ItemQuantity": "1",  
        "ItemPrice": "2000",  
        "PaymentMethod": "Credit Card",  
        "TotalAmount": "2200"  
      }  
    }  
  ]  
}
```

This triggers the flow.

Checking the sent email, it was successfully personalized. Success.

![]()

## Summary

Until now, personalization using Data Graphs was possible, but there was a limitation:  
**real-time values could not be directly passed during API execution**, making it difficult to flexibly customize instant transactional notifications such as:

- Order completion
- Payment completion
- Reservation confirmation

However, starting with Spring ’26:

✅ You can directly pass arbitrary values via REST API  
✅ You can pre-format dates, amounts, and values in Apex  
✅ You can send immediately with On-Demand Flow

By combining these:

**“Deliver the necessary data, personalized, at that exact moment.”**

This enables more practical and real-time communication.

Especially suitable for:

- Order confirmation emails
- Payment notifications
- Shipping notices
- Reservation confirmations
- One-time information alerts

These transactional messages work extremely well with this approach.

By combining **Marketing Cloud Next** and the **Salesforce Platform (Apex)**, it is no longer just an email delivery tool, but can be utilized as an **application platform tightly integrated with business logic**.

Please try **On-Demand Flow × Apex personalization** in your own environment.

That’s all for this time.

Stay tuned for more Salesforce Marketing Cloud tips! 😎

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
