# Get Pardot Engagement Data in Marketing Cloud Next

**Source:** https://the-agentic-marketer.com/marketing-cloud-next-deep-dives/pardot-engagement-data-agentforce-marketing

---

We’ll get two distinct types of data in Data 360 (fka Data Cloud) from Account Engagement (fka Pardot): **Asset Performance and Prospect Activity**. Once done several Data Streams will be populated and new data from Account Engagement will flow into them. As these Data Streams will be mapped to standard performance and activity DMO, Agentforce Marketing (MC Next) will be able to use them as its own data.

## Asset Performance Ingestion

For this type of data, we’ll first need to install a Package for Data Cloud as Data Bundle. Let’s go to Data Cloud Setup > Salesforce CRM.

[![](https://the-agentic-marketer.com/wp-content/uploads/2025/11/Screenshot-2025-11-09-at-12.07.00-1024x558.png)](https://the-agentic-marketer.com/wp-content/uploads/2025/11/Screenshot-2025-11-09-at-12.07.00-scaled.png) 

Marketing Account Engagement CRM Data Data Bundle

Locate the Marketing – Account Engagement CRM Data in the Standard Data Bundles list and click Install. Keep the Install for Admins Only option and then Install. After some time the Bundle should be installed, and you should have the same value in the Latest Version in the Installed versoin columns.

We just installed the definition, and the mappings of the following Asset performance Data Stream:

- Marketing Form
- Marketing Link
- Landing Page
- List Email

We will then Deploy them in Data 360 (fka Data Cloud). Go to Data Cloud > Data Stream > New > Salesforce CRM and select Marketing – Account Engagement CRM.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20436%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/11/Screenshot-2025-11-09-at-12.20.57-scaled.png) 

Installing the Account Engagement Data Bundle

Next. Keep the Default Fields. Next, and finally Deploy. You now have 4 new Data Streams, and after some time (you may force their refresh).

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20436%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/11/Screenshot-2025-11-09-at-12.31.03-scaled.png) 

Account Engagement Asset Performance DSO are deployed

These Data Streams are mapped to the same Standard Performance DMO used by Agentforce Marketing (Marketing Cloud Next). You can then use them as standard data. **That’s Asset Performance data Convergence in action.**

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20436%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/11/Screenshot-2025-11-09-at-12.37.29-scaled.png) 

List Email Performance data is mapped to the standrad Bulk Email Message DMO

## Prospect Activity Ingestion

As a Pardot user, you surely know the Engagement History component  to display your Prospects’ activities on their related Leads or Contact layouts. Agentforce Marketing / Marrketing Cloud Next has a similar component called Data Cloud Profile Engagement (see [display Marketing Cloud Next Data in Salesforce](https://the-agentic-marketer.com/marketing-cloud-next-tips-from-the-trenches/marketing-cloud-next-unlocking-data-on-the-salesforce-prospect-lead-contact-campaign-objects/) for more information). For this latter component to be filled with Account Engagement Data, let’s ingest and map them.

### Select which Business Units to Ingest

Go to Setup > Integration Definitions > Account Engagement > Data Cloud Integration (previously this was available directly from Data Cloud Setup) and then click Get Started.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20436%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/11/Screenshot-2025-11-09-at-13.59.47-scaled.png) 

Select which Business Unit you want to Connect to Data Cloud

Once you send the Business Unit/s you want to get Prospect Activity data from using the arrows, click Done. This triggers the following:

- On each selected Account Engagement Business Unit, the Data Cloud – Account Engagement Connector now dsiplays “Connected” (it was Disconnected before the previous step)
- An Account Engagement Data Source is now available in Data 360, which we will leverage in the following step

### Deploy the Prospect Activity Data Streams

Go to Data Cloud > Data Streams > New.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20436%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/11/Screenshot-2025-11-09-at-14.11.30-scaled.png) 

The Account Engagement Data Source is now available as a Connected Source

Select the Account Engagement Connected source and click Next. Then select your first  Business Unit and the Email Engagement Data Kit.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20436%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/11/Screenshot-2025-11-09-at-14.21.09-scaled.png) 

Selecting which data type to deploy

Then click Deploy. This will create a Data Stream called EmailActivity\_xyz. You need to create the other DSO for each of the Business Units you created in the first step. So eventually, for a given Pardot Business Unit you will install 5 Data Streams:

- Email Engagement
- Web Page Engagement
- Form Handler Engagement
- Form Engagement
- Custom Url Engagement

The name are self explantory and the first Data Stream is mapped to the Email Engagement DMO, the other ones are mapped to the Website Engagement DMO. **This means your Prospect Activity Data from Account Engagement will participate to the Agentforce Marketing Score and be visible from the Data Cloud Profile Engagement component. This is Prospect Activity Convergence.**

### Activate the Account Engagement Data Cloud Connector

We need to perform a final step for your Account Engagement Prospects’ activity data. In each Account Engagement Business Unit you selected and installed the Data Streams for previously, go to Account Engagement Settings > Connector. The Data Cloud Connector should be in a Pause Status. Click Edit Settings.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20436%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/11/Screenshot-2025-11-09-at-14.42.49-scaled.png) 

Select the Engagement Data timeframe the connector will ingest

You can ingest data up to 2 years old. Once defined, Save Connector and finally Resume Sync. Do this operation for each Business Unit you connected early.

### Things to notice about Account Engagement Prospect Activity Ingestion

Only Assigned Prospect can have their activity ingested, provided it is the defined timeframe. The activity must be an interaction with a Pardot Asset tied to a Connected Campaign. Operational Email related activities and Preference Center clicks are not ingested.

The initial import can take long (up to several weeks) depending on the amount of data, then new activity is checked for every hour, and the actual ingestion can take up to several hours.

If you change the timeframe to ingest more recent data only, the Connector does not remove previously ingested data. In that case, you’d need to pause the connector and remove the existing Data Streams to eventually recreate them.
