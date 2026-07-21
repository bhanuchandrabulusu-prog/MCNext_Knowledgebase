# Configure an Engagement Signal

**Source:** https://help.salesforce.com/s/articleView?id=mktg.persnl_engagement_signals_configure.htm&language=en_US&type=5

---

SALESFORCE PERSONALIZATION
Configure an Engagement Signal

Engagement signals are configured using a primary engagement data model object (DMO). You then use mapped DMO fields to identify and track individual engagements.

REQUIRED EDITIONS
USER PERMISSIONS
NEEDED
To configure engagement signals:	Engagement Signals

When creating and using engagement signals, keep these considerations in mind.

Engagement signals are used when configuring various PersonalizationSalesforce Personalization features. These features include custom recommender objectives, custom attribution models, and personalization experiments. We recommend that you define engagement signals before configuring these features.
You can configure engagement signals using only DMOs categorized as Engagement.
You can select from only mapped DMOs and DMO fields.
You can configure an engagement signal using the fields of the primary DMO and related DMOs with a cardinality of one-to-one or many-to-one.
If you choose to configure an engagement signal using fields from a related DMO, you can use fields from only one related DMO.
You must specify a value for the item identifier if you plan to use the engagement signal in custom objective-based recommenders.
By default, a count-based engagement signal metric is created for each engagement signal that you configure. This count metric provides insights on how individuals are interacting with personalized content.

To configure an engagement signal:

From the App Launcher, search for and select Engagement Signals.
Click New.
Choose how you want to get started.
To create the engagement signal from scratch, select Manual Setup and click Next.
To import an engagement signal from an installed data kit, select Use a Data Kit and click Next.
For the Manual Setup configuration method:
Select the data space that contains the DMO you want to use as an engagement signal source.
Select an engagement DMO to use for your engagement signal tracking. The Engagement Data Model Object menu presents only DMOs in the data space that are mapped and of the category Engagement.
(Optional) Select the checkbox to make this engagement signal available in flows. Related object fields are unsupported in flows. Selecting this checkbox excludes any related objects from being selected as the engagement DMO. When selected, this option enables use of the engagement signal for both Salesforce Personalization as well as Marketing Cloud Next automation-event-triggered flows.
Click Next.
Select the fields from the DMO, or from one related DMO, to use to define the new engagement signal. Only mapped fields are provided as selectable options.
IDENTIFIER	DESCRIPTION
User Identifier	Select a general user identifier for the engagement signal. This value is often an identifiable field from the DMO that you're using for the engagement signal, like an email address, address, phone number, or some other user identifier field.
Timestamp Identifier	Select a timestamp identifier that you want the engagement signal to use. For example, a date or time value that you want the engagement signal to capture when an engagement occurs.
Item Identifier	Select an item identifier that the engagement signal can use to better isolate the engagement. For example, a specific item or data point that you want the engagement signal to use when determining a specific individual engagement.
Event Identifier	Select a unique event identifier for the engagement signal. This selection enables you to group identical engagements and eliminate duplicate records.
Click Next.
Define how events are counted.
By default, each engagement event is counted as a single, discrete event. However, you can choose to combine discrete engagement events, using added fields to uniquely identify them, and count them as a single event.
OPTION	DESCRIPTION
Count each event as a discrete engagement signal	Events are counted as individual occurrences, even if the same person triggers the same event each time. For example, total email clicks.
Define added fields to group repeat events, and count them as one signal	Repeated events are identified using added fields, combined, and counted as a single event. For example, you can define a unique email click as a combination of an individual ID, email bulk message ID, and a click event.
If you select the option to group repeat events using additional fields, select the fields that you want to use to uniquely identify the event occurrence.
For example, you can add fields to further define what makes an event unique. These fields can include individual IDs, personalization-focused IDs, specific product IDs or descriptions, and so on.
For the Use a Data Kit configuration method:
Select a data space.
Search for or select a data kit to view its contents.
Select the engagement signal to import.
Click Next.
(Optional) Select the checkbox to make this engagement signal available in flows. Related object fields are unsupported in flows. Selecting this checkbox excludes any related objects from being selected as the engagement DMO. When selected, this option enables use of the engagement signal for both Salesforce Personalization as well as Marketing Cloud Next automation-event-triggered flows.
Proceed through the confirmation screens until you reach the filters page, and then define your conditions.
NOTE
Before installing from a data kit, verify that the required data model objects (DMOs) and field mappings exist in the org.
Only unmanaged data kits are available for this configuration method. If no unmanaged data kits contain the object, create it manually.
(Optional) Define filters to better identify specific engagements. By default, no filters are used and the engagement signal applies to all engagements as defined, and using the field selections made.
Click Add Condition.
Select an option from Condition Requirements.
OPTION	DESCRIPTION
All Conditions Are Met	If all conditions are met for an individual, the engagement is captured. This selection uses the AND operator.
Any Conditions Is Met	If any one of the conditions is met for an individual, the engagement is captured. This selection uses the OR operator.
Choose a filter resource.
Select an object and field that you want to use to filter engagement options. The filter resource is a field associated with the DMO, or the related DMO, that you selected as the engagement object.
Configure the operator and value that you want to use for this filter.
OPERATOR	SUPPORTED DATA TYPE	DESCRIPTION
Is Equal To	All	Matches a provided string.
Is Less Than	Number, Percent, Currency	Matches values that are lower than the specified value.
Is Less than Or Equal To	Number, Percent, Currency	Matches values that are lower than or equal to the specified value.
Is Greater Than	Number, Percent, Currency	Matches values that are higher than the specified value.
Is Greater Than Or Equal To	Number, Percent, Currency	Matches values that are higher than or equal to the specified values.
Is Not Equal To	String, Number, Percent, Currency	Excludes the specified value.
Has No Value	All	Evaluates for a null or missing value.
Has Value	All	Evaluates for any existing value.
(Optional) Add more conditions to continue defining the engagement.
Name the engagement signal.
The API name is auto-generated.
Save your work.
SEE ALSO
Example Engagement Signals
Create a Custom Objective
Configure an Objective-Based Recommender
Engagement Signal Metrics and Compound Metrics
