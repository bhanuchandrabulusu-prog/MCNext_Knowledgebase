# Assign a Default Data Graph to a Data Space

**Source:** https://help.salesforce.com/s/articleView?id=mktg.persnl_setup_default_dg_to_ds.htm&language=en_US&type=5

---

SALESFORCE PERSONALIZATION
Assign a Default Data Graph to a Data Space

You can assign default profile data graphs to specific data spaces, providing selection guidance for Salesforce Personalization configurations. After the data graph is assigned, it is automatically populated as the default data graph whenever you select its associated data space in a Salesforce Personalization configuration.

REQUIRED EDITIONS
USER PERMISSIONS
NEEDED
To assign default data graphs to data spaces:	Personalization Admin

When selecting a default data graph for a data space, keep these considerations in mind:

Profile data graph assignments are on by default. However, you can turn them off at any time using the Data Graph Defaults toggle switch.
Turning off data graph defaults using the toggle switch globally disables all default data graph assignments to all data spaces. You can’t disable only a single default assignment.
After you assign a default profile data graph to a data space, you can edit or delete the assignment at any time.
Editing the default profile data graph value doesn’t affect existing Salesforce Personalization configurations.

To assign a default profile data graph to a data space:

In the org containing your Personalization install, click Setup and select Personalization Setup.
Under Personalization Setup Options, click the Data Graph Defaults tab.
From the Data Space menu, select a data space that you want to assign a default profile data graph to.
From the Default Profile Data Graph menu, select a profile data graph that you want the selected data space to use when configuring Salesforce Personalization.
Save your work.

You can edit or delete the default data graph assignment at any time.

SEE ALSO
Create a Personalization Campaign
