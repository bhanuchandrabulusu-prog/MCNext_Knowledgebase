# Data Model Objects | Use Case Examples | Data 360 Connect REST API

**Source:** https://developer.salesforce.com/docs/data/connectapi/guide/dmo-use-case.html

---

Business Goal: Continuously integrate all new and existing customer engagement systems into Data 360 to maintain a complete, unified Customer 360 profile. By relying on identity resolution to unify this data, businesses enable comprehensive analysis and effective segmentation.

Use Case: A newly onboarded project requires ingesting subscriber profile data from an AWS S3 CSV file and mapping it to the Data Model Objects (DMOs) that make up the standard unified individual data model. These DMOs include key objects, such as Individual, Contact Point Phone, Contact Point Email, and Contact Point Address. A data engineer uses Connect API to streamline initial onboarding and subsequent change management processes.

The DMO Connect API prepares data for a unified customer view, transforming raw Data Lake Object (DLO) data into structured DMOs. This programmatic approach provides granular administrative control, streamlining implementation and ensuring seamless check-in to external change management.

For limit information, see Data 360 Limits and Guidelines.

Use the create data model object mapping endpoint to initiate the creation of the object mapping in Data 360.

Map the ingested subscribers data from the DLO to the existing Individual DMO, which is the gateway for identity resolution processing. Include field mappings, such as ID, last name, and first name in the request.

The API call confirms the creation of the mapping, with the status set to CREATING, indicating that the job is being processed.

Use the same create data model object mapping endpoint from the previous step to create another object mapping.

Map the ingested subscribers data to the Contact Point Email DMO to establish the primary email address for identity resolution and engagement. Include the ID and email address fields in the request.

The API call confirms the creation of the mapping, with the status again set to CREATING, indicating that the job is being processed.

Verify the status of a specific object mapping by using the get data model object mapping endpoint.

Confirm the status and creation of the mapping (completed in Step 1) from the source S3 Subscriber data to the target Individual DMO.

The mapping process for the Individual DMO is completed and all defined field mappings are confirmed and active. Use the same endpoint to verify the completion status of the Contact Point Email DMO mapping.

If you need to add another field mapping after creation of the initial mapping, use the update data model field mappings endpoint to add fields or to update existing mappings.

Add a new mapping from the DateOfBirth__c DLO field to the BirthDate DMO field.

The API call confirms the update by returning the full object-mapping payload, including the newly added field mapping. The status is set to UPDATING to indicate the mapping is in the process of being updated.

Make sure that all relevant data columns from the source DLO are correctly standardized against the DMO structure. Review the API response, which confirms the new field mapping aligns the source data format (for example, data type or length) with the expected DMO field structure.

For governance or cleanup, you can delete a specific field mapping without affecting the overall DLO-to-DMO relationship. Use the delete data model field mapping endpoint to remove an individual field relationship.
