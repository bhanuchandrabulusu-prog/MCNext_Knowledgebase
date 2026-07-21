# Send Context to the Agent via Enhanced Chat

**Source:** https://help.salesforce.com/s/articleView?id=mktg.persnl_agentforce_send_context_to_the_agent_via_embedded_service_deployment.htm&language=en_US&type=5

---

SALESFORCE PERSONALIZATION
Send Context to the Agent via Enhanced Chat

To allow the agent to fetch context from the data graph, pass the Data 360 Web SDK anonymous ID to the chat client. This configuration makes the Individual_Id available to the agent.

window.addEventListener("onEmbeddedMessagingReady", () => {
   embeddedservice_bootstrap.prechatAPI.setHiddenPrechatFields({
      "Individual_Id": SalesforceInteractions.getAnonymousId()
   });
});

window.addEventListener("onEmbeddedMessagingConversationStarted", (event) => {
   SalesforceInteractions.sendEvent({
      interaction: { 
         name: 'conversation-started', 
         eventType: 'agentEngagement', 
         conversationId: event.detail.conversationId 
      }
   });   
});

For details on where to place this code, see Configure a Data 360 Web Connector.

SEE ALSO
Salesforce Help: Set Up Enhanced Chat for Context Passing
