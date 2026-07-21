# Using Content Schemas

**Source:** https://help.salesforce.com/s/articleView?id=mktg.persnl_content_schema_using.htm&language=en_US&type=5

---

SALESFORCE PERSONALIZATION
Using Content Schemas

Personalization content schemas (previously called response templates) are required when configuring personalization points, personalization campaigns, and personalization decisions. A content schema defines the configuration options available to marketers when they’re building a personalization decision. The content schema also ensures that all decision responses for a given personalization point or campaign return data in the same format.

The primary functions of a content schema include:

Configuration Definition: The content schema specifies the personalization attributes and configuration options available when creating personalization decisions or experiment cohorts.
Data Shape: A schema defines the "shape" or format of the data returned in a decision response, such as which specific item attributes (IDs, URLs, prices, sizes, colors, and so on) to include. The schema ensures a consistent user experience within a specific channel and across different channels.
Channel Reuse: Unlike models requiring channel-specific assignments, content schemas are channel-independent, enabling use of the same personalization point logic across web, mobile, or server-side applications.

When using content schemas keep these considerations in mind:

Content schemas are defined using a personalization type. The personalization type defines the personalization category the schema can support.
There are two personalization types—Recommendations or Dynamic Content (formerly called Manual Content)
Recommendations: Dynamic and highly personalized, recommendations often leverage machine learning to deliver individualized 1:1 experiences using a defined recommender that's built against both a profile and item data graph. Recommenders rely on Data 360 data graphs to determine who is eligible to receive personalized content and what content is available to recommend.
Dynamic Content: Using a rules-based form of personalization, dynamic content uses specifically configured content, such as CTA text or image URLs, directly into configuration fields defined by the associated content schema. This content is stored on the personalization decision itself rather than in Data 360, and it is typically used for elements like banners, infobars, or pop-ups.
Personalization points support the use of content schemas configured with either recommendations or dynamic content personalization types. However, personalization campaigns currently support using content schemas configured with the dynamic content personalization type only.
SEE ALSO
Content Schemas
Configure a Personalization Content Schema
Personalization Points in Salesforce Personalization
Configure a Personalization Point
Personalization Campaigns
Create a Personalization Campaign
