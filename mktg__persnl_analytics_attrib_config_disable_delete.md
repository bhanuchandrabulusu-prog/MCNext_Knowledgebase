# Disable or Delete an Attribution Configuration

**Source:** https://help.salesforce.com/s/articleView?id=mktg.persnl_analytics_attrib_config_disable_delete.htm&language=en_US&type=5

---

SALESFORCE PERSONALIZATION
Disable or Delete an Attribution Configuration

You can disable or delete an attribution configuration at any time.

When disabling or deleting an attribution configuration, keep these considerations in mind:

Enabled attribution configurations show a status of Active.
Disabled attribution configurations show a status of Inactive.
Deleting a predefined attribution configuration removes the model from the Attributions tab. However, the objects created when the model was initially deployed aren’t deleted, and any gathered data is maintained.
To recover a predefined attribution configuration that you deleted, you must redeploy attribution intelligence using the Salesforce Personalization attribution intelligence setup process. Redeploying attribution intelligence recreates the predefined attribution configurations. However, it doesn’t overwrite or delete any data previously gathered and stored by their data lake or data model objects.

To disable or delete an attribution configuration:

From the App Launcher, search for and select Attributions.
Locate the attribution configuration that you want to disable or delete.
From the menu, click Disable to disable the model, or Delete to delete it.
SEE ALSO
Create a Custom Attribution Configuration
Install a Personalization Pipeline Intelligence Dashboard
