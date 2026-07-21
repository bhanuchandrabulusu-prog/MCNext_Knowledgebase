# Set Up Content Zones | Personalize Web Experiences

**Source:** https://developer.salesforce.com/docs/marketing/einstein-personalization/guide/set-up-content-zones.html

---

Use content zones to designate areas on web pages across your website as targets for rendering personalized content from Personalization. You can define content zones in the Interactions SDK Sitemap either globally or for a specific page type. The content zones that you define in the Sitemap are then made available to personalization experience developers via Web Personalization Manager (WPM).

A content zone contains two fields — a name and a selector.

Field Name	Type	Required	Description
name	String	Yes	The name of the content zone. For example, global_popup and product_detail_recommendations.
selector	String	No	The CSS selector of the web page element that the content zone targets.

You can define content zones in the Interactions SDK Sitemap globally using the global configuration. Alternatively, you can define content zones for specific page types using the pageTypes configuration.

Example: Defining content zones in the global configuration of the Sitemap.

Example: Defining content zones in the pageTypes configuration of the Sitemap.
