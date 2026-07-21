# Configure Data 360

**Source:** https://help.salesforce.com/s/articleView?id=mktg.persnl_agentforce_configure_data_cloud.htm&language=en_US&type=5

---

SALESFORCE PERSONALIZATION
Configure Data 360

Update the web schema in Data 360 to capture user query intent as a new event and map that data correctly so it can be used for personalization.

REQUIRED EDITIONS
USER PERMISSIONS NEEDED
To manage web schema in Data 360:	Data Cloud Architect
To update data streams, mappings, and data graphs	Data Cloud Architect
Add a new event type User Query to your website's existing event schema to allow the system to capture, log, and track user intent using the standard agent action.
In Data Cloud Setup, search for and select Websites & Mobile Apps.
Select your connection from the list and download the existing schema.
Append the following User Query event JSON object to the events section in your schema file. This new event includes standard fields and a custom query field that holds the user's search term.
{
      "developerName": "query",
      "masterLabel": "Query",
      "category": "Engagement",
      "availabilityStatus": "INUSE",
      "externalDataTranFields": [
        {
          "masterLabel": "category",
          "dataType": "Text",
          "developerName": "category",
          "isDataRequired": true,
          "isCurrencyIsoCode": false
        },
        {
          "masterLabel": "dateTime",
          "dataType": "DateTime",
          "developerName": "dateTime",
          "isDataRequired": true,
          "isCurrencyIsoCode": false
        },
        {
          "masterLabel": "deviceId",
          "dataType": "Text",
          "developerName": "deviceId",
          "isDataRequired": true,
          "isCurrencyIsoCode": false
        },
        {
          "masterLabel": "eventId",
          "dataType": "Text",
          "developerName": "eventId",
          "isDataRequired": true,
          "primaryIndexOrder": 1,
          "isCurrencyIsoCode": false
        },
        {
          "masterLabel": "eventType",
          "dataType": "Text",
          "developerName": "eventType",
          "isDataRequired": true,
          "isCurrencyIsoCode": false
        },
        {
          "masterLabel": "query",
          "dataType": "Text",
          "developerName": "query",
          "isDataRequired": true,
          "isCurrencyIsoCode": false
        },
        {
          "masterLabel": "sessionId",
          "dataType": "Text",
          "developerName": "sessionId",
          "isDataRequired": true,
          "isCurrencyIsoCode": false
        },
        {
          "masterLabel": "sourceChannel",
          "dataType": "Text",
          "developerName": "sourceChannel",
          "isDataRequired": false,
          "isCurrencyIsoCode": false
        }
      ],
      "fieldCount": 8,
      "availabilityStatusLabel": {
        "label": "In Use",
        "rawValue": "INUSE"
      },
      "streamingAppLabel": "Consumer agent test site"
    }
Upload the updated schema file.
Sync the updated schema data with your data stream and map the new fields to a Data Model Object (DMO).
In Data 360, go to the Data Streams tab, and select your data stream from the list.
Click Sync Schema to bring in the new User Query event fields.
Go to the Data Lake Objects tab, and access the updated DLO.
Under Data Mapping, click Review.
Map the User Query event to the Web Search Engagement DMO.
USERQUERY DLO	WEB SEARCH ENGAGEMENT DMO
eventType	Engagement Type
query	Search Query
sourceChannel	Unmapped
Go to the Data Model tab, and select the Web Search Engagement DMO.
Select Relationships, and use the Edit option to add an N:1 relationship to the Individual DMO, if it’s not present.
Add the newly mapped DMO to your Profile Data Graph to make it available for personalization.
In Data 360, go to the Data Graphs tab, and select your profile data graph from the list.
Add the Web Search Engagement DMO under the Individual object.
Under DMO Fields, make sure to select the Search Query field, as well as other key fields for creating an engagement signal (such as Individual ID and Created Date).
NOTE For the semantic model to function efficiently, make sure that your catalog DMOs are updated with relevant metadata.
