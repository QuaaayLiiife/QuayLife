# How to Configure Single Sign-On with PingOne

For the security of your SaaS-based infrastructure and the convenience of users in your organisation, the ThousandEyes service offers login via single sign-on (SSO). ThousandEyes supports SAML2-based identity providers for single sign-on. There are **two steps** to set up single sign-on:

1.  1\.

    Identity Provider configuration, done within your SSO system (in this article we use

    [PingOne](https://www.pingidentity.com/en/products/pingone.html)

    )
2.  2\.

    Service Provider configuration, which is done within ThousandEyes using one of the following options (the last two are normally easier and quicker to use):

    * Static Configuration: requires manual settings of the parameters.
    * Imported Metadata Configuration: a metadata file is used to configure the parameters.
    * Dynamic Configuration: a URL is used to configure the parameters.

Configuration is normally simple. Here's what you need:

* ThousandEyes account assigned a role with the _Edit security & authentication settings_ permission
*   A SAML2 authentication provider (in this example,

    [PingOne](https://www.pingidentity.com/en/products/pingone.html)

    )

### Identity Provider Configuration <a href="#identity-provider-configuration" id="identity-provider-configuration"></a>

1.  1\.

    Log in to the PingOne

    [Admin Console](https://admin.pingone.com/web-portal/)

    , and go to the **Application Catalog** tab of the **Applications** page.
2.  2\.

    Search for "**Thousand Eyes**" and click on the logo to expand the details.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-9d3832171b5ae7780788fd83ed4520c8aa5e7c33%2Fproduct-documentation\_user-management\_how-to-configure-single-sign-on-with-pingone-1.png?alt=media)

1.  1\.

    Click the **Setup** button to open the configuration panel.
2.  2\.

    If you want to use ThousandEyes Static Configuration, click on the **Download** button to save the **Signing Certificate** on your local drive.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-a3fed346a5959de53f60d15558b47f3e18badf03%2Fproduct-documentation\_user-management\_how-to-configure-single-sign-on-with-pingone-2.png?alt=media)

1.  1\.

    Again, only in case of ThousandEyes Static Configuration, copy the value of the **idpid** field of the query string, found at the end of the **Initiate Single Sign-On (SSO) URL**. Copy the string starting after the '=' character (see image below as example)

    **NOTE**: the **idpid** is a unique identifier generated when the ThousandEyes application is added. If the ThousandEyes application is removed from the PingOne and re-added, the **idpid** will change, and require you to reconfigure per these steps). Append the **idpid** string to this URL:

    [https://sso.connect.pingidentity.com/sso/idp/SSO.saml2?idpid=](https://sso.connect.pingidentity.com/sso/idp/SSO.saml2?idpid=)

    ​

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-5d1a49b5773143f3003478d7d1f5f9135c0528af%2Fproduct-documentation\_user-management\_how-to-configure-single-sign-on-with-pingone-3.png?alt=media)

1.  1\.

    At the bottom of the page click on **Continue to Next Step** to display the connection details:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-25562034700b9f92237a48e3b2f423fcf93555c2%2Fproduct-documentation\_user-management\_how-to-configure-single-sign-on-with-pingone-4.png?alt=media)

1.  1\.

    Click the **Continue to Next Step** button to display the attribute mapping.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-3cb296bfb995ad5ade00b0f32c73d1c26e4d14b2%2Fproduct-documentation\_user-management\_how-to-configure-single-sign-on-with-pingone-5.png?alt=media)

1.  1\.

    Click the **Continue to Next Step** button to display the application customization:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-90548f5150efb687e09fac13a0b822c15be7d240%2Fproduct-documentation\_user-management\_how-to-configure-single-sign-on-with-pingone-6.png?alt=media)

1.  1\.

    Click the **Save & Publish** button to review the configuration: if you are using the Imported Metadata Configuration, download the SAML Metadata file.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-9b41ed49bea46c6633eb0c501e206cd84a21ce2a%2Fproduct-documentation\_user-management\_how-to-configure-single-sign-on-with-pingone-7.png?alt=media)

1.  1\.

    Click **Finish** to complete the application setup.
2.  2\.

    Go to the **Users > User Groups** tab and click on the **Edit** button of the **\[email protected]** group name.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-f96182f3436978664b542e4acedb1211f893a73a%2Fproduct-documentation\_user-management\_how-to-configure-single-sign-on-with-pingone-8.png?alt=media)

1.  1\.

    Check the **ThousandEyes (SSO)** check-box and click the **Save** button.
2.  2\.

    Go to **Dashboard** and click the **Your PingOne dock URL** link.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-0cf4b5a0b126f32eba56772731bbf24e1b14d8f7%2Fproduct-documentation\_user-management\_how-to-configure-single-sign-on-with-pingone-9.png?alt=media)

1.  1\.

    The ThousandEyes application should be available in the dashboard when you go to your PingOne dock URL page:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-41540efa851b4d25c3ba06e3ceb4d2f639a625b6%2Fproduct-documentation\_user-management\_how-to-configure-single-sign-on-with-pingone-10.png?alt=media)

1.  1\.

    To add new users to the Single Sign-On, go to the **Users** page in PingIdentity and click **Add Users**. The new user can be "created" by filling out all the information or "invited" by providing only the email address.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-77fbbda2c0a1fc2020becbcad08975693088cf84%2Fproduct-documentation\_user-management\_how-to-configure-single-sign-on-with-pingone-11.png?alt=media)

### ThousandEyes Static Configuration <a href="#thousandeyes-static-configuration" id="thousandeyes-static-configuration"></a>

Follow these steps to configure your ThousandEyes organization to use single sign-on:

