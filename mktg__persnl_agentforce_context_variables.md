# Configure Context Variables

**Source:** https://help.salesforce.com/s/articleView?id=mktg.persnl_agentforce_context_variables.htm&language=en_US&type=5

---

SALESFORCE PERSONALIZATION
Configure Context Variables

Context variables pass data, such as a customer's identity or browsing history, from your website to the agent. For example, the AWAC can pass a context variable IndividualId to the agent. This immediate context allows the agent to personalize interactions–like suggesting outdoor gear based on the Northern Trail Outfitters–without asking redundant questions.

Consider a scenario where a user accesses the Northern Trail Outfitters website, browses for “winter hiking boots,” and opens the chat widget to ask about sizing.

Without a context variable such as IndividualId, the agent sees only an unauthenticated guest user on the Boots page. The agent must ask questions such as, "What is your name?" or "Have you shopped with us before?" to understand the user’s history. Consequently, the user feels treated like a stranger despite being a loyal customer.
With the IndividualId context variable configured, the website automatically passes the variable to the agent. The agent uses the IndividualId to instantly query Data 360. This query returns the user profile, revealing purchase history and preferences. The agent can skip the basic questions and immediately ask: "Hi! Are you looking for boots to match the hiking socks you bought last month? We have the XTrekker boots available in your usual size 8."

To use context variables, see . Use Context Variables in Messaging Conversations.

SEE ALSO
Salesforce Help: Configure the Context Passing Framework for Agentforce
Salesforce Developers Blog: Control Agent Access and Decision-Making with Variables and Filters
