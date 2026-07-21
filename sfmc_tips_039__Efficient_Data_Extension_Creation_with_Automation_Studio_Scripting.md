# SFMC Tips #39 : Efficient Data Extension Creation with Automation Studio Scripting

**Source:** https://medium.com/@marketingcloudtips/efficient-data-extension-creation-with-automation-studio-scripting-8257c4e9b324

---

# SFMC Tips #39 : Efficient Data Extension Creation with Automation Studio Scripting

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--8257c4e9b324---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--8257c4e9b324---------------------------------------)

3 min read

·

May 8, 2024

--

Photo by [Cristian Escobar](https://unsplash.com/@cristian1?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

Are you manually entering data for a data extension with lots of fields, starting from scratch each time?

Consider this: it might be more efficient to enter the necessary information into Excel and then use Automation Studio’s script activity to generate it automatically. It’s not only convenient for managing data but also handy for when you need to reorder things.

Here’s the script I use. **The script above is for creating a sendable data extension, while the script below is for creating a non-sendable data extension**.

## - Script Template for a Sendable Data Extension

```
<script runat="server">  
    Platform.Load("core", "1");  
  
    var dataExtensionConfig = {  
        "CustomerKey" : "",  
        "Name" : "Enter_the_DE_name",  
        "Fields" : [  
  
*** Copy & Paste ***  
  
        ],  
        "SendableInfo" : {  
            "Field" : { "Name" : "Enter_the_Key_Field_Name_for_SUBSCRIBER_RELATIONSHIP", "FieldType" : "Text" },  
            "RelatesOn" : "Subscriber Key"  
        }  
    };  
  
    var createdDataExtension = DataExtension.Add(dataExtensionConfig);  
</script>
```

## - Script Template for a Non-Sendable Data Extension

```
<script runat="server">  
    Platform.Load("Core", "1");  
  
    var dataExtensionConfig = {  
        "CustomerKey": "",  
        "Name": "Enter_the_DE_name",  
        "Fields": [  
  
*** Copy & Paste ***  
  
        ]  
    };  
  
    var createdDataExtension = DataExtension.Add(dataExtensionConfig);  
</script>
```

Feel free to leave “CustomKey” blank for auto-generation or input your own. **Don’t forget to input the “Name” (the data extension’s name)**.

For the “\*\*\* Copy & Paste \*\*\*” part under “Fields”, you can generate the script using the provided Excel. **Just copy and paste column H**.

## ★★★ Excel Tool (download) ★★★

![]()

<https://image.s12.sfmc-content.com/lib/fe2c11737164047d721379/m/1/DE_creation_SSJS_Nobuyuki_Watanabe.xlsx>

If you’re creating a sendable data extension, input your data extension’s “***Key\_Field\_Name\_for\_SUBSCRIBER\_RELATIONSHIP***” in “SendableInfo”. For example, in the sample Excel provided, it would be “Text”.

Executing this script will generate an empty data extension **in the top-level data extension folder**.

I recommend starting with my sample for testing purposes. 😎

Thank you for reading.

Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
