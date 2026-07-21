# Create a Batch Personalization

**Source:** https://help.salesforce.com/s/articleView?id=mktg.persnl_batch_create_batch_persnl.htm&language=en_US&type=5

---

SALESFORCE PERSONALIZATION
Create a Batch Personalization

Create and configure a batch personalization to generate personalization decisions for a customer segment.

REQUIRED EDITIONS
USER PERMISSIONS NEEDED
To create batch personalizations	

Personalization Batch Decision

Market Segment Definitions

From the App Launcher, search for and select Batch Personalizations.
Click New.
In the New Batch Personalization window, select a data space.

The data space you select determines the target segments that are available for you to select from.

Select a target segment.

You can select individual or unified individual segments. The segment you select can impact the personalization points available for selection in the subsequent step.

Selecting a segment rooted on the individual object makes all personalization points available for selection.

Selecting a segment rooted on the unified individual object makes only personalization points that have data graphs built against the same unified individual object available for selection.

Select a personalization point to evaluate the target segment against and click Next.
IMPORTANT If the personalization point is configured against a profile data graph rooted on the unified individual object, all individual IDs of that object receive the same decision output. To avoid unnecessary credit consumption for duplicate decisions, Batch Personalizations select only one underlying individual ID to generate the decision output.
(Optional) Select contact points to filter your target segment for batch personalization and click Next.

Contact point filtering makes sure that batch personalization generates decisions for only individuals who can be contacted using outbound channels like email, SMS, and so on.

Contact points available for selection are based on the contact point DMOs defined on the profile data graph used in the personalization point.

You can select multiple contact points. Decisions are processed only for ‌profiles with at least one of the selected contact points. If you don't select a contact point, decisions are made for every profile in the target segment.

Enter a batch personalization name and an optional description.

The batch personalization API name, output DMO label, and output DMO name are auto-generated. The output DMO name is used to name the DMO where batch personalization decisions are saved.

The output DMO is used in Data 360 DMO Activations to send the batch personalization decision output to a 3rd party system like MCE, Azure, SFTP, GCP, or S3. For more information about DMO activations, see Activation for Data 360 Data Model Objects.

(Optional) Update the batch personalization schedule.

By default, this field is set to the existing schedule of the selected segment. To change the schedule, edit the publish schedule of the segment selected for this batch personalization. Possible refresh options include 1hr, 4hrs, 12hrs, 24hrs, and no refresh.

Select a refresh type.
OPTION	DESCRIPTION
Full	This option generates new decisions for all members in a segment.
Incremental	This option generates decisions only for the new members added to the segment after the last run.
(Optional) To trigger the linked DMO activation when a batch personalization completes, select DMO Activation Trigger.
NOTE Selecting this checkbox doesn’t automatically create an associated DMO activation. Use Data 360 Activations to create a DMO activation against the batch personalization output DMO.
(Optional) Select the status of batch personalization.

You can either activate or pause a batch personalization. Only an active batch personalization generates decisions when the associated segment refreshes. You can have 20 active batch personalization jobs.

NOTE To determine whether a batch personalization job is active, check the Batch Status attribute in the batch personalization object. This attribute indicates only the object synchronization status. It doesn't dictate whether the batch personalization job runs.
Save the batch personalization.
Active batch personalizations automatically run when the selected segment refreshes. To manually trigger a batch personalization, select Run Batch Personalization from the action menu.
Batch personalization decisions are stored in the related output DMO for 30 days. All decisions are recorded in the personalization log for analytics and attribution reporting.

After creating a batch personalization, make sure you create a corresponding DMO activation in Data 360 to send the outputs of the batch personalization to a third party system. For more information, see Activation for Data 360 Data Model Objects.
