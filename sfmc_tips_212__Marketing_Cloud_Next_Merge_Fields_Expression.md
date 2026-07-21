# SFMC Tips #212 : Marketing Cloud Next: Merge Fields {!$Expression.○○○}

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-next-merge-fields-expression-4056d537af72

---

# SFMC Tips #212 : Marketing Cloud Next: Merge Fields {!$Expression.○○○}

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--4056d537af72---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--4056d537af72---------------------------------------)

3 min read

·

Dec 10, 2025

--

Photo by [Nick Hillier](https://unsplash.com/@nhillier?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

In Marketing Cloud Next Growth & Advanced Edition, you can dynamically merge “Name” and other attribute information into your email body when creating email content.

![]()

However, this configuration step occasionally — actually quite often — fails.  
When it fails, nothing is displayed.

So what kind of workaround is available in this situation?

## Workaround

1. First, go to the merge field settings to insert the name.

2. Select “First Name” directly from the attributes.

3. After entering the API Name, copy and save it just in case (regardless of success or failure).

① If successful

![]()

② If unsuccessful — nothing will be displayed

4. If it fails, place the cursor in the target position and type the following

> {!$Expression.[API Name]}

For example, in this case with “First\_Name”: {!$Expression.First\_Name}

> *⚠️ Uppercase and lowercase are treated differently.*`first_name` *will not work.*

![]()

5. Right when you type the last “ } ”, the field appears correctly

![]()

## Summary

This issue occurs fairly frequently.  
Not only in regular email bodies like this example, but also inside repeat components and many other places where merge fields are used.

Therefore:

- **Always copy the API Name beforehand**
- **Memorize the syntax** `{!$Expression.○○○}` **and be ready to type it manually**

That’s all for now.

Stay tuned for more Salesforce Marketing Cloud tips! 😎

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
