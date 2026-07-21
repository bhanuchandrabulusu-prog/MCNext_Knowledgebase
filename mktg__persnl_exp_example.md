# Experimentation Example: Recommender Comparison

**Source:** https://help.salesforce.com/s/articleView?id=mktg.persnl_exp_example.htm&language=en_US&type=5

---

SALESFORCE PERSONALIZATION
Experimentation Example: Recommender Comparison

Experimentation supports various test scenarios. These scenarios can include testing personalized dynamic content, recommender-based content, or agent-based experiences. This experiment tests a rule-based recommender against an objective-based recommender to determine which option performs better.

Experiment Prerequisite Configurations
Before creating the experiment, we created the required components that the experiment uses during configuration. These components include the two recommenders that the experiment compares, the response template that defines the format and shape of the personalized content, and the personalization point that gathers these components together for presentation.
Recommender Comparison Example Configuration
Experiments are created, started, and managed on personalization points. For this experiment example, configure two cohorts — one as the control and the other as a variation — using the recommenders that you created and want to test. Each cohort is configured with 50 percent of the defined test population.
