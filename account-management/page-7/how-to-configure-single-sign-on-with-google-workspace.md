# How to Configure Single Sign-On with Google Workspace

For the security of your SaaS-based infrastructure and the convenience of users in your organization, the ThousandEyes service offers login via single sign-on (SSO). ThousandEyes supports SAML2-based identity providers (IdPs) for single sign-on. In this configuration example, we use Google Workspace (formerly Google Apps) as the identity provider.

There are **two steps** to set up single sign-on:

1.  1\.

    Identity provider configuration, which is done within your identity provider's system (in this case, Google)
2.  2\.

    Service provider configuration, which is done within ThousandEyes using one of the following options:

* **Static Configuration**: Requires manual settings of the parameters.
* **Imported Metadata Configuration**: A metadata file is used to configure the parameters (recommended method).
* **Dynamic Configuration**: A URL is used to configure the parameters (not yet supported by Google Workspace SAML)

Here's what you need to configure single sign-on:

* A user in a role with the _Edit security & authentication settings_ permission in ThousandEyes.
* A Google Workspace administrator account.

### Identity Provider (Google) Configuration <a href="#identity-provider-google-configuration" id="identity-provider-google-configuration"></a>

1.  1\.

    Log in to Google Workspace using an administrator account.
2.  3\.

    Click **Apps (Manage apps and their settings)**.
3.  5\.

    Click the **+** icon to configure a new SAML application.

    ​

    ![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-6a29321b8c66255b6a7224ae67384138be88886d%2Fproduct-documentation\_user-management\_how-to-configure-single-sign-on-with-google-g-suite-1.png?alt=media)

    ​
4.  6\.

    Click **SETUP MY OWN CUSTOM APP**.

    ​

    ![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-8d2f291de0f98eb084b4c5c2997f8dbc05df35d8%2Fproduct-documentation\_user-management\_how-to-configure-single-sign-on-with-google-g-suite-2.png?alt=media)

    ​
5.  7\.

    Obtain the Google identity provider information for configuration in ThousandEyes.

    **Option 1** is used for static configuration of the Service Provider. Copy and paste the SSO URL and IdP Entity ID values into a separate document, and download the certificate. Then click **Next.**

    **Option 2** is used for imported metadata configuration of the Service Provider. Download the IDP Metadata file. Then click **Next**.

    ​

    ![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-c7908eae7cdf873a8b5010d4f8a83a6a23d8bf58%2Fproduct-documentation\_user-management\_how-to-configure-single-sign-on-with-google-g-suite-3.png?alt=media)

    ​

Enable the ThousandEyes application for all users by clicking the More Options menu (three vertical dots) and selecting **ON for everyone**.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-e1d3b66f3d6c2898810ed2f3cb67f89363fc3afc%2Fproduct-documentation\_user-management\_how-to-configure-single-sign-on-with-google-g-suite-4.png?alt=media)

### Service Provider Configuration <a href="#service-provider-configuration" id="service-provider-configuration"></a>

1.  1\.

    Log in to ThousandEyes as a user having a role with the _Edit security & authentication settings_ permission.
2.  3\.

    In the **Setup Single Sign-On** section:

    ​

    ![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-2f1fad0b413f9332f6d918e144db06f5d4c95363%2Fproduct-documentation\_user-management\_how-to-configure-single-sign-on-with-google-g-suite-5.png?alt=media)

    ​

    * Check the **Enable Single Sign-On** box.
    * Enter the **Login Page URL** (SSO URL from previous section - step 7).
    * Enter a **Logout Page URL** (Optional).
    * Enter the **Identity Provider Issuer** (Entity ID from the previous section - step 7).
    * Enter the Service Provider Issuer (SP Entity ID from the previous section - step 9; do **not** use the Entity ID from step 7).
    * Click the **Choose File** button to upload the verification certificate (certificate downloaded from the previous section).
3.  5\.

    Click **Run Single Sign-On Test** to verify that the single sign-on works as expected.

#### Imported Metadata Configuration <a href="#imported-metadata-configuration" id="imported-metadata-configuration"></a>

Follow these steps to configure your ThousandEyes organization to use single sign-on:

