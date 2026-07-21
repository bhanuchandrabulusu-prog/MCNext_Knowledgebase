# Set Up the Collection | Postman Collection | Data 360 Connect REST API

**Source:** https://developer.salesforce.com/docs/data/connectapi/guide/set-up-the-collection.html

---

You can follow along in a video that walks you through the steps of setting up Postman. See Data 360 Connect APIs and Postman Quick Start Video. The Postman setup and authentication instructions for Data 360 Connect APIs are similar to the ones for the Salesforce Platform APIs in Quick Start: Connect Postman to Salesforce in Trailhead.

Use the Postman web app or download and install the Postman desktop app.
Fork the collection in Postman.
On the collection’s Variables tab, assign a value to the loginUrl collection variable based on your Salesforce org type.
(Recommended) Use the My Domain login URL for your org.
Keep https://login.salesforce.com if you are using a production org, Trailhead Playground, or Developer Edition org.
Use https://test.salesforce.comfor sandboxes or scratch orgs.
Save your changes.
On the collection’s Authorization tab, click Get New Access Token.
When prompted, log in to your Salesforce org and allow access to Salesforce APIs Collection for Postman.
From the token details view, copy the value of the instance_url field.
Click Use Token.
On the collection’s Variables tab, replace the dne_cdpInstanceUrl current value with the value copied from the instance_url field.
Save your changes.

Postman parses the response body and sets the variables for dne_cdpAuthToken and dne_cdpInstanceUrl that are used in Connect API requests.
