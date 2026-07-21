# Unlock your CMS Workspaces in Marketing Cloud Next: 8 features you need to know

**Source:** https://the-agentic-marketer.com/marketing-cloud-next-deep-dives/unlock-cms-workspaces

---

Marketing Cloud Next (Growth and Advanced) uses an Enhanced Workspace in Digital Experience CMS to store many types of assets:

- Tracked Links, Forms and Landing Pages
- Email, SMS Messages, WhatsApp (Template & Session) Messages and Expressions
- Documents, Audio, Videos
- Brands
- Directories

A default CMS is created during MCG/A setup. Here are 7 ways to spice-up your daily usage of it.

## 1/ Direct access to your Workspace from the menu

By default, MCG/A Menu has a “Content” entry. Unfortunately, it leads to the list of existing Workspaces. Among others, you may find there the Pardot Standard Workspace, the Pardot Enhanced Workspace used to copy assets, the Pardot Enhanced Workspace used to store your “New Email Experience”, not to mention the Commerce Cloud Workspace, etc.

[![](https://the-agentic-marketer.com/wp-content/uploads/2025/08/009-Content-Menu-Item-List-of-all-your-Workspaces-1024x557.png)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/009-Content-Menu-Item-List-of-all-your-Workspaces.png) 

Content Menu Item List of all your Workspaces

You then need to open the Workspace MCG/A uses (“Content Workspace for Marketing Cloud”). I like to remove unnecessary clicks, **so let’s create a direct access to your Workspace from the Menu**.

First, open the Workspace (it’s the last time you’ll need to search for it in the list 😎) and copy its URL. Then go to the Setup and search for “Tabs” in the Quick Find and open it and scroll to the Web Tabs section.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20435%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/010-Scroll-to-the-Web-Tabs-section.png) 

Scroll to the Web Tabs section

Create a new one by clicking *New*, then Next (we’ll keep the Full Tab Width default). For Tab Type select *URL* then choose a Label and a Tab Style

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20435%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/011-Choose-your-Menu-entry-name-for-your-Content-and-add-a-description-if-you-wish.png) 

Choose your Menu entry name for your Content and add a description if you wish

*Next*. In *Button or Link URL* area input the URL of your MCG/A Workspace. Then select the Profiles you want to give direct access and add the Tab to the Marketing App. Then reorder your Menu items either at the App level or by clicking the right pencil from the App. There you have it, a direct access to your Content, right in the menu (when clicking it, the Content menu will be selected again, but that’s no big deal).

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20435%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/012-A-new-Menu-item-directly-opening-your-Content.png) 

A new Menu item directly opening your Content

## 2/ Define default images

When creating an Email (Segment Triggered Flow) or a Landing Page (Form Triggered Flow) from a Campaign, default images are used.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20435%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/013-Default-images-used-to-create-an-Email-from-a-Campaign.png) 

Default images used to create an Email from a Campaign

**The good news is that these images can be changed in the CMS, so that every generated Email or Landing Page uses your own pictures**. To locate the images to replace, search for “*Default*” in your workspace.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20435%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/014-Default-images-located-in-the-CMS.png) 

Default images located in the CMS

Open each image, *+Edit* then delete the default images and upload yours. Try to keep the original size of the images (download them to check this). publish your new image.

There you have it, now on every Email or Landing Page will use your default images (this is not retroactive, already created assets won’t be affected).

## 3/ Create Multiple Workspace to manage visibility

Marketing Cloud Next (Growth & Advanced) can access every Enhanced Marketing Workspaces. A given user sees all Workspaces she/he has been added to as a Contributor (the Role can be either Content Admin, Manager or Author).

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20435%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/015-Adding-a-user-to-a-Workspace.png) 

Adding a user to a Workspace

**This can be leveraged to handle Assets visibility by creating several Workspaces and selecting which user to add in which Workspace** (with a specific role).

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20435%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/016-A-given-user-can-select-Assets-from-all-Workspace-shehe-is-in-as-a-Contributor.png) 

