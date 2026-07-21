# Set Up Agent Engagement Tracking

**Source:** https://help.salesforce.com/s/articleView?id=mktg.persnl_agentforce_engagement_tracking.htm&language=en_US&type=5

---

SALESFORCE PERSONALIZATION
Set Up Agent Engagement Tracking

To capture agent interactions and send them to Data 360 to further enrich profiles, configure event listeners. Agent engagement events track conversations, messages, and user actions. These events flow to Data 360 and update customer profiles for improved, future personalization.

Because these steps are technical, we recommend contacting your Salesforce account executive for assistance.

The following Enhanced Chat events are tracked by default.

EVENT	LISTENER	DESCRIPTION
Conversation Started	onEmbeddedMessagingConversationStarted	Customer begins a conversation
Conversation Closed	onEmbeddedMessagingConversationClosed	Conversation ends
Agent Ready	onEmbeddedMessagingReady	Agent component initializes
Message Sent	onEmbeddedMessageSent	Customer sends a message
Message Click	onEmbeddedMessageClick	Customer clicks a link in a message
Transfer Requested	onEmbeddedMessagingConversationRouted	Conversation routes to a human agent
To connect web sessions to customer profiles, access your website's embedded messaging script, and then add Individual_Id as a prechat field.
window.addEventListener("onEmbeddedMessagingReady", () => {
    const chatIndividualId = SalesforceInteractions.getAnonymousId();
    embeddedservice_bootstrap.prechatAPI.setHiddenPrechatFields({
        "Individual_Id": chatIndividualId
    });
});
To capture agent engagement events and send them to Data 360, access your website's embedded messaging script, and then add the following event listener code.
function addMiawEventListeners(eventListenerName, interactionName, eventType, attributes) {
    window.addEventListener(eventListenerName, (event) => {
        SalesforceInteractions.sendEvent({
            interaction: {
                name: interactionName,
                eventType: eventType,
                attributes: attributes
            }
        })
    })
}

var attributes = {
    embeddedServiceDeployment: 'Your_Deployment_Name',
    conversationId: event.detail.conversationId
}

addMiawEventListeners('onEmbeddedMessagingButtonClicked', 'agent-click', 'agentEngagement', attributes)
addMiawEventListeners('onEmbeddedMessagingConversationStarted', 'agent-conversation-started', 'agentEngagement', attributes)
addMiawEventListeners('onEmbeddedMessagingConversationClosed', 'agent-conversation-closed', 'agentEngagement', attributes)
addMiawEventListeners('onEmbeddedMessagingReady', 'agent-ready', 'agentEngagement', attributes)
addMiawEventListeners('onEmbeddedMessageSent', 'agent-message-sent', 'agentEngagement', attributes)
addMiawEventListeners('onEmbeddedMessageClick', 'agent-message-click', 'agentEngagement', attributes)
SEE ALSO
Developers: Event Listeners
