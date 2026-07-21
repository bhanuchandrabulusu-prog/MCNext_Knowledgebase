# Personalization Data Model Object Reference

**Source:** https://developer.salesforce.com/docs/marketing/einstein-personalization/guide/data-model-object-reference.html

---

The Personalization Data Model subject area includes multiple data model objects (DMOs) that store Personalization decision activities and experiment data.

Personalization pipeline DMOs include design-time and run-time objects. These pipeline objects accumulate run-time data specific to the Personalization request process. They define where personalizations appear, eligibility for receiving personalized content, and how to present content to users or site visitors.

Pipeline DMO	Description
Personalization Point DMO	Gathers the information for generating and presenting personalized content. This information includes eligibility, content decisions, and presentation.
Personalization Decision DMO	Enables decisioning to determine Personalization eligibility and present personalized content.
Personalization Schema DMO	Defines options for decision configuration and presentation and how each decision response appears.
Personalizer DMO	Determines whether to call an additional service at run-time to retrieve the information for a complete decision response, for example, calling a recommender service to retrieve targeted, personalized content.
Personalization Log DMO	Gathers pipeline operational and attribution data associated with a Personalization engagement.

Personalization attribution DMOs record the attributed data for a personalization point and the content that the model recommended. This data is essential to understanding how effective personalized content is on a customer’s behavior and purchases. For example, in a commerce implementation, you can attribute engagement to revenue directly associated with a specific personalization point.

Attribution DMO	Description
Personalization Point First Touch View-Based Attribution DMO	Determines attribution based on whether an individual is eligible to receive personalization content from a personalization point.
Personalization Content First Touch View-Based Attribution DMO	Determines attribution based on whether an individual views personalized content presented at a personalization point.
Personalization Point Last Touch View-Based Attribution DMO	Determines attribution based on how individuals engage with a personalization point. For example, an amount of revenue is attributed directly to engaging with a personalization point grid component on a specific page.
Personalization Content Last Touch View-Based Attribution DMO	Determines attribution based on specific content provided in a personalized engagement. For example, a visitor to a website is presented with several recommendations. The visitor’s clicks and purchases are attributed to the personalized content that they were shown.

Experiment DMOs record the metadata and performance of personalization experiments. This data provides insights about the personalization strategies that are most effective and drive desired business outcomes.

Experiment DMO	Description
Experiment DMO	Defines the core metadata of an experiment, such as its name, description, state, start and stop times, and primary metrics.
Experiment Cohort DMO	Defines the metadata of different cohorts within an experiment, including control and treatment groups, their allocation weights, and associated personalization details.
Experimentation Log DMO	Gathers data from individual personalization experiment events.
Experimentation Summary DMO	Captures the aggregated summary of your experiments. This DMO includes key metrics, participant counts, and statistical analysis results for overall experiment performance.
Experimentation Daily Summary DMO	Captures the daily aggregated summary of your experiments, offering a day-by-day view of performance metrics and participant engagement.

The Batch Personalization output DMO records the output created for a batch personalization. This data provides information about the decisions created against a segment and personalization point. The DMO output can then be sent to other systems, like MCE, using Data Cloud DMO Activations.

Batch Personalization DMO	Description
Batch Personalization Output DMO	Captures the decisions created for a batch personalization.
