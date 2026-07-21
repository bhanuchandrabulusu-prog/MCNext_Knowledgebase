# Configure Content Security Policies | Personalize Web Experiences

**Source:** https://developer.salesforce.com/docs/marketing/einstein-personalization/guide/configure-content-security-policies.html

---

Content Security Policies (CSP) help secure web applications by limiting loadable and executable JavaScript resources. While implementing Personalization on your website using Interactions SDK and Web Personalization Manager (WPM), you must configure certain CSPs to ensure secure and seamless functionality.

At this time, Interactions SDK and WPM use inline scripts, necessitating their enablement within your CSP. Due to potential security implications, we strongly recommend implementing a CSP nonce. A nonce is a cryptographically-generated random value that changes with each page load. By including the correct nonce in your CSP and <script> tags, you explicitly allowlist these specific scripts, preventing the execution of any other inline scripts.

If you can’t implement a nonce-based CSP, you can alternatively use the unsafe-inline source expression. However, using unsafe-inline is less secure than nonce-based CSPs and should only be used when absolutely necessary.

To implement a nonce-based CSP, generate a unique, random nonce on your server for every HTTP response and include it in your CSP header. For detailed information about the nonce CSP attribute, see nonce.

Use the same nonce value for both the script-src and style-src directives in your CSP.

Then, include the generated nonce in the <script> and <style> tags for the web SDK.

Replace <unique-nonce-value> with the actual nonce you generated on your server.

If opting for this approach to configure CSPs, make sure that you use a server-side framework that supports nonce generation and injection. Also make sure that you apply the same nonce value to the CSP header and <script> and <style> tags on your web page.

The simplest way to enable and use the web SDK and WPM is adding the unsafe-inline source expression to your CSP.

While using unsafe-inline is less secure, it allows unrestricted execution of inline scripts and dynamically evaluated code. Using unsafe-inline is especially helpful for development or quick implementation testing.

While Interactions SDK can function with a nonce-based CSP, WPM requires the unsafe-inline source expression within the style-src directive due to Lightning Web Components (LWC) using inline styles. WPM can operate correctly without the unsafe-inline source expression when your CDN URLs are allowlisted.

Replace <webSdkUrl> with the SDK URL and <WPMScriptUrl> with the URL that hosts your WPM script. For information on URL specifications in CSP, see <host-source> on MDN Web Docs.

If you’re using other Salesforce SDKs or third-party libraries, make sure that their script sources are also accounted for in your CSP.
Regularly audit and update your CSP configurations to adapt to changes in your implementation and its dependencies.
