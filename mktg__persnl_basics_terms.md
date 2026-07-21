# Terminology in Salesforce Personalization

**Source:** https://help.salesforce.com/s/articleView?id=mktg.persnl_basics_terms.htm&language=en_US&type=5

---

SALESFORCE PERSONALIZATION
Terminology in Salesforce Personalization

To deliver personalized experience across clouds and other channels, Personalization uses a variety of objects, DMOs, and functions across Data 360 and Salesforce apps. Learn the terms that appear throughout the Salesforce Personalization user interface and documentation.

TERM	DEFINITION
Calculated Insight (CI)	A tool in Data 360 that queries, transforms, and creates complex calculations based on stored data.
Data Graph	

A grouping of data created by combining and transforming normalized table data from data model objects (DMOs) into new, materialized views. You can make fewer calls, and queries respond in near real-time, because the data is precalculated.

You can use two data graphs with Salesforce Personalization: profile and item. The profile data graph builds a single, unified profile for individuals by identifying and linking a user's activities from different channels. The item data graph supports recommendations.


Data Stream	A data source brought into Data 360. For example, behavioral data from a website.
Decisioning API	The primary service endpoint used by Salesforce Personalization to request and process personalized decisions for your users.
Mapping	

The process of associating data lake objects (DLOs) to data model objects (DMOs) after data has been ingested into Data 360.

The number of mapped fields and how you map them impacts the availability and complexity of your personalization options.


Personalization point	A personalization point represents a "point" in an experience that’s eligible for a personalization decision. A personalization point has a type and response template that defines the kind of personalization that you can configure on a decision and which personalized content that decision returns.
Personalization type	The personalization type identifies the kind of personalized content that you want to present, such as a recommendation.
Personalization content schema	A personalization content schema defines the configuration options available to marketers when they’re building a personalization decision. The response template also ensures that all decision responses for a given personalization point return data in the same format.
Personalization decision	A personalization decision determines who’s eligible to receive a personalization response using optional targeting rules. Decisions also determine what content to return, for example, a set of product recommendations or a banner image. A personalization point can contain multiple personalization decisions targeted at different sets of individuals. You can prioritize decisions so that if a person qualifies for more than one, Personalization returns only one decision.
Personalizer	The personalizer calls an additional service at run time to retrieve the information necessary for a complete decision response. For example, if you configure a decision to present recommendations, the personalizer calls the recommender service configured for that decision. The recommender then retrieves the targeted, personalized content for specific individuals.
Recommender	A recommender is a type of personalizer that provides targeted product or item recommendations. A recommendation is based on machine learning strategies or calculated insights and is usable across channels. When creating a recommender, you can define it to provide either goal-based recommendations or rule-based recommendations.
Sitemap	

A JavaScript file that outlines the data capture logic across different pages of your website.

The sitemap determines how SDK captures user interactions from your website during site navigation.


Targeting rule	A targeting rule determines who’s eligible to view personalized content provided by a decision based on specific data points, such as attributes, related attributes, calculated insights, or segment memberships. Using data points defined on the selected Data 360 profile data graph, you can create a targeting rule on any associated personalization point decisions.
SEE ALSO
Salesforce Help: Manage Data Spaces
Salesforce Help: Data Graphs