*   Enter the ThousandEyes application information that will be visible with the user's Google environment.

    **Description** and **Upload logo** are both optional. A pre-sized logo is available below the screenshot.

    ​

    ![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-92804f3f5f52e0c6bb142c9daedabc570fd22e58%2Fproduct-documentation\_user-management\_how-to-configure-single-sign-on-with-google-g-suite-6.png?alt=media)

    ​

    A ThousandEyes logo, sized to fit with Google Apps:

    ​

    ![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-71fb30cb7b7833512a0d3eecc6063faa0d587e5b%2Fproduct-documentation\_user-management\_how-to-configure-single-sign-on-with-google-g-suite-7.png?alt=media)

    ​

    Right-click on the image above to save it to your local storage, then upload to Google Apps with the **Choose File** button.
*   Enter the required ThousandEyes Service Provider details:

    ​

    ![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-04544feabcd05750425983a09274f2791afdd77b%2Fproduct-documentation\_user-management\_how-to-configure-single-sign-on-with-google-g-suite-8.png?alt=media)

    ​
*   Skip the optional **Attribute Mapping**, and click **Finish:**

    ​

    ![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-2cbd3ee3419357f2601e144dc83f07735467b512%2Fproduct-documentation\_user-management\_how-to-configure-single-sign-on-with-google-g-suite-9.png?alt=media)

    ​

    * Log in to ThousandEyes as a user with a role that has the _Edit security & authentication settings_ permission.
    *   In the **Setup Single Sign-On** section:

        * Check the **Enable Single Sign-On** box.
        * Enter the **Login Page URL** (SSO URL from previous section - step 7).
        * Enter a **Logout Page URL** (Optional).
        * Enter the **Identity Provider Issuer** (Entity ID from the previous section - step 7).
        * Enter the Service Provider Issuer (SP Entity ID from previous section - step 9; do **not** use the Entity ID from step 7).
        * Click the **Choose File** button to upload the verification certificate (certificate downloaded from the previous section - step 7).

        ​

        ![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-058895e4c115eed1e6373c808b4320e31dc5fa67%2Fproduct-documentation\_user-management\_how-to-configure-single-sign-on-with-google-g-suite-10.png?alt=media)

        ​
    * Click **Run Single Sign-On Test** to verify that the single sign-on works as expected.
    * Log in to ThousandEyes using an account with a role that has the _Edit security & authentication settings_ permission.
    * Check the **Enable Single Sign-On** box.
    * Click the **Imported Metadata Configuration** button.
    * Click the **Import File** button and upload the **IDP Metadata File** downloaded at Step 7 of the **Identity Provider configuration** section. The configuration section should populate with the SSO parameters (see screenshot below).
    *   Click **Run Single Sign-On Test** to verify that the single sign-on works as expected.

        ​

        ![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-12c39b1f4e51c9442610e850da79ed242dcc1ae5%2Fproduct-documentation\_user-management\_how-to-configure-single-sign-on-with-google-g-suite-11.png?alt=media)

        ​

        ![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-a2a2d180d8d90ecceebf4d610e9efe00b76519e9%2Fproduct-documentation\_user-management\_how-to-configure-single-sign-on-with-google-g-suite-12.png?alt=media)

        ​

1.  2\.

    Input the SSO-enabled email address, and click **Log In**.
2.  3\.

    When the Google authorization page appears, enter your email and password, and click **Sign On**. You should automatically log in to ThousandEyes.

### Returning to Standard (non-SSO) Login Page <a href="#returning-to-standard-non-sso-login-page" id="returning-to-standard-non-sso-login-page"></a>

If your organization discontinues use of SSO at any time, you can return to the login page, by using this special login:

This will return you to the normal, non-SSO login page.

The following information describes the permissions required in ThousandEyes in order to configure or use single sign-on. For more information on configuring roles and permissions, see

[Role-Based Access Control, Explained](broken-reference)

.

In order to configure single sign-on in ThousandEyes, a user in a role with the _Edit security & authentication settings_ permission is required, as described above.

For a user to log in using single sign-on, they must be assigned a role with the _Login via Single Sign-On_ permission. To restrict users to log in only via SSO, remove the _Login via ThousandEyes login page_ permission. Note that for users with management permissions, it is not possible to remove the _Login via ThousandEyes login page_ permission. This feature ensures that administrators cannot be prevented from logging in when they have issues with an identity provider.
