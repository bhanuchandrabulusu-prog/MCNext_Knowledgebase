# Predefined Attribution Configurations

**Source:** https://help.salesforce.com/s/articleView?id=mktg.persnl_analytics_attribution_settings.htm&language=en_US&type=5

---

SALESFORCE PERSONALIZATION
Predefined Attribution Configurations

Using Salesforce Personalization setup, you can install two predefined attribution configurations. After these configurations are deployed, you can view the attribution data for them from the Attributions tab.

The predefined attribution configurations use attribution parameter settings for a specific group of key performance indicators (KPIs) – Views, Clicks, Add to carts, and Orders.

For this out-of-the-box attribution configuration to work, you must install a specific set of required engagement objects – Product Browse Engagement, Shopping Cart Engagement, and Product Order Engagement. If you don’t plan to use these objects, this predefined attribution setup is optional.

We’ve outlined the predefined attribution settings here, along with the included key performance indicators (KPIs).

PARAMETER	SETTING	DESCRIPTION
Attribution Model Type	First Touch	

When using this model type, multiple qualifying engagements for a desired business conversion are resolved by assigning the first engagement 100% of the value.

As an example, if an individual purchases a product that was recommended three different times within the attribution window, the first engagement (view or impression) receives 100% of the value for that purchase.


Last Touch	

When using this model type, multiple qualifying engagements for a desired business conversion are resolved by assigning the last engagement 100% of the value. 

As an example, if an individual purchases a product that was recommended three different times within the attribution window, the last engagement (view or impression) receives 100% of the value for that purchase.


Attribution Window	7 days	The attribution window is the maximum allowed time between two engagements for a conversion to occur.  For example, if an individual engages with recommended content, revenue from them ordering that content within the 7 day engagement window is counted for that personalization point. Any revenue for orders outside of the engagement window isn't counted.
ATTRIBUTION KPIS	VALUE	DESCRIPTION
Engagement	Impressions	Attribution-eligible metrics, like cart conversions, orders, and revenue, are attributed to viewing personalized content. Revenue is considered attributed if the individual has seen the content. Direct engagement with the content isn't required.
Clicks	Attribution-eligible metrics, like cart additions, orders, and revenue, are attributed to clicking on personalized content.
Business Metrics	Add to Carts	The total number of add to cart actions for the recommended content that was purchased within the attribution window.
Orders	The number of discrete orders containing recommended content that were purchased within the attribution window.
Revenue	The total amount of revenue for orders containing recommended content that was purchased within the attribution window.
SEE ALSO
Types of Salesforce Personalization Analytics
Deploy Preconfigured Personalization Attribution Intelligence Data
View Attribution Intelligence for Active Attribution Configurations
Using the Personalization Attribution Intelligence Dashboard
Salesforce Personalization Data Model Objects
