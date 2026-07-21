# SFMC Tips #209 : Marketing Cloud Next: Conducting an Online Survey (Smart Capture-style Form)

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-next-conducting-an-online-survey-smart-capture-form-c3fb77606565

---

# SFMC Tips #209 : Marketing Cloud Next: Conducting an Online Survey (Smart Capture-style Form)

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--c3fb77606565---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--c3fb77606565---------------------------------------)

8 min read

·

Dec 2, 2025

--

Photo by [Dan Meyers](https://unsplash.com/@dmey503?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

With Marketing Cloud Next Growth & Advanced Edition, you can guide customers from an email to a landing page and conduct a survey — **just like the Smart Capture form functionality in Marketing Cloud Engagement**.

In terms of how the survey data can ultimately be used, possible scenarios include:

1. Displaying the collected survey responses as a related list on CRM record pages
2. Using the survey results as segmentation criteria within Marketing Cloud Next

Since the full implementation involves many setup steps, this article highlights only the key points and explains them in a simple and accessible way.

> *For this example, I will walk through a* ***vehicle-related online survey****, as shown below.*

## “Online Survey — Winter ’25”

## Dropdown Questions (3 Types)

(*Single selection only — radio buttons are not available yet*)

### 1. What type of vehicle are you currently driving?

- Sedan
- SUV
- Hatchback
- Minivan
- Truck
- Other

### 2. How old is your current vehicle?

- Less than 1 year
- 1–3 years
- 4–6 years
- 7–10 years
- More than 10 years

### 3. How likely are you to purchase a new car in the next 12 months?

- Very likely
- Somewhat likely
- Not sure
- Not very likely
- Not at all likely

## Checkbox Questions (3 Types)

(*Multiple selections allowed*)

### 4. Which features are most important to you when buying a car?

- Fuel efficiency
- Safety features
- Interior comfort
- Advanced infotainment system
- Exterior design
- Price
- Brand reputation

### 5. Which powertrain options would you consider?

- Gasoline
- Hybrid
- Plug-in Hybrid
- Electric (EV)
- Diesel

### 6. Which services would you like the dealership to provide?

- Regular maintenance reminders
- Online test drive booking
- Trade-in evaluation
- Extended warranty options
- Mobile app for vehicle management

## Free Text Question (1 Type)

### 7. Please share any additional comments or suggestions regarding your vehicle or dealership experience.

A **text area** will be provided for this response.

## Setup Steps (Excerpt)

1. First, start by hashing the Contact ID.

> *The reason for hashing the ID is to prevent the Contact ID from being exposed in plain text in the URL when navigating to the landing page.*

In the Contact data stream, create a new “**formula field**”, enter the following formula, and save it as a text field. The name used here is “Subscriberkey Hash”, but any name is acceptable.

```
SHA256(sourceField['Id'])
```

2. After creating the formula field, create a corresponding custom field in the Individual DMO and map it. The name used here is also “Subscriberkey Hash”.

3. Next, set this field to be “available” in the **Data Graph**.

> *This will allow you to insert it later as a URL parameter in an email.*

## Preparing the Custom Object

1. Next, move to CRM and create a **custom object** to store survey responses. The name used here is “**Online Survey — Winter ‘25**”.

First, create the following two fields (names are optional):

- Subscriberkey Hash (hashed value of the Contact ID)
- Response DateTime (response timestamp)

Then, create the fields that will store the actual survey answers.

Dropdown questions are single-select, so one field is enough for each question.   
Checkbox questions allow multiple selections, so you must create an individual field for each selectable option.

2. After preparing the custom object, go to the data stream and set it as a Data Cloud ingestion target.

> *You may wonder whether it belongs to the “Engagement” or “Other” category, but in this case, it was created under the “Engagement” category.*

3. After that, create a custom Data Model Object (DMO) and map it. The mapping is performed automatically.

4. Click the red-circled area shown above to configure the relationship and link **Subscriberkey Hash** in the Individual DMO with **Subscriberkey Hash** in this object.

> *This allows the survey results to be used as related attributes in Marketing Cloud Next segments.*

## Creating the Form

1. Next, create a form for submitting survey responses.

> *When starting the creation process, it is easiest to use the “Signup form” template under Campaigns.*

Since the custom object is the storage destination, the data source selection on the left menu is not required. Create the form from scratch.

2. The key point here is adding a **hidden field** for the Subscriberkey Hash.  
Check the “**Hide this field**” option. In this example, the URL parameter used was “**h**”, but any value is acceptable.

## Setting Up the Flow for the Form

1. Next, navigate to Flow and create the mapping to the custom object “Online Survey — Winter ‘25”.

- For Subscriberkey Hash, use the value captured by the hidden field
- For Response DateTime, use the flow execution timestamp
- In addition, map all survey answer fields that were created

> *Make sure all required fields already exist in CRM.*
>
> *\*Additionally, in Flow formula resources, form data cannot be handled directly, so it seems that you cannot store values from a* ***multi-select checkbox*** *into a single CRM field within the Flow.*
>
> *If anyone knows a way to achieve this, please let me know how to do it.*

2. After activating the flow, the form will automatically enter the “Published” state. Wait until the publication process is completed.

> *If the form is not published, the landing page cannot be published.*

## Landing Page and Email Setup

1. Complete the landing page and publish it.

> *The “form” placed inside the landing page may sometimes appear visually distorted, but the submission will still work correctly.*

2. A “public URL” will be issued. This will be used in the email.

3. Create the email.

4. In the button link URL, select “Dynamic URL” and configure the following format:

https://www.nac-care.com/lp/landing-page/Online-Survey-Winter25**?h={Subscriberkey Hash}** (The part after `h=` is an “**Merge field**”.)

> *As mentioned earlier, if the Data Graph setup has been completed,* ***Subscriberkey Hash*** *should be available as a merge field.*

5. Send the email and click the survey button.

![]()

6. You will then see that the hashed Contact ID appears as the “h” parameter in the landing page URL.  
After that, answer the survey and submit it.

> *Example:  
> https://www.nac-care.com/lp/landing-page/Online-Survey-Winter25?****h=1596f6896450ea3440068540073139ed1c53aadc71b47ba4c7a6a87fbf8a1da9****&sftoken=...*

## Checking the Submitted Data

1. After submitting the survey, you can verify that the data has been stored in the CRM survey object.

If all fields were created correctly and mapping was configured properly in the flow, all values should be stored without issues.

## Linking to Contact

1. Now, from here, I configure the linkage between the survey record and the Contact.  
First, create a new field “Subscriberkey Hash” on the standard Contact object. Name is optional.

2. Next, use **Data Cloud Copy Field** to sync the hashed value field from the Individual DMO to the Subscriberkey Hash field on the Contact object.

3. With this, the Contact record will hold the hashed value.

4. However, since the survey object also does not contain a Contact ID, the survey records cannot yet be displayed in the Contact’s “Related List”.  
Therefore, create a lookup field **Contact\_\_c** (reference field) on the survey object.

5. To automatically populate the Contact ID into this field when a survey record is created, build a **record-triggered flow**.

6. Set the flow to trigger when the survey object is created (or updated).  
The additional filter condition shown here is optional and only prevents unnecessary runs.

7. Next, using the Subscriberkey Hash synced via Data Cloud Copy Field and the Subscriberkey Hash coming through the record-triggered flow, retrieve the corresponding Contact record.

8. Finally, extract the Contact ID from the retrieved Contact record and update the survey object’s **Contact\_\_c** field.  
With this, the Contact ID is automatically populated when a survey record is created, allowing the relation to be established.

## Confirming the Results

1. When you check the Contact record page, you can see that the survey object now appears as a “Related List”.

2. Additionally, about **15 minutes after** the survey record is created, the survey data becomes available in Marketing Cloud Next segments.

> *It is not synced in real time.  
> Data is synchronized every 10 minutes as a differential sync, so it becomes usable approximately 15 minutes later.*

## Conclusion

Although the configuration was extensive and may have felt a bit overwhelming, you should now understand that even in the current version of Marketing Cloud Next, surveys can be conducted similarly to Smart Capture Forms.

This article is intended to show that, in terms of “whether it can be done or not”, the answer is **“it can be done”.**  
There are multiple implementation methods, and the optimal approach will vary depending on your requirements, so please explore the method that best fits your environment.

That is all for now.

Stay tuned for more Salesforce Marketing Cloud tips! 😎

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