A given user can select Assets from all Workspace she or he is in as a Contributor

Note that the Assets Created from the Campaigns (Emails, SMS and WhatsApp messages, Landing Pages and Forms) will be created into the default Workspace, the one created at setup time, with no option to select another Workspace.

## 4/ Auto-Apply a default Brand

A Brand can be applied to Emails, Landing Pages and Form, directly from the Editor. A Brand defines text fonts, sizes, colors, spacings, etc. so your communications has a visual consistent look and feel. HTML emails: [drag & drop vs code mode](/marketing-cloud-next-deep-dives/html-emails-vs-code-mode/).

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20435%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/017-Brand-definition.-A-Brand-is-stored-in-a-CMS-Workspace.png) 

Brand definition. A Brand is stored in a CMS Workspace

You can create several Brands, and **the good news is that you can define a default one for a Workspace**, so that every Asset created inside that Workspace (either directly from the Workspace using *+Add > Content* or from a Campaign) has it automatically applied.

From the Workspace main page, click the *Gear (Settings)* and then select *Default Brand.*

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20435%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/018-Setting-a-Default-Brand-for-new-Asset-Creation.png) 

Setting a Default Brand for new Asset Creation

You’ll then be prompted to select the default Workspace.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20435%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/019-Selecting-the-default-Brand.png) 

Selecting the default Brand

*+Add:* there you have it, now any newly created Email, Landing Page or Form will be applied your default Brand.

## 5/ Disable Approval Workflows

By default, you can trigger a Flow from every Asset, so that your Asset is appoved prior to Publishing. Even though Marketing Cloud Growth and Advanced creates a basic Approval Flow during the CMS setup, you still need to setup your own process and you can also create your own Flow (this is a Specific Flow type).

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20435%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/020-The-Approval-Workflow-from-an-Email-in-a-CMS-Workspace.png) 

The Approval Workflow from an Email in a CMS Workspace.

Here is how the default Workflow is defined:

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20435%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/021-The-default-Basic-Approval-Workflow.png) 

The default Basic Approval Workflow

**You can disable the Approval Workflow if you don’t use it, so it’s not confusing for your users**. From your Workspace (you now have a direct link 😎) select *Settings (Gear) > Workflow.*

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20435%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/022-The-Approval-Workflow-management-page.png) 

The Approval Workflow management page

You can disable the Workflow for some types of Assets only: select you approval process (we only have the default here) and move the asset which do not need approval from the *Select* column to the *Available* columns using the middle arrows.

**You may also completly disable any Approval Workflow by switching the “*Workflows and Approvals*” from *On* to *Off***. There you have it, now you don’t see the Approval Process from your Assets.

## 6/ Find the public URL of an image

Every Image (or Documents, Video and Audio Files) have public URLs. This can useful to get them, for instance to store them in Custom Field which you will then be able to use as merge Fields in you Email for example.

