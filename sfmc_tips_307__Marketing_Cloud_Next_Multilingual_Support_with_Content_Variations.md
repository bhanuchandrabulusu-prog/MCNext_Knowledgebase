# SFMC Tips #307 : Marketing Cloud Next: Multilingual Support with Content Variations

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-next-multilingual-support-with-content-variations-175963c1fb97

---

# SFMC Tips #307 : Marketing Cloud Next: Multilingual Support with Content Variations

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--175963c1fb97---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--175963c1fb97---------------------------------------)

8 min read

·

Jun 12, 2026

--

Photo by [Jason Leung](https://unsplash.com/@ninjason?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

The [Summer ’26 release](/@marketingcloudtips/marketing-cloud-next-summer-26-release-highlights-04f6c5abdee6) for Marketing Cloud Next Growth & Advanced Editions introduced language support through Content Variations, enabling flexible localization of various content blocks such as emails, images, headers, footers, and promotional sections.

Because translations can be centrally managed within a single email or content block, the operation of global campaigns becomes significantly simpler.

In addition, optimal content can be delivered according to each recipient’s language setting without duplicating emails, enabling a more personalized customer experience while reducing operational workload.

In this article, I will explain the setup procedure for this feature.

## Add Languages to a CMS Workspace

### Considerations

- To perform the steps in this article, you must have the **Content Admin** role as a workspace contributor.
- In a CMS workspace, you can add any language supported by your Salesforce organization as a translation language.

**Important:** Once a language is added, it is locked and cannot be deleted. Therefore, it is important to carefully consider which languages will be used before starting operations.

![]()

1. Open your marketing workspace from the **Content** tab, and from Settings select **Languages**.

2. Select the language to add from the **Add Language** list and save.

![]()

## Exporting and Importing Content for Translation

### Considerations

- In a Salesforce organization, you can use up to 500 content items per license. Content versions and translations are not counted separately against this limit. For example, a content item with two versions and three translations is still counted as one content item.

1. Next, after selecting the content to translate in the workspace, select **Manage → Translations → Export**.

2. Select the language and export. Content is generated as a separate `.xlf` file for each language.

3. After processing is complete, a notification email containing a download link for a `.zip` archive of the `.xlf` files is sent. Download the archive.

![]()

The contents of the XLF file look like the following.

```
<?xml version="1.0"?>  
<xliff xmlns="urn:oasis:names:tc:xliff:document:2.0" version="2.0" srcLang="en-US" trgLang="ja" xmlns:fs="urn:oasis:names:tc:xliff:fs:2.0">  
 <file id="9PsHo00000RdA3V">  
  <mda:metadata xmlns:mda="urn:oasis:names:tc:xliff:metadata:2.0">  
  <mda:metaGroup category="variant_details">  
  <mda:meta type="contentType">sfdc_cms__email</mda:meta>  
  </mda:metaGroup>  
</mda:metadata>  
  <unit id="1" name="title">  
   <segment>  
    <source>Content Variation</source>  
    <target></target>  
   </segment>  
  </unit>  
  <unit id="2" name="urlName">  
   <segment>  
    <source>appointment-reschedule-reminder-email</source>  
    <target></target>  
   </segment>  
  </unit>  
  <group id="3" name="contentBody">  
   <unit id="4" name="subjectLine">  
    <segment>  
     <source>Need to Reschedule Your Appointment?</source>  
     <target></target>  
    </segment>  
   </unit>  
   <unit id="5" name="preheader">  
    <segment>  
     <source>Let us know if your plans have changed.</source>  
     <target></target>  
    </segment>  
   </unit>  
   <group id="6" name="sfdc_cms:block">  
    <group id="7" name="89d55798-edd0-46a8-96ce-c01865c82b03">  
     <group id="8" name="attributes">  
      <unit id="9" name="text">  
       <segment>  
        <source>Dear {{$content.firstName}},<ph id="0" fs:fs="br"/><ph id="1" fs:fs="br"/>We understand that plans can change. If you need to reschedule your appointment, simply click the link below to update your booking.<ph id="2" fs:fs="br"/><ph id="3" fs:fs="br"/>If you have any questions or need assistance, please reply to this email. We're happy to help.</source>  
        <target></target>  
       </segment>  
      </unit>  
     </group>  
    </group>  
    <group id="10" name="aca2b249-199f-4559-bddd-383dd9c1d629">  
     <group id="11" name="attributes">  
      <unit id="12" name="text">  
       <segment>  
        <source><pc id="0" fs:fs="a" fs:subFs="shape::rect::target::_blank::href::https://www.facebook.com/salesforce/::rel::noopener noreferrer noopener noreferrer noopener noreferrer noopener noreferrer noopener noreferrer noopener noreferrer">Facebook</pc> | <pc id="1" fs:fs="a" fs:subFs="shape::rect::target::_blank::href::https://www.instagram.com/salesforce/::rel::noopener noreferrer noopener noreferrer noopener noreferrer noopener noreferrer noopener noreferrer noopener noreferrer">Instagram</pc></source>  
        <target></target>  
       </segment>  
      </unit>  
     </group>  
    </group>  
    <group id="13" name="aff491fb-dd65-457c-a113-a2be414360d5">  
     <group id="14" name="attributes">  
      <unit id="15" name="text">  
       <segment>  
        <source>{!$organization.Address}<pc id="0" fs:fs="div"><ph id="1" fs:fs="br" fs:subFs="clear::none"/></pc><pc id="2" fs:fs="div">© Salesforce, Inc. All rights reserved.</pc></source>  
        <target></target>  
       </segment>  
      </unit>  
     </group>  
    </group>  
   </group>  
  </group>  
 </file>  
</xliff>
```

4. Send the generated file to a generative AI, translation company, or localization service for translation.

*Considering the time, effort, and cost involved in translation work, I believe generative AI is sufficient.*

Paste the generated code into Notepad or a similar editor and save it using the same filename as the exported XLF file with the `.xlf` extension.

```
<?xml version="1.0"?>  
<xliff xmlns="urn:oasis:names:tc:xliff:document:2.0" version="2.0" srcLang="en-US" trgLang="ja" xmlns:fs="urn:oasis:names:tc:xliff:fs:2.0">  
 <file id="9PsHo00000RdA3V">  
  <mda:metadata xmlns:mda="urn:oasis:names:tc:xliff:metadata:2.0">  
  <mda:metaGroup category="variant_details">  
  <mda:meta type="contentType">sfdc_cms__email</mda:meta>  
  </mda:metaGroup>  
</mda:metadata>  
  <unit id="1" name="title">  
   <segment>  
    <source>Content Variation</source>  
    <target>Content Variation</target>  
   </segment>  
  </unit>  
  <unit id="2" name="urlName">  
   <segment>  
    <source>appointment-reschedule-reminder-email</source>  
    <target>appointment-reschedule-reminder-email</target>  
   </segment>  
  </unit>  
  <group id="3" name="contentBody">  
   <unit id="4" name="subjectLine">  
    <segment>  
     <source>Need to Reschedule Your Appointment?</source>  
     <target>ご予約の変更をご希望ですか？</target>  
    </segment>  
   </unit>  
   <unit id="5" name="preheader">  
    <segment>  
     <source>Let us know if your plans have changed.</source>  
     <target>ご予定が変更になった場合はお知らせください。</target>  
    </segment>  
   </unit>  
   <group id="6" name="sfdc_cms:block">  
    <group id="7" name="89d55798-edd0-46a8-96ce-c01865c82b03">  
     <group id="8" name="attributes">  
      <unit id="9" name="text">  
       <segment>  
        <source>Dear {{$content.firstName}},<ph id="0" fs:fs="br"/><ph id="1" fs:fs="br"/>We understand that plans can change. If you need to reschedule your appointment, simply click the link below to update your booking.<ph id="2" fs:fs="br"/><ph id="3" fs:fs="br"/>If you have any questions or need assistance, please reply to this email. We're happy to help.</source>  
        <target>{{$content.firstName}} 様<ph id="0" fs:fs="br"/><ph id="1" fs:fs="br"/>ご予定が変更になることもあるかと思います。ご予約日時の変更をご希望の場合は、以下のリンクからお手続きください。<ph id="2" fs:fs="br"/><ph id="3" fs:fs="br"/>ご不明な点やサポートが必要な場合は、このメールにご返信ください。喜んでお手伝いいたします。</target>  
       </segment>  
      </unit>  
     </group>  
    </group>  
    <group id="10" name="aca2b249-199f-4559-bddd-383dd9c1d629">  
     <group id="11" name="attributes">  
      <unit id="12" name="text">  
       <segment>  
        <source><pc id="0" fs:fs="a" fs:subFs="shape::rect::target::_blank::href::https://www.facebook.com/salesforce/::rel::noopener noreferrer noopener noreferrer noopener noreferrer noopener noreferrer noopener noreferrer noopener noreferrer">Facebook</pc> | <pc id="1" fs:fs="a" fs:subFs="shape::rect::target::_blank::href::https://www.instagram.com/salesforce/::rel::noopener noreferrer noopener noreferrer noopener noreferrer noopener noreferrer noopener noreferrer noopener noreferrer">Instagram</pc></source>  
        <target><pc id="0" fs:fs="a" fs:subFs="shape::rect::target::_blank::href::https://www.facebook.com/salesforce/::rel::noopener noreferrer noopener noreferrer noopener noreferrer noopener noreferrer noopener noreferrer noopener noreferrer">Facebook</pc> | <pc id="1" fs:fs="a" fs:subFs="shape::rect::target::_blank::href::https://www.instagram.com/salesforce/::rel::noopener noreferrer noopener noreferrer noopener noreferrer noopener noreferrer noopener noreferrer noopener noreferrer">Instagram</pc></target>  
       </segment>  
      </unit>  
     </group>  
    </group>  
    <group id="13" name="aff491fb-dd65-457c-a113-a2be414360d5">  
     <group id="14" name="attributes">  
      <unit id="15" name="text">  
       <segment>  
        <source>{!$organization.Address}<pc id="0" fs:fs="div"><ph id="1" fs:fs="br" fs:subFs="clear::none"/></pc><pc id="2" fs:fs="div">© Salesforce, Inc. All rights reserved.</pc></source>  
        <target>{!$organization.Address}<pc id="0" fs:fs="div"><ph id="1" fs:fs="br" fs:subFs="clear::none"/></pc><pc id="2" fs:fs="div">© Salesforce, Inc. All rights reserved.</pc></target>  
       </segment>  
      </unit>  
     </group>  
    </group>  
   </group>  
  </group>  
 </file>  
</xliff>
```

5. Compress the created XLF file into a ZIP file for import. After creating the ZIP file, return to the workspace and select **Manage → Translations → Import**.

6. After uploading the ZIP file, click **Import**.

## Review and Publish Translated Content

1. After the import is complete, open the target content. You can now review the content for each language.

2. Switch to Japanese and review the translated content.

3. If there are no issues with the content, publish it.

4. Whether content is published or not can be selected independently for each language.

## Preview the Email

1. The preview screen was significantly updated in Summer ’26 and now supports multilingual content.

2. Switch to Japanese and generate the preview.

3. You can now preview the Japanese version of the email.

![]()

4. It is also possible to send test emails using the Japanese version.

![]()

## Production Sending Using Multilingual Emails

1. Prepare a picklist field such as **Language** in your CRM data in advance. For Japanese, use **ja**. **JA** also works.

Supported Salesforce languages are listed here.

[## Salesforce Help

### Edit description

help.salesforce.com](https://help.salesforce.com/s/articleView?id=xcloud.faq_getstart_what_languages_does.htm&type=5&source=post_page-----175963c1fb97---------------------------------------)

2. Next, ingest the **Language** field through a data stream, map it to the **Individual DMO**, and perform Identity Resolution once.

*Be careful with credits because all profile source records will be processed.*

3. Preparation is now complete. Open the email send element and scroll to the bottom. There is a **Locale** section, so enable it.

4. You could enter **ja** directly while keeping the **Enter Text** option and send Japanese emails to the entire audience, but this time we will personalize using the language field on the Lead object created earlier.

![]()

> *The method described below may become easier to configure in the future as more resources become available, but this article describes the current method for Segment Flows.*

5. First, place a **Get Records** element and select **Lead**. Use the following condition:

**Lead ID = Attributes > Individual Id**

*”Attributes” refers to values available from the Individual DMO in the data graph.*

6. Next, create a new **Variable** resource and set the **Language (Picklist)** value retrieved from **Get Lead Records** as a Text type variable.

![]()

7. After saving the resource, return to the email send element and insert that resource into **Locale**.

![]()

8. Activate the flow and send the email.

9. Some recipients received the email in English.

![]()

10, Some recipients received the email in Japanese. Success.

![]()

## Conclusion

By using language support with Content Variations, multilingual content can be managed within a single email, significantly reducing the operational burden of multilingual campaigns.

In addition, optimal content can be automatically delivered according to the recipient’s language settings, enabling a more personalized customer experience without duplicating emails.

This is a very useful feature for organizations operating globally or requiring multilingual support, so be sure to take advantage of it.

That’s all for this article.

Stay tuned for more Salesforce Marketing Cloud tips! 😎

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
