# Integrate Salesforce Personalization with Modern Frontend Frameworks | Personalize Web Experiences

**Source:** https://developer.salesforce.com/docs/marketing/einstein-personalization/guide/integrate-personalization-modern-frontend-frameworks.html

---

Seamlessly integrate Salesforce Personalization into frontend frameworks such as React, Vue, Angular, and others using a component-based approach. With this approach, you can create custom components that register themselves as content zones, ensuring robust, reliable delivery and rendering of personalized content.

Traditional DOM manipulation by the SDK can conflict with the virtual DOM or rendering strategies of modern frameworks, causing personalized content to disappear. By creating a custom component that registers itself as a content zone handler, you make sure that personalized content is delivered and rendered using your framework’s own methods. This approach works well for any component-based frontend architecture.

Web Personalization Manager (WPM)

The UI for previewing and managing personalized content zones.

Content Zone Handler

A registration for a specific area or component in your app that can be personalized. Use the Personalization module's Config.ContentZoneHandler.set function to register your handler, providing a unique name and configuration object.

To enable personalization, register each content zone handler using the set function. This function ensures that your content zone is recognized by the Personalization module and can be targeted for dynamic content replacement.

This table describes the parameters required by the set function:

Parameter	Type	Required	Description
ContentZoneHandlerName	String	Yes	Unique, machine-friendly name for the content zone handler (for example, home_banner).
ContentZoneHandlerProperties	Object	Yes	Configuration object defining how the content zone behaves and is rendered.

The ContentZoneHandlerProperties interface defines the configuration object used when registering a content zone handler.

Property	Required?	Description
onReady	Yes	onReady is called when personalized content is ready for rendering. This property receives personalized content from Personalization as an input parameter and enables you to define custom rendering logic inside your component.
onRevert	No, but recommended	Used only at design time (not at runtime). onRevert is called when a preview is cancelled in WPM. When a business user cancels a preview in WPM, your page must revert to rendering the original, non-personalized content of the page.
label	No	User-friendly name of the registered content zone handler that appears within WPM. If not provided, this property defaults to showing the handler name.
path	No	Used only at design time (not at runtime). Specifies a CSS selector that WPM uses to visually highlight the content zone handler in the page editor. This helps business users easily locate and identify the content zone handler’s position on the page when setting up personalization experiences.
onHighlight	No	Used only at design time (not at runtime). Custom logic for WPM to visually highlight the content zone handler. Use onHighlight only if you can’t use the path property. For example, when your component uses Shadow DOM or other advanced rendering techniques that make CSS selectors unreliable.
		

Don’t define both path and onHighlight at the same time.

Here’s an example that demonstrates how to implement a content zone handler using vanilla JavaScript:

Here’s an example that demonstrates how to implement a custom content handler component in React. This component registers itself as a content zone handler and manages the rendering of personalized content:

Here’s how you can use the custom content handler component in your application.

Each content zone handler must have a unique, machine-friendly name.
Implement onRevert for proper WPM preview/cancel support.
Use path for simple highlight scenarios; use onHighlight for advanced or Shadow DOM cases.
The onReady callback must render the personalized content. If not set, show the original children.
Unregister or reset handlers on component unmount if needed.
The label property makes the handler user-friendly in WPM.
If personalized content disappears, ensure you are not manipulating the DOM outside React.
If preview cancel in WPM does not work, implement onRevert.
If WPM cannot highlight your zone, check your path or implement onHighlight.
Personalize Web Experiences
Integrate the Salesforce Interactions SDK
Example Sitemap
