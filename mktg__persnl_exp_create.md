# Create an Experiment

**Source:** https://help.salesforce.com/s/articleView?id=mktg.persnl_exp_create.htm&language=en_US&type=5

---

SALESFORCE PERSONALIZATION
Create an Experiment

Create and run experiments to determine which recommender or personalized content performs best for a defined personalization point. Selecting metrics for the experiment to measure, and creating targeting rules for selecting eligible participants, you can test recommender effectiveness against control and variant cohorts that you define.

REQUIRED EDITIONS
USER PERMISSIONS
NEEDED
To create an experiment:	Personalization Points
 	Experiments
From the App Launcher, search for and select Personalization Points.
Open the personalization point that you want to create an experiment for.
From the Related tab, in the Experiment section, click New.
The New Experiment page opens and shows any inherited personalization point properties that the experiment uses when generating results.
Enter an experiment name, and an optional description.
The experiment API name is auto-generated.
Click Next
Select the primary metric that you want this experiment to test against.
This metric determines which variation wins across all cohorts defined for the experiment.
NOTE If your engagement signal metric isn't showing, ensure its signal and metric DMOs and fields are in the personalization point's profile data graph.
(Optional) Select any secondary metrics in the Available window and move them to the Selected window.
Click Next
(Optional) Define any targeting rules that you want to use to select only a portion of the population for this experiment, instead of allowing the full population to participate in the experiment.
Define how you want the experiment to select individuals.
OPTION	DESCRIPTION
Always (No Conditions)	This option enables all visitors to participate in the experiment and engage with the personalized content.
All Conditions Are Met	If all conditions are met for a visitor, they can participate in the experiment and engage with the personalized content. This option requires that you add at least one condition or group.
Any Condition Is Met	If any one of the conditions is met for a visitor, they can participate in the experiment and engage with the personalized content. This option requires that you add at least one condition or group.
(Optional) Click Add Condition.

You can also choose to add groups of conditions. The Add Groups option enables you to create and combine conditions to build more complex rules.

Select the resource that you want the condition to use.
Clicking a resource opens a menu extension showing additional options that you can select.
RESOURCE OPTION	DESCRIPTION
Direct Attributes	This option uses attributes on the root object of the data graph to determine eligibility.
Related Attributes	This option uses attributes on the root object of the data graph to determine eligibility.
Segments	This option uses available segment memberships defined at the root of the data graph.
Calculated Insights	This option uses available calculated insights defined at the root of the data graph.
Scheduling	This option provides date range or day and time selections to define when personalized content can be made available and displayed in response to a personalization request.
Source	Enables you to specify a Uniform Resource Locator (URL) for use as part of a decision request. For example, creating a targeting rule to return decisions only if individuals access a specific web page or if a URL contains a specific path or slug (page description) at the end of the path.
UTM Parameters	Enables you to target Urchin Tracking Module (UTM) parameters in a URL as part of a decision request. UTM parameters are passed automatically with the URL. For example, you can create a targeting rule to return decisions only if individuals access a web page that contains a specific UTM value.
Visit Context	Enables you to specify a page type (for example, home page, product page, category page, and so on) as part of a decision request. For example, you can create a targeting rule that returns (or doesn’t return) decisions if individuals are accessing certain web pages.
Configure the operator, values, or dates to define the targeting rule condition.
(Optional) Repeat these steps to add more conditions or groups of conditions.
Click Next.
(Optional) Define the experiment’s control cohort by selecting the recommender or content that you want to test against.
(Optional) Enable the Defer response to the Personalization Decisions option.
You can bypass configuring a specific recommender for the control cohort. When enabled, this option enables control cohort traffic to fall through to any configured decisions on the personalization point for evaluation.
Define a variation cohort. Variation cohorts are the test subjects of the experiment. Each variation cohort tests a single variation against the control cohort and against any other configured variation cohorts.
Specify the percentage of the total population that you want the variation cohort to contain.
Select the recommender or content that you want to test as the variation against the control.
(Optional) Click Add Cohort and repeat this step to define another variation cohort.
Save your work.

Saved experiments are automatically placed in a Created state. You can then manage the experiment from the Related tab in the personalization point record.

SEE ALSO
Experiment Considerations
Manage an Experiment
View Experiment Analytics
Using Experiment Analytics
