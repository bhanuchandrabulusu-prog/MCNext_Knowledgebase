# Response Structure for Adaptive Web Agent Component

**Source:** https://help.salesforce.com/s/articleView?id=mktg.persnl_agentforce_response_structure.htm&language=en_US&type=5

---

SALESFORCE PERSONALIZATION
Response Structure for Adaptive Web Agent Component

Configure prompt templates to return a structured JSON response that renders rich content in the Adaptive Web Agent Component (AWAC).

Include these fields in the response payload to define the message text, personalization data, and visual templates.

FIELD	TYPE	PURPOSE
text	string	Message displayed in the chat window.
curation	array	Personalization data for the content zone.
template	array	Template name(s) for rendering content.
options	array	Quick-action buttons in the chat window.
Example - Full Response

Use the complete response structure to trigger personalization recommendations and define the output format directly.

{
  "text": "Here are some boots for you",
  "curation": [
    {
      "personalizations": [
        {
          "personalizationPointName": "Generic_Boots_Recs",
          "data": [
            {
              "ssot__Name__c": "NTO Chukka",
              "UnitPrice__c": "160.0",
              "ImageURL__c": "https://example.com/image.jpg"
            }
          ],
          "attributes": {
            "IntroductionText": "Recommended For You"
          }
        }
      ]
    }
  ],
  "template": [
    {
      "name": "ProductRecommendations"
    }
  ],
  "options": [
    { "name": "Show me hiking gear" },
    { "name": "What about jackets?" }
  ]
}
Example - Minimal Response

Return a minimal structure containing only the personalization point name for lightweight responses. The client-side template then retrieves the detailed data.

{
  "text": "Here are some boot recommendations",
  "curation": [
    {
      "personalizations": [
        {
          "personalizationPointName": "Generic_Boots_Recs"
        }
      ]
    }
  ],
  "template": [
    {
      "name": "ProductRecommendations"
    }
  ]
}
SEE ALSO
Set Up the Adaptive Web Agent Component
