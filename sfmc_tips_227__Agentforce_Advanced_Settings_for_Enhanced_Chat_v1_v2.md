# SFMC Tips #227 : Agentforce: Advanced Settings for Enhanced Chat (v1 / v2)

**Source:** https://medium.com/@marketingcloudtips/sfmc-tips-227-agentforce-detailed-settings-for-the-embedded-chat-window-cd3c375cc6ea

---

# SFMC Tips #227 : Agentforce: Advanced Settings for Enhanced Chat (v1 / v2)

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--cd3c375cc6ea---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--cd3c375cc6ea---------------------------------------)

6 min read

·

Jan 2, 2026

--

Photo by [Tim Mossholder](https://unsplash.com/@timmossholder?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

The embedded chat window used for Service Agents and live chat agents provides various customization settings to improve the customer experience.

In this article, I will explain each of these settings one by one.

These settings can be edited by selecting an existing Embedded Service from **Setup > Embedded Service Deployments**, and then clicking **Settings** displayed in the upper-left corner.

***Note:*** *After saving your settings, be sure to click* ***Publish*** *in the upper-right corner.*

## Customer User Interface

## ① Show Delivery Receipts

*(Available in both v1 and v2)*

![]()

### **Overview**

When a customer sends a message and the live agent’s status is anything other than Offline (Online or Busy), a **Delivered** status is displayed to indicate that the message was successfully delivered.

![]()

Enhanced Chat v1 Display Screen

### **Benefits**

- Clearly confirms that the message has reached the other party
- Reduces anxiety and uncertainty, improving user experience (UX)

*\*This feature is available only for live chat.  
\*For AI Agents, the status remains “Sent” even when enabled.*

## ② Show Read Receipts

*(Available in both v1 and v2)*

![]()

### **Overview**

When an agent actually checks (opens) a message from a customer, a **“Read”** notification is displayed on the customer side.

![]()

Enhanced Chat v1 Display Screen

For example, if an agent is responding to another chat in a different tab, messages received during that time will not be marked as “Read”.  
They are only displayed as “Read” when the agent views the message.

### **Benefits**

- Allows customers to know whether the agent has seen the message
- Reduces anxiety caused by unread messages and prevents excessive follow-ups

*\*This feature is available only for live chat.  
\*For AI Agents, the status remains “Sent” even when enabled.*

## ③ Show Typing Indicator

*(Available in v1 only)*

![]()

### **Overview**

While a live agent is typing a message, an animated indicator such as **“is typing…”** is displayed in the chat window.

![]()

Enhanced Chat v1 Display Screen

This allows customers to visually recognize in real time that an agent is actively responding.

### **Benefits**

- Enhances the feeling of real-time conversation
- Allows customers to anticipate whether a reply is coming soon

*\*This feature is available only for live chat.  
\*For AI Agents, the typing indicator is not displayed.*

## ④ Show Emoji Keyboard

*(Available in v1 only)*

![]()

### **Overview**

Allows customers to select emojis directly from the chat window and send them as messages.

![]()

Enhanced Chat v1 Display Screen

This makes it easier to express emotions and nuances that are difficult to convey with text alone.

### **Benefits**

- Enables casual and friendly communication
- Creates a softer and more approachable tone

## ⑤ **Press Enter/Return to start a new line of text**

*(Available in v1 only)*

![]()

### **Overview**

You can choose the behavior when pressing the Enter / Return key.  
When this option is enabled, pressing Enter / Return does not send the message and instead inserts a new line.

If this option is disabled:

- **Enter / Return key**: Send message
- **Option + Enter / Return key**: New line

### **Example Use Cases**

- Conversations often include line breaks and longer inputs  
   → Checking this option (enabled) is recommended
- Conversations mainly consist of short messages  
   → Leaving this option unchecked (disabled) is recommended

## ⑥ Show Agentforce Footer

*(Available in v2 only)*

### Overview

Displays **“Powered by Agentforce from Salesforce”** in the footer section of the chat window.

Enhanced Chat v2 Display Screen

This allows customers to see that the chat functionality is powered by Salesforce Agentforce.

### Benefits

- Informs customers that the chat is powered by Salesforce technology.
- May improve trust through Agentforce branding.

*\*When this setting is turned off, “Powered by Agentforce from Salesforce” is not displayed.  
\*This setting controls display only and does not affect chat functionality or behavior.*

## Terms of Use

## ① **Show Terms and Conditions in Pre-Chat**

*(Available in both v1 and v2)*

![]()

### **Overview**

Displays the Terms of Use (link to the terms or policy) to the customer before the chat starts.  
 ※ This is displayed regardless of whether a pre-chat form is used.

![]()

Enhanced Chat v1 Display Screen

### **Configuration Points**

- Must be configured using **Custom Labels**
- Text supports multiple languages
- The Privacy Policy URL can be freely customized

### **How to Configure**

1. From **Settings**, select **Custom Labels**.

2. Configure with the following values:

- Language: **English (or Other Language, etc.)**
- Chat Group: **Pre-Chat**
- Display Label Group: **Terms of Use**
- Display Label Type: **Standard**

3. As a sample, enter the following:

- URL Text: **Privacy Policy**
- URL: **https://link.com**

4. A Terms of Use label such as **[Privacy Policy](https://link.com)** is generated.  
Copy this and paste it into the **Terms and Conditions Label**, then save.

*※ How to display another language is explained in* ***Section 3*** *of the article below.*

[## SFMC Tips #224 : Agentforce: How to Set Up a Pre-Chat Form and How to Utilize It Afterwards

### When installing Agentforce (Service Agent) on an external site, you can configure a “pre-chat form” that asks users to…

medium.com](/@marketingcloudtips/sfmc-tips-224-agentforce-how-to-set-up-a-pre-chat-form-and-how-to-utilize-it-afterwards-6626d3d7907b?source=post_page-----cd3c375cc6ea---------------------------------------)

## ② **Require Users to Accept Terms and Conditions Before Chatting**

*(Available in both v1 and v2)*

![]()

### **Overview**

This setting prevents the chat from starting unless the customer clicks the consent button.

### **Benefits**

- Helps reduce legal and compliance risks
- Clearly communicates data usage policies and terms to customers

## Business Hours

## ① Configure Business Hours

*(Available in both v1 and v2)*

![]()

### **Overview**

Sets the available receiving hours, in other words, the time periods during which agents can respond.

### **Behavior**

- **Within business hours**  
   → Chat is displayed and available
- **Outside business hours**  
   → Chat is not displayed and unavailable

*This setting is particularly important when using live agents. It is a fundamental setting for aligning agent availability with the customer experience.*

## Conclusion

Although the various embedded chat window settings may appear to be a collection of small options, they are actually important elements that directly impact the customer experience (UX), operational efficiency, and legal/compliance requirements.

There is no need to enable everything uniformly. Instead, it is important to choose the settings that best fit your support model, customer base, and the roles of AI Agents and live agents.

We hope this article serves as a useful reference when reviewing your embedded chat settings.

That’s all for this time.

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
