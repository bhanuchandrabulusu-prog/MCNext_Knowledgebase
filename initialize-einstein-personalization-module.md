# Initialize the Personalization Module | Personalize Web Experiences

**Source:** https://developer.salesforce.com/docs/marketing/einstein-personalization/guide/initialize-einstein-personalization-module.html

---

To use the Personalization module, you must initialize it at the beginning of your sitemap. Initialize the module using the SalesforceInteractions.Personalization.Config.initialize method, as shown in this example.

Since the module initialization must occur before the sitemap is initialized, you must call the SalesforceInteractions.Personalization.Config.initialize method before you call SalesforceInteractions.init.

The SalesforceInteractions.Personalization.Config.initialize method accepts the objects described in this table.

Object	Type	Description
personalizationExperienceConfigs	Array	Optional. Specify personalization experiences to be included in the configuration.
customFlickerDefenseConfig	Array	Optional. Configure flicker defense mechanisms used to prevent content flicker when retrieving and rendering personalized content.
customEngagementConfig	Array	Optional. Define custom destinations to send engagement data.
