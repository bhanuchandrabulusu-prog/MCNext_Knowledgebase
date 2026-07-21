# Batch Personalization Decisions for Customer Segments

**Source:** https://help.salesforce.com/s/articleView?id=mktg.persn_batch_persn_decisions_for_customer_segments.htm&language=en_US&type=5

---

SALESFORCE PERSONALIZATION
Batch Personalization Decisions for Customer Segments

With Batch Personalizations, you can create personalized decisions for a Data 360 segment and save the decisions to Data Model Objects (DMO) in Data 360. You can then send the batch personalization output to other platforms like Marketing Cloud Engagement (MCE), Google Cloud Platform (GCP), Amazon S3, and Azure to power your cross-channel marketing campaigns. For example, using Data 360, Salesforce Personalization, and MCE, you can use recommendations created for a Data 360 customer segment in MCE emails to notify your customers about an upcoming year-end sale.

REQUIRED EDITIONS
Available in: Lightning Experience in Enterprise, Unlimited, Professional, and Developer editions with Data 360.

To create and use batch personalization decisions in external systems like MCE, make sure you perform these tasks.

In Data 360, configure the segment of users that you want to target. For example, build a segment on unified individuals who made a purchase during the previous year-end sales.

In Salesforce Personalization, configure a personalization point that you want to evaluate the segment against. For example, create a personalization point to provide recommendations on products that are eligible for the year-end sale.

In Salesforce Personalization, create a batch personalization for the targeted segment and personalization point. When you run a batch personalization, the output is saved to a batch personalization output DMO in Data 360.

In Data 360, create a DMO activation for the batch personalization output DMO and select the target system (like MCE or S3) to send your output to.

In the external system, leverage batch personalization output attributes to power your campaign. For example, in MCE, you can use AMPscript to include batch personalization output attributes to compose your campaign messages. For sample Ampscript templates, see Sample AMPscript Templates for Batch Personalization.

Create a Batch Personalization
Create and configure a batch personalization to generate personalization decisions for a customer segment.
Understanding the Batch Personalization Output DMO
When a batch personalization is run, it creates a related decision output DMO in Data 360. The DMO stores the decision payload along with other details related to the batch personalization.
Create DMO Activation Against a Batch Personalization Output DMO
To send the output of a batch personalization to other systems like MCE, create a corresponding DMO activation in Data 360.
Batch Personalization FAQs
Answers to your questions about Batch Personalizations for Salesforce Personalization.
SEE ALSO
Salesforce Help: Create Segments in Data 360
Salesforce Help:Activation and Activation Targets
Batch Personalization Output DMO
Create a Batch Personalization
Sample AMPscript Templates for Batch Personalization
