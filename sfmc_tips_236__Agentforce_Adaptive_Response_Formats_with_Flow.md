# SFMC Tips #236 : Agentforce: Adaptive Response Formats with Flow

**Source:** https://medium.com/@marketingcloudtips/agentforce-adaptive-response-formats-with-flow-2a0cb5012f16

---

# SFMC Tips #236 : Agentforce: Adaptive Response Formats with Flow

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--2a0cb5012f16---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--2a0cb5012f16---------------------------------------)

6 min read

·

Jan 17, 2026

--

Photo by [Steve Johnson](https://unsplash.com/@steve_j?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

In the previous article, we verified the display of **Adaptive Response Formats** using Salesforce Apex sample code.

[## SFMC Tips #235 : Agentforce: Adaptive Response Formats with Apex

### In the previous and the one before that articles, I introduced UI customization for Agentforce chat using “Custom…

medium.com](/@marketingcloudtips/agentforce-adaptive-response-formats-with-apex-65adccf18547?source=post_page-----2a0cb5012f16---------------------------------------)

This **Adaptive Response Formats** feature can be implemented not only with Apex, but also with **Flow**.  
Therefore, in this article, I will introduce how to **build it from scratch using Flow**.

The theme this time is **Jazz records**, which I personally love.  
When a user asks:

**“What products do you recommend?”**

the following flow will be implemented:

- Using **Rich Choice Response**  
  → Display products in a **carousel format**
- When one of the items is clicked  
  → Using **Rich Link Response**, display a **web page link with a text title and image**

![]()

![]()

## Setup Steps

※ Since the detailed steps were carefully explained in the previous article, this time I will focus only on the **important points**.

## 1. Prepare Object Fields

Prepare the following fields on the product object.  
 ※ Either a standard object or a custom object is fine.

- Name
- Description
- Link\_URL
- Image\_URL
- MIME\_Type

The naming of field names is optional, but it is important to use names that are **easy for the agent to understand semantically**.

As a sample, I registered **six products** as shown below.

- **Name**  
  A Love Supreme — John Coltrane
- **Description**  
  A spiritual jazz masterpiece expressing devotion and transcendence through a powerful four-part suite.
- **Link URL**  
  <https://www.discogs.com/release/15902627-John-Coltrane-A-Love-Supreme-The-Complete-Masters>
- **Image URL**  
  <https://i.discogs.com/8WOE9IZUwP-5BRLyFs1oix4oeJm3MuPSuElmyPHH7TU/rs:fit/g:sm/q:90/h:600/w:600/czM6Ly9kaXNjb2dz/LWRhdGFiYXNlLWlt/YWdlcy9SLTE1OTAy/NjI3LTE1OTk4OTQ5/MzMtMTY0OS5qcGVn.jpeg>
- **MIME Type**  
  image/jpeg  
  ※ MIME types were explained in the [previous article](/@marketingcloudtips/agentforce-adaptive-response-formats-with-apex-65adccf18547)

## 2. Register Trusted URLs

Register the URLs used this time as **Trusted URLs**.  
Without this, the service agent cannot use the link URLs or image URLs.

Register the following two URLs:

- <https://www.discogs.com> (for link URL)
- https://i.discogs.com (for image URL)

## 3. Create the Flow (Autolaunched Flow)

Create a new **Autolaunched Flow (no trigger)** and place a **Get Records** element.  
Select the Salesforce object that stores the products.  
(In my case, I am using “Product”.)

My filter condition is:

- Only records where the **MIME Type is populated**

This may not be necessary in some cases, so please configure it freely according to your use case.

Also, since **carousel display in Enhanced Chat v1 is limited to a maximum of 5 items**, limit the number of retrieved records to **5 in advance**.

> ***Important:*** *If you pass* ***6 or more items****, they will not display correctly.*

## 4. Create Output Resources

Store the retrieved records in a new resource called **productList**.  
Only store the **five fields prepared above**.

- **Name**
- **Description**
- **Link\_URL**
- **Image\_URL**
- **MIME\_Type**

> *Adding unnecessary fields can cause* ***ambiguity in the agent’s decision-making****.*

![]()

Create the resource with the following settings:

- **Data Type:** Record
- **Allow multiple values (collection):** ✔
- **Available for output:** ✔

Also, although it is not used this time, prepare an input variable **recordId (Text)**.

> *To use a Flow as an* ***Agent Action****, at least* ***one input and one output*** *are required.*

Once everything is ready, **activate the Flow**.

![]()

## Agentforce Configuration

For instructions on how to create a service agent and embed it into an external website, please refer to the following article.

[## SFMC Tips #221 : Agentforce: How to Implement a Service Agent Using Knowledge

### Salesforce partners implementing Marketing Cloud Next have likely noticed a growing trend: projects where Marketing…

medium.com](/@marketingcloudtips/sfmc-tips-221-agentforce-how-to-implement-a-service-agent-using-knowledge-ef7a9e0cdc6b?source=post_page-----2a0cb5012f16---------------------------------------)

[## SFMC Tips #222 : Agentforce: Deploying Service Agents to Your Website

### Previously, I wrote an article about how to install Agentforce on an external site (CloudPages in Marketing Cloud…

medium.com](/@marketingcloudtips/sfmc-tips-222-agentforce-deploying-service-agents-to-your-website-8b5f38c6b0b9?source=post_page-----2a0cb5012f16---------------------------------------)

[## SFMC Tips #193 : Agentforce: Deploying Service Agents on CloudPages (External Sites)

### In this article, I’ll explore how to embed the Agentforce Service Agent on an external website using CloudPages in…

medium.com](/@marketingcloudtips/agentforce-deploying-service-agents-on-cloudpages-external-sites-d4fb5edacb91?source=post_page-----2a0cb5012f16---------------------------------------)

## Permission Set Configuration

You must grant **Read access** to the object that stores the product records to the **service agent user**.

Create a permission set and make sure to assign it.

## Create a Topic

Open the created service agent and create a **new topic** with the following content.

### **Classification Description**

Handles inquiries related to searching for products, including gathering user requirements and presenting product options. For example, use this topic when the user says: “What product do you have?”

### **Scope**

My job is only to assist customers with searching for products by gathering user requirements and presenting available product options based on user requests.

### **Instructions**

Use the Get\_Products action to get product options.

## Add an Action

Add the following action to the topic.

- **Reference Action Type:** Flow
- **Reference Action:** Get Products Flow
- **Action Label:** Get Products
- **API Reference Name:** Get\_Products  
  (\*This name is also used in Instructions, so keep it consistent.)

## Agent Action Configuration

### Agent Action Instructions

Retrieves product records based on the user’s request.  
For each product, returns the product name, description, image URL, and link URL.  
Use this action when a user asks about available products or requests a product list.

### Loading Text

Getting product information…

### recordId (Input)

**Instructions:**  
The ID of the Salesforce record that contains the product information.

- Require input: ✘
- Collect data from user: ✘  
   （※ Not used this time）

### productList (Output)

**Instructions:**  
A list of products including the following fields: the product name, description, image URL, and link URL.

- Show in conversation (only): ✔

## Connected Messaging Settings

From the menu, open **Connection → Messaging**.  
Since **Adaptive Response Formats are a messaging-only feature**, configure them here.

Confirm that **Adaptive Response Formats are enabled**, and then **activate the agent**.

## Verification

After the setup is complete, verify it in chat.

When you ask:

**“What products do you recommend?”**

the products are displayed in a **carousel format**.

> *If they are displayed as plain text, check whether the Flow is limiting the results to* ***five or fewer items****.*

![]()

Then, when you select one product, a **Rich Link Response** with an integrated image and link is displayed.  
Success!!

![]()

## Conclusion

This time, using **Flow only**, we implemented Adaptive Response Formats from **carousel display → rich link display**.

Even without using Apex:

- Keep the data structure simple
- Properly control the number of displayed items and fields

By keeping these two points in mind, **Agentforce can still deliver a sufficiently rich UI experience**.

Start with familiar data and give it a try.

That’s all for this time.

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
