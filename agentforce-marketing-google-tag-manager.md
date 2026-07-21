# Agentforce Marketing: How to add Google Tag Manager to Marketing Cloud Next

**Source:** https://the-agentic-marketer.com/marketing-cloud-next-tips-from-the-trenches/agentforce-marketing-google-tag-manager

---

**For quite a while, adding Google Tag Manager (GTM) to Salesforce Marketing Cloud Next (MCN) felt like a mystery. There’s no obvious place to add global scripts and trying to force JavaScript into MCN components usually leads nowhere.  
It took me some time to figure it out, but once you understand how MCN pages are actually delivered, the solution turns out to be pretty simple.  
The trick is not to try and add scripts directly in Marketing Cloud Next, but to use the Experience Builder for the site that hosts your landing pages.**

## The Key Insight: MCN Pages Run on Experience Cloud

Marketing Cloud Next landing pages are served through an automatically generated Experience Cloud site, typically called Marketing Landing Pages. This means that:

- MCN itself doesn’t control theor page-level scripts
- Experience Cloud does
- Global tools like Google Tag Manager should live at the site level, not inside MCN

Once you accept this, everything falls into place..

## Step-by-Step: Adding Google Tag Manager

### 1. Access the Experience Builder

1. Go to **Salesforce Setup**
2. Navigate to **Digital Experiences → All Sites**
3. Find the site used for Marketing Cloud Next landing pages (usually Marketing Landing Pages)
4. Click **Builder**

### 2. Enable Relaxed Security (Important)

Before scripts like GTM can run, you’ll need to relax the site’s security configuration:

1. In Experience Builder, open **Settings**
2. Go to **Security & Privacy**
3. Set the **Security Level to: Relaxed CSP**: Permit Access to Inline Scripts and Allowed Hosts

Without this step, the GTM script will be blocked by the Content Security Policy.

### 3. Add the GTM Script to the Head Markup

1. In Settings, go to Advanced
2. Click Edit Head Markup Paste the Google Tag Manager snippet (from Google) into the head markup block:

```
				
					 &lt;script data-noptimize&gt;(function(w, d, s, l, i) {
 w[l] = w[l] || [];
 w[l].push({
 'gtm.start': new Date().getTime(),
 event: 'gtm.js'
 });
 var f = d.getElementsByTagName(s)[0],
 j = d.createElement(s),
 dl = l != 'dataLayer' ? '&amp;l=' + l : '';
 j.async = true;
 j.src = 'https://www.googletagmanager.com/gtm.js?id=' + i + dl;
 f.parentNode.insertBefore(j, f);
 })(window, document, 'script', 'dataLayer', 'GTM-XXXXXX');&lt;/script&gt; 
				
			
```

Make sure your GTM container ID is correct. This ensures GTM loads on every MCN landing page hosted on this site.

[![](https://the-agentic-marketer.com/wp-content/uploads/2026/04/Adding-a-Google-Tag-Manager-Script-in-Salesforce-Marketing-Cloud-Next-1-1024x524.jpg)](https://the-agentic-marketer.com/wp-content/uploads/2026/04/Adding-a-Google-Tag-Manager-Script-in-Salesforce-Marketing-Cloud-Next-1.jpg) 

Adding a Google Tag Manager Script in Salesforce Marketing Cloud Next

### 4. Publish and Verify

- **Publish** the Experience Cloud site
- Open one of your Marketing Cloud Next landing pages
- Check Google Tag Manager (or use Tag Assistant / browser DevTools)

If it doesn’t immediately show up:

- Double-check the GTM ID
- Refresh a few times
- Give it some time

It *will* work once everything is lined up.

### 5. Whitelist Required Domains

After GTM starts loading, you’ll likely see new warnings in: **Settings → Security & Privacy.** These warnings indicate external domains being accessed (via GTM and its tags). Make sure to:

- Review the listed domains
- Whitelist only the ones you actually need

This keeps your setup secure while allowing GTM to function properly.

[![](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20800%20552%22%3E%3C/svg%3E)](https://the-agentic-marketer.com/wp-content/uploads/2026/04/How-to-Whitelist-Required-Tracking-Domains.png) 

How to Whitelist Required Tracking Domains

## What I learned from this

Trying to force scripts directly into Marketing Cloud Next is a dead end. MCN isn’t meant to manage global scripts **Experience Cloud is**.
Once you leverage the Experience Builder correctly, adding Google Tag Manager becomes a clean, supported, and scalable solution. Sometimes the problem isn’t *how* to do it, it’s knowing *where* to do it.