1.  1\.

    Log into ThousandEyes using an account with a role that has the _Edit security & authentication settings_ permission.
2.  3\.

    In the **Setup Single Sign-On** section, check the **Enable Single Sign-On** box.
3.  4\.

    Click the **Static Configuration** button.
4.  5\.

    Configure the **Setup Single Sign-On** fields according to the settings below and click the **Save** button.
5.  6\.

    To test the configuration use the instructions provided in a section below.

| Field                        | Value                                                                                             |
| ---------------------------- | ------------------------------------------------------------------------------------------------- |
| **Login Page URL**           | Use the URL created at **Step-5** of the Identity Provider configuration section.                 |
| **Logout Page URL**          | https://app.thousandeyes.com/login/sso                                                            |
| **Identity Provider Issuer** | https://pingone.com/idp/thousandeyes                                                              |
| **Service Provider Issuer**  | https://www.thousandeyes.com                                                                      |
| **Verification Certificate** | Use the certificate file downloaded at **Step-4** of the Identity Provider configuration section. |

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-8825429a579557dad154db987d974abea2f0d1ee%2Fproduct-documentation\_user-management\_how-to-configure-single-sign-on-with-pingone-12.png?alt=media)

**IMPORTANT:** Ensure that the **Service Provider Issuer** field matches the "service provider entityId" provided by PingOne. Any mismatch, including a protocol mismatch (http vs https) will cause the request to be rejected.

**NOTE:** The **Logout Page URL** is optional. If used, the URL should point to the page you wish your users to see when logging out of ThousandEyes.

Follow these steps to configure your ThousandEyes organization to use single sign-on:

1.  1\.

    Log into ThousandEyes using an account with a role that has the _Edit security & authentication settings_ permission.
2.  3\.

    Check the **Enable Single Sign-On** box.
3.  4\.

    Click the **Imported Metadata Configuration** button.
4.  5\.

    Click the **Import File** button and upload the **Metadata XML File** downloaded at Step-9 of the **Identity Provider configuration** section. The configuration section should populate with the SSO parameters (see screenshot below).
5.  7\.

    To test the configuration use the instructions provided

    [here.](broken-reference)

    ​

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-2d8bf6b5f851306f99119058a1b0a0feabf9f96f%2Fproduct-documentation\_user-management\_how-to-configure-single-sign-on-with-pingone-13.png?alt=media)

### ThousandEyes Dynamic Configuration <a href="#thousandeyes-dynamic-configuration" id="thousandeyes-dynamic-configuration"></a>

Currently, PingOne does not support dynamic configuration, so the most automated way to configure SSO is using the Imported Metadata Configuration option.

### Test the Configuration in PingIdentity <a href="#test-the-configuration-in-pingidentity" id="test-the-configuration-in-pingidentity"></a>

1.  2\.

    Go to **Dashboard** and click the **Your PingOne dock URL:**

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-0cf4b5a0b126f32eba56772731bbf24e1b14d8f7%2Fproduct-documentation\_user-management\_how-to-configure-single-sign-on-with-pingone-14.png?alt=media)

1.  1\.

    Click the **ThousandEyes** logo, you should automatically login into ThousandEyes.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-f54c095e0fbb80650ee3107c71103699c1004100%2Fproduct-documentation\_user-management\_how-to-configure-single-sign-on-with-pingone-15.png?alt=media)

### Test the Configuration in ThousandEyes <a href="#test-the-configuration-in-thousandeyes" id="test-the-configuration-in-thousandeyes"></a>

1.  1\.

    In the ThousandEyes **Security & Authentication** tab, click the **Run Single Sign-On Test** button. This button is present in all the configuration types (Static, Imported Metadata and Dynamic), but it only needs to be checked once for the selected configuration.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-e7a6c804ba44789d9510658a6926010ae48ce912%2Fproduct-documentation\_user-management\_how-to-configure-single-sign-on-with-pingone-16.png?alt=media)

1.  1\.

    If the SSO is configured properly, you should get a message indicating success, as shown in this screenshot:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-333f8266de812e6a92950924dbafb9c1c8df05b2%2Fproduct-documentation\_user-management\_how-to-configure-single-sign-on-with-pingone-17.png?alt=media)

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-d05d0a291d4a309169fb26f73040e687f9ebf4a5%2Fproduct-documentation\_user-management\_how-to-configure-single-sign-on-with-pingone-18.png?alt=media)

1.  1\.

    Input the SSO-enabled email address, and click the **Log In** button.
2.  2\.

    When the PingOne authorization page appears, enter your email and password, and press the **Sign On** button, you should automatically log into ThousandEyes.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-b40471cf91703ed7b6300b3fa97ce4b502c6a488%2Fproduct-documentation\_user-management\_how-to-configure-single-sign-on-with-pingone-19.png?alt=media)

1.  1\.

    Alternatively, users can access the ThousandEyes application through the user's PingOne dashboard. Please refer to the "**Test the configuration in PingIdentity"** section presented above.

If your single sign-on login fails, verify that certain SAML settings are configured as below:

* **Destination**: https://www.thousandeyes.com
* **AuthnContextClassRef**: PasswordProtectedTransport
*   **AudienceRestriction**: http://www.thousandeyes.com/

    **Note**: The **AudienceRestriction** element generated by your identity provider's configuration must match _exactly_ the value set for the **Service Provider Issuer** field in ThousandEyes. Any mismatch, including a protocol mismatch (http vs https) will cause the request to be rejected.
* **Recipient**: http://www.thousandeyes.com/
* **NameID Format**: emailAddress
* **AssertionConsumerServiceURL**: https://app.thousandeyes.com/login/sso/acs
