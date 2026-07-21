# Using Calculated Affinities

**Source:** https://help.salesforce.com/s/articleView?id=mktg.persnl_calculated_affinities_using.htm&language=en_US&type=5

---

SALESFORCE PERSONALIZATION
Using Calculated Affinities

Calculated affinities (CAs) measure characteristics that indicate a natural interest in or liking of an object. You can create real-time calculated affinities, and use them with personalization decision targeting rules, segments, and recommendation filters, to generate highly-focused personalized content based on customer preferences.

For example, a calculated affinity’s output scores can show that a customer is more interested in one product, brand, category, etc. over another. Leveraging Data 360 calculated insights (CIs), you can use calculated affinity numerical score output for decision targeting, recommendation filtering, and Data 360 segmentation.

When creating calculated affinities, keep these considerations in mind:

Calculated affinities use Data 360 calculated insights to power affinity scoring calculations. When you create a new calculated affinity, a corresponding calculated insight is generated automatically in Data 360 for the DMO field you select to calculate an affinity score against.
Each generated calculated insight that is named as a combination of the calculated affinity object name and attribute field name.

For example, creating a calculated affinity called Product Affinity using the goods product DMO brand attribute generates a calculated insights called Product Affinity Brand.

IMPORTANT Calculated insight names are limited to 40 characters. Creating long calculated affinity names, or selecting attributes with long names, can result in truncated calculated insight names.
Calculated Insights generated for real-time calculated affinity models are automatically added to the real-time profile data graph when you save the affinity.
Generated calculated insights provide two scoring values—a base affinity score and a raw affinity score. The base affinity score can range from 0 through 100. The raw affinity score has no bound, enabling it to have negative values or exceed 100.
After you create a calculated affinity, you can use the calculated insights generated when you save the affinity when defining various, personalization-related features and functions:
Data 360 segmentation—Reference calculated affinities in Data 360 segmentation by selecting any calculated insights generated when you created the affinity model.
Personalized recommendations—Each calculated insight generated when you save a calculated affinity becomes available for use when defining recommendation filters. For example, reference a brand affinity CI to only return products with a brand that matches high affined brands of the individual.
Decision targeting—Calculated insights generated when you create a calculated affinity are available for use in decision targeting logic along with other calculated insights mapped in the profile data graph. Using these calculated insights, for example, you can target customers with a high affinity toward a specific topic or brand.
Agent Grounding–Affinity scores are excellent data points for agents to reference as context data when attempting to execute actions with increased relevance.
SEE ALSO
Calculated Affinities
How Affinities are Calculated
Configure a Real-Time Calculated Affinity
