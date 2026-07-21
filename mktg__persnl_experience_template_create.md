# Create an Experience Template

**Source:** https://help.salesforce.com/s/articleView?id=mktg.persnl_experience_template_create.htm&language=en_US&type=5

---

SALESFORCE PERSONALIZATION
Create an Experience Template

Set up an experience template to use predefined structures for a personalization experience. You can build the template from scratch or use a predefined global template.

REQUIRED EDITIONS
USER PERMISSIONS NEEDED
To create and edit experience templates:	Personalization Admin
Define template properties.
On the Personalization app, select Experience Templates, and click New.
Select the data space, and select Web as the channel.
Enter a unique template name and an API name.
Click Next.
Connect to your site.
Choose the specific websites where you want to use the template.
Click Next.
Choose a template type and creation method.
Select a template type.
Select a template creation method.
To prepopulate your experience template with an existing layout, select Global template.
To build a custom layout from a blank page, select Start from scratch.
If you use a global template, select a foundational starting point from the Global Template list.
Click Next.
Define data variables and map them.
Select the Personalization Response Template that defines your data fields.
Define or review your template variables.
When you select a global template, the Variables list is automatically populated based on that template's structure. Review, or update the Label and API Name for each variable.
When you start from a blank page, define the placeholders for your content. To use variables based on your Response Template, click Populate from Response Template. To define variables manually, click Add Variable, and then enter a label and a unique API Name.
In the Default Value field for each variable, select the attribute from your response template that corresponds to it.

For example, map an image variable to a background URL attribute from your response template.

Add any new variables that you need, and define their default values.
To control variable behavior for agentic experiences, such as making a variable required or overridable, see Template Variables Advanced Options.
Click Next.
Customize and validate your template code.
Review the values. To add content or modify existing elements, update the code in the editor. To include dynamic content, select a variable from the Select variable… list, and then click Insert.
To prevent tracking user interactions with this content, such as views and clicks, select Turn off auto-engagement tracking. By default, tracking is enabled.
To store your changes and continue later, click Save. To activate the template, click Save & Activate.

Now that your experience template is ready, you can use it in WPM to create a personalization experience that delivers content to your customers. See Use Templates.

SEE ALSO
Connect a Website or Mobile App to Data 360
Configure a Personalization Point
Track Personalization Engagement
Configure a Personalization Response Template
