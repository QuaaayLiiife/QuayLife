# Customer Security and Privacy Responsibilities

As a cloud service provider, ThousandEyes shares the responsibility for security and privacy with its customers. Review the information below to understand your role in the implementation of security, privacy controls, and operational activities.

### Identity and Access Management <a href="#identity-and-access-management" id="identity-and-access-management"></a>

* Initially, ThousandEyes creates a single account group and assigns the designated _permitted user_ with the customer's built-in admin role.
*   The customer configures groups and users using

    [role-based access controls (RBAC)](broken-reference)

    to ensure that only authorized users can access or view sensitive data (including personal information). Note that ThousandEyes allows masking, through RBAC, permissions to certain personal information that the Endpoint Agent collects.
*   The customer creates users and accounts with appropriate roles (the use of

    [SCIM API](broken-reference)

    is supported for automation). There is no charge associated with user accounts on the ThousandEyes platform.
*   Permitted users with management permissions can remove permitted users from account groups in which they have management permissions. The customer is responsible for promptly removing permitted users’ access to the ThousandEyes application, when appropriate.

    Customers with a

    [SAML2](broken-reference)

    \-compliant identity provider system can configure the ThousandEyes application to require permitted users to be authenticated using single sign-on (SSO).
* **Passwords.** If local authentication is in use, passwords are required to be at least eight (8) characters long and require at least one digit, uppercase or non-alphanumeric character.
  * If a permitted user has more than ten (10) failed login attempts to access the application, the permitted user's account will be suspended and will require a password reset via the forgotten-password facility.
  * Use appropriate password policies that enforce complexity and maximum password age. The use of shared logins should be avoided at all times.
  * Authentication for access through the API occurs via an authentication token that the application generates randomly upon your first login. This token does not expire and is revocable at any point in time either by the user who owns the authentication token, or by a user with management permissions in the context of the user’s account group. Once the token is revoked, any API access attempts using the revoked authentication token will be blocked.
  * When using ThousandEyes appliances (virtual and physical), the customer’s admins must change the password of the virtual appliance as part of the initial setup process.
* The customer must periodically review access to the ThousandEyes application to make sure only authorized workers have access, with proper access levels.
* If you enable single sign-on (SSO) for your ThousandEyes organization, this does not limit all users and user roles to logging in via SSO only.
  * User login options for your ThousandEyes organization are configured via the “Login via Single Sign-On” and “Login via ThousandEyes login page” role-based permissions. User roles assigned with both permissions can choose to login via SSO or via the standard ThousandEyes login page. It’s important to note that built-in roles - Organization Admin, Account Admin, and Regular User - are preconfigured with the “Login via Single Sign-On” and “Login via ThousandEyes login page” permissions. This presents an unintended risk of brute-force attacks of those credentials, and does not enable the control that the organization desires to remove access to the ThousandEyes platform when a user is no longer with the organization.
  * To constrain users to log in via SSO only, create a custom role with the “Login via Single Sign-On” permission enabled. Ensure that the “Login via ThousandEyes login page” permission is disabled for this custom role.

### Infrastructure Protection Services <a href="#infrastructure-protection-services" id="infrastructure-protection-services"></a>

