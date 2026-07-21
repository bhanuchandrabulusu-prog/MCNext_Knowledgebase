# SFMC Tips #315 : Agentforce: Multilingual Display for Enhanced Chat Based on Browser Language

**Source:** https://medium.com/@marketingcloudtips/agentforce-multilingual-display-for-enhanced-chat-based-on-browser-language-0046c8b45d56

---

# SFMC Tips #315 : Agentforce: Multilingual Display for Enhanced Chat Based on Browser Language

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--0046c8b45d56---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--0046c8b45d56---------------------------------------)

5 min read

·

Jun 23, 2026

--

Photo by [Jasper Garratt](https://unsplash.com/@jaspergarrattphotography?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

In this article, I will explain **how to make the chat multilingual based on the browser language** when displaying a Service Agent on an external website.

By doing this, you can edit text such as the “**Ask Me Anything**” text in Service Agent Enhanced Chat v2.

![]()

***Note:*** *I confirmed with Salesforce Support that, at this time, multilingual support for* ***agent names*** *is not available. Therefore, if you need to support multiple languages, it’s probably safest to use an English agent name. Hopefully, this will be supported in a future release.*

## Translation Language Settings

1. Search for “**Translation Language Settings**” in Setup, and enable the feature if it is not already enabled.

2. Add languages.

3. This time, I will create English, Japanese, Korean, Chinese (Simplified), and Chinese (Traditional), so first register English, check Active, and select a user as the translator.

*\*A translator is a user who can create and edit translations for that language.*

4. Configure Japanese, Korean, Chinese (Simplified), and Chinese (Traditional) in the same way.

5. After finishing the language settings, go to Setup > **Embedded Service Deployments** and click “**Custom Labels**” in Enhanced Chat v2.

6. First, switch the language to Japanese and select “**General**” in the chat group.

7. Select “**All**” in the display label group.

8. When you set the display label type to Standard, a list of configurable labels is displayed. Enter the custom display label and click Save. Of course, leaving the default value is also fine.

This time, I will change “Ask Me Anything” to “We will guide you according to your request”（ご用件に合わせてご案内します）.

9. After editing all text, click “Finish”.

10. Configure the other languages in the same way.

## Modifying the Code Snippet

1. Obtain the code snippet from Embedded Service Deployments.

2. Normally, the code looks something like the following.

```
<script type='text/javascript'>  
 function initEmbeddedMessaging() {  
  try {  
   embeddedservice_bootstrap.settings.language = 'en_US'; // For example, enter 'en' or 'en-US'  
  
   embeddedservice_bootstrap.init(  
    '00Dg7000005ArbF',  
    'Service_Agent',  
    'https://na1777983780331.my.site.com/ESWServiceAgent1780374048210',  
    {  
     scrt2URL: 'https://na1777983780331.my.salesforce-scrt.com'  
    }  
   );  
  } catch (err) {  
   console.error('Error loading Embedded Messaging: ', err);  
  }  
 };  
</script>  
<script type='text/javascript' src='https://na1777983780331.my.site.com/ESWServiceAgent1780374048210/assets/js/bootstrap.min.js' onload='initEmbeddedMessaging()'></script>
```

3. Change this code as follows.

```
<script type='text/javascript'>  
function initEmbeddedMessaging() {  
 try {  
  const userLang = (navigator.language || navigator.userLanguage || 'en').toLowerCase();  
  
  let chatLang = 'en_US';  
  
  if (userLang.startsWith('ja')) {  
   chatLang = 'ja';  
  } else if (userLang.startsWith('ko')) {  
   chatLang = 'ko';  
  } else if (userLang.startsWith('zh-cn') || userLang.startsWith('zh-sg')) {  
   chatLang = 'zh_CN';  
  } else if (userLang.startsWith('zh-tw') || userLang.startsWith('zh-hk') || userLang.startsWith('zh-mo')) {  
   chatLang = 'zh_TW';  
  }  
  
  embeddedservice_bootstrap.settings.language = chatLang;  
  
  embeddedservice_bootstrap.init(  
   '00Dg7000005ArbF',  
   'Service_Agent',  
   'https://na1777983780331.my.site.com/ESWServiceAgent1780374048210',  
   {  
    scrt2URL: 'https://na1777983780331.my.salesforce-scrt.com'  
   }  
  );  
 } catch (err) {  
  console.error('Error loading Embedded Messaging: ', err);  
 }  
}  
</script>  
  
<script type='text/javascript'  
 src='https://na1777983780331.my.site.com/ESWServiceAgent1780374048210/assets/js/bootstrap.min.js'  
 onload='initEmbeddedMessaging()'>  
</script>
```

4. The main part to change is the following section.

This section obtains the browser language setting and switches the Agentforce chat display language based on that language.

```
const userLang = (navigator.language || navigator.userLanguage || 'en').toLowerCase();  
  
let chatLang = 'en_US';  
  
if (userLang.startsWith('ja')) {  
    chatLang = 'ja';  
} else if (userLang.startsWith('ko')) {  
    chatLang = 'ko';  
} else if (userLang.startsWith('zh-cn') || userLang.startsWith('zh-sg')) {  
    chatLang = 'zh_CN';  
} else if (userLang.startsWith('zh-tw') || userLang.startsWith('zh-hk') || userLang.startsWith('zh-mo')) {  
    chatLang = 'zh_TW';  
}  
  
embeddedservice_bootstrap.settings.language = chatLang;
```

For this section, I think it is faster to ask a generative AI to generate it using the above example as a reference.

If you specify the default language and the languages you want to use, it should adjust the code to fit your environment.

> Tips: The language code returned by the browser varies depending on the environment.
>
> For example, even for Japanese, either `ja` or `ja-JP` may be returned. For Korean, either `ko` or `ko-KR` may be returned.
>
> In addition, for Chinese, simplified and traditional Chinese are distinguished, so values such as `zh-CN` (Simplified Chinese), `zh-TW` (Traditional Chinese), and `zh-HK` (Traditional Chinese - Hong Kong) may be returned.
>
> Therefore, rather than checking for an exact match with a specific value, it is recommended to use `startsWith()` for the comparison.

5. Finally, embed the modified code into your external website.

## Trying It Out

To verify the behavior by changing the browser language, enter the following URL in the Google Chrome address bar.

```
chrome://settings/languages
```

Then switch the display language and check whether the chat button and chat window display changes.

If the chat display switches according to the browser language as shown below, the configuration is successful.

### English

![]()

### Japanese

![]()

### Korean

![]()

### Chinese (Simplified)

![]()

### Chinese (Traditional)

![]()

How was it?

I could not easily find this information through searching, so I decided to leave it here as a memo.

When providing Agentforce chat in multiple languages, it is very important to switch the display language according to the browser language.

In particular, I think this is a configuration that companies supporting multiple languages such as Japanese, English, Korean, and Chinese should implement.

That’s all for this time.

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
