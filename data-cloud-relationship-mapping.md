# Marketing Cloud Next: Understand the difference between a Relationship and a Mapping in Data Cloud

**Source:** https://the-agentic-marketer.com/marketing-cloud-next-tips-from-the-trenches/data-cloud-relationship-mapping

---

We described the main concepts of Data Cloud in our [Data Cloud for Marketers](/marketing-cloud-next-learning-path/data-cloud-foundations-value/) guide. But two concepts, the Mapping and the Relationships can look close, but they are actually completely different concepts.

## What is a Mapping?

A mapping is how you relate a DSO / DLO to a DMO. Let’s take the example of the Lead DSO/DLO (Lead\_Home). This Data Cloud Object is synced from the standard Lead Salesforce Object thanks to the Data Cloud – Salesforce Connector.

[![](https://the-agentic-marketer.com/wp-content/uploads/2025/09/Screenshot-2025-09-09-at-17.24.09-1024x559.png)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/Screenshot-2025-09-09-at-17.24.09-scaled.png) 

The mapping feature on a DSO/DLO

The Review button (or Start in case no Mapping was previously made) is where you access the Mapping interface.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20437%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/Screenshot-2025-09-09-at-17.45.10-scaled.png) 

The Mapping interface

**A Mapping bridges one DSO/DLO with one or more DMO, and defines which DSO/DLO fields are mapped to which DMO Fields**. For example, The Lead DSO/DLO is mapped to the Individual DMO and the Lead Id Field of the DSO is mapped to the Individual Id on the Individual DMO.

So in practice, whenever a Lead Record is ingested in the Lead\_Home DSO/DLO, a Record is created is the Lead DMO  and the value of the Fields is defined from the Mapping. The new Individual record in the DMO will have the value of the Lead Id in the DSO/DLO, the same one as in the Salesforce Lead Record.

A DSO/DLO can be mapped to several DMO and a Field from the DSO/DLO can be mapped to several Fields in distinct DMO. For example, the Lead DSO/DLO is also mapped the Contact Point Email Address DMO

When looking at a DMO, the list of mapped DSO/DLO is visible.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20437%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/Screenshot-2025-09-09-at-17.56.49-scaled.png) 

The list of mapped DSO from a DMO

## How do Relationships differ from Mappings

The **relationship is a concept related to DMO**, not to DSO or DLO. It is available on the DMO Page under the Relationship Tab.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20437%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/Screenshot-2025-09-09-at-18.11.43-scaled.png) 

The Case DMO and its relationships with other DMO

In the above Case DMO example, we see on the second line that it is related to the Account DMO in a ManyToOne Relationship. This states an Account can be related to multiple Cases. It also says that a Case is related to an Account when the Account Field named Account Id has the same value as a Case Field called Account.

The value of the Account Id Field in Account DMO and of the Account Field in the Case DMO are coming from their Mappings with DSO/DLO (or from a Data Transform).

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20437%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/09/Screenshot-2025-09-09-at-18.24.51-scaled.png) 

Graph view in of the Data Model in Data Explorer. Case Relationships

## Final Thoughts

As a summary Mappings are used to define how ingested Data is created in the Data Model at ingestion time.

Once ingested, DMO Records are related to each other using the Relationships. Relationships are used to define Container Paths in Segments or to generate a Data Graph record.
