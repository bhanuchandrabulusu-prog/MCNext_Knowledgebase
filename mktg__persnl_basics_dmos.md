# Salesforce Personalization Data Model Objects

**Source:** https://help.salesforce.com/s/articleView?id=mktg.persnl_basics_dmos.htm&language=en_US&type=5

---

SALESFORCE PERSONALIZATION
Salesforce Personalization Data Model Objects

The Salesforce Personalization data model subject area includes multiple data model objects (DMOs) that store personalization decision activities.

Salesforce Personalization pipeline DMOs include design time and runtime objects. These pipeline objects accumulate runtime data specific to the personalization request process. They define where personalizations appear, eligibility for receiving personalized content, and how to present content to users or site visitors.

PIPELINE DMO	DESCRIPTION
Personalization Point DMO	Gathers the information for generating and presenting personalized content. This information includes eligibility, content decisions, and presentation.
Personalization Decision DMO	Enables decisioning to determine eligibility and present personalized content.
Personalization Content Schema DMO	Defines options for decision configuration and presentation and how each decision response appears.
Personalizer DMO	Determines whether to call an additional service at run time to retrieve the information for a complete decision response, for example, calling a recommender service to retrieve targeted, personalized content.
Personalization Log DMO	Gathers pipeline operational and attribution data associated with a personalized engagement.

Personalization attribution DMOs record the attributed data for a personalization point and the content or items recommended. This data is essential to understanding how effective personalized content is on a customer’s behavior and purchases. For example, in a commerce implementation, engagement can be attributed to clicks, orders, or revenue directly associated with a specific personalization point or with specific personalized content presented to an individual.

ATTRIBUTION DMO	DESCRIPTION
Personalization Point First Touch View-Based Attribution DMO	

Determines attribution based on first touch engagement with a personalization point.

The first touch mechanism attributes business key performance indicators to the initial individual engagement when multiple engagements qualify.

Multiple qualifying engagements are resolved by assigning the first engagement 100% of the value. For example, if an individual purchases a product that was recommended three different times from a personalization point, within the attribution window, the first engagement (view or impression) receives 100% of the value for that purchase.


Personalization Content First Touch View-Based Attribution DMO	

Determines attribution based on first touch engagement with content presented during a personalized experience.

The first touch mechanism attributes business key performance indicators to the initial individual engagement when multiple engagements qualify.

Multiple qualifying engagements are resolved by assigning the first engagement 100% of the value. For example, if an individual purchases a recommended product that they viewed multiple times within the attribution window, the first engagement (view or impression) receives 100% of the value for that purchase.


Personalization Point Last Touch View-Based Attribution DMO	

Determines attribution based on last touch engagement with a personalization point.

The last touch mechanism attributes business key performance indicators to the final individual engagement when multiple engagements qualify.

Multiple qualifying engagements are resolved by assigning the last engagement 100% of the value. For example, if an individual purchases a product that was recommended three different times from a personalization point, within the attribution window, the last engagement (view or impression) receives 100% of the value for that purchase.


Personalization Content Last Touch View-Based Attribution DMO	

Determines attribution based on last touch engagement with content presented during a personalized experience.

The last touch mechanism attributes business key performance indicators to the final individual engagement when multiple engagements qualify.

Multiple qualifying engagements are resolved by assigning the last engagement 100% of the value. For example, if an individual purchases a recommended product that they viewed multiple times within the attribution window, the last engagement (view or impression) receives 100% of the value for that purchase.

Experiment DMOs record the metadata and performance of personalization experiments. This data provides insights about the personalization strategies that are most effective and drive desired business outcomes.

EXPERIMENT DMO	DESCRIPTION
Experiment DMO	Defines the core metadata of an experiment, such as its name, description, state, start and stop times, and primary metrics.
Experiment Cohort DMO	Defines the metadata of different cohorts within an experiment, including control and treatment groups, their allocation weights, and associated personalization details.
Experimentation Log DMO	Gathers data from individual personalization experiment events.
Experimentation Summary DMO	Captures the aggregated summary of your experiments. This DMO includes key metrics, participant counts, and statistical analysis results for overall experiment performance.
Experimentation Daily Summary DMO	Captures the daily aggregated summary of your experiments, offering a day-by-day view of performance metrics and participant engagement.

The Batch Personalization output DMO records the output created for a batch personalization. This data provides information about the decisions created against a segment and personalization point. The DMO output can then be send to other systems, such as Marketing Cloud Engagement, using Data 360 DMO Activations.

BATCH PERSONALIZATION DMO	DESCRIPTION
Batch Personalization Output DMO	Captures the decisions created for a batch personalization.
SEE ALSO
Personalization Data Model Objects
How Salesforce Personalization Works
