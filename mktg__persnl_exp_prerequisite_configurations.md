# Experiment Prerequisite Configurations

**Source:** https://help.salesforce.com/s/articleView?id=mktg.persnl_exp_prerequisite_configurations.htm&language=en_US&type=5

---

SALESFORCE PERSONALIZATION
Experiment Prerequisite Configurations

Before creating the experiment, we created the required components that the experiment uses during configuration. These components include the two recommenders that the experiment compares, the response template that defines the format and shape of the personalized content, and the personalization point that gathers these components together for presentation.

Configure the Example Rule-Based Recommender
The rule-based recommender provides recommendations for top-selling products based on total sales value.
Configure the Example Objective-Based Recommender
The object-based recommender provides Maximize Revenue recommendations based on increased checkout frequency, increased cart value at checkout, or both.
Configure the Example Content Schema
The content schema (previously called the response template) defines the configuration options marketers can use to build a personalization decision. The content schema also makes sure that all personalization point decision responses return data in the same format. For this example, the personalization point requires a content schema that uses a recommendations personalization type.
Configure the Example Personalization Point
This personalization point is for use on a website cart or checkout page, providing recommendations to site visitors who have added items to their carts.
