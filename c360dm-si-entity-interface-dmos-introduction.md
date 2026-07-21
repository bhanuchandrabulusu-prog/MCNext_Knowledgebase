# Standard DMOs | Model Data in Data 360 | Data 360 DMO and Mapping Guide

**Source:** https://developer.salesforce.com/docs/data/data-cloud-dmo-mapping/guide/c360dm-si-entity-interface-dmos-introduction.html

---

This documentation is available as a developer preview. Documentation isn’t generally available unless or until Salesforce announces its general availability in documentation or in press releases or public statements. All commands, parameters, and other information is subject to change or deprecation at any time, with or without notice. Don’t implement functionality in production with these commands or tools.

Data model objects (DMOs) organize and harmonize your data in Data 360. They’re categorized into standard (std__ prefix) and legacy (ssot__ prefix) types.

When you deploy a new data bundle, standard DMOs have the following traits:

No auto-replacement: If an ssot__ DMO already exists, it won’t be replaced by an std__ DMO.
Identical performance: They work exactly like legacy DMOs, supporting all the same queries, operations, field types, and relationships.
Environment flexibility: They’re data space agnostic, meaning they function consistently across all your different data environments.
Fixed configuration: They’re non-editable; you can’t modify API names or primary keys.

Standard and legacy DMOs may appear identical in the UI, but can have different field names or field name capitalization. Fields may have been added to standard DMOs to extend the functionality of frozen legacy objects.

View the list of available objects below:

