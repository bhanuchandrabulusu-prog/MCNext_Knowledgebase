# SFMC Tips #35 : Understanding Update Contact Activity in Journey Builder

**Source:** https://medium.com/@marketingcloudtips/understanding-update-contact-activity-in-journey-builder-02820fdd853b

---

# SFMC Tips #35 : Understanding Update Contact Activity in Journey Builder

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--02820fdd853b---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--02820fdd853b---------------------------------------)

8 min read

·

Mar 28, 2024

--

Photo by [Riccardo Annandale](https://unsplash.com/@pavement_special?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

In Salesforce Marketing Cloud, **there is an activity called “Update Contact” that can be used in Journey Builder**. This time, I would like to summarize how to use this activity.

![]()

**Update Contact — Official Help Documentation**

[## Help And Training Community

### Edit description

help.salesforce.com](https://help.salesforce.com/s/articleView?id=sf.mc_jb_update_a_contact.htm&type=5&source=post_page-----02820fdd853b---------------------------------------)

With the “Update Contact” activity, **you can update values in a data extension with specific values (Static or Dynamic) when a contact reaches this activity on the journey**.

Regarding this update method, if the contact already exists within the target data extension, it will be updated with overwrite. If the corresponding contact does not exist, a new record will be added.

**- If the contact already exists … the value will be updated.   
- If the contact does not exist … a new record will be added.**

Additionally, it’s important that the target data extension is a “Sendable Data Extension.” If it’s not a “Sendable Data Extension”, it won’t appear when selecting a target.

\*In this “Sendable Data Extension”, it’s necessary to set up a “Send Relationship”. The field used in this setting will automatically become the joining key for this activity’s updates. **Typically, you should set the same field as the key in the target data extension as the one used in the send relationship you’re using during sending in the journey**.

\*Sometimes, I receive a question about whether it’s necessary to link the target data extension in advance with the Data Designer in Contact Builder. **This step is unnecessary as it’s unrelated. Simply creating it as a “Sendable Data Extension” is enough**.

Also, when using the “Update Contact” activity to add contacts to the target data extension, **make sure to include all mandatory field values; otherwise, the contact won’t be added**.

Now, let’s go through the setup steps based on the above.

## Updating with Static Values

Below, I’ve configured a data extension for the entry source.

Later, I’d like to use the “Last Purchase Product” field to create decision splits in the journey.

Next, create the target data extension. This time, I’ve added a field called “Path” to identify which path was taken. **As mentioned earlier, create the data extension as “Sendable” and set up the “Send Relationship”**.

For demonstration purposes, besides adding a new record, I’ve created a dummy record (AOR501) as an example of updating.

Once the data extension setup is complete, configure the decision split in the journey. If the “Last Purchase Product” is “Apple PC”, it should go through the upper path, and if it’s “Windows PC”, it should go through the lower path.

Finally, place the “Update Contact” activity and select the target data extension created earlier as the destination. Then, select “Path” in the left attribute field and enter “1” in the right value field. This “1” represents a static value.

For the attribute setting, **setting for “Id” is unnecessary**. **Even without this setting, it will be automatically linked based on the send relationship field**. Be careful not to set unnecessary static values for “Id”, as it could result in incorrect values.

Similarly, input “2” in the “Update Contact” activity for the lower path.

Once the configuration for the “Update Contact” activity is complete, activate the journey to start flowing contacts.

After the contacts flow, when you check the target data extension, you’ll see that the “Path” contains either “1” or “2”.

While the dummy record AOR501 initially had “XXX” in the “Path”, it has been overwritten to “1”. Also, the contacts AOR502 and AOR503, which didn’t exist previously, have been added as new records, each with its respective path.

\*By the way, the attribute setting for the “Update Contact” activity can handle not only text but also date types. As shown below, it can return either a “static date” (Date Type) entered from the calendar or the “date and time when the contact passed through this activity” (Datetime Type). For the latter case, **be cautious as it returns the date and time in the CST timezone**.

This concludes the explanation for updating with static values.

Next, I would like to explain that it is also possible to dynamically input values of entry source data extensions (referred to as “Journey Data”), or dynamically input real-time data (referred to as “Contact Data”).

## Updating with Journey Data

This input method doesn’t allow the use of standard “personalization strings”. Instead, you’ll input as follows:

```
{{Event.DEAudience-EventDefinitionKey."FieldName"}}
```

- Be precise in casing since uppercase and lowercase are distinguished.  
- If a field name contains spaces, enclose it in double quotes (“”).  
- This is an example where the entry source is a “data extension”; it may differ in cases such as “API”.

Finding the “**Event Definition Key**” can be a bit tricky. Here’s how to find it:

**Ensure at least the entry source data extension is set up on the Journey Canvas**. Right-mouse-button click on the Journey Canvas and invoke the browser’s “Inspect” function to open the “Developer Console”. Once this screen opens, **press “Ctrl + F” to call up “Search” and input “Event.DEAudience” to execute the search**. You’ll see a marker at the searched location as below. Move the cursor over it, right-mouse-button-click, and copy the element.

Pasting this copied element into Notepad will show a code like below. **You’ll find the description for the “Event Definition Key”**, which you’ll use.

```
<li data-value="{{Event.DEAudience-9b897ef4-f37a-ce4d-9468-ac8e01c5a1ee."Email"}}" data-selected="true"><a href="#">Email</a></li>
```

Generally, even if the Journey version differs, the same “Event Definition Key” is returned. **However, be mindful that if you delete and reset the entry source, the “Event Definition Key” changes with each reset**.

After obtaining the “Event Definition Key”, configure the “Update Contact” activity as you did with static values. Since the values retrieved here are assumed to be personalized, no decision splits are necessary.

Here, in the attribute field of the “Update Contact” activity, input the following value. This will return the value of “Last\_Purchase\_Product” for each contact stored in the entry source to the target data extension.

```
{{Event.DEAudience-9b897ef4-f37a-ce4d-9468-ac8e01c5a1ee."Last_Purchase_Product"}}
```

Once the setup is complete, activate the journey to flow the contacts.

You’ll see that the “Last\_Purchase\_Product” values for each contact stored in the entry source have been inputted as shown below.

The values stored are **snapshots taken at the time of entry, not real-time values**.

In this method, **you cannot dynamically input values for “date type” fields into “date type” fields**. In such cases, create a “text type” field and set it up to store dates as text. Later, you can use SQL to cleverly convert these text dates into normal “date type” values.

## Updating with Contact Data

Lastly, if you want to use real-time data called “contact data”, it would look like this:

```
{{Contact.Attribute."DataExtensionName"."FieldName"}}
```

- Be precise in casing since uppercase and lowercase are distinguished.  
- If a field name or a data extention name contains spaces, enclose it in double quotes (“”).

To do this, **you need to create links in advance in the Data Designer of Contact Builder to use the data extension as contact data**. Make sure to do this link processing in the Data Designer. Forgetting this step will result in all values being returned as empty.

Here, it’s important to note that while in the case of journey data, you can match all contact keys because you’re looking for the “Id” from the entry source, which naturally matches all contact keys… In the case of contact data, **it’s not guaranteed that records with the same contact key will always exist. Moreover, if it’s a “1: N” data, multiple records might match**.

Therefore, **if a record doesn’t exist, empty values will be inputted. And if multiple records match, the value from the first matching record will be inputted**. Be aware of this rule.

- If the record doesn’t exist … **empty values will be inputted**.   
- If multiple records match … **the value from the first matching record**.

Now, let’s perform the following process to verify:

- AOR501: Normal ⇒ **Expected to retrieve data normally**
- AOR502: No data ⇒ **Expected to retrieve empty values**
- AOR503: Multiple records exist ⇒ **Expected to retrieve the value from the first matching record**

As a data extension to retrieve contact data, create a data extension like the one below.

![]()

Then, as mentioned earlier, **link the data extension in the Data Designer**.

Once this is done, configure the “Update Contact” activity as before. Since the values are assumed to be personalized, no decision splits are necessary this time either.

In this case, you don’t need to use the “Event Definition Key”. Instead, input the following value to return the value of “Last\_Purchase\_Product” for each contact stored in the entry source to the target data extension.

```
{{Contact.Attribute."PurchaseData"."Purchase_Product"}}
```

Once the setup is complete, activate the journey to flow the contacts.

You’ll see that the “Purchase\_Product” values for each contact stored as contact data have been inputted as shown below.

The validation of the scenarios mentioned earlier should be as expected:

- AOR501: Normal ⇒ **Data retrieved normally**
- AOR502: No data ⇒ **Empty values retrieved**
- AOR503: Multiple records exist ⇒ **Value from the first matching record retrieved**

## Conclusion

While static values are commonly used in “Update Contact” activities, experimenting with dynamic values for individual contacts can offer new possibilities. Try both methods to see what works best for your needs.

Thank you for reading.

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
