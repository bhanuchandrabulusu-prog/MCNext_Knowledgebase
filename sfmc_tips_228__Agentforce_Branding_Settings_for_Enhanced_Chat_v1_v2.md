# SFMC Tips #228 : Agentforce: Branding Settings for Enhanced Chat (v1 / v2)

**Source:** https://medium.com/@marketingcloudtips/sfmc-tips-228-agentforce-branding-settings-for-the-embedded-chat-window-b6b4ddbadb30

---

# SFMC Tips #228 : Agentforce: Branding Settings for Enhanced Chat (v1 / v2)

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--b6b4ddbadb30---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--b6b4ddbadb30---------------------------------------)

7 min read

·

Jan 3, 2026

--

Photo by [Alvan Nee](https://unsplash.com/@alvannee?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

In the previous article, I explained various customization settings available in the chat window used for Service Agents and live chat agents to improve the customer experience.

[## SFMC Tips #227 : Agentforce: Detailed Settings for the Embedded Chat Window

### In the embedded chat window used by service agents (Agentforce) and live human chat, various customization settings can…

medium.com](/@marketingcloudtips/sfmc-tips-227-agentforce-detailed-settings-for-the-embedded-chat-window-cd3c375cc6ea?source=post_page-----b6b4ddbadb30---------------------------------------)

Following on from that article, this article explains the branding settings available for the chat window.

Branding settings can be configured by selecting an existing Embedded Service from **Setup > Embedded Service Deployments**, and then clicking **Branding** in the upper-right corner.

***Note:*** *After saving your settings, be sure to click* ***Publish*** *in the upper-right corner.*

## Color

- The examples in this article intentionally use highly visible color combinations to make the settings easier to understand.
- To change a color, click the dropdown and scroll through the color picker, or enter a hexadecimal color code directly into the **#** field.

## **① Chat Button and Invitation**

- **Background:** Background color of the **Chat Button** and **Auto-Invitation** popup.
- **Text:** Text color displayed on the **v2 button** and **Auto-Invitation** popup.
- **Dismiss Invitation Button:** Color of the **X** icon on the Auto-Invitation popup.

*\*v2 does not support invitations, so there is no setting for the Dismiss Invitation Button.   
\*The Auto-Invitation popup is displayed only if Auto-Invitation is enabled.*

![]()

![]()

Enhanced Chat v1 Chat Button

![]()

Enhanced Chat v2 Chat Button

## ② Header

- **Background:** Header background color.
- **Text:** Header text and Navigation icon color.

![]()

![]()

Enhanced Chat v1 Header

![]()

Enhanced Chat v2 Header

## ③ AI Agent and Service Representative

These settings control the message bubbles displayed on the agent side.

- **Background:** Background color of messages, avatars, and initials thumbnails.
- **Text:** Text color displayed for AI agent messages.
- **Link:** Link text color displayed for AI agent messages.

![]()

![]()

Enhanced Chat v1 Message Body

![]()

Enhanced Chat v2 Message Body

## ④ End User

These settings control the message bubbles displayed on the customer side.

- **Background:** Background color of end-user messages and thumbnails.
- **Text:** Text color displayed for end-user messages.
- **Link:** Link text color displayed for end-user messages.

![]()

![]()

Enhanced Chat v1 Message Body

![]()

Enhanced Chat v2 Message Body

## ⑤ Conversation Body

- **Text:** Color of system-generated text and text entered by end users (customers).  
  *\*This setting also affects the text entered in the pre-chat form.*

![]()

![]()

Enhanced Chat v1 System Text

![]()

![]()

Enhanced Chat v2 System Text

![]()

Example of a Pre-Chat Form

## ⑥ Footer

- **Icon:** Color of the Attachment, Emoji, and Send icons.
- **Header:** Underline color.
- **Footer:** Border color.  
  *\*For v2, the footer border color does not appear to change and remains black.*

![]()

![]()

Enhanced Chat v1 Footer

![]()

Enhanced Chat v2 Footer

## ⑦ Citations

- **Background**: The highlight background color of the source title section
- **Text**: The title text color of the quoted source link

***Note:*** *Citation settings control the appearance of source links displayed with responses. Depending on the features and configuration being used, citations may not be displayed.*

## ⑧ Badges and Buttons

- **Start Button:** Controls the appearance of the Start button in the pre-chat form.
- **Badge:** Controls the appearance of badges such as the indicator used to jump to the latest message in a thread.  
  *\*v2 does not support badges, so there are no badge settings.*

![]()

![]()

Enhanced Chat v1 Pre-Chat Start Button

![]()

Enhanced Chat v2 Pre-Chat Start Button

![]()

Enhanced Chat v1 Badge

## Font

*(Available in both v1 and v2)*

The chat window supports the following predefined fonts:

*Arial, Salesforce Sans, Georgia, Palatino Linotype, Times New Roman, Arial Black, Comic Sans MS, Impact, Lucida Sans Unicode, Tacoma, Trebuchet MS, Veranda, Courier New, Lucida Console*

### Using a Custom Font

Instead of predefined fonts, you can also use your own custom font.

1. Upload the font you want to use as a static resource.
2. Select **Custom Font** from the “Font” dropdown menu.
3. In the displayed “Custom Font Family Name” field, enter the name of the uploaded static resource.

### Font Size

In the “Font Size” field, you can select one of the following:

- Small
- Medium
- Large

Below are size examples when applying three font sizes using Palatino Linotype (from left to right: small, medium, large).

## Images

You must first use an image hosting service to convert your image into a URL. Then add the URL in the **Images** section.

## ① Service Representative Avatar

*(Available in both v1 and v2)*

Displayed on the left side of service representative message bubbles. For live chat agents, this avatar is used.

## ② Bot and AI Agent Avatar

*(Available in both v1 and v2)*

Displayed on the left side of text message bubbles initiated by a bot or AI agent. For AI Agents, this avatar is used.

## ③ Logo

*(Available in both v1 and v2)*

Displayed in the chat header.

![]()

Enhanced Chat v1 Logos and Avatars

![]()

Enhanced Chat v2 Logos and Avatars

## ④ Chat Button

*(Available in v1 only)*

Displayed on the chat button. Animated GIFs are also supported.

![]()

***Note:***[*The* ***“Ask Me Anything”*** *text displayed on the v2 chat button can be localized by editing it from the* ***Custom Labels*** *menu*](/@marketingcloudtips/agentforce-multilingual-display-for-enhanced-chat-based-on-browser-language-0046c8b45d56)*.*

![]()

*If you would like to test immediately, click the links below and use the sample images. Before using them, add* [***https://image.s12.sfmc-content.com***](https://image.s12.sfmc-content.com) *to* ***Setup > Trusted URLs****. If you do not register it, the images will not appear in the chat.*

- [Service representative avatar](https://image.s12.sfmc-content.com/lib/fe3311727364047e721170/m/1/agent_a.png)
- [Bot and AI agent avatar](https://image.s12.sfmc-content.com/lib/fe3311727364047e721170/m/1/agent_b.png)
- [Logo](https://image.s12.sfmc-content.com/lib/fe3311727364047e721170/m/1/ABC_logo.png)
- [Chat button](https://image.s12.sfmc-content.com/lib/fe3311727364047e721170/m/1/chatbutton.png)

## Chat Window Size

(Available in both v1 and v2)

You can customize the chat window by specifying the **Width** and **Height** independently.

This allows you to expand the default chat window size and display it more prominently based on your use case.

### Default Size

- v1: 320 pixels (Width) × 480 pixels (Height)
- v2: 480 pixels (Width) × 673 pixels (Height)

### Minimum Size

- 80 pixels (Width) × 120 pixels (Height)

### Maximum Size

- No limit

Because width and height can be configured independently, you can also create vertically oriented or horizontally oriented layouts. Adjust the size to best fit your website layout and device sizes.

Example of a Wider Chat Window

## Conclusion

Branding settings for the chat window are more than simple visual adjustments. They are an important element in providing users with a sense of trust and a consistent brand experience.

By customizing colors, fonts, icons, logos, and other visual elements, you can create a chat experience that naturally aligns with the overall tone of your website and services.

At the same time, there is no need to customize everything. Even adjusting highly visible elements such as the **header**, **message bubbles**, and **chat button** can significantly change the overall impression.

Whether you are planning to implement Agentforce or are already using it, consider reviewing your branding settings not only from the perspective of **how it works**, but also **how it looks** and **how it feels** to users.

That’s all for this time.

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
