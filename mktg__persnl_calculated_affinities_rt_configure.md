# Configure a Real-Time Calculated Affinity

**Source:** https://help.salesforce.com/s/articleView?id=mktg.persnl_calculated_affinities_rt_configure.htm&language=en_US&type=5

---

SALESFORCE PERSONALIZATION
Configure a Real-Time Calculated Affinity

Define calculated affinity within specific boundaries. These boundaries include the selected data space, objects, and fields that you want to calculate affinity against, and within a defined engagement timeframe. You also specify the strength of an engagement signal, and the relative impact the signal has when calculating the affinity.

REQUIRED EDITIONS
USER PERMISSIONS
NEEDED
To configure a real-time calculated affinity:	Calculated Affinities, Data Graph Definitions, Engagement Signals
From the App Launcher, search for and select Calculated Affinity.
Click New.
Define calculated infinity properties.
Select the data space that you want to use as a calculated affinity source.
Specify a lookback window that you want to use for this affinity calculation.
The lookback window defines the engagement time period considered for calculating affinity.
Specify an affinity name and an optional description.
The API name is auto-generated.
(Optional) Activate affinity decay to enable affinity scores to degrade over time.
The decay value is calculated periodically in a batch process, according to the schedule for refreshing calculated insights. When enabled, affinity decay considers how recently and how often engagement occurred within the set lookback window. The decay calculation uses an exponential decay model, where the affinity value drops to 1% of its starting value over the specified lookback window in days.
Click Next.
Select a real-time profile data graph to define what DMOs and engagement signals are available for use with the calculated affinity.
You can select from only profile data graphs that use the individual or unified individual DMO as the primary object and reside in the selected data space.
Select an object that you want to use to calculate an affinity score against.
You can select from only DMOs related to at least 1 engagement object in the selected profile data graph.
Select a field that you want to use to calculate an affinity score against. To select a field, move it from the Available Fields list to the Selected Fields list.
You can select from only mapped, text-based fields. For example, if using the Goods Product DMO, you can select from attributes like brand, style, or category for calculating affinity. Upon save, a calculated insight is created for the field you selected.
Click Next.
Select at least 1 engagement signal to start affinity calculations. You can add up to 10 engagement signals to the calculated affinity.
You can select from only engagement signals associated with engagement DMOs on the selected profile data graph that are related to the affinity object, and have a configured item identifier. For more information, see Engagement Signals.
Specify a strength for the engagement signal.
Strength indicates the level of significance to assign a signal when calculating affinity. You can choose a strength of high, medium, or low.
Specify the desired strength and impact of the engagement signal.
Impact indicates whether the signal provides a positive or negative effect to the calculation.
Save your work.
Calculated Insights generated when you create a real-time calculated affinity are automatically added to the selected profile data graph.
SEE ALSO
Using Calculated Affinities
Engagement Signals
Calculated Affinities
