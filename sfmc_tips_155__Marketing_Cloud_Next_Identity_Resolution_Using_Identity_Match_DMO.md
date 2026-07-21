# SFMC Tips #155 : Marketing Cloud Next: Identity Resolution Using Identity Match DMO

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-next-identity-resolution-using-identity-match-dmo-d5c47b599d5e

---

# SFMC Tips #155 : Marketing Cloud Next: Identity Resolution Using Identity Match DMO

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--d5c47b599d5e---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--d5c47b599d5e---------------------------------------)

4 min read

·

Aug 7, 2025

--

Photo by [Ronny Rondon](https://unsplash.com/@ronnyrondonph?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

In Marketing Cloud Next Growth & Advanced Edition, the Summer ’25 release introduced the ability to add Identity Match DMO as an “identity resolution match rule”. This enhancement makes it possible to maintain linkage to the same unified individual ID even if a lead’s email address is changed and no longer matches the original prospect’s email address, thereby mitigating the risk of losing identity resolution based on email.

As a result, engagement data accumulated at the prospect stage can continue to be reliably leveraged after the conversion to a lead.

> *With the Winter ’26 release,* ***“device-to-known”*** *and* ***“lead-to-contact”*** *are now incorporated as default match rules.*

[## SFMC Tips #183 : Marketing Cloud Next: Smarter Identity Resolution Match Rules

### With the Winter ’26 release of Marketing Cloud Next Growth & Advanced Edition, the contents of the “default identity…

medium.com](/@marketingcloudtips/marketing-cloud-next-smarter-identity-resolution-match-rules-ea432cbb5cc5?source=post_page-----d5c47b599d5e---------------------------------------)

## What is Identity Match Data Model Object?

The Identity Match DMO stores association records, such as when a prospect is converted to a lead.

### Conversion Patterns:

- Prospect to Lead Conversion
- Prospect to Contact Conversion
- Lead to Contact Conversion

You can check the association records of these conversions by running the following query in Query Editor: (\*Timezone: JST)

```
SELECT  
    ssot__DataSourceObjectId__c AS DataSounceName,  
    ssot__RecordId__c AS RecordId,  
    ssot__MatchingRecordId__c AS MatchingRecordId,  
    ssot__IdentityMatchType__c AS IdentityMatchType,  
    ssot__CreatedDate__c + interval '9 hour' AS CreatedDate,  
    ssot__IdentityMatchWeight__c AS IdentityMatchWeight,  
    ssot__IsAMatch__c AS IdentityMatchFlag  
FROM  
    ssot__IdentityMatch__dlm  
ORDER BY  
    ssot__IdentityMatchWeight__c DESC,  
    ssot__CreatedDate__c DESC  
LIMIT 10
```

## Record Definitions:

- **RecordId**: ID before conversion (e.g., Prospect ID)
- **MatchingRecordId**: ID after conversion (e.g., Lead ID)

These association records are used as “Match Rules” for Identity Resolution.

## What are “Match Rules” and “Rule Sets” in Identity Resolution?

In Identity Resolution, “Match Rules” and “Rule Sets” are used to define the criteria for determining identity unification.

- **Match Rule**: A match rule consists of one or more *Criteria* (e.g., Email Address, Phone Number, Address, Last Name, First Name, Customer ID, etc.), all of which are applied with an **AND** condition. The more criteria you add, the stricter the rule becomes, which lowers the consolidation rate.
- **Rule Set**: A rule set is a collection of one or more match rules, where the rules are evaluated with an **OR** condition. By adding more match rules, you create more possible patterns for identity resolution, thereby increasing the consolidation rate.

You can configure **Identity Match DMO** as one of these **Match Rules**.

## Steps to Configure a Match Rule

1. Click the **“Edit”** button for Match Rules, then click **“Add Match Rule”.**

2. Select **“Custom Rule”**.

3. Enter a desired **Match Rule Name** and configure the following fields:

- **Data Model Object**: Identity Match
- **Field**: Identity Match Type
- **Match Method**: Exact

4. Click **“Configure”** under **Advanced Settings**.

5. Enter **“prospect-to-lead”** in the **Identity Match Type** field.

6. Click **“Next”**.

7. **Save** the Match Rule.

### **Why the ⚠️ Warning is Displayed?**

When performing Identity Resolution using only a single identifier (such as an email address or phone number), there is a risk of **“over-merging”** — unintentionally linking data that belongs to a different person. Therefore, the system displays a warning as a precautionary alert.

However, Identity Match DMO cannot be combined with other criteria and allows setting only a single criterion. Thus, this warning is expected and does not indicate a problem. It will not interfere with the identity unification process, so you can safely proceed.

## Conclusion

In this walkthrough, I created a match rule for when a **prospect is converted to a lead**. However, as mentioned earlier, there are other conversion scenarios as well, such as:

- **Prospect to Contact Conversion**
- **Lead to Contact Conversion**

Therefore, it is recommended to create separate match rules using the values **“prospect-to-contact”** and **“lead-to-contact”** for these conversion patterns.

### **Recommended Configuration**

Add the following four types to the identity resolution match rules (automatically applied with an OR condition):

- Match Type: **prospect-to-lead**
- Match Type: **prospect-to-contact**
- Match Type: **lead-to-contact**
- Match Type: **device-to-known**

> *Note: You can add up to* ***10 Match Rules*** *in a single Rule Set.*

That’s all for now.

Stay tuned for more Marketing Cloud Growth & Advanced Edition tips! 😊

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
