# Einstein Studio Model Predictions for Personalization

**Source:** https://help.salesforce.com/s/articleView?id=mktg.persnl_esi_realtime_prediction_for_persnl.htm&language=en_US&type=5

---

SALESFORCE PERSONALIZATION
Einstein Studio Model Predictions for Personalization

Use real-time predictions from Einstein Studio models in Salesforce Personalization targeting rules to refine your personalization decisions. For example, consider you have a predictive model in Einstein Studio that predicts the chances of customers buying an item from your website. You can use this output in your targeting rules to determine the customers eligible for a special discount.

REQUIRED EDITIONS
Available in: Lightning Experience in Enterprise, Unlimited, Professional, and Developer editions with Data 360.

To use the predictions of a model, map the model to data graphs used in personalization points. You can use an existing model or create one. Before you create and map your model, keep these considerations in mind.

Build your model using Model Builder in Einstein Studio. If you want to use an existing model in Einstein Studio, make sure the model is built using Model Builder. For prerequisites and considerations, see Use Real-Time Predictions to Drive Personalized Recommendations .
Map your model to real-time personalization data graphs.

After you map a model to a data graph, you can use the model's predictions when defining the targeting rules to make real-time personalization decisions. To create and configure targeting rules to use Einstein Studio model predictions, see Create a Targeting Rule.
