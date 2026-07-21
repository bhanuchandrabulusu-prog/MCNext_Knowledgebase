# What to Know About Personalization Use Case Setup

**Source:** https://help.salesforce.com/s/articleView?id=mktg.persnl_setup_use_case_wtk.htm&language=en_US&type=5

---

SALESFORCE PERSONALIZATION
What to Know About Personalization Use Case Setup

The use case setup provides a one-time configuration and deployment of a Personalization use case to a data space. The setup process creates all assets necessary for a complete and functional Personalization use case.

When using the use case setup process, keep these considerations in mind:

The use case options currently supported in this setup are intended for customers who don’t have any profile data graphs in the data space they intend to deploy the use case.
Completing this process creates and deploys a profile data graph for the selected use case. For this reason:
You can’t deploy a use case to a data space that already contains any profile data graphs.
You can’t deploy a use case more than once to the same data space using this process.
After creating the necessary use case assets, the setup process automatically verifies proper data model configuration. During this verification, the process flags any objects missing from the data stream, or any unmapped object fields. Before you can deploy the use case and its assets, you must repair any missing or unmapped data.
SEE ALSO
What the Use Case Setup Deploys
Deploy a Preconfigured Personalization Use Case