Abn Experiment Cohort DMO
Abn Experiment DMO
Abn Experiment Log DMO
Abn Experimentation Cohort Summary DMO
Abn Experimentation Daily Summary DMO
Abn Experimentation Summary DMO
Acad Term Enrl Policy Rule Log DMO
Academic Credential DMO
Academic Interest DMO
Academic Session Attendance DMO
Academic Session DMO
Academic Target DMO
Academic Term DMO
Academic Term Enrollment DMO
Academic Term Regstrn Timeline DMO
Academic Year DMO
Account Contact DMO
Account DMO
Account Location DMO
Account Plan DMO
Account Plan Objective DMO
Account Plan Participant DMO
Account Plan Product DMO
Account Plan Ptcp Stakeholder DMO
Account Plan Related Object Analysis DMO
Account Plan Relationship DMO
Account Plan Stakeholder Action DMO
Account Plan Stakeholder DMO
Account Plan Stakeholder Product DMO
Account Relationship DMO
Account Role DMO
Accounting Period DMO
Action Plan DMO
Action Plan Item DMO
Action Plan Template Assignment DMO
Action Plan Template DMO
Action Plan Template Item DMO
Action Plan Template Version DMO
Actionable List DMO
Actionable List Member DMO
Activity DMO
Activity Participant DMO
Activity Plan DMO
Activity Plan Sales Territory DMO
Activity Timing DMO
Activity Topic DMO
Ad Conversion Tag DMO
Ad DMO
Ad Exchange DMO
Ad Keyword DMO
Ad Site DMO
Ad Strategy DMO
Address DMO
Adverse Event Action DMO
Adverse Event Cause DMO
Adverse Event Contributing Factor DMO
Adverse Event DMO
Adverse Event Identifier DMO
Adverse Event Outcome DMO
Adverse Event Party DMO
Adverse Event Resulting Effect DMO
Adverse Event Support Info DMO
Affiliation DMO
Age Band Hlth Rsk Adj Fctr DMO
Agent Service Presence DMO
Agent Work DMO
Agent Work Skill DMO
Ai Agent Action DMO
Ai Agent Generative Ai Usage DMO
Ai Agent Interaction DMO
Ai Agent Interaction Message DMO
Ai Agent Interaction Step DMO
Ai Agent Message Attachment DMO
Ai Agent Moment DMO
Ai Agent Moment Interaction DMO
Ai Agent Session Attachment DMO
Ai Agent Session DMO
Ai Agent Session Log DMO
Ai Agent Session Participant DMO
Ai Agent Tag Association DMO
Ai Agent Tag Definition Association DMO
Ai Agent Tag Definition DMO
Ai Agent Tag DMO
Ai Agent Topic DMO
Ai Gateway Req Model Diag DMO
Ai Gateway Req Obj Rec Ctn DMO
Ai Gateway Req Obj Rec DMO
Ai Participant Insight DMO
Ai Retriever Quality Metric DMO
Air Travel Emissions Factor DMO
Air Travel Energy Use DMO
Allergy Intolerance DMO
Alternate Payment DMO
Analytics Generative Metadata DMO
Annual Emissions Inventory DMO
Annual Emssn Inventory Extension DMO
Annual Emssn Rdctn Target DMO
Anti Corruption Initiative Summary DMO
Applicant DMO
Application Decision DMO
Application DMO
Application Item DMO
Application Participant DMO
Application Recommendation DMO
Application Recommender DMO
Application Related Code DMO
Application Review DMO
Application Review Participant DMO
Application Task DMO
Application Task Item DMO
Application Timeline DMO
Appraisal Adjustment DMO
Appraisal DMO
Appraisal Item Add On DMO
Appraisal Item DMO
Appraisal Item Provider Val DMO
Asmt Qstn Materiality Tpc DMO
Assessment Action Item DMO
Assessment Definition DMO
Assessment DMO
Assessment Envelope DMO
Assessment Envelope Item DMO
Assessment Indicator Defined Value DMO
Assessment Indicator Definition DMO
Assessment Indicator Value DMO
Assessment Question Assignment DMO
Assessment Question DMO
Assessment Question Response DMO
Assessment Question Set DMO
Assessment Question Version DMO
Assessment Signature DMO
Assessment Task Content Document DMO
Assessment Task Definition DMO
Assessment Task DMO
Assessment Task Indicator Definition DMO
Assessment Task Order DMO
Asset Action Source DMO
Asset Depreciation DMO
Asset DMO
Asset Milestone DMO
Asset Operation DMO
Asset Operation Operator Behavior DMO
Asset Participant DMO
Asset Performance Summary DMO
Asset Sales Action DMO
Asset Service Action DMO
Asset Service Level Objective Consequence DMO
Asset Service Level Objective DMO
Asset State Period DMO
Asset Telematics Event DMO
Asset Telematics Event Fault Cd Mapping DMO
Asset Title DMO
Asset Warranty Term DMO
Assortment Assignment DMO
Assortment DMO
Assortment Product DMO
Attribute Definition DMO
Attribute Value DMO
Auth Location Permit Schedule DMO
Authorization Application Asset DMO
Authorization Application DMO
Authorization Application Place DMO
Authorization Form Consent DMO
Authorization Form Data Use DMO
Authorization Form DMO
Authorization Form Text DMO
Bank Transfer Tender DMO
Banker DMO
Benefit Action DMO
Benefit Application DMO
Benefit Assignment Adjustment DMO
Benefit Assignment DMO
Benefit Disbursement Adjustment DMO
Benefit Disbursement DMO
Benefit Disbursement Hold DMO
Benefit Disbursement Period DMO
Benefit DMO
Benefit Item Code DMO
Benefit Prvd Searchable Fld DMO
Benefit Schedule Assignment DMO
Benefit Schedule DMO
Benefit Session DMO
Benefit Specialty DMO
Benefit Type DMO
Billing Account DMO
Billing Arrangement DMO
Billing Forecast DMO
Billing Policy DMO
Billing Schedule DMO
Billing Schedule Group DMO
Billing Schedule Group Relationship DMO
Billing Treatment DMO
Billing Treatment Item DMO
Biodiversity Summary DMO
Bldg Enrgy Intensity Val DMO
Bldg Size Category DMO
Bnft Asgnt Bnft Item Code DMO
Bot DMO
Bot Version DMO
Branch Unit DMO
Branch Unit Related Record DMO
Brand DMO
Budget Allocation DMO
Budget Category DMO
Budget Category Value DMO
Budget DMO
Budget Period DMO
Building Energy Intensity DMO
Bulk Email Message DMO
Bulk Message DMO
Bundle Product DMO
Bus Oper Proc Cmpl Plcy Cl Ver DMO
Bus Reg Auth Type Dependency DMO
Business Insight DMO
Business Insight Indicator DMO
Business License Code Set DMO
Business Milestone DMO
Business Operations Process DMO
Business Period DMO
Business Process Definition DMO
Business Process Feedback DMO
Business Process Group DMO
Business Profile DMO
Business Regulatory Auth Type DMO
Business Type DMO
Buyer Intent DMO
Calendar Event DMO
Campaign DMO
Campaign Member DMO
Capture Payment DMO
Carbon Emission Scope Allocation DMO
Card Account DMO
Care Barrier Determinant DMO
Care Barrier Type DMO
Care Barrier2 DMO
Care Determinant DMO
Care Gap DMO
Care Limit Type DMO
Care Metric Target DMO
Care Observation DMO
Care Observation Identifier DMO
Care Observation Item DMO
Care Pgm Prov Healthcare Provider DMO
Care Plan Activity Detail DMO
Care Plan Activity DMO
Care Plan Detail DMO
Care Plan DMO
Care Plan Identifier DMO
Care Plan Template Benefit DMO
Care Plan Template DMO
Care Plan Template Goal DMO
Care Preauthorization DMO
Care Preauthorization Item DMO
Care Processing Error DMO
Care Program Assistance DMO
Care Program Campaign DMO
Care Program Detail DMO
Care Program DMO
Care Program Eligibility Rule DMO
Care Program Enrollee DMO
Care Program Enrollee Product DMO
Care Program Enrollee Status Period DMO
Care Program Enrollment Card DMO
Care Program Goal DMO
Care Program Identifier DMO
Care Program Product DMO
Care Program Provider Product DMO
Care Program Site Contract DMO
Care Program Site DMO
Care Program Status Period DMO
Care Program Team Member DMO
Care Program Team Member Role Period DMO
Care Request Diagnosis DMO
Care Request Diagnosis Identifier DMO
Care Request DMO
Care Request Drug DMO
Care Request Exchange Info DMO
Care Request Identifier DMO
Care Request Item DMO
Care Request Reviewer DMO
Care Request Supporting Cntnt DMO
Care Service Visit DMO
Care Service Visit Plan DMO
Care Specialty DMO
Case DMO
Case Episode DMO
Case Milestone DMO
Case Milestone Type DMO
Case Participant DMO
Case Proceeding Complaint DMO
Case Proceeding DMO
Case Proceeding Infraction DMO
Case Proceeding Participant DMO
Case Proceeding Result DMO
Case Program DMO
Case Related Issue DMO
Case Team Member Program DMO
Case Update DMO
Cash Tender DMO
Category Access DMO
Category DMO
Cc Aggr Controller Request DMO
Cc Aggr Detail Product Rcmd Rcmdr DMO
Cc Aggr Include Controller Rqst DMO
Cc Aggr Inventory By Location DMO
Cc Aggr Inventory By Location Grp DMO
Cc Aggr Ocapi Request DMO
Cc Aggr Payment Sales Summary DMO
Cc Aggr Product Co Buy DMO
Cc Aggr Product Rcmd Rcmdr DMO
Cc Aggr Product Recommendation DMO
Cc Aggr Product Sales Summary DMO
Cc Aggr Promotion Activation DMO
Cc Aggr Promotion Co Use DMO
Cc Aggr Promotion Sales Summary DMO
Cc Aggr Registration DMO
Cc Aggr Sales Summary DMO
Cc Aggr Scapi Request DMO
Cc Aggr Search Conversion DMO
Cc Aggr Search DMO
Cc Aggr Search Query DMO
Cc Aggr Source Code Activation DMO
Cc Aggr Source Code Sales DMO
Cc Aggr Visit Checkout DMO
Cc Aggr Visit DMO
Cc Aggr Visit Ip Address DMO
Cc Aggr Visit Referrer DMO
Cc Aggr Visit Robot DMO
Cc Aggr Visit User Agent DMO
Cc Dim Business Channel DMO
Cc Dim Campaign DMO
Cc Dim Coupon DMO
Cc Dim Currency DMO
Cc Dim Customer DMO
Cc Dim Date DMO
Cc Dim Geography DMO
Cc Dim Locale DMO
Cc Dim Location DMO
Cc Dim Location Group DMO
Cc Dim Payment Method DMO
Cc Dim Product DMO
Cc Dim Promotion DMO
Cc Dim Site DMO
Cc Dim Source Code Group DMO
Cc Dim Time DMO
Cc Dim Time Zone DMO
Cc Dim User Agent DMO
Cc Fact Customer List Snapshot DMO
Cc Fact Customer Registration DMO
Cc Fact Inv Rec Snapshot DMO
Cc Fact Inv Rec Snapshot Hourly DMO
Cc Fact Order Line Item DMO
Cc Fact Order Payment DMO
Cc Fact Promotion Activation DMO
Cc Fact Promotion Order Line Item DMO
Cc Fact Realtime Metric DMO
Cc Fact Source Code Activation DMO
Change Request Configuration Item DMO
Change Request DMO
Change Request Related Issue DMO
Change Request Related Item DMO
Channel Engagement DMO
Check Tender DMO
Claim Case DMO
Claim Coverage DMO
Claim Diagnosis DMO
Claim DMO
Claim Item DMO
Claim Item Participant DMO
Claim Participant DMO
Claim Payment Detail DMO
Claim Payment DMO
Claim Supporting Information DMO
Clean Energy Project DMO
Climate Chg Emssn Finc Summary DMO
Climate Chg Risk Opp Summary DMO
Clinical Alert DMO
Clinical Encounter Diagnosis DMO
Clinical Encounter DMO
Clinical Encounter Facility DMO
Clinical Encounter Identifier DMO
Clinical Encounter Provider DMO
Clinical Encounter Reason DMO
Clinical Encounter Service Request DMO
Clinical Measure DMO
Clinical Service Request Detail DMO
Clinical Service Request DMO
Clinical Service Request Identifier DMO
Cnfg Item Attribute DMO
Cnfg Item Attribute Value DMO
Cnfg Item Relationship DMO
Cnfg Item Type Definition DMO
Code Set Bundle DMO
Code Set DMO
Collection Plan DMO
Collection Plan Item DMO
Collection Plan Reason DMO
Command Center Alert DMO
Commodity Usage DMO
Communication Subscription Channel Type DMO
Communication Subscription Consent DMO
Communication Subscription DMO
Communication Subscription Timing DMO
Competency DMO
Competency Related Object DMO
Complaint Case DMO
Complaint DMO
Complaint Participant DMO
Compliance Audit DMO
Compliance Audit Policy Clause DMO
Compliance Audit Regulation Clause DMO
Compliance Audit Risk DMO
Compliance Control DMO
Compliance Control Version DMO
Compliance Evidence Artifact DMO
Compliance Evidence Request Artifact DMO
Compliance Evidence Request DMO
Compliance Plcy Cmpl Cl Ver DMO
Compliance Policy Clause DMO
Compliance Policy Clause Version DMO
Compliance Policy Comms Recipient DMO
Compliance Policy Comms Response DMO
Compliance Policy Communication DMO
Compliance Policy DMO
Compliance Policy Version DMO
Cond Intrctn Hlth Rsk Adj Fctr DMO
Configuration Item DMO
Consent Action DMO
Consent Status DMO
Constituent Role DMO
Consumed Location Product DMO
Contact Encounter DMO
Contact Encounter Participant DMO
Contact Point Address DMO
Contact Point App DMO
Contact Point Consent DMO
Contact Point Digital Id DMO
Contact Point DMO
Contact Point Email DMO
Contact Point OTT Service DMO
Contact Point Phone DMO
Contact Point Social DMO
Contact Profile DMO
Contact Request DMO
Content Document DMO
Content Document Relationship DMO
Content Document Version DMO
Content Link DMO
Content Source DMO
Content Taxonomy DMO
Content Taxonomy Model DMO
Content Taxonomy Related Term DMO
Content Taxonomy Term DMO
Content Taxonomy Term Rel Object DMO
Content Taxonomy Term Rel Type DMO
Content Taxonomy Term Relationship DMO
Contract DMO
Contract Doc Ver Content Doc DMO
Contract Document Version DMO
Contract Line DMO
Conv Channel Engagement Summary DMO
Conv Channel Engmt Summary Subject DMO
Conv Chnl Engmt Summary Ptcp DMO
Conv Reason Report Definition DMO
Conv Reason Report Segment Def DMO
Conversation DMO
Conversation Entry DMO
Conversation Entry Transcript Excerpt DMO
Conversation Reason Category DMO
Conversation Reason DMO
Conversion Engagement Summary DMO
Cost Book DMO
Cost Book Entry DMO
Country DMO
Coupon Definition DMO
Coupon DMO
Course Credit Transfer Appln DMO
Course Offering Attendance DMO
Course Offering DMO
Course Offering Participant DMO
Course Offering Participation DMO
Course Offering Ptcp Result DMO
Course Offering Relationship DMO
Course Offering Rgstr Timeline DMO
Course Offering Rubric DMO
Course Offering Schedule DMO
Course Offering Schedule Tmpl DMO
Course Ofr Ptcp Activity Grade DMO
Coverage Benefit DMO
Coverage Benefit Item DMO
Coverage Benefit Item Limit DMO
Coverage Benefit Verification Request DMO
Crbn Credit Alloc DMO
Crbn Credit Alloc Item DMO
Crbn Credit Distribution DMO
Crbn Credit Project DMO
Crbn Emssn Scope Alloc DMO
Crbn Emssn Scope Alloc Val DMO
Credit Memo DMO
Credit Memo Line DMO
Credit Memo Line Tax DMO
Credit Tender DMO
Currency Dated Conversion Rate DMO
Currency Static Conversion Rate DMO
Custody Chain Entry DMO
Custody Item DMO
Custody Item Regulatory Code Violation DMO
Custody Item Relation DMO
Customer Intelligence Journey Stage DMO
Data Use Legal Basis DMO
Data Use Purpose Consent Action DMO
Data Use Purpose DMO
Dcsn Optimization Option Summary DMO
Dcsn Optimization Summary DMO
Dedup Engmt Anlss Text Insight Assoc DMO
Dedup Engmt Anlss Text Insight DMO
Delivery Engagement Summary DMO
Delivery Verification Engmt Summary DMO
Deposit Account DMO
Depreciation Plan DMO
Device Application Engagement DMO
Device Application Template DMO
Device DMO
Device Type Configuration DMO
Diagnostic Summary DMO
Diagnostic Summary Identifier DMO
Digital Content Channel DMO
Digital Content DMO
Digital Content Electronic Media DMO
Digital Content Publish Channel DMO
Digital Content Relationship DMO
Digital Content Space Channel DMO
Digital Content Space DMO
Digital Signature DMO
Digital Wallet DMO
Disclosure DMO
Disclosure Reporting Period DMO
Disease Criteria Condition DMO
Disease Criteria DMO
Disease Definition DMO
Disease Investigation Case DMO
Disease Investigation DMO
Disease Outbreak DMO
Diversity Equity Inclusion Summary DMO
Doc Clause Set Asmt Qstn DMO
Document Checklist Item DMO
Document Clause DMO
Document Clause Set DMO
Document Playbook DMO
Document Playbook Version DMO
Donor Gift Concept DMO
Donor Gift Concept Opportunity DMO
Donor Gift Summary DMO
Driver Performance Summary DMO
Economic Performance Summary DMO
Educ Inst Searchable Profile DMO
Educ Institution Offering DMO
Education Application DMO
Educational Info Request DMO
Electr Lifecycl Emssn Fctr Set DMO
Electricity Emissions Factor Set DMO
Electronic Media DMO
Email Content DMO
Email Engagement DMO
Email Engagement Frequency DMO
Email Engagement Quality Score DMO
Email Engagement Score DMO
Email Message DMO
Email Message Fragment DMO
Email Publication DMO
Email Send Time Optimization DMO
Email Template DMO
Email Template Fragment DMO
Email Template Related Fragment DMO
Email Template Snapshot DMO
Emissions Activity DMO
Emissions Allocation DMO
Emissions Forecast Fact DMO
Employee Demographic Summary DMO
Employee Development Summary DMO
Employee DMO
Employment Benefit Summary DMO
Employment Compensation Summary DMO
Employment DMO
Employment Offer DMO
Employment Offer Vetting Evaluation DMO
Emssn Rdctn Commitment DMO
Emssn Reduction Target DMO
Energy Attr Cert Credit DMO
Energy Attr Cert Purchase DMO
Energy Attr Credit Dstr DMO
Engagement Action DMO
Engagement Analysis Command Execution DMO
Engagement Analysis Grouping Execution DMO
Engagement Analysis Text Assoc DMO
Engagement Analysis Text Association DMO
Engagement Analysis Text Direct Feedback DMO
Engagement Analysis Text DMO
Engagement Analysis Text Insight DMO
Engagement Analysis Text Participant DMO
Engagement Analysis Text Session DMO
Engagement Channel Action DMO
Engagement Channel DMO
Engagement Channel Participant DMO
Engagement Channel Type Consent DMO
Engagement Channel Type DMO
Engagement Channel Usage DMO
Engagement Participant App Role DMO
Engagement Topic DMO
Engmt Insight Knwlg Article Version DMO
Enrollment Eligibility Criteria DMO
Enterprise User Activity DMO
Enterprise User Activity Ptcp DMO
Entp User DMO
Entp User Email DMO
Entp User Identification DMO
Environmental Risk DMO
Error Engagement DMO
Estmt Energy Use Criteria DMO
Estmt Energy Use Job Run DMO
Event Management Participant Type DMO
Event Mgmt Participant Role DMO
Event Mgmt Participant Type Role Map DMO
Event Plan DMO
Examination DMO
Expense Type DMO
Expert DMO
External Assessment Definition DMO
External Learning DMO
External Learning Ptcp Result DMO
Extl Ptcp Rslt Lrnr Pgm Rqmt DMO
Feature Usage DMO
Financial Account Address DMO
Financial Account Balance DMO
Financial Account Custodian Advisor DMO
Financial Account DMO
Financial Account Fee DMO
Financial Account Interest Rate DMO
Financial Account Limit DMO
Financial Account Milestone DMO
Financial Account Party DMO
Financial Account Performance Snapshot DMO
Financial Account Transaction DMO
Financial Application DMO
Financial Application Item DMO
Financial Application Item Proposal DMO
Financial Asset Portfolio Target Allocation DMO
Financial Custodian Advisor DMO
Financial Custodian DMO
Financial Customer DMO
Financial Goal DMO
Financial Goal Funding DMO
Financial Goal Party DMO
Financial Holding Closed Position DMO
Financial Holding DMO
Financial Holding Summary DMO
Financial Plan DMO
Financial Security DMO
Fincl Acct Asset Und Mgmt Snpsht DMO
Fiscal Calendar DMO
Fld Svc Obj Chg DMO
Fld Svc Obj Chg Dtl DMO
Fleet Asset DMO
Fleet DMO
Fleet Participant DMO
Flow DMO
Flow Element DMO
Flow Element Run DMO
Flow Run DMO
Flow Version DMO
Flow Version Occurrence DMO
Forecast Item Manager Version Amount DMO
Forecast Item Owner Version Amount DMO
Forecasting Fact DMO
Forecasting Item DMO
Forecasting Item Historical Trend DMO
Forecasting Prediction DMO
Forecasting Quota DMO
Forecasting Type DMO
Formulary DMO
Formulary Item DMO
Freight Hauling Emission Factor DMO
Freight Hauling Energy Use DMO
Fulfillment Order DMO
Fulfillment Order Price Adj DMO
Fulfillment Order Price Adj Tax DMO
Fulfillment Order Product DMO
Fulfillment Order Product Price Adj DMO
Fulfillment Order Product Tax DMO
Fulfillment Order Tax DMO
Fulfillment Plan DMO
Fulfillment Step Dependency DMO
Fulfillment Step DMO
Fulfillment Step Source DMO
Funding Award Amendment DMO
Funding Award Disbursement DMO
Funding Award DMO
Funding Award Requirement DMO
Funding Opportunity DMO
Game Definition DMO
Game Participant DMO
Game Participant Reward DMO
Game Reward DMO
Gen Ai Content Quality Category DMO
Gen Ai Content Quality DMO
Gen Ai Feedback Additional Info DMO
Gen Ai Feedback DMO
Gen Ai Gateway Req Obj Rec Ctn DMO
Gen Ai Gateway Req Obj Rec DMO
Gen Ai Gateway Request Addl Info DMO
Gen Ai Gateway Request DMO
Gen Ai Gateway Request Tag DMO
Gen Ai Gateway Response DMO
Gen Ai Gtwy Req Model Diagnostic DMO
Gen Ai Response App Generation DMO
Gen Ai Response Generation DMO
Generated Action Insight DMO
Generated Operation Plan DMO
Generated Operation Plan Execution DMO
Generated Operation Plan Step DMO
Generated Operation Plan Step Execution DMO
Generated Waste DMO
Geo Demographic Distribution DMO
Gift Actuarial Entry DMO
Gift Agreement DMO
Gift Batch DMO
Gift Cmt Change Attr Log DMO
Gift Commitment DMO
Gift Commitment Schedule DMO
Gift Default Designation DMO
Gift Designation DMO
Gift Entry DMO
Gift Refund DMO
Gift Soft Credit DMO
Gift Stewardship Activity DMO
Gift Stewardship DMO
Gift Transaction Designation DMO
Gift Transaction DMO
Gift Value Forecast DMO
Goal Assignment Detail DMO
Goal Assignment DMO
Goal Definition DMO
Goal Definition Product DMO
Goods Product DMO
Gov Financial Assistance Summary DMO
Ground Travel Emission Factor DMO
Ground Travel Energy Use DMO
Harmonized Content Association DMO
Harmonized Content DMO
Hcp Facility Network DMO
Hcp Network Contract DMO
Hcp Treated Condition DMO
Health Cond Definition Relationship DMO
Health Condition Definition DMO
Health Risk Eval Detail DMO
Health Risk Evaluation DMO
Health Score Category DMO
Health Score DMO
Health Score Range Classification DMO
Healthcare Diagnosis DMO
Healthcare Facility DMO
Healthcare Facility Identifier DMO
Healthcare Facility Service DMO
Healthcare Payer Network DMO
Healthcare Performer DMO
Healthcare Practitioner Facility DMO
Healthcare Procedure DMO
Healthcare Provider DMO
Healthcare Provider Facility Specialty DMO
Healthcare Provider Network Tier DMO
Healthcare Provider NPI DMO
Healthcare Provider Searchable Field DMO
Healthcare Provider Service DMO
Healthcare Provider Specialty DMO
Healthcare Provider Taxonomy DMO
Healthcare Service Detail DMO
Healthcare Service DMO
Healthcare Taxonomy DMO
Hier Cond Hlth Code Mapping DMO
Hier Cond Hlth Rsk Adj Fctr DMO
Hlthcr Practitioner Facility Identifier DMO
Hotel Stay Emission Factor DMO
Hotel Stay Energy Use DMO
Household DMO
Identity Match DMO
Image DMO
Impact Strategy Assignment DMO
Impact Strategy DMO
In Person Engagement DMO
In Person Meeting DMO
In Store Location DMO
Incident Configuration Item DMO
Incident DMO
Incident Related Item DMO
Indicator Assignment DMO
Indicator Definition DMO
Indicator Performance Period DMO
Indicator Result DMO
Individual DMO
Inflation Rate DMO
Info Library External Document DMO
Inspection Assessment Indicator DMO
Inspection Type DMO
Insurance Coverage Type DMO
Insurance Policy Asset DMO
Insurance Policy Coverage DMO
Insurance Policy Coverage Participant DMO
Insurance Policy DMO
Insurance Policy Member Asset DMO
Insurance Policy Participant DMO
Insurance Policy Transaction DMO
Interest Tag Definition DMO
Inventory Product Disbursement DMO
Inventory Request DMO
Inventory Request Item DMO
Inventory Serialized Product DMO
Inventory Transfer DMO
Investment Account DMO
Invoice Address Group DMO
Invoice Batch Run DMO
Invoice DMO
Invoice Line DMO
Invoice Line Tax DMO
Involvement Group DMO
Involvement Group Member DMO
Issue Relationship DMO
Job Appln Searchable Field DMO
Job Position Assignment DMO
Job Position DMO
Job Position Pay Grade DMO
Job Position Qualification DMO
Job Position Recruitment Requisition DMO
Job Position Shift DMO
Job Posting Searchable Field DMO
Journey Decisioning Agent Decision DMO
Knowledge Article Category DMO
Knowledge Article DMO
Knowledge Article Engagement DMO
Knowledge Article Feedback DMO
Knowledge Article Version DMO
Knowledge Src File Ref Dmo DMO
Lead DMO
Lead Engagement DMO
Lead Line Item DMO
Lead Preferred Seller DMO
Learner Campus Spaces Activity DMO
Learner Cost Item DMO
Learner Cost Summary DMO
Learner Financial Aid Application DMO
Learner Financial Aid Standing DMO
Learner Learning System Activity DMO
Learner Pathway DMO
Learner Pathway Item DMO
Learner Profile DMO
Learner Program DMO
Learner Program Requirement DMO
Learner Program Rqmt Progress DMO
Learning Achievement DMO
Learning Course DMO
Learning DMO
Learning Equivalency DMO
Learning Eqv Achv Mapping DMO
Learning Foundation Item DMO
Learning Outcome Item DMO
Learning Pathway Template DMO
Learning Pathway Template Item DMO
Learning Pathway Tmpl Pgm Plan DMO
Learning Program DMO
Learning Program Plan DMO
Learning Program Plan Rqmt DMO
Legal Entity Accounting Period DMO
Legal Entity DMO
Life Science Drug Distribution Data DMO
Life Science Drug Prescription Data DMO
Life Science Marketable Product DMO
Linked Knowledge Article DMO
Loan Account DMO
Locale DMO
Location DMO
Location Group Assignment DMO
Location Group DMO
Location Group Prod Excl Chg DMO
Location Group Prod Inv Chg DMO
Location Product Inventory Change DMO
Location Product Inventory DMO
Location Shipping Carrier Method DMO
Loyalty Aggregated Point Expiration Ledger DMO
Loyalty Benefit DMO
Loyalty Benefit Type DMO
Loyalty Journal Subtype DMO
Loyalty Journal Type DMO
Loyalty Ledger DMO
Loyalty Ledger Traceability DMO
Loyalty Member Currency DMO
Loyalty Member Tier DMO
Loyalty Membership Lifecycle DMO
Loyalty Partner Product DMO
Loyalty Pgm Member Linked Partner DMO
Loyalty Program Badge DMO
Loyalty Program Currency DMO
Loyalty Program Currency Subtype DMO
Loyalty Program Currency Tier DMO
Loyalty Program DMO
Loyalty Program Engagement Attribute DMO
Loyalty Program Engmt Attribute Promotion DMO
Loyalty Program Group Member Relationship DMO
Loyalty Program Member Attribute Value DMO
Loyalty Program Member Badge DMO
Loyalty Program Member Case DMO
Loyalty Program Member DMO
Loyalty Program Member Merge DMO
Loyalty Program Member Promotion DMO
Loyalty Program Partner Currency DMO
Loyalty Program Partner DMO
Loyalty Program Partner Ledger DMO
Loyalty Program Partner Ledger Summary DMO
Loyalty Program Partner Prepaid Pack DMO
Loyalty Program Partner Promotion DMO
Loyalty Tier Benefit DMO
Loyalty Tier DMO
Loyalty Tier Eligibility Src DMO
Loyalty Tier Group DMO
Loyalty Tier Model DMO
Loyalty Tier Mshp Fee Option DMO
Loyalty Tier Promotion DMO
Loyalty Transaction Journal DMO
Mail Letter DMO
Mail Letter Engagement DMO
Managed Care Program Prfm DMO
Managed Event DMO
Managed Event Session DMO
Managed Event Type DMO
Market Audience DMO
Market Journey Activity DMO
Market Segment DMO
Marketing Channel DMO
Marketing Channel Engaged Audience DMO
Marketing Channel Targeted Segment DMO
Marketing Email List DMO
Marketing Grounding File U Dmo DMO
Marketing Journey Activity DMO
Marketing Journey Activity Run DMO
Marketing Journey DMO
Master Product DMO
Materiality Topic DMO
Materiality Topic Doc Clause Set DMO
Materiality Topic Reference DMO
Meal Card Activity DMO
Measure Definition DMO
Media Buy DMO
Media Buy Package DMO
Media Engagement DMO
Medical Insight Account DMO
Medical Insight DMO
Medical Insight Goal Definition DMO
Medical Insight Product DMO
Medical Insight User Reaction DMO
Medication DMO
Medication Identifier DMO
Member Benefit DMO
Member Plan DMO
Mentoring Profile DMO
Message Engagement DMO
Message Template DMO
Messaging Session DMO
Mgd Event Sess Subject Assignment DMO
Mkt Expert Channel Rate Table DMO
Mng Event Budget DMO
Mng Event Participant DMO
Mng Event Product DMO
Mng Event Resource DMO
Mng Event Resource Preference DMO
Monthly Usage Trkg Data Gap DMO
Network DMO
Network Referenced Object DMO
Network Usage DMO
Notebook Ai Grounding File Udmo DMO
Object Milestone DMO
Occupation DMO
Occupation Group DMO
Offer DMO
Offer Group Assigned Offer DMO
Offer Group DMO
Offer Market Segment DMO
Offer Marketing Email List DMO
Offer Product Category DMO
Offer Product DMO
Offer Product Order Engagement DMO
Offer Sales Order Product Engagement DMO
Offer Treatment DMO
Operating Hours DMO
Operating Hours Time Slot DMO
Operator Performance Summary DMO
Opportunity Contact DMO
Opportunity DMO
Opportunity Historical Trend DMO
Opportunity History DMO
Opportunity Influence DMO
Opportunity Preferred Seller DMO
Opportunity Product DMO
Opportunity Split DMO
Opportunity Split Type DMO
Opportunity Stage DMO
Order Delivery Method DMO
Org Payment Prac Summary DMO
Organization Incident Summary DMO
Other Emission Factor Set Item DMO
Other Emissions Factor Set DMO
Othr Lifecycl Emssn Fctr Set DMO
Othr Lifecycl Emssn Fctr Set Item DMO
Outcome Activity DMO
Outcome Intent DMO
Outreach Source Code DMO
Outreach Summary DMO
Party Accreditation DMO
Party Award DMO
Party Board Certification DMO
Party Board Certification Identifier DMO
Party Business License DMO
Party Category DMO
Party Consent DMO
Party DMO
Party Expense DMO
Party Financial Asset DMO
Party Financial Liability DMO
Party Identification DMO
Party Income DMO
Party Interest Tag DMO
Party Philanthropic Assessment DMO
Party Philanthropic Indicator DMO
Party Philanthropic Milestone DMO
Party Philanthropic Occurrence DMO
Party Philanthropic Rsrch Prfl DMO
Party Profile Address DMO
Party Profile DMO
Party Promotion Usage DMO
Party Publication DMO
Party Related Party DMO
Party Relationship Type DMO
Party Role DMO
Party Role Type DMO
Patient DMO
Patient Health Condition Detail DMO
Patient Health Condition DMO
Patient Health Reaction DMO
Patient Immunization DMO
Patient Immunization Identifier DMO
Patient Med Recile Stmt Recommendation DMO
Patient Med Recon Recommendation DMO
Patient Medical Procedure Detail DMO
Patient Medical Procedure DMO
Patient Medical Procedure Identifier DMO
Patient Medication Administration DMO
Patient Medication Administration Dtl DMO
Patient Medication Dispense DMO
Patient Medication Dosage DMO
Patient Medication Reconciliation DMO
Patient Medication Request DMO
Patient Medication Statement Detail DMO
Patient Medication Statement DMO
Patient Medication Statement Identifier DMO
Patient Registered Device DMO
Patient Registered Device Identifier DMO
Pay Grade DMO
Pay Grade Step DMO
Pay Grade Step Location DMO
Payment Card DMO
Payment Instrument DMO
Payment Method DMO
Payment Request DMO
Payment Request Line DMO
Payment Term DMO
Payment Term Item DMO
Persnl Rcmd Item Log DMO
Persnl Rcmd Log DMO
Person Academic Credential DMO
Person Affinity DMO
Person Competency DMO
Person Disability DMO
Person Education DMO
Person Employment DMO
Person Examination DMO
Person Language DMO
Person Life Event DMO
Person Location Availability DMO
Person Name DMO
Person Public Profile DMO
Person Public Profile Pref Set DMO
Person Skill DMO
Person Trait DMO
Personalization Decision DMO
Personalization Log DMO
Personalization Point DMO
Personalization Schema DMO
Personalizer DMO
Petition Type DMO
Petitionable Outcome DMO
Plan Benefit DMO
Plan Benefit Item DMO
Planned Gift Annuity Rate DMO
Planned Gift DMO
Planned Gift Performance DMO
Planning Annual Read Measure DMO
Planning Daily Read Measure DMO
Planning Dimension Node DMO
Planning Dimension Node Hierarchy DMO
Planning Dimension Node Relation DMO
Planning Monthly Read Measure DMO
Pltn Impact Risk Opp Summary DMO
Position Benefit DMO
Position DMO
Position Pay Grade DMO
Position Qualification DMO
Prepaid Card DMO
Presentation Click Stream Entry DMO
Presentation DMO
Presentation Forum DMO
Presentation Linked Page DMO
Presentation Page DMO
Presentation Page Product DMO
Presentation Party Access DMO
Price Adjustment Group DMO
Price Book DMO
Price Book Entry DMO
Privacy Consent Log DMO
Problem Configuration Item DMO
Problem DMO
Problem Related Item DMO
Process Exception DMO
Procurement Emission Factor Set DMO
Procurement Emission Factor Set Item DMO
Prod Svc Cmpn Def Ptnr Inv DMO
Prod Svc Cmpn Grp Def Ptnr DMO
Prodt Svc Campaign Grp Def DMO
Prodt Svc Cmpn Cse Prodt DMO
Prodt Svc Cmpn Pref Ptnr DMO
Prodt Svc Cmpn Prodt Btch DMO
Prodt Svc Cmpn Rel Cse DMO
Prodt Svc Cmpn Work Type DMO
Producer DMO
Producer Policy Assignment DMO
Product Attribute DMO
Product Browse Engagement DMO
Product Catalog Category DMO
Product Catalog DMO
Product Category DMO
Product Category Product DMO
Product DMO
Product Emissions Factor DMO
Product Guidance DMO
Product Image DMO
Product Order Engagement DMO
Product Packaging Unit DMO
Product Related Component DMO
Product Related Product DMO
Product Service Campaign DMO
Product Service Campaign Item DMO
Product Svc Campaign Def DMO
Product Translation DMO
Production Batch DMO
Prog Based Hlth Rsk Asmt Fctr DMO
Program Benefit DMO
Program Cohort DMO
Program Cohort Member DMO
Program DMO
Program Enrollment DMO
Program Enrollment Eligibility Criteria DMO
Program Initiative DMO
Program Initiative Enrl DMO
Program Term Application Timeline DMO
Promotion Account DMO
Promotion Actionable List DMO
Promotion Channel DMO
Promotion DMO
Promotion Engagement DMO
Promotion Item Engagement DMO
Promotion Limit DMO
Promotion Loyalty Partner Product DMO
Promotion Market Segment DMO
Promotion Offer DMO
Promotion Offer Product DMO
Promotion Offer Product Measure DMO
Promotion Party Transaction DMO
Promotion Product Category DMO
Promotion Product DMO
Promotion Product Measure DMO
Promotion Reward Def Audience DMO
Promotion Reward Definition DMO
Promotion Reward Definition Product DMO
Promotion Stage DMO
Promotion Stage Template DMO
Promotion Template DMO
Prospect DMO
Provider Activity Goal DMO
Provider Activity Goal Measure DMO
Provider Activity Measure Type DMO
Provider Offering DMO
Provider Visit DMO
Provider Visit Dtl Product Message DMO
Provider Visit Marketing Item DMO
Provider Visit Product Detailing DMO
Provider Visit Product Discussion DMO
Provider Visit Requested Sample DMO
Purchaser Plan Association DMO
Purchaser Plan DMO
Quote DMO
Quote Product DMO
Real Estate Property DMO
Rebate Claim DMO
Rebate Member Product Aggregate DMO
Rebate Payment DMO
Rebate Pgm Rbt Type Bnft Mapping DMO
Rebate Prgm Mbr Payout Adjustment DMO
Rebate Program DMO
Rebate Program Member DMO
Rebate Program Member Payout DMO
Rebate Program Payout Period DMO
Rebate Program Rbt Typ Benefit DMO
Rebate Program Rbt Typ Filter DMO
Rebate Program Rbt Typ Payout DMO
Rebate Program Rbt Typ Payout Src DMO
Rebate Program Rbt Typ Src Itm DMO
Rebate Program Rbt Type Product DMO
Rebate Program Rebate Type DMO
Received Document DMO
Record Action Selectable Item Extract DMO
Record Aggregation Result DMO
Record Alert DMO
Recruitment Content Section DMO
Recruitment Posting Content Section DMO
Recruitment Posting DMO
Recruitment Requisition DMO
Recruitment Requisition Location DMO
Recruitment Requisition Participant DMO
Recurrence Schedule DMO
Reference Data Load Log DMO
Referral DMO
Refrigerant Emission Factor DMO
Reg Cl Cmpl Control Ver DMO
Reg Cl Cmpl Plcy Cl Ver DMO
Regulation Clause DMO
Regulation Clause Version DMO
Regulation DMO
Regulatory Auth Type Product DMO
Regulatory Authority DMO
Regulatory Authorization Type DMO
Regulatory Code Assessment Ind DMO
Regulatory Code DMO
Regulatory Code Relation DMO
Regulatory Code Violation DMO
Regulatory Transaction Fee DMO
Regulatory Transaction Fee Item DMO
Rela Anlss Node DMO
Rela Anlss Node Rela DMO
Rela Anlss Node Rela Evid DMO
Rela Anlss Source DMO
Relationship Analysis DMO
Rental Car Emissions Factor DMO
Rental Car Energy Use DMO
Reported Consumption DMO
Required Document DMO
Required Product DMO
Required Skill DMO
Research Study Candidate DMO
Research Study Candidate Identifier DMO
Research Study Candidate Status Period DMO
Research Study DMO
Research Study Identifier DMO
Research Study Protocol Definition DMO
Research Study Relationship DMO
Resource Work Shift DMO
Retail Store DMO
Retail Store Group Assignment DMO
Retail Store Group DMO
Retail Store Product DMO
Retail Visit KPI DMO
Return Order DMO
Return Order Prod Price Adj DMO
Return Order Product DMO
Return Order Product Tax DMO
Revenue Transaction Error Log DMO
Rglty Code Reg Clause Ver DMO
Rglty Code Viol Reg Cl Ver DMO
Risk Cmpl Ctl Version DMO
Risk DMO
Risk Eval Survey Invt DMO
Risk Evaluation DMO
Risk Impacted Record DMO
Sales Agreement DMO
Sales Agreement Prod Schedule DMO
Sales Agreement Product DMO
Sales Channel DMO
Sales Model DMO
Sales Order Change Log DMO
Sales Order Delivery Group DMO
Sales Order DMO
Sales Order Payment Summary DMO
Sales Order Price Adjustment DMO
Sales Order Product DMO
Sales Order Product Engagement DMO
Sales Order Product Price Adjustment DMO
Sales Order Product Price Adjustment Tax DMO
Sales Order Product Tax DMO
Sales Store DMO
Sales Territory Account Prodt Msg Score DMO
Sales Territory Account Rcmd Action DMO
Sales Territory Account Score DMO
Sales Territory Business Plan DMO
Sales Territory DMO
Sales Transaction Fulfillment Request DMO
Saved Application Reference DMO
Scheduling Policy DMO
Scope3Carbon Footprint DMO
Scope3Emissions Source DMO
Scope3Procurement Item DMO
Scope3Procurement Summary DMO
Search Resource DMO
Searchable Reference Document DMO
Service Appointment Assigned Resource DMO
Service Appointment DMO
Service Campaign DMO
Service Campaign Member DMO
Service Campaign Member Item DMO
Service Presence Status DMO
Service Proc Prodt Catg Prodt Extract DMO
Service Process Definition DMO
Service Request DMO
Service Schd Rqst Rsrc Assignment DMO
Service Schd Rqst Rule Violation DMO
Service Schedule Request DMO
Service Schedule Rqst Appointment DMO
Service Territory DMO
Service Territory Resource DMO
Sfdc Api Total Usage Event Log DMO
Sfdc Fld Svc Mobile Ux Actvty Event Log DMO
Sfdc Fld Svc Mobile Ux Error Event Log DMO
Sfdc Fld Svc Mobile Ux Log Event Log DMO
Sfdc Lght Page View Event Log DMO
Sfdc Login Event Log DMO
Sfdc Report Event Log DMO
Sfdc Ui Agent Intrctn Event Log DMO
Shipment DMO
Shipment Product DMO
Shipping Carrier DMO
Shipping Carrier Method DMO
Shopping Cart DMO
Shopping Cart Engagement DMO
Shopping Cart Event Type DMO
Shopping Cart Product Engagement DMO
Shopping Wishlist Engagement DMO
Shopping Wishlist Item Engagement DMO
Skill DMO
SMS Publication DMO
SMS Template DMO
Social Contribution Summary DMO
Social Message DMO
Social Message Engagement DMO
Social Page DMO
Software Application DMO
Specimen DMO
Sprint DMO
Staged Regulation Clause DMO
Staged Regulation DMO
State Province DMO
Stationary Asset Carbon Footprint DMO
Stationary Asset Energy Use DMO
Stationary Asset Env Source DMO
Stationary Asset Water Activity DMO
Stnry Asset Annual Fact DMO
Stnry Asset Crbn Ftprnt Itm DMO
Stnry Asset Water Footprint DMO
Stnry Asset Wtr Ftprnt Itm DMO
Store Product Summary DMO
Subject Assignment DMO
Subject Category DMO
Subject DMO
Success Team DMO
Suggested Assessment Definition DMO
Suggested Assessment Reason DMO
Supplier DMO
Supplier Product DMO
Supplier Risk Score DMO
Survey DMO
Survey Invitation DMO
Survey Page DMO
Survey Question Choice DMO
Survey Question DMO
Survey Question Response DMO
Survey Question Score DMO
Survey Question Section DMO
Survey Response DMO
Survey Subject DMO
Survey Version DMO
Sustainability Credit DMO
Sustainability Purchase DMO
Sustainability Scorecard DMO
Sustainability Stakeholder DMO
Sustainability Task DMO
Sustainability Task Group DMO
Sustn Material Use Summary DMO
Svc Schd Request Terr Summary DMO
Task DMO
Tax Disclosure Summary DMO
Tax DMO
Tax Policy DMO
Tax Treatment DMO
Team DMO
Team Member DMO
Telematics Provider DMO
Telemetry Log DMO
Telemetry Metrics DMO
Telemetry Trace Span DMO
Tenant Consumption Insights DMO
Territory Model DMO
Time Period DMO
Tracked Communication Detail DMO
Tracked Communication DMO
Trade In Tender DMO
Unified Catalog Enrichment DMO
Unified Catalog Metadata DMO
Unified Catalog Metadata Rel DMO
Unit Of Measure DMO
Unitof Measure Conversion DMO
User DMO
User Group DMO
User Group Relationship DMO
User Role DMO
User Sales Territory DMO
Vehicle Asset Carbon Footprint DMO
Vehicle Asset Emissions Source DMO
Vehicle Asset Energy Use DMO
Vehicle Definition DMO
Vehicle DMO
Vehicle Performance Summary DMO
Vehicle Telematics Event DMO
Vehicle Telematics Event Fault Cd Map DMO
Vehicle Trip DMO
Vehicle Trip Driver Behavior DMO
Vetting Evaluation DMO
Video Call DMO
Violation Enforcement Action DMO
Violation Type Assessment Ind DMO
Violation Type DMO
Violation Type Relation DMO
Visit DMO
Visitor DMO
Voice Call DMO
Voice Call Engagement DMO
Volunteer Initiative DMO
Voucher Definition DMO
Voucher DMO
Warranty Term DMO
Waste Footprint DMO
Waste Footprint Item DMO
Watchlisted Learner DMO
Web Event Engagement Summary DMO
Web Page Engagement Summary DMO
Web Search Engagement DMO
Web Store DMO
Web Store Product Catalog DMO
Webpage DMO
Website DMO
Website Engagement DMO
Website Event DMO
Website Item Engagement DMO
Website Publication DMO
Website Source DMO
Website Web Store DMO
Work Order DMO
Work Order Item DMO
Work Resource Absence DMO
Work Resource DMO
Work Resource Skill DMO
Work Type DMO
Work Type Group Role DMO
Worker Compensation Coverage Class DMO
Wst Dispo Emssn Fctr Set DMO
Wst Dispo Emssn Fctr Set Itm DMO
Yearly Usage Trkg Data Gap DMO

Standard DMOs can be used in the same way as standard DMOs. They support all standard operations including:

Data queries and filtering
Field access and manipulation
Relationship navigation
Integration with file-based data kits
