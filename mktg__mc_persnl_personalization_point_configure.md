# Configure a Personalization Point

**Source:** https://help.salesforce.com/s/articleView?id=mktg.mc_persnl_personalization_point_configure.htm&language=en_US&type=5

---

SALESFORCE PERSONALIZATION
Configure a Personalization Point

When you configure a personalization point, you define the data space that the personalization point uses for data and the profile data graph to use for making decisions. You also select a personalization type to define the kind of personalization to provide and a schema to ensure that decision responses appear in a consistent format.

REQUIRED EDITIONS
USER PERMISSIONS NEEDED
To configure personalization points:	Change and Edit Personalization Points
From the App Launcher, search for and select Personalization Points.
Click New.
Choose how you want to get started.
To create the personalization point from scratch, select Manual Setup and click Next.
To import a personalization point from an installed data kit, select Use a Data Kit and click Next.
For the Manual Setup configuration method:
Select the data space that you want the personalization point to use.
Select the profile data graph for determining which profiles are eligible to receive personalized content.
The menu shows only the profile data graphs contained in the selected data space.

The profile data graph you choose impacts how you configure experiment cohorts and decisions. For more information about the impact of profile data graphs on Personalization Points, see Profile Data Graphs in Personalization Points.

Enter a name for the personalization point and an optional description.
The API name is auto-generated.
Select the type of personalization that you want the personalization point to provide. Making a selection activates the Personalization Content Schema menu. Selecting the Recommendations option shows and enables the Maximum Number of Recommendations to Return property.
(Optional) Change the maximum number of recommendations to return.
Select a personalization content schema.
The menu shows only the schemas that use a format consistent with the selected personalization type.
(Optional) For added security when using Data 360 authenticated server-to-server real-time data capture, select the Authentication Required checkbox.
Enabling this setting requires that the personalization point use only authenticated endpoints when sending real-time events to and requesting authenticated recommendations from Data 360.
For the Use a Data Kit configuration method:
Select a data space.
Search for or select a data kit to view its contents.
Select the personalization point to import.
Click Next.
(Optional) Change the personalization point name and description.
(Optional) Change the maximum number of recommendations to return if this is a personalization type for recommending content.
NOTE Only unmanaged data kits are available for this configuration method. If no unmanaged data kits contain the object, create it manually.
To save the personalization point without adding personalization decisions, click Save.
You can add decisions at any time.
To add personalization decisions, click Save & Add Personalization Decisions.
See Add a Decision to a Personalization Point for details.
SEE ALSO
Personalization Point Considerations
Configure a Personalization Content Schema
Add a Decision to a Personalization Point
Create a Targeting Rule
