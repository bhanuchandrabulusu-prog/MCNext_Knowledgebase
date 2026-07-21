# Track Personalization Engagement | Personalize Web Experiences

**Source:** https://developer.salesforce.com/docs/marketing/einstein-personalization/guide/track-personalization-engagement.html

---

To power Personalization’s advanced machine learning, it’s essential to capture and analyze how users interact with your site, especially with personalized content. This continuous data collection helps Personalization better understand user behavior, allowing the system to deliver recommendations that become more accurate and hyper-personalized over time.

User interaction event logs are automatically sent from the Web SDK sitemap to Data Cloud for tracking. This data is crucial for powering machine learning algorithms and for reporting and analytics within Data Cloud. The Data Cloud module processes these structured events by flattening them, assigning an eventType for categorization, and organizing them into data streams. You can even merge multiple event types into a single data stream.

To ensure events are categorized correctly, you must update your Data Cloud Web Schema. The schema defines the structure for event types, including their available fields, required fields, and field names. For more information on the structure of the Data Cloud Web Schema, see Mobile and Web SDK Schema Quick Guide for Data Cloud.

An Engagement Destination is a configuration that determines how user interaction events are processed, categorized, and sent to Data Cloud for analysis. When you configure a personalization experience in the Web Personalization Manager, you can choose a standard, out-of-the-box (OOTB) destination or create a custom one to fit your needs.

For more information on configuring a personalization experience and setting an engagement destination, see Creating a Personalization Experience.

Personalization provides two OOTB destinations for common use cases: Product Engagement and Website Engagement. These destinations use predefined event types to map engagement data to the correct Data Model Objects (DMOs).

Engagement Destination	Associated Event Type	Recommended DMO
Product Engagement	catalog	Product Browse Engagement
Website Engagement	userEngagement	Website Engagement
Use this destination exclusively for personalization experiences that are based on recommendations.
The event payload always uses the catalog event type.
The SDK automatically sends specific interaction names: catalog-object-view-start for views and catalog-object-click for clicks.
The event always includes an id field, that contains the unique identifier of the recommended item from your catalog, and a type field, which has a static value of Product.

Here’s an example payload for a Product Engagement sent to Data Cloud.

Use this destination for personalization points that use manual content.
The event payload uses the userEngagement event type.
The SDK sends the following interaction names by default: personalization-view for views and personalization-click for clicks.
Because this destination is for manual content that doesn’t correspond to a catalog item, the event payload doesn’t contain an id or type field.

Here’s an example payload for a Website Engagement sent to Data Cloud.

While OOTB destinations cover standard scenarios, you may require more control to handle unique tracking requirements or to modify event data. Custom engagement destinations give you granular control over how engagement events are categorized before they’re sent to Data Cloud.

To create a custom destination, you add code to your sitemap in a two-step process:

Retrieve the current engagement configuration.
Define and add your custom engagement destination.

First, retrieve the live engagement configuration from the SDK using the SalesforceInteractions.Personalization.Config.Engagement.get function.

This function fetches the current configuration object and stores it in a variable, currentEngagementConfig, making it available for modification.

Once you’ve retrieved the configuration object, you can define and add your new destination to its destination property. These parameters make up the engagement destination.

label

A user-friendly name for the destination that appears in the Web Personalization Manager UI.

description

A brief explanation of what this destination is used for. You can also use the label as your description.

disableSendingNonItemEngagementEvents

A boolean that, if set to true, denotes that the personalization experience involves recommendations (such as product or article recommendations). If set to false, it denotes manual content being recommended.

eventModifiers

An object containing properties that will override the default values in the engagement event payload. The eventModifiers object accepts these parameters.

type

The type of the item being recommended. This is valid only for personalization experiences based on product recommendations.

event-type

The Data Cloud event type that needs to be mapped to the appropriate DMOs. Ensure that the event type is defined in the Data Cloud web schema and mapped to the correct DMOs.

interaction-name

Specifies the type of interaction that occurred, such as a view or a click. You can also define this as a function where it receives a single context parameter. This context object contains a name property with a string value of either view or click, depending on the user's action. You can use this context.name value within your function to return custom interaction names.

Here’s a complete example of retrieving the existing configuration, adding a new destination, and applying it during the SDK initialization.

While many out-of-the-box templates handle engagement tracking automatically, you may need to manually send engagement events for custom-built experiences. For this alternative path, use the standard SalesforceInteractions.sendEvent function of the Interactions SDK to send engagement events.

For accurate tracking, add the personalizationId and personalizationContentId values from the personalization response to every engagement event you send manually.

Always set id and contentId. For a specific product, set contentId to the personalizationContentId value from the JSON response. Otherwise, set it to the personalizationId.