* Customers must ensure the security of their endpoints (end-user computers) and connectivity. If Enterprise Agents are in use, it is the customer’s responsibility to protect the underlying physical infrastructure, virtualization, and containerization (if present). If the Enterprise Agent is delivered as a Linux application, the customer must also secure the underlying Linux server.
*   When you deploy a ThousandEyes Enterprise Agent and configure an HTTP server test to use a proxy server, the test will utilize the CONNECT method. This method transmits proxy authentication credentials in clear text, which is a limitation of the protocol and not of the ThousandEyes product. If you use an external proxy, this could result in proxy authentication credentials being transmitted over the internet in clear text. We recommend that you encrypt the proxy authentication credentials (i.e., using NTLM proxy authentication). For instructions on configuring this setting, see

    [Configuring an Enterprise Agent to Use a Proxy Server](https://docs.thousandeyes.com/product-documentation/global-vantage-points/enterprise-agents/proxy/configuring-an-enterprise-agent-to-use-a-proxy-server#4.-configure-proxy-settings-on-linux-package-based-enterprise-agents)

    .
* When you communicate with ThousandEyes Customer Engineering via email and chat, attachments from those communications are stored in ThousandEyes AWS S3 bucket. Each attachment utilizes a unique path but is available publicly to any user with the URL path. We recommend that you not forward the email with the embedded URL for these attachments to any unauthorized party. There is a low risk of unauthorized users brute-forcing the AWS S3 path before being detected.

### Key and Certificate Management <a href="#key-and-certificate-management" id="key-and-certificate-management"></a>

If desired, the customer is also responsible for replacement of a self-signed SSL certificate for the ThousandEyes Virtual Appliance management interface with an SSL certificate of their choice and to make sure all required DNS entries are created in their DNS management system (forward and/or reverse zones).

The customer assigns the "Keep session alive on auto-update" permission only for those roles containing users who need to have it (such as a NOC user). The ThousandEyes application has a 30-minute session timeout that does not apply when the user has any of the following views open in their browser:

* **Cloud & Enterprise Agents > Agent Settings**

The views listed above implement automatic content refreshing that happens periodically (the alerts list refreshes every two minutes; dashboards refresh every minute; agent settings refresh every minute). These content-refresh events also reset the session timer, preventing an inactive user's browser session from timing out.

The automatic session prolongation described above requires that the "Keep session alive on auto-update" permission be enabled for the user. For more details about user roles and permissions, see the

[article on role-based access control](broken-reference)

.

ThousandEyes has integrated a convenient _credentials repository_, which is to be used in conjunction with web transaction tests that require authentication to run successfully. These credentials are handled securely by way of modern algorithms and technologies, both in-transit and at rest.

Naturally, it remains important to restrict access to this particular area. You should designate a ThousandEyes user with the **Organizational Admin** role to appropriately delegate access to the credentials repository, so that your organization can control exactly who can view and use sensitive information with the transaction tests feature. You can disallow all users, regardless of their permissions, from accessing transaction test credentials after they have been entered into the credentials repository as described in

[Disallowing Access to the Credentials Repository](https://docs.thousandeyes.com/product-documentation/browser-synthetics/transaction-tests/working-with-secure-credentials#disallowing-access-to-the-credentials-repository)

.

In relation to the ThousandEyes SaaS Application, the most important steps for customers to execute as part of the “Policies and Standards” domain management are to:

1.  1\.

    Classify data stored and processed by ThousandEyes;
2.  2\.

    Establish a worker awareness and training program;
3.  3\.

    Comply with Data Subject Access Requests requirements (ThousandEyes will redirect data subjects to your Administrators).

The customer should review and understand data retention policies and consider the use of API for export or archival.

Review the information below to understand your role in the implementation of privacy controls and operational activities.

* Update your data inventory to note the:
  * purposes for which ThousandEyes will be used.
  * lawful basis for processing.
* If using an Endpoint agent to gather end user information you should determine if consent is needed. If it is needed, obtain and record the consent for the processing of PII.
*   Determine if your organization requires a Privacy Impact Assessment for ThousandEyes. Our

    [Privacy Data sheet](https://trustportal.cisco.com/c/r/ctp/trust-portal.html?doctype=Privacy%20Data%20Sheet|Privacy%20Data%20Map\&search\_keyword=thousandeyes#/1610384661419206)

    and

    [security brief](https://trustportal.cisco.com/c/r/ctp/trust-portal.html?search\_keyword=thousandeyes#/1606232312674803)

    can provide relevant information.
*   Ensure your contract with ThousandEyes includes all the necessary elements such as the new Cisco

    [Master Data Protection Addendum](https://trustportal.cisco.com/c/dam/r/ctp/docs/dataprotection/cisco-master-data-protection-agreement.pdf)

    (MDPA) with the newly revised Standard Contractual Clauses (SCCs) for data transfers from the European Union to the United States.
* Provide information to your internal users about data within the ThousandEyes platform if they make a Subject Access Request (SAR) that relates to ThousandEyes.
  *   Platform user information can be obtained by looking on the Users tab as described in these

      [instructions](broken-reference)

      .
  *   Endpoint Agent data can be obtained through reports to note any data collected for a particular user by following these

      [instructions](https://docs.thousandeyes.com/product-documentation/global-vantage-points/endpoint-agents/reporting-on-data-collected-by-endpoint-agent)

      .
  *   ThousandEyes Platform support case information can be obtained by looking on the

      [Cases tab](https://app.thousandeyes.com/sfdc/community/home?communityTabId=Cases)

      .
* File a case with Customer Success if additional assistance is needed to address a subject access request (SAR) for access, correction, or deletion which involves User or Endpoint agent data on the ThousandEyes platform.
* Minimize the PII data provided to ThousandEyes to that which is relevant, proportional, and necessary for your purposes.
* Properly store and transmit any PII data downloaded from the ThousandEyes platform according to your organization’s policies.
* Properly retain or dispose of PII data downloaded from the ThousandEyes platform according to your organization’s policies.
*   If an end-user asset leaves the customer’s operational ownership, it is recommended that they uninstall the ThousandEyes Endpoint Agent from the system. For all uninstalled or retired systems with an Endpoint Agent, ThousandEyes recommends you remove the Endpoint Agent entry from the ThousandEyes Endpoint Agent inventory, as these are not removed automatically. Alternatively, it is encouraged that you utilize the auto-delete feature to set a threshold that will automatically delete, disable, or re-enable the Endpoint Agent. For details on the auto-delete feature, see

    [Auto-Manage the Status of Endpoint Agents](https://docs.thousandeyes.com/product-documentation/global-vantage-points/endpoint-agents/managing/manage-endpoint-agent-settings#auto-manage-the-status-for-endpoint-agents)

    .
*   Review any email notifications about changes to the

    [Authorized Subprocessors](https://docs.thousandeyes.com/product-documentation/privacy-related/authorized-subprocessors-for-thousandeyes-network-intelligence-platform)

    used by ThousandEyes and contact Thousandeyes if you have any issues or concerns with any change.
*   Due to the possibility of displaying sensitive data during transaction tests, ThousandEyes has released a feature to disable the use of the screenshot capability. The screenshot capability can be disabled on an individual test or globally for the organization. For instructions on making this change, see

    [Test Settings for Page Load and Transaction Tests](https://docs.thousandeyes.com/product-documentation/browser-synthetics/test-settings-page-load-transaction#browser-options)

    .

### Other Security Guidelines to Consider <a href="#other-security-guidelines-to-consider" id="other-security-guidelines-to-consider"></a>

* A customer can request from ThousandEyes Support the removal of access permissions into their organization from ThousandEyes personnel. This permission is enabled by default to facilitate support and other activities related to service operations.
* Carefully consider who in your organization should have the ability to perform Snapshot Sharing, as this functionality allows your internal users to share network events with third parties (such as service providers) in a way that allows the data in question to be accessed anonymously.
* If Enterprise Agents are deployed in your network, consider changing Enterprise Agent NTP settings by pointing to your authorized NTP servers (otherwise, the defaults for your operating systems will be used).
* Make sure your users are refreshing their API tokens according to your policy.
* If you have deployed a ThousandEyes Enterprise Agent Virtual Appliance (TEVA) and have configured it to use a proxy that requires authentication, due to a limitation of the underlying Linux platform, those credentials will be stored on the appliance in clear text.
