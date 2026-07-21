# Experiment Considerations

**Source:** https://help.salesforce.com/s/articleView?id=mktg.persnl_exp_considerations.htm&language=en_US&type=5

---

SALESFORCE PERSONALIZATION
Experiment Considerations

When creating and running an experiment, keep these considerations in mind.

Because you configure experiments on personalization points, the experiments inherit properties used to configure that personalization point. These inherited properties appear on the first page of the experiment configuration, and are used by the experiment. For example, the profile data graph is inherited from the personalization point. Profile data graph DMOs and selected fields are used to filter engagement signal metrics available for selection as primary and secondary metrics during experiment configuration.. The response template is also inherited from the personalization point. The response template setting determines whether the experiment tests recommendations, content, or some other custom experience, like a Salesforce agent.
If an individual is eligible to participate in an experiment based on configured targeting rules, they can join that experiment. Qualifying individuals remain in the same cohort they’re assigned for the duration of the experiment. As long as individuals qualify, they can also participate in multiple experiments simultaneously.
No matter what percentage of total eligible participants you assign to a cohort, each cohort must include a participant sample size of at least 1,000. This limit ensures proper statistical evaluation for chance to beat all and chance to beat control calculations.
The first cohort is always the control. When you configure a control cohort, each variation cohort tests its variation against the control variation. The resulting calculation indicates a percentage chance of beating control in the experiment's analytics.
You can choose not to configure a control cohort. In this case, you defer responses for the control cohort to use already-configured personalization decisions already configured on the personalization point.
Weighted analysis is supported, so you can create cohorts of different traffic sizes. However, the total percentage of cohorts must equal 100%. Any unallocated percentage is automatically applied to the control cohort.
SEE ALSO
Create an Experiment
Manage an Experiment
View Experiment Analytics
Using Experiment Analytics