Such technique was used for example in the article related to the [Repeater](https://the-agentic-marketer.com/marketing-cloud-next-deep-dives/repeaters/) feature.

**The public URL is not directly available from the Image page, and has the following format** ([source](https://help.salesforce.com/s/articleView?id=004576431&type=1)):

```
				
					&lt;𝐨𝐫𝐠 𝐝𝐨𝐦𝐚𝐢𝐧&gt;/𝐜𝐦𝐬/𝐝𝐞𝐥𝐢𝐯𝐞𝐫𝐲/𝐦𝐞𝐝𝐢𝐚/&lt;𝐜𝐨𝐧𝐭𝐞𝐧𝐭 𝐤𝐞𝐲&gt;?𝐜𝐡𝐚𝐧𝐧𝐞𝐥𝐈𝐝=&lt;15 𝐜𝐡𝐚𝐫𝐚𝐜𝐭𝐞𝐫 𝐜𝐡𝐚𝐧𝐧𝐞𝐥 𝐢𝐝&gt;&amp;𝐨𝐢𝐝=&lt;15 𝐜𝐡𝐚𝐫𝐚𝐜𝐭𝐞𝐫 𝐨𝐫𝐠𝐚𝐧𝐢𝐳𝐚𝐭𝐢𝐨𝐧 𝐈𝐝&gt;
				
			
```

So we’ll need to get

- *The Org Domain*
- *The Channel Id*
- *The Org Id*
- *The Content Key*

All three parameters are common to every Images, only the *Content Key* changes. The *Content Key* can be found when opening the Asset.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20435%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/023-Get-the-Content-Key-of-a-given-Asset.png) 

Get the Content Key of a given Asset

*The Org Domain* can be Search by searching for “*Domain*” in Setup and use your “*Experience Cloud Sites Domain”* or “*CDN”.*

*The Org Id* can be found in Company information in the settings.

Finally, the trickiest element to get is the *Channel Id*. As it is common to all Public URLs, we just need to get it once. The source article above as a specific method, but sending an email to yourself with just an image in it and get the message source is the simplest way to find it (note the URL may need to be decoded, for instance, in our example, “&amp;” need to be replaced by “&”, the procedure and decoding depends on you Email client).

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20435%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/024-Getting-the-Channel-Id-from-an-Image.png) 

Getting the Channel Id from an Image.

Alternatively, you can also add the image into a Landing Page, publish it, and look for the URL in the page code to get the Channel Id.

**That’s it, you now have everything you need to craft any Asset’s Public URL from its *Content Id*** *(the Org Domain, the Channel Id and the Org Id* always having the same value*).*

## 7/ Expose content from another Workspace

You may have noticed that every Enhance Marketing CMS Workspace in Digital Experiences has a “*Shared With Workspace*” Folder.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20435%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/025-Shared-with-Workspace-Folder.png) 

Shared with Workspace Folder

This is used to share Assets from another Workspace, and it must be setup from the source Workspace. For Example of you want to make avaible the ressources in your All Commerce Workspace, open it, then *Settings (Gear) > Workspace Sharing*.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20435%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/026-Defining-target-Workspaces.png) 

Defining target Workspaces.

**Then you can add which of your Workspaces will gain access to a specific Workspace (you’ll receive an email once available) by moving them from the *Unshared* to the *Shared* column using the arrows**.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20435%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/027-Adding-a-target-Workspace.png) 

Adding a target Workspace.

There you have it, your target Workspace now has access to the Source Workspace Assets and Directories (When you share a workspace, all items from the source workspace, including drafts, become accessible in the target workspace).

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20435%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/028-MCGA-Workspace-accessing-another-Workspace-from-the-Shared-With-Workspace-Fold.png) 

MCGA Workspace accessing another Workspace from the “Shared With Workspace” Fold

To modify or delete shared content, you must have the role of Content Admin, Content Manager, or Content Author in the source workspace. To publish or unpublish shared content, you must be a Content Admin or Content Manager in the source workspace.

## 8/ Import/Export of Assets between Workspaces

**You can export every Asset from a Workspace and re-import it in another Worspace**. This is handy in case for an Org migration for example. You select the Assets you want export, and then *+Manage > Export*.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20435%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/029-Exporting-an-Email.png) 

Exporting an Email

The full definition of the exported assets is stored in JSON files, which include content properties, metadata, media files, and translation variant definitions.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20435%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2025/08/030-Final-step-to-export-an-Asset.png) 

Final step to export an Asset

Once the Export is over you get an Email, and you can check the Export status at anytime in *+Setting (Gear) > Export & Import Status*. You can get your export Files from both the Email and the Status page.

Finally, the process to import is the same as the export one in the target Workspace.

## Final Thoughts

Quite every Asset Type can be Cloned directly right from the Workspace (into the same Workspace) without opening it.

Workspaces, as of Summer ’25, can now be deleted.

Every Asset can be moved into a new Folder by selecting it from the list and the *Manage > Move* to select the target directory.

A workspace Contributor can access every Assets and Directory inside the Workspace. To handle visibility, store your Assets in several Workspaces (see the 3rd point above).
