# Creating and Training Salesforce Personalization Recommenders

**Source:** https://help.salesforce.com/s/articleView?id=mktg.persnl_recommender.htm&language=en_US&type=5

---

SALESFORCE PERSONALIZATION
Creating and Training Salesforce Personalization Recommenders

Salesforce Personalization in Marketing Cloud Next generates multichannel, focused, and individualized recommendations based off of deep, digital, and offline behavioral and business context data. To create personalized recommendations, you configure a recommender and train it using Data 360 data graphs that you select.

Machine Learning for Objective-Based Recommenders
The Salesforce Personalization recommendation system uses machine learning and AI to analyze user behavior along with data from profile and item data graphs. The system then predicts user actions that support business goals, such as increasing revenue or reducing unsubscribes. When you understand how the system works, you can provide adequate inputs that influence the learning and lead to better recommendations.
Choosing a Recommendation Type
The recommendation type defines the method that the recommender uses to provide content. You can choose either objective-based recommendations or rule-based recommendations. Objective-based recommendations use a deep learning model to produce personalized, targeted recommendations for an individual. Rule-based recommendations use business logic to mathematically determine a list of recommendations based on Data 360 calculated insights. For both recommendation types, you can add filters to include or exclude items.
Configure a Recommender
A recommender presents personalized recommendations to visitors based on the recommendation type and criteria that you select.
Recommendation Filters
Use Recommendation Filters to control which items the recommender suggests to your customers.
Simulate a Recommender
After you create a recommender and train it, you can preview recommendations for specific users and for the items that the user is viewing at the time the recommendations are presented. By previewing recommendation results, you can verify the simulation before publishing the recommender.
Co-Bought Recommender with Multiple Dimension Filters Configuration Example
Use calculated insights and the power of filters to configure a recommender to generate a list of products that have frequently been purchased together.
Training a Personalization Recommender
After you create a personalization recommender, it uses Customer 360 data from the selected data graphs to begin training. You can track the training on the recommender record.
Set Up a Fallback Recommender
Select a fallback recommender to use when your recommender doesn’t return sufficient recommendation items. If restrictive filters or insufficient data prevent a recommender from returning sufficient items, Salesforce Personalization uses the fallback recommender to fill the remaining slots.
