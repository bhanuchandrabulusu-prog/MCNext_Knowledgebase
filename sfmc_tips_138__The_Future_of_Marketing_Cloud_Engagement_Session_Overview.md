# SFMC Tips #138 : The Future of Marketing Cloud Engagement Session Overview

**Source:** https://medium.com/@marketingcloudtips/the-future-of-marketing-cloud-engagement-session-overview-2794b9b3e83e

---

# SFMC Tips #138 : The Future of Marketing Cloud Engagement **Session Overview**

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--2794b9b3e83e---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--2794b9b3e83e---------------------------------------)

9 min read

·

Jun 13, 2025

--

The highly anticipated session, **“The Future of Marketing Cloud Engagement”**, which was also a personal highlight of mine at Connections 2025 (CNX 25), took place on June 12, 2025, at 11 PM JST.

### On-Demand Videos are now available on Salesforce+

[## Salesforce+ The Future of Marketing Cloud Engagement

### Step into the future of engagement. Learn about three new ways to supercharge your customer journeys with your expanded…

www.salesforce.com](https://www.salesforce.com/plus/experience/connections_2025/series/marketers_at_connections_2025/episode/episode-s1e5?source=post_page-----2794b9b3e83e---------------------------------------)

To start, as you may already know, the release of **Marketing Cloud Next** was announced during the main keynote at Connections 2025.

[## Salesforce Ends the Era of 'Do-Not-Reply' Marketing with Marketing Cloud Next

### The first full-funnel agentic marketing solution that turns every channel into a two-way conversation - and every…

www.salesforce.com](https://www.salesforce.com/news/stories/marketing-cloud-next-announcement/?source=post_page-----2794b9b3e83e---------------------------------------)

In this session, three new features aimed at revolutionizing the customer experience from the perspective of **Marketing Cloud Engagement** were unveiled. These announcements were exciting and highly inspiring, especially for current Marketing Cloud Engagement users. In this article, I will review these latest updates from my perspective.

\*It is important to note that, as the session title suggests, these features represent **future possibilities** and are not immediately available. Additionally, there is no guarantee that they will be implemented.

The session was organized into the following three themes:

1. **Measure the impact journeys have on your business goals**
2. **Orchestrate cohesive experiences across journeys**
3. **Prioritize the most effective journey for each individual**

At first glance, the connection between these themes and the new features announced may seem a bit unclear. However, each theme represents significant enhancements or improvements closely tied to existing capabilities, including:

1. **Campaigns**
2. **Flows**
3. **Agentforce**

## 1. Measuring the Impact of Journeys on Business Goals

This theme primarily emphasized the significance of the **Campaign** functionality within Marketing Cloud Next. The key points of the announcement were as follows:

How extensively are you leveraging the campaign features in the current Marketing Cloud Engagement? As many of you know, the existing campaign functionality is somewhat legacy-oriented. This has led many users to experience usability challenges, especially when integrating it with **Journey Builder** for sending communications.

With the introduction of Marketing Cloud Next, the integration between **Marketing Cloud Engagement** and **Marketing Cloud Next** will be realized. This integration will enable the incorporation of journeys built in Journey Builder into campaigns within Marketing Cloud Next, facilitating a more effective analysis of the impact journeys have on business goals.

### Marketing Cloud Next Campaigns Page

The following demo slides showcase the campaign pages within Marketing Cloud Next. Notice the frequent appearance of the term “Journey” throughout these pages. Moreover, the third slide explicitly displays the phrase **Open Journey**, signifying a seamless integration of journeys on the Marketing Cloud Next platform.

### Marketing Performance Analysis with Tableau Next

Campaigns in Marketing Cloud Next are equipped with advanced analytical capabilities powered by **Tableau Next**. This enables detailed performance measurement at the campaign level using the following data sources:

- **Journey initiatives** from Marketing Cloud Engagement
- **Flow-based campaign initiatives** from Marketing Cloud Next

Here are examples of the marketing performance analysis screens:

### Incorporating Journeys into Campaigns

A demonstration was also provided on how to incorporate journeys into campaigns. A new feature allows users to directly add journeys to campaigns within Marketing Cloud Next during the **journey validation phase**. This streamlined process ensures that journeys can be seamlessly linked to campaigns without the risk of omission.

### Relationship with Existing Campaigns

This raises an important question: how does this new integration affect the existing campaigns in Marketing Cloud Engagement? Conversely, what happens to existing journeys that do not utilize any campaign functionality? Unfortunately, the session did not address these finer details, leaving room for future clarification.

## 2. Orchestrating Cohesive Experiences Across Journeys

The next theme delves into the orchestration between **Flows** and **Journeys**, bringing a new level of flexibility to creating marketing and customer experience scenarios.

With this latest feature, you can now **trigger a Flow from Journey Builder** or, conversely, **trigger a Journey from Flow**. This enhancement enables seamless integration between marketing processes and customer experiences, fostering a cohesive journey.

> Iain McElroy pointed out that Core Flow and MCE had already been integrated in a similar way before, so I’d like to mention that as well. Thank you.  
>  [https://medium.com/p/fcbb013ffc55](/p/fcbb013ffc55)

### Journey Event Triggers

Take a look at the diagram below. The newly introduced **Journey Event Trigger** offers three distinct types of triggers:

**1. Entry Journey**

- Triggers a Flow when a contact enters a journey.

**2. Exit Journey**

- Triggers a Flow when a contact exits a journey.

**3. Goal Met**

- Triggers a Flow when a contact meets a defined goal.

These triggers allow specific actions within a journey to automatically activate a Flow, ensuring smooth coordination across your marketing initiatives.

### Demonstration Use Case

During the session, a demo showcased a scenario where contacts who achieved a goal triggered a Flow. The Flow executed subsequent actions and sent the contacts into a new journey, activating an entry trigger.

**1. Configuring an Event-Triggered Flow**

- Create a Flow and configure a new **Journey Event Trigger**.

**2. Selecting Journey Goals**

- Set the goal conditions for the relevant journey.

**3. Placing Conditional Logic**

- Use decision elements to branch processes based on contact attributes or states.

**4. Branching Based on Ratings**

- Distribute contacts to different paths depending on their ratings (e.g., engagement scores).

**5. Sending Contacts to a Journey**

- Use the “Send to Journey” element in each path to direct contacts to corresponding journeys.

### Value of These New Capabilities

Such workflows have often been challenging to implement in the existing Journey Builder. For example, automatically transitioning contacts based on state changes to subsequent actions in a Flow or a new journey typically required manual intervention or intricate configurations.

This new functionality extends the capabilities of current **Marketing Cloud Engagement**, offering robust tools to create more complex and seamless customer experiences. It represents a significant leap forward in orchestrating comprehensive and adaptive marketing journeys.

## 3. Prioritizing the Optimal Journey for Each Customer

The final theme highlighted the integration of **Agentforce** with **Marketing Cloud Engagement**, showcasing the transformative potential of the newly introduced **Marketing Cloud Orchestration Agent**. This innovation significantly reduces the time and complexity involved in creating sophisticated marketing scenarios.

### Features of the Marketing Cloud Orchestration Agent

This agent streamlines **automation** and **content creation** by enabling the following actions:

**1. Evaluation Journey**

- Guide the agent in analyzing a customer’s current journey status and determining if adjustments or optimizations are needed to improve engagement and conversion rates.

**2. Trigger Journey Entry Event**

- Instructs the agent to recognize and trigger customer entry into the appropriate journey, using behavior-based criteria or campaign logic.

**3. Create Content**

- Allows the agent to draft tailored email or SMS content using GenAI, drawing from your brand tone, customer data, and campaign goals.

**4. Send Copy to Data Extension**

- Sends generated content to the appropriate Data Extension, ensuring it’s available for personalization and delivery across selected channels.

These capabilities greatly enhance personalization, making the agent an invaluable asset for elevating customer experiences.

### Demonstration Example of Agentforce

Below are the steps demonstrated to configure and utilize the Marketing Cloud Orchestration Agent within Agentforce.

**1. Selecting an Agent Template**

- Open the **Agent Builder** and select the newly added **Marketing Cloud Orchestration Agent** template.

**2. Reviewing Topics and Actions**

- Review the default topics and actions included with the template.

**3. Configuring Basic Settings**

- Define the agent’s purpose and set other foundational parameters.

**4. Choosing a Data Library**

- Specify the data library that the agent will use for its operations.

**5. Selecting Journeys**

- Choose up to five journeys the agent will orchestrate and input details for content areas that require automated generation.

**6. Initiating an Event-Triggered Flow**

- Launch a Flow and construct an event-triggered flow.

**7. Choosing Actions**

- Configure actions within the event-triggered flow and select the Marketing Cloud Orchestration Agent created earlier.

**8. Placing the Agent**

- Add the selected agent to the flow to finalize the setup.

### Example Use Case

The Agentforce integration enables the creation of flows like:

- **Branching Conditions:** Determine whether a customer should join a follow-up campaign or transition to a promotional journey post-purchase.
- **Optimized Delivery:** Select the appropriate journey for each branch and execute tailored actions.

### Benefits of This Integration

- **Streamlined Scenario Creation:** Automates complex decision-making and configuration.
- **Enhanced Customer Experience:** Utilizes real-time data to deliver personalized experiences.
- **Increased Team Productivity:** Dramatically reduces the time marketers spend on content creation and scenario development.

By leveraging these features, **Marketing Cloud Engagement** expands its potential, enabling highly sophisticated and impactful customer engagement strategies.

## Closing Thoughts

How did you find this overview?

To speak candidly, while the announcements highlight a promising direction toward “integration,” the practical application of this connectivity remains largely limited to **Journey Builder** at this stage. It still feels like a work in progress, and calling it a fully unified ecosystem seems premature.

### Challenges Across the Three Themes

**1. Measuring the Impact of Journeys on Business Goals**

- The position and role of existing journeys in Marketing Cloud Engagement remain unclear. It’s also uncertain how deeply integrated other tools beyond Journey Builder will be.

**2. Building Consistent Experiences Across Journeys**

- This functionality might be highly dependent on specific use cases. Not all companies may find value in this, especially in scenarios where complex journey designs aren’t necessary. The implementation costs might outweigh the benefits for simpler use cases.

**3. Prioritizing Optimal Journeys for Each Customer**

- Fully leveraging Agentforce requires substantial resources and a mature marketing framework. For companies currently using Marketing Cloud Engagement as a standalone solution, this might appear as an optional rather than essential feature for now.

## The Future of Marketing Cloud Engagement

That said, one significant takeaway from **Connections 2025 (CNX 25)** is the reassurance that Marketing Cloud Engagement is not being discontinued in favor of Marketing Cloud Next. This announcement alleviates concerns and represents a positive step forward.

**Marketing Cloud Next** could be viewed as an **extension** of Marketing Cloud Engagement rather than a replacement. This positioning allows for gradual upgrades and extensions, creating a scalable and adaptable foundation to meet the diverse needs of various companies. For now, this framing seems to make the most sense.

## Conclusion

While this session provided an essential glimpse into the future direction of Marketing Cloud, it’s clear that not all solutions presented will be immediately actionable for every business. Even so, the focus on scalability and connectivity signals a promising evolution.

We eagerly await the next updates and specific release details.

That’s all for now!

Stay tuned for more Salesforce Marketing Cloud tips! 😊

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
