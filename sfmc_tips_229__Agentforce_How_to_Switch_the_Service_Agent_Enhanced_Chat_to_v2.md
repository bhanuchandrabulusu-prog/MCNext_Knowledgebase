# SFMC Tips #229 : Agentforce: How to Switch the Service Agent Enhanced Chat to v2

**Source:** https://medium.com/@marketingcloudtips/sfmc-tips-229-agentforce-how-to-switch-the-service-agent-enhanced-chat-to-v2-1893565bf813

---

# SFMC Tips #229 : Agentforce: How to Switch the Service Agent Enhanced Chat to v2

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--1893565bf813---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--1893565bf813---------------------------------------)

4 min read

·

Jan 5, 2026

--

Photo by [Wren Meinberg](https://unsplash.com/@wrenaylameinberg?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

With the [**Agentforce Winter ’26 release**](https://help.salesforce.com/s/articleView?id=release-notes.rn_einstein_agent_ecv2_channel.htm&release=258&type=5), **Extended Chat v2** has been newly introduced. This feature has been available since **October 24, 2025**.

Currently, Agentforce Extended Chat has **two versions, v1 and v2**. However, at the time of writing, **v1 is enabled by default**. Therefore, to use **Extended Chat v2**, an administrator must **explicitly enable it**.

## How to Switch to Enhanced Chat v2

The switching process is very simple.

1. Open **Settings** ＞ **Embedded Service Deployments**
2. Select an existing embedded service deployment
3. Click **“Switch to V2”** displayed in the upper left

That’s all it takes to enable v2.

You can **switch back to v1 at any time**, so you can safely test it.

***Note:***[*Some features are not available in v2*](https://help.salesforce.com/s/articleView?language=en_US&id=service.enhanced_chat_feature_comparison.htm&type=5)*. Therefore, it is strongly recommended that you thoroughly test v2 in a Sandbox environment before deploying it to production. Certain features currently in use may no longer be available after migrating to v2, so be sure to assess the impact in advance.*

## Features of Enhanced Chat v2

### ① The Biggest Change: A Future-Ready Architecture

Unlike v1, which was primarily designed for text-based conversations, Enhanced Chat v2 introduces a new architecture built with future multimodal experiences in mind. This includes support for combining text, images, voice, buttons, cards, and other rich UI elements.

- Support for defining and rendering both standard and custom Lightning Types
- Ability to introduce and leverage custom Lightning Web Components directly within chat conversations

Custom Lightning Types are covered in more detail in the following article.

[## SFMC Tips #233 : Agentforce: Custom Lightning Types (Collection Renderer Override)

### In Agentforce, standard Lightning Types are typically used by default, so the UI tends to be simple.

medium.com](/@marketingcloudtips/sfmc-tips-233-agentforce-custom-lightning-types-collection-renderer-override-c3b7ad840303?source=post_page-----1893565bf813---------------------------------------)

[## SFMC Tips #234 : Agentforce: Custom Lightning Types (Editor + Renderer Override)

### In the previous article, I introduced how to display a rich UI in Agentforce by using Custom Lightning Types with a…

medium.com](/@marketingcloudtips/agentforce-custom-lightning-types-editor-renderer-override-c4e408bc7819?source=post_page-----1893565bf813---------------------------------------)

As a result, chat experiences are no longer limited to plain text interactions. Organizations can create far more flexible, interactive, and extensible user experiences.

### ② Improved Performance

The architectural redesign also delivers significant performance improvements.

Compared to previous versions, chat windows load faster and provide a smoother overall user experience.

### ③ Enhanced User Interface

The default chat window width has been increased, making conversations easier to read and input.

*Note: Window width can also be customized in v1.*

![]()

![]()

![]()

## Major Features Available in v1 but Not in v2

*(Updated: June 2026)*

- File attachments
- Custom Parameters
- Parameter Mapping

*\*Custom Parameters and Parameter Mapping are used to pass website context information — such as product IDs, order numbers, or customer IDs — to Agentforce.*

## Major Features Available in v2 but Not in v1

*(Updated: June 2026)*

## Future-Focused Extensibility Features

### Custom Lightning Types

Custom Lightning Types allow Agentforce responses to be rendered as custom Lightning Web Components.

Unlike traditional text-based chat responses, organizations can display information such as product cards, reservation options, and order status information through rich visual interfaces.

When combined with Agentforce Actions, retrieved data can be presented through sophisticated UI components, making this a foundational capability for future multimodal chat experiences.

### Context Event API

The Context Event API enables websites to notify Agentforce of user actions in real time.

This allows Agentforce to generate responses that take current user behavior into account, resulting in more context-aware and personalized interactions.

### Inline Mode

Instead of displaying the chat window as a floating widget in the bottom-right corner of the screen, Inline Mode allows the chat component to be embedded anywhere within a web page.

This makes it possible to create more natural user experiences on pages such as FAQs, product pages, or reservation pages.

## Conclusion

Enhanced Chat v2 should not be viewed as a complete replacement for traditional chat functionality. Rather, it serves as a foundation for future extensibility, including multimodal experiences and custom UI capabilities.

While some existing features are not yet supported, the integration possibilities with Lightning components and the performance improvements make v2 a compelling glimpse into the future of Agentforce-powered experiences.

### Organizations That Should Consider v2

- Want to leverage Custom Lightning Types
- Are implementing Agentforce for the first time
- Prioritize long-term extensibility and future enhancements

### Organizations That May Prefer to Stay on v1

- Rely on file attachments
- Use Custom Parameters and Parameter Mapping

That’s all for this time.

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
