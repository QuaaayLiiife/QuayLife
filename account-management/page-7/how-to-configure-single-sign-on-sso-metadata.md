# How to Configure Single Sign-On (SSO): Metadata

For the security of your SaaS-based infrastructure and the convenience of users in your organization, ThousandEyes offers login via single sign-on (SSO). ThousandEyes supports

[SAML 2.0](https://en.wikipedia.org/wiki/SAML\_2.0)

\-based SSO.

### ThousandEyes-Side Configuration <a href="#thousandeyes-side-configuration" id="thousandeyes-side-configuration"></a>

* Login URL for your SAML provider
* Logout URL for your SAML provider (optional)
* Verification certificate(s)

There are three methods to set these options:

*
  * Each parameter must be supplied manually, including verification certificate(s).
* **Imported Metadata Configuration**
  * ThousandEyes will parse a user-supplied metadata XML file and load the parameters.
*
  * ThousandEyes will parse a metadata file from a provided URL on demand (for each user login).

### Identity Provider-Side Configuration <a href="#identity-provider-side-configuration" id="identity-provider-side-configuration"></a>

Alternatively, you can opt for manual configuration of your Identity Provider. The following information lists the characteristics of ThousandEyes as a SAML Service Provider:

* ThousandEyes supports both Service-Provider-initiated (i.e., ThousandEyes login page initiated) and Identity-Provider-Initiated (i.e., clicking a link from inside the customer portal) based logins
* SAML Assertion NameID (unspecified or emailAddress format): The email address of the user to be authenticated (must be already a registered user in the ThousandEyes platform).
  * If a valid email address (as registered in ThousandEyes) is not found in the NameID field, the assertion will be parsed for additional name claims.
*
  * Destination: https://app.thousandeyes.com
  * **AuthnContextClassRef: PasswordProtectedTransport**
  *   Audience Restriction: https://app.thousandeyes.com

      _Note: When using static configuration, the Audience Restriction configured in your Identity Provider's configuration **must**  **exactly**  **match** the value set for the Service Provider Issuer field in ThousandEyes. Any mismatch, including a protocol mismatch (http:// vs https://) and trailing slashes will cause the request to be rejected._ _When using dynamic or imported metadata configurations, make sure you configure your IdP to use_

      [https://app.thousandeyes.com](https://app.thousandeyes.com/)

      _as the Audience Restriction._

### Key Points in ThousandEyes Assertion Validation <a href="#key-points-in-thousandeyes-assertion-validation" id="key-points-in-thousandeyes-assertion-validation"></a>

* ThousandEyes parses the email (our primary identifier of users) on the SamlResponse created by your Identity Provider. We require that you configure your IdP to supply a registered user's email address in one of the following attributes of the assertion (failure to find a registered email address in any of these attributes will break the SSO process):
  * NameID in the format "urn:oasis:names:tc:SAML:1.1:nameid-format:unspecified”
  * NameID in the format "urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress"
* Make sure that at least one of the uploaded verification certificates corresponds to the private key that signs the SamlResponse assertion.
* Verify that the AudienceRestriction configured in your IDP is an **exact match** of the service provider issuer string within ThousandEyes SSO configuration.

### Vendor-Specific Configurations <a href="#vendor-specific-configurations" id="vendor-specific-configurations"></a>

ThousandEyes supports the use of any SAML 2.0-based identity provider for single sign-on.
