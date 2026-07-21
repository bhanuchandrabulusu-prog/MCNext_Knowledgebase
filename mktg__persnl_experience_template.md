# Experience Templates

**Source:** https://help.salesforce.com/s/articleView?id=mktg.persnl_experience_template.htm&language=en_US&type=5

---

SALESFORCE PERSONALIZATION
Experience Templates

An experience template provides a structural layout for how personalized content, such as a hero banner or product carousel, appears to customers. The template transforms raw data from the personalization engine into specific variables, such as a product name or image URL, with the help of a guided interface.

NOTE Salesforce automatically migrates any templates that you previously created to experience templates. If migration doesn't occur, contact Salesforce Customer Support.

Instead of hard-coding logic into your site's sitemap or SDK, you define how data is processed directly within the Personalization app. A single template can handle different data scenarios, such as displaying "Recent Articles" or "Recommended Products".

Ways to Build Templates

An experience template supports different template types, each suited to a different kind of experience.

Handlebars
Create dynamic web content by separating visual structure from data using this simple HTML templating language. Configure and inject personalized HTML content into your website pages to match your website styles. See What is Handlebars?.
Agent Script
Create experience templates to build and power agentic experiences. Agent Script combines natural language instructions for conversational tasks with programmatic expressions for business rules. Use expressions to define if-then-else conditions, transitions, and loops to build predictable, context-aware workflows. This template type manages state variables and specifies when an agent transitions between topics or sequences actions. See Agent Script.
Global Templates

For complete control over layout and logic, you can code a custom experience template from the ground up. To get a headstart, try a preconfigured blueprint. These global templates offer a streamlined way to create an experience template without extensive manual configuration.

By starting with a global template, such as a hero banner template, you start with a standard structure and logic. The template includes recommended data mappings and guidance for Data 360 ingestion. Use it as a foundation, and then modify it for your brand's specific design and requirements.

While the experience template controls what appears in the final output, a global template is for internal use and helps you build that experience template faster.

Template Variables

Variables act as placeholders that collect field values from a Response Template to create experience templates. They provide the necessary structure for your template code, allowing you to build and organize personalized experiences for your website.
