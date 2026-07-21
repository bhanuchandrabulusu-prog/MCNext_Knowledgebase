# SFMC Tips #150 : Marketing Cloud Next: Custom Event-Triggered Flow

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-next-custom-event-triggered-flow-7ae54b7798b5

---

# SFMC Tips #150 : Marketing Cloud Next: Custom Event-Triggered Flow

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--7ae54b7798b5---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--7ae54b7798b5---------------------------------------)

7 min read

·

Jul 17, 2025

--

Photo by [Jordan Whitfield](https://unsplash.com/@whitfieldjordan?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

With the Summer ’25 new feature release of Marketing Cloud Next Growth & Advanced Editions, it became possible to create custom event-triggered flows by leveraging Salesforce Personalization **“Engagement Signals”.** This makes it possible to trigger flows when configured conditions are met.

Standard event-triggered flows that existed previously include actions such as email opens and link clicks. However, with the newly available custom event-triggered flows, the following use cases can now be considered.

- Create a ToDo when a text link on a website is clicked
- Send a company introduction email when a PDF download button is clicked
- Send an order confirmation email when a purchase is completed
- Send a reservation confirmation email when a reservation is completed

**Examples of signals provided by Salesforce**:

- [Product View](https://help.salesforce.com/s/articleView?id=mktg.persnl_es_examples_prod_view_engmt.htm&language=en_US&type=5)
- [Product Click](https://help.salesforce.com/s/articleView?id=mktg.persnl_es_examples_prod_click_engmt.htm&language=en_US&type=5)
- [Add To Cart](https://help.salesforce.com/s/articleView?id=mktg.persnl_es_examples_add_to_cart_engmt.htm&language=en_US&type=5)
- [Product Order](https://help.salesforce.com/s/articleView?id=mktg.persnl_es_examples_product_order_engmt.htm&language=en_US&type=5)
- [Knowledge Article Click](https://help.salesforce.com/s/articleView?id=mktg.persnl_es_examples_article_click_engmt.htm&language=en_US&type=5)

## Considerations When Configuring Signal Definitions

- With the Summer ’26 new feature release, when selecting DMOs used for signals, **not only Engagement DMOs but also Profile DMOs can now be selected.**
- In Salesforce Personalization itself, signals are designed so that, in addition to the fields of the selected Engagement DMO (Primary DMO), fields from all related DMOs (Secondary DMOs) can also be used in conditions.
- However, to use this in event-triggered flows within Marketing Cloud Growth & Advanced Editions, it is necessary to check **“Enable this engagement signal for use in flows”.** In this case, only fields from the Primary Engagement DMO become available.
- This has been improved in the Summer ’26 new feature release, allowing **one additional related DMO** to be added. Related DMOs can only be configured when the relationship between the Primary DMO and Secondary DMO is **Many:1 or 1:1. (1:Many relationships are not supported.)**
- Up to **10 fields** from the added related DMO can be used in signal definitions and filter conditions.
- For example, it is now possible to select the Website Engagement DMO (Primary DMO) together with the Individual DMO (Secondary DMO), trigger a flow when a document request PDF is downloaded, and reference the customer’s Title field so that emails are triggered only for people with specific job titles.

## Configuration Steps

1. Select the “Engagement Signals” tab and click “New”.

2. To make the engagement signal available for use in flows, make sure to check this checkbox. Select the DMO for the target engagement category and click “Next”.

*Note: As mentioned earlier, checking this checkbox limits available fields from related DMOs. However, when using this in Marketing Cloud Next,* ***enabling the checkbox is mandatory.***

3. On the next page, in this example the Web Engagement DMO is selected, resulting in the following input example.

- **User Identifier:** Individual
- **Timestamp Identifier:** Engagement Date Time
- **Item Identifier:** Blank
- **Event Identifier:** Website Engagement ID

Item Identifier is an identifier used by the signal to better distinguish engagement activity. For example, a specific “Product SKU” used to identify a particular engagement.

Event Identifier allows grouping of the same engagement and exclusion of duplicate records.

Reference: If **“Enable this engagement signal for use in flows”** is not checked, the next screen requires configuration of how events are counted.

**Option Descriptions**

- **Count events individually (default)**Even if the same user performs the same action multiple times, each occurrence is recorded as a separate event.  
  Example: If the same person clicks the same email multiple times, each click is counted separately and reflected in the total click count.
- **Count repeated events together (using additional fields)**By grouping events using specific conditions (such as User ID or bulk email send ID), events can be counted as a single grouped event. Up to **three fields** can be added.  
  Example: Even if one user clicks multiple times within the same email, those clicks can be counted as a single click event. (For example, grouped by User ID + Email ID + Event Type.)

4. Next, define filters in order to better identify specific engagement activity.

For example, it is possible to trigger only when there is a history of viewing a specific web page. In this example, the trigger is configured when the page **“Product\_Pricing\_Page”** is viewed.

**Operators Available for Filters**

- For both text fields and date fields, the only available operators are:  
  **“Equals (Not Equals is unavailable for date fields) / Has Value / No Value”.**
- For numeric fields (including currency), in addition to:  
  **“Equals (Not Equals) / Has Value / No Value”,**the following are also available:  
  **“Less Than / Less Than or Equal / Greater Than or Equal / Greater Than”.**

**Filter Conditions for Text Fields**

- **English uppercase and lowercase characters are treated as case-sensitive exact matches.**
- Japanese values such as “商品価格表” also trigger successfully.
- If spaces exist between words such as **“Product Pricing Page”, the trigger will not work.** Use a single-word format such as **“Product\_Pricing\_Page”.** “Product-Pricing-Page” is not treated as a single word.

*Although AND conditions and OR conditions can be configured,* ***complex combinations mixing AND and OR conditions are not supported.*** *If using AND conditions, all conditions become AND. If using OR conditions, all conditions become OR.*

5. Finally, decide the signal name and save to complete the configuration.

**Editing Restrictions and Deletion Method**

- **Once a signal is created, its definition and filters cannot be edited.** To delete and recreate it, the related flow must first be deactivated, and then the flow itself must also be deleted.

6. Confirmed that it also appears in the Event Library of event-triggered flows.

7. Create and execute a flow that actually creates a ToDo.

8. When the Product Pricing Table link on the landing page was clicked, a ToDo indicating that the existing lead clicked the pricing table was created after approximately **2 to 15 minutes.** Success.

**About Trigger Time Lag**

- Normally, there is a delay of approximately **2 to 15 minutes** between the occurrence of the event and the trigger execution. The relevant engagement data must first be stored in the Engagement DMO.
- In rare cases, it may not trigger within 2 to 15 minutes and may appear stuck, then suddenly trigger several hours later.

**About the Email Address Used for Sending**

Regarding this sending email address, the Spring ’26 new feature release introduced the ability to specify the source used for retrieving contact points.

- ① If included in the Primary DMO, retrieve directly from the event data
- ② Retrieve from the Data Graph

*※ In case ② is selected,* ***emails are sent to all email addresses linked to the Unified Individual. This behavior is by design.***

The flow automatically retrieves contact points based on the selected method. This ensures that messaging actions are executed reliably, even for newly created person records or records currently under data processing.

**More Detailed Event Trigger Configuration Available (Summer ’26 and Later)**

With the Summer ’26 new feature release, it became possible to configure more detailed trigger conditions using fields from the Primary DMO. To configure trigger conditions, select **“Add Condition”** in the **“Additional Criteria”** section of the Start element.

Additionally, by defining re-entry conditions, it is now possible to flexibly control whether the same user can enter the flow again.

The following controls are available:

- **Always**: Allow re-entry every time the event occurs
- **After completion**: Allow re-entry only after the flow completes
- **Never**: Execute only once (re-entry not allowed)

## Conclusion

This is just my personal interpretation, but because the term “**Engagement Signals**” sounds somewhat unfamiliar, it may feel like a completely new and special feature. However, in reality, **since Data Cloud-triggered flows do not include major marketing-related elements such as “Send Email Message,” it becomes much easier to understand when viewed simply as a mechanism that compensates for those missing capabilities through another flow**.

Fundamentally, the concept is simply that when data enters a DMO, records matching configured conditions are triggered.

At first, it may feel slightly difficult to understand, but by actually working with it, you will gradually develop a sense of:

- what types of scenarios it should be used for
- how to design it in a manageable way

My recommendation is to start with small experiments and gradually become familiar with it.

That’s all for this time.

Stay tuned for more Salesforce Marketing Cloud tips! 😊

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
