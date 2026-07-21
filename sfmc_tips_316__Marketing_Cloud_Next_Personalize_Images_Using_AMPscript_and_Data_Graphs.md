# SFMC Tips #316 : Marketing Cloud Next: Personalize Images Using AMPscript and Data Graphs

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-next-personalize-images-using-ampscript-and-data-graphs-bd852129efbb

---

# SFMC Tips #316 : Marketing Cloud Next: Personalize Images Using AMPscript and Data Graphs

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--bd852129efbb---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--bd852129efbb---------------------------------------)

4 min read

·

Jun 24, 2026

--

Photo by [KNXRT](https://unsplash.com/@knxrt?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

With the [Summer ’26 new feature release](/@marketingcloudtips/marketing-cloud-next-summer-26-release-highlights-04f6c5abdee6) for Marketing Cloud Next Growth & Advanced Editions, **AMPscript has finally arrived**.

[## SFMC Tips #280 : Marketing Cloud Next: Customize messages flexibly with AMPscript

### One of the biggest topics in the Summer ’26 new feature release for Marketing Cloud Next Growth & Advanced Editions is…

medium.com](/@marketingcloudtips/marketing-cloud-next-summer-26-ampscript-support-has-arrived-18272b5f6a1e?source=post_page-----bd852129efbb---------------------------------------)

Although some important functions are still unavailable compared to Marketing Cloud Engagement, AMPscript supports IF statements (conditional logic), making it possible to create dynamic content-like experiences using AMPscript.

## IF Statements

An IF statement is conditional logic used to change displayed content based on specific conditions.

For example, in the following sample, the variable `@test` is assigned the fixed value `"True"`, and the displayed content changes depending on that value.

```
%%[  
SET @test = "True"   
IF @test == "True" THEN  
]%%  
  
Condition met!  
  
%%[ELSE]%%  
  
Condition not met.  
  
%%[ENDIF]%%
```

In this example, `"True"` is hardcoded, so **"Condition met!"** is always displayed. Values enclosed in quotation marks (`" "`) are treated as fixed strings.

***Important:*** *If you place an AMPscript block inside a Paragraph component in the Visual Editor, an error occurs and sending or previewing becomes impossible. Be sure to place AMPscript inside an* ***HTML component*** *instead.*

In actual implementations, you would use values from a **Data Graph** or **Content Variables** instead of fixed values.

For example, with a Data Graph:

```
SET @test = $dataGraph.Favorite_Genre__c
```

Or with a Content Variable:

```
SET @test = $content.Favorite_Genre
```

By retrieving dynamic values in this way, you can display different content for each customer.

## Sample Code

In this example, images are displayed dynamically based on the value of the **Favorite Genre** field in the Data Graph.

The possible values for **Favorite Genre** are:

- Rock
- Jazz
- Pop
- Classical

```
%%[IF $dataGraph.Favorite_Genre__c == "Rock" THEN]%%  
  
<div>  
    <img alt="Rock"  
         src="https://nac-plus.cdn.salesforce-experience.com/cms/delivery/media/MCEHNOMYTGGBDAXCHLSRMCVCGNEY?channelId&#61;0apgC000000BcYE&amp;oid&#61;00DgC0000024nxA"  
         style="width:100%;display:block;"  
         width="568">  
</div>  
  
%%[ELSEIF $dataGraph.Favorite_Genre__c == "Jazz" THEN]%%  
  
<div>  
    <img alt="Jazz"  
         src="https://nac-plus.cdn.salesforce-experience.com/cms/delivery/media/MCP4LDVOJKOVFJBIC4QIZC52Z4YY?channelId&#61;0apgC000000BcYE&amp;oid&#61;00DgC0000024nxA"  
         style="width:100%;display:block;"  
         width="568">  
</div>  
  
%%[ELSEIF $dataGraph.Favorite_Genre__c == "Pop" THEN]%%  
  
<div>  
    <img alt="Pop"  
         src="https://nac-plus.cdn.salesforce-experience.com/cms/delivery/media/MCBFUZ5WF34FBMVHBHCXPGTCBUG4?channelId&#61;0apgC000000BcYE&amp;oid&#61;00DgC0000024nxA"  
         style="width:100%;display:block;"  
         width="568">  
</div>  
  
%%[ELSEIF $dataGraph.Favorite_Genre__c == "Classical" THEN]%%  
  
<div>  
    <img alt="Classical"  
         src="https://nac-plus.cdn.salesforce-experience.com/cms/delivery/media/MCRGSXERQVOBFRHOEZVV5TAD4QQY?channelId&#61;0apgC000000BcYE&amp;oid&#61;00DgC0000024nxA"  
         style="width:100%;display:block;"  
         width="568">  
</div>  
  
%%[ELSE]%%  
  
<div>  
    <img alt="Other"  
         src="https://nac-plus.cdn.salesforce-experience.com/cms/delivery/media/MCKI6HMM4EZZC2REX4HAEVJSREMU?channelId&#61;0apgC000000BcYE&amp;oid&#61;00DgC0000024nxA"  
         style="width:100%;display:block;"  
         width="568">  
</div>  
  
%%[ENDIF]%%
```

## Notes

- Each image tag must be wrapped in a `<div>` element.
- For instructions on how to obtain the URL of an image uploaded to CMS, see [here](/@marketingcloudtips/marketing-cloud-next-how-to-find-the-url-of-an-uploaded-image-13f385e07ba5).

At this point, some of you may be wondering: *“****Can’t we use Content Block functions inside the IF statement?****”*

[According to the AMPscript reference documentation](https://developer.salesforce.com/docs/marketing/marketing-cloud-ampscript/references/mc-ampscript-references/mc-ampscript-references.html), the following functions appear to be available:

- `ContentBlockById()` — Retrieve a content block by ID
- `ContentBlockByKey()` — Retrieve a content block by Key
- `ContentBlockByName()` — Retrieve a content block by Name

However, based on my investigation, these functions are not currently usable.

The reason is that when AMPscript is placed in the Visual Editor, it is automatically converted into the following Handlebars format in Code View:

- `ContentBlockById()` ⇒ `getContentBlockByContentKey`
- `ContentBlockByKey()` ⇒ `getContentBlockByContentKey`
- `ContentBlockByName()` ⇒ `getContentBlockByApiName`

However, these Handlebars functions do not currently exist and do not appear to be supported. They may become available in the future, but for now they generate an internal error.

Currently, [the only content-related Handlebars function available is](https://developer.salesforce.com/docs/marketing/handlebars-for-marketing-cloud-next/references/mcn-handlebars-content-references/mcn-handlebars-reference-content-getcontentblock.html):

```
getContentBlock
```

*\*Be aware that Handlebars is case-sensitive.*

As a result, some people may think that instead of:

```
%%=ContentBlockByKey("MCMQ7DESJCTNCTHGD63VCEILTLQI")=%%
```

they could simply use:

```
{{getContentBlock key="MCMQ7DESJCTNCTHGD63VCEILTLQI"}}
```

This is only partially correct.

The syntax does work. However, this function can only return **text content**. Images and HTML tags are not returned.

Therefore, at the current time, I do not believe it is possible to use referenced content blocks inside IF statements for dynamic image content.

*That is why the example above directly uses* `<img>` *tags.*

I also confirmed that changing the target audience causes different images to be displayed.

## Conclusion

In my opinion, one of the biggest Summer ’26 enhancements is that tasks that previously required the Code Editor can now be performed directly within the Visual Editor. This is a much larger update than it might initially appear to be.

In addition, the ability to combine AMPscript and Handlebars provides significant flexibility.

Another important point to understand is that in Marketing Cloud Next, AMPscript code is internally converted into Handlebars before being processed.

As a result, even if a feature is listed as supported in AMPscript syntax, it cannot be used if the corresponding functionality is not supported on the Handlebars side.

For the three referenced content block functions discussed in this article:

- `ContentBlockById()` — Retrieve a content block by ID
- `ContentBlockByKey()` — Retrieve a content block by Key
- `ContentBlockByName()` — Retrieve a content block by Name

it has been explicitly stated that support is planned in the future.

Once these become available, they should enable more flexible content management and conditional logic — assuming image support is added as well.

When that happens, I will share updated test results.

That’s all for this article.

Stay tuned for more Salesforce Marketing Cloud tips! 😎

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
