# Batch Personalization FAQs

**Source:** https://help.salesforce.com/s/articleView?id=mktg.persnl_batch_persnl_faqs.htm&language=en_US&type=5

---

SALESFORCE PERSONALIZATION
Batch Personalization FAQs

Answers to your questions about Batch Personalizations for Salesforce Personalization.

What happens if the individual ID selected for the decision against a personalization point rooted on a unified individual isn’t the ID I want to send my message to in Marketing Cloud Engagement (MCE)?

In addition to the individual ID used for the decision, batch personalization also writes the unified individual ID that it was derived from. If a table exists in MCE that has all individual IDs related to a unified individual, use the unified individual ID as the entry point to find the individual ID required for the outbound message.

Does personalization attempt to retry batch decision jobs if they fail?

Yes, Salesforce Personalization retries a failed job up to three times. If the failure persists, an error code is logged on the fault code attribute visible on the batch personalization detail page. The job then moves into an error state and doesn’t process until triggered manually.

How many batch personalization jobs can I have?

You can have 20 active batch personalization jobs. “Active” means that the personalization job runs on segment refresh and is defined by the “Batch Status” attribute on the batch personalization object. The “Status” attribute is indicative of the object sync status and doesn't dictate whether the personalization job runs.

Why are decision credits consumed for batch personalization less than the members of the segment?

If contact point filtering is used, the number of decisions made for a given segment can differ from the number of individuals in the segment.

Will my batch personalization and corresponding DMO activation run automatically after I set them up?

Yes, the batch personalization job runs each time the corresponding Data 360 segment refreshes. If you select “Trigger linked DMO Activation” on your batch personalization, it automatically triggers the DMO activation to run.
