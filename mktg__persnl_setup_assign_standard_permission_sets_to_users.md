# Personalization Standard Permission Sets

**Source:** https://help.salesforce.com/s/articleView?id=mktg.persnl_setup_assign_standard_permission_sets_to_users.htm&language=en_US&type=5

---

SALESFORCE PERSONALIZATION
Personalization Standard Permission Sets

Use standard, predefined permission sets to define Salesforce Personalization user roles, or clone a standard permission set and customize it.

Using Standard Permission Sets

Streamline Salesforce Personalization user permission setup using predefined, standard permission sets. You can choose permissions for either the Personalization Admin or Personalization User roles.

Personalization Admin: For users needing full control to configure and manage Salesforce Personalization, this permission set provides create, read, update, and delete access.
Personalization User: Ideal for roles like channel marketers, this permission set enables users to create and manage market-focused personalization features without granting unnecessary access to underlying data configuration.

This table provides details about system permissions granted for each permission set role.

SYSTEM PERMISSIONS	PERSONALIZATION ADMIN	PERSONALIZATION USER
Access Personalization Platform	Yes	Yes
Allows user access Data 360	Yes	Yes
Attribution Model User	Yes	Yes
Personalization Intelligence User	Yes	Yes
Use CRM Analytics Templated Apps	Yes	Yes
View Developer Name	Yes	Yes

This table provides details about the default object settings for each permission set role.

SYSTEM PERMISSIONS	PERSONALIZATION ADMIN	PERSONALIZATION USER
Data Graph Definitions	
Read
View All
	
Read
View All

Data Model Field	
Read
View All
	
Read
View All

Data Model Object	
Read
View All
	
Read
View All

Data Model Taxonomy	
Read
View All
	
Read
View All

Data Model Category	
Read
View All
	
Read
View All

Data Space Definitions	
Read
View All
	
Read
View All

Data Space	
Read
View All
	
Read
View All

Engagement Signals	
Read
Create
Edit
Delete
View All
Modify All
	
Read
View All

Experiments	
Read
Create
Edit
Delete
View All
Modify All
	
Read
Create
Edit
Delete
View All

Streaming App Data Connectors	
Read
Create
Edit
Delete
View All
Modify All
	
Read
Create
Edit
Delete
View All

Personalization Objectives	
Read
Create
Edit
Delete
View All
Modify All
	
Read
View All

Personalization Points	
Read
Create
Edit
Delete
View All
Modify All
	
Read
Create
Edit
Delete
View All

Personalization Recommenders	
Read
Create
Edit
Delete
View All
Modify All
	
Read
Create
Edit
Delete
View All

Content Schemas (previously called Response Templates)	
Read
Create
Edit
Delete
View All
Modify All
	
Read
Create
Edit
Delete
View All

Batch Decisions	
Read
Create
Edit
Delete
View All
Modify All
	
Read
View All

Engagement Signal Compound Metrics	
Read
Create
Edit
Delete
View All
Modify All
	
Read
View All

Attribution Models	
Read
Create
Edit
Delete
View All
Modify All
	
Read
View All

Market Segment Definitions	
Read
Create
Edit
Delete
View All
Modify All
	
Read
View All

Data Object Tag Suggestion	
Read
View All
	
Read
View All
Assign a Standard Permission Set
Select a predefined set of permissions to assign Personalization Admin or Personalization user roles to users.
Customize Permission Sets
While the standard permission sets cover most use cases, you can clone a permission set to create a custom version with more granular control.
