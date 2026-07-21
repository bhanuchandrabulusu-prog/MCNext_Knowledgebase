# Model Data in Data 360 | Data 360 DMO and Mapping Guide

**Source:** https://developer.salesforce.com/docs/data/data-cloud-dmo-mapping/guide/c360dm-model-data.html

---

This documentation is available as a developer preview. Documentation isn’t generally available unless or until Salesforce announces its general availability in documentation or in press releases or public statements. All commands, parameters, and other information is subject to change or deprecation at any time, with or without notice. Don’t implement functionality in production with these commands or tools.

As of October 14, 2025, Data Cloud has been rebranded to Data 360. During this transition, you may see references to Data 360 in our application and documentation. While the name is new, the functionality and content remains unchanged.

Learn about the key terms and concepts related to data ingestion and modeling in Data 360. Find reference material on standard data model objects (DMOs), including fields, descriptions, and relationships, along with mappings associated with data bundles.

Standard DMOs
Standard DLO to DMO Mappings
Standard Data Bundles
Data 360 Extensibility Readiness Matrix
Legacy DMOs
Legacy Data Bundles

The Customer 360 Data Model is the standard data model used by Data 360 to aid in data modeling and extensibility across platforms. It serves as the framework for unifying raw data into a single, actionable view.

Data lake objects (DLOs) are the foundational storage containers where ingested or federated data is first held. They act as the raw building blocks of the data lake, capturing the initial state of information brought into the system. Data model objects (DMOs) are created by mapping DLOs into standardized groupings. These objects provide physical or virtual views of the underlying data, allowing for either standard or custom configurations.

A data bundle is a Salesforce-defined data stream definition that includes mapping to Data 360 DMOs. After a data stream is deployed, the data bundle automatically maps source objects from the source to a DMO in Data 360. You can add or customize the data mappings to meet your business needs.

 Salesforce Developer: Standard Objects

 Salesforce Developers: Data Model Diagrams for Salesforce Objects

 Salesforce Help: Data Model Concepts

 Salesforce Developers: Data Model Gallery for Data 360

 Trailhead: Customer 360 Data Model for Data 360

 Salesforce Help: Customer 360 Data Model

 Salesforce Help: Data Mapping

 Salesforce Help: Data Types and Date Formats
