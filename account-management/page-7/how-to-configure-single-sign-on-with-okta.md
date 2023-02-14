# How to Configure Single Sign-On with Okta

ThousandEyes supports use of any SAML2-based identity provider for single-sign on. There are two parts to an SSO configuration - the service provider configuration, which is what you set inside ThousandEyes, and the Identity Provider configuration, which you set in your SSO system. In this configuration example, we use Okta as the Identity Provider.

### How to Configure ThousandEyes for SSO <a href="#how-to-configure-thousandeyes-for-sso" id="how-to-configure-thousandeyes-for-sso"></a>

Configuration is fairly simple, but can come with a few gotchas. Here's what you need:

* User in a role with the **Edit security & authentication settings** permission in ThousandEyes
* An authentication provider which provides SAML authentication
*   From the SAML provider (in this case,

    [Okta](http://www.okta.com/)

    ):

    * Login URL for your SAML provider
    * Logout URL for your SAML provider (not required)
* A post-back URL from ThousandEyes: https://app.thousandeyes.com/login/sso/acs
*
  * Destination: http://www.thousandeyes.com
  * **autnContextClassRef: PasswordProtectedTransport**
  * Audience Restriction: http://www.thousandeyes.com **Note**: it is very important that the Audience Restriction configured in your Identity Provider's configuration exactly match the value set for the Service Provider Issuer field in ThousandEyes. Any mismatch, including a protocol mismatch (http:// vs https://) will cause the request to be rejected.
  * Recipient: http://www.thousandeyes.com
  * Name ID Format: Email Address

To configure the system for Single Sign-on, configuration must be done on both the SAML provider's site, and on ThousandEyes.

#### In the Identity Provider's site (Okta), follow these steps: <a href="#in-the-identity-providers-site-okta-follow-these-steps" id="in-the-identity-providers-site-okta-follow-these-steps"></a>

1.  3\.

    Select the **Applications** tab
2.  4\.

    Locate the ThousandEyes app using the search or scrolling through the list of apps
3.  6\.

    Accept the defaults on **General Settings** or select values appropriate for your environment
4.  8\.

    Click the **View Setup Instructions** to open ThousandEyes-specific configuration information in a new page.

    You will need the information on this page for the single sign-on configuration in the ThousandEyes app. If you close this page and need to re-open, you can use the URL http://saml-doc.okta.com/SAML\_Docs/How-to-Configure-SAML-2.0-for-ThousandEyes.html, but you must be logged into your Okta Administrator account to be able to access the ThousandEyes-specific configuration information for your organization.
5.  10\.

    Assign the app to people in your SAML organization using the checkbox next to a user's name
6.  12\.

    Modify as needed any user logins (email addresses) for ThousandEyes for your users. The username here must match the username configured in ThousandEyes for this user.

#### In ThousandEyes, follow these steps: <a href="#in-thousandeyes-follow-these-steps" id="in-thousandeyes-follow-these-steps"></a>

1.  3\.

    Check the box to **Enable Single Sign-On**
2.  4\.

    Copy the value found in the **Redirect Login URL** field of the ThousandEyes-specific configuration page (from step 8 above) into the **Login Page URL** field on the **Security & Authentication** tab
3.  5\.

    The **Logout Page URL** is optional, but should point to the page you wish your users to see when logging out of ThousandEyes.

    Recommended: **https://app.thousandeyes.com/login/sso**
4.  6\.

    Copy the value found in the **Identity Provider Issuer** field of the ThousandEyes-specific configuration page into the **Identity Provider Issuer** field on the **Security & Authentication** tab. This should be **http://www.okta.com/{externalKey}**.
5.  7\.

    Enter **http://app.thousandeyes.com** in the **Service Provider Issuer** field.

    **NOTE**: It is extremely important to make sure that the **Service Provider Issuer** field in ThousandEyes reflects the value set by the Identity Provider's response in the **audienceRestriction** field. Any mismatch, including a protocol mismatch (http:// vs https://) will cause the request to be rejected.
6.  8\.

    For the **Verification certificate** option, upload the file downloaded from the ThousandEyes-specific configuration page (from step 8 above).

When you visit ThousandEyes for the first time on your computer, enter your username into the Email Address field, and click the SSO link, indicated with the number (1) in the image below:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-0536d1ba6ebcf4ef2b91bb5d35946d658ffaa940%2Fproduct-documentation\_user-management\_how-to-configure-single-sign-on-with-okta-1.png?alt=media)

This redirects to your SAML provider's login page, and validate the login, then redirects back to ThousandEyes, and your user will be logged in. After logging in for the first time successfully, a cookie is written to your system, indicating that you are an SSO user - and in the future, you will be taken to a special SSO-only login page, shown below.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-42c1d235781fe8be995743995faff7ba408643dd%2Fproduct-documentation\_user-management\_how-to-configure-single-sign-on-with-okta-2.png?alt=media)

### To Return to the Normal Login Page <a href="#to-return-to-the-normal-login-page" id="to-return-to-the-normal-login-page"></a>

This will return you to the normal, non-SSO login page.

In order to configure SSO, a user in a role with the **Edit security & authentication settings** permission needs to configure the settings identified above.

For a user to login using SSO, they must be in a role with the _Login via Single Sign-On_ permission. To restrict users to login via SSO, modify the role of these users to remove the _Login via ThousandEyes login page_ permission. It is important to note that for users with management permissions, it is not possible to remove the Login via ThousandEyes login page permission, in order to prevent lockout when you have issues with your Identity Provider.

Contact ThousandEyes Customer Engineering, should you have further questions on configuration of SSO with ThousandEyes.
