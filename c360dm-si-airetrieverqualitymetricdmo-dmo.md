# Ai Retriever Quality Metric DMO | Model Data in Data 360 | Data 360 DMO and Mapping Guide

**Source:** https://developer.salesforce.com/docs/data/data-cloud-dmo-mapping/guide/c360dm-si-airetrieverqualitymetricdmo-dmo.html

---

Description: The Context Precision Score for the metric result. The score indicates the proportion of relevant chunks in the response.
Field API Name: std__CreatedById__c
Data Type: TEXT
Description: The ID of the user who created the record.
Field API Name: std__CreatedDate__c
Data Type: DATETIME
Description: The date and time when the record was created.
Field API Name: std__DataSourceId__c
Data Type: TEXT
Description: A unique, system-generated identifier for this record.
Field API Name: std__DataSourceObjectId__c
Data Type: TEXT
Description: A unique, system-generated identifier for this record.
Field API Name: std__ExternalRecordId__c
Data Type: TEXT
Description: The ID of the corresponding record from an external data source system.
Field API Name: std__ExternalSourceId__c
Data Type: TEXT
Description: The ID of the corresponding record from an external data source system.
Field API Name: std__FaithfulnessRelevancyScoreNumber__c
Data Type: DOUBLE
Description: The Faithfulness Relevancy Score for the metric result. The score indicates the proportion of detected hallucinations.
Field API Name: std__Id__c
Data Type: TEXT
Description: Required. A unique, system-generated identifier for the AiRetrieverQualityMetric record. Maximum size is 15 characters.
Field API Name: std__InternalOrganizationId__c
Data Type: TEXT
Description: A unique, system-generated identifier for this record.
Field API Name: std__LastModifiedById__c
Data Type: TEXT
Description: The user who most recently changed the record.
Field API Name: std__LastModifiedDate__c
Data Type: DATETIME
Description: The date and time when a user last modified the record.
Field API Name: std__LastProcessedReqTimestamp__c
Data Type: DATETIME
Description: The timestamp when the AIRetrieverRequest was last processed for metric evaluation.
Field API Name: std__MetricCreatedTimestamp__c
Data Type: DATETIME
Description: The timestamp when the metric result was generated.
Field API Name: std__RetrievedContextIdListText__c
Data Type: TEXT
Description: A list of Context IDs (Top-K) that’s extracted for reporting from the ResultText in the Retriever Response.
Field API Name: std__RetrieverApiName__c
Data Type: TEXT
Description: The name of the Retriever that corresponds to the request.
Field API Name: std__RetrieverTraceId__c
Data Type: TEXT
Description: The Trace ID (from OTel) that’s generated during the Retriever Request.
Field API Name: std__RetrieverTraceSpanId__c
Data Type: TEXT
Description: The Trace Span ID (from OTel) that’s generated during the Retriever Request. The ID refers to the Telemetry Trace Data Model Object (DMO).
Field API Name: std__SourceDocumentIdListText__c
Data Type: TEXT
Description: A list of Source Record IDs that’s extracted for reporting from the Retriever Response.
Field API Name: std__SystemModstamp__c
Data Type: DATETIME
Description: The date and time when the record was last modified by a user or an automated process.
Field API Name: std__UserUtteranceText__c
Data Type: TEXT
Description: The context that’s extracted for reporting from the User Utterance in the Retriever Request.
