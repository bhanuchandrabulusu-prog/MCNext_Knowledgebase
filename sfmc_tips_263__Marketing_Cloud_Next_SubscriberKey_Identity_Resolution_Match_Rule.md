# SFMC Tips #263 : Marketing Cloud Next: SubscriberKey Identity Resolution Match Rule

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-next-subscriberkey-identity-resolution-match-rule-ce345a3ae072

---

# SFMC Tips #263 : Marketing Cloud Next: SubscriberKey Identity Resolution Match Rule

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--ce345a3ae072---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--ce345a3ae072---------------------------------------)

5 min read

·

Mar 8, 2026

--

Photo by [Noah Buscher](https://unsplash.com/@noahbuscher?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

When using data from Marketing Cloud Engagement in the operation of Marketing Cloud Next, person data must be managed using a data model based on **Unified Individual**.

In this case, ID resolution is configured using an **Identity Resolution pattern based on Party Identification**.

In general ID resolution, people are unified using attributes such as the following:

- Individual attributes (last name, first name, etc.)
- Contact Point attributes (email address, phone number, address, etc.)

However, ID resolution using **Party Identification** is used in cases where individuals are unified not by these attributes, but by a **company-specific identifier** (such as a membership number).

In Marketing Cloud Engagement, the **SubscriberKey** is often operated as this type of company-specific identifier (membership number), so it corresponds to this pattern.

## ID Resolution Using Party Identification

ID resolution using Party Identification has a specific characteristic.

Unification occurs **only when the following three fields in the Party Identification DMO completely match**.

- **① Party Identification Type**
- **② Identification Name**
- **③ Identification Number**

Therefore, when using the **SubscriberKey from Marketing Cloud Engagement** for unification, these values must be **intentionally fixed and configured**.

Here, the explanation follows the **Salesforce recommended configuration based on the MC Starter Bundle settings**.

## Fields to Configure in the Profile Data Extension

For the **profile data Data Extension linked from Marketing Cloud Engagement**, configure the following formula fields in the **DLO** and map them to the **Party Identification DMO**.

### ① Party Identification Type (DMO field name)

Create a new formula field (Text type) with the same name in the DLO and set the following fixed value.

```
'Person Identifier'
```

### ② Identification Name (DMO field name)

Create a new formula field (Text type) with the same name in the DLO and set the following fixed value.

```
'MC Subscriber Key'
```

### ③ Identification Number (DMO field name)

Map the **SubscriberKey field** here.

## Additional Fields That Must Also Be Configured

The following DMO fields are **not directly used in Identity Resolution matching**, but they are required due to the **data model structure**, so they must be configured.

### ④ Party Identification Id (Party Identification DMO)

Create a new formula field (Text type) with the same name in the DLO and set the following calculation formula.

```
'PersonIdentifier_MCSubKey_' + sourceField['SubscriberKey field']
```

It is a common design pattern to generate an ID with a prefix that indicates the type of identifier.

This allows the system to distinguish IDs by identifier type when **other identifiers (such as CRM Contact Id or External Id)** are added in the future.

### ⑤ Party (Party Identification DMO)

Map the **SubscriberKey field** here.

### ⑥ Individual Id (Individual DMO)

Map the **SubscriberKey field** here as well.

Once all fields have been created, aim for a mapping configuration like the following.

## Steps to Configure the Match Rule

1. Start creating a new match rule.

2. Select **Custom Rule**.

3. Enter **“MC Subscriber Key”** as the match rule name and select **Party Identification** as the Data Model Object. The name can be arbitrary.

4. Next, enter **Identification Number** as the field, select **Exact** for the Match Method, and then click the **Configure** link.

5. On the next screen, enter the following values and click **Back To Basic Setting**.

- **Party Identification Type ・・・ Person Identifier**
- **Party Identification Name ・・・ MC Subscriber Key**

6. When returning to the screen, the rule set name may revert to the previous name, so enter **MC Subscriber Key** again before proceeding.

7. Save the match rule configuration.

## Conclusion

By configuring it this way, **person unification based on the SubscriberKey from Marketing Cloud Engagement becomes possible**, and in **Marketing Cloud Next**, event data and behavioral data can be utilized through the **Unified Individual model**.

In addition, with a **new feature in Spring ’26**, when ID resolution is enabled in **Marketing Cloud Engagement+**, the ruleset using **Party Identification described in this article will be automatically created as a standard (OOTB) configuration**.

Therefore, it is no longer necessary to manually create the Identity Resolution ruleset as before.

However, even if the ruleset is created automatically, **the creation of formula fields on the Data Extension side still needs to be performed manually**.

For this reason, the **Party Identification configuration explained in this article will continue to be an important point**, so please be sure to remember it.

That’s all for this time.

Stay tuned for more Salesforce Marketing Cloud tips! 😎

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
