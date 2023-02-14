# ThousandEyes Support for SCIM

ThousandEyes is now able to add, update and delete users from identity providers who support the

[SCIM 2.0 and 1.1](http://www.simplecloud.info/)

standards, dramatically decreasing time to provision users into ThousandEyes and perform ongoing user management.

ThousandEyes has made available two SCIM API endpoints to receive user addition, update and deletion requests:

*
  * For SCIM 1.1 based API calls.
*
  * For SCIM 2.0 based API calls.

The operation of SCIM is simple: a Service Provider is able to map attributes from its local user database, and generate SCIM API calls to one of our endpoints in order to generate, update or delete the users on ThousandEyes end:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-e74e43134d7c01f9af5d20e9dfe5fecb15105851%2Fproduct-documentation\_user-management\_thousandeyes-support-for-scim-1.png?alt=media)

The structure of those calls must be compliant to the SCIM 1.1 or 2.0 protocol and schema, and also need to be compliant with our currently supported operations, discussed below.

In order to leverage ThousandEyes SCIM API endpoints, a ThousandEyes user having a role with the following permissions is required:

Both SCIM 1.1 and 2.0 Endpoints require the user to authenticate either with HTTP Basic Authentication using your Basic Authentication Token or an OAuth Bearer Token, both which can be created in the

[Security & Authentication](https://app.thousandeyes.com/settings/account/?section=security)

tab of ThousandEyes' Account Settings page.

By default, users added through SCIM to ThousandEyes will be assigned the "Regular User" role in all Account Groups of the organization where they are created. This default assignment can be changed in the SCIM Settings Section of the

[Security & Authentication](https://app.thousandeyes.com/settings/account/?section=security)

tab of ThousandEyes Account Settings. Once the users have been created in ThousandEyes, their individual roles can be freely modified in the

[Users](https://app.thousandeyes.com/settings/account/?section=users)

tab of Account Settings.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-e93236acfc1474d69a01b2893fbaeb5a53934ddd%2Fproduct-documentation\_user-management\_thousandeyes-support-for-scim-2.png?alt=media)

In this particular example, the "SCIM API User Role" under the "Support" Account Group will be granted to all the newly pushed SCIM users. All Roles and Account Groups can be used, as long as the API user making the SCIM API calls has permissions to grant them. Lacking those privileges will cause the SCIM provisioning process to fail.

*   ​

    [Filtering](https://tools.ietf.org/html/rfc7644#section-3.4.2.2)

    is supported for both SCIM 1.1 and 2.0 endpoints on the ExternalID and UserName attributes only.
* As of now, there is no support for SCIM Group creation or mapping, meaning that the SCIM /vX/Groups endpoint has no functionality.
* Operations on /Bulk endpoint are not supported.

Below is the list of endpoints and their supported operations:

*
  * accepted "type" values: "users" or "groups"
  * GET - returns schemas for provided type
*
  * GET (returns supported configurations)

From ThousandEyes perspective, the only needed configuration is creating an API user with the necessary privileges to create the accounts you will be importing. Only two attributes from ThousandEyes will be populated:

1.  2\.

    Email (mandatory and unique)

From the Service Provider's perspective, the trick is in the mapping of values from the Provider's directory to ThousandEyes' user database. From the provided attributes in the POST data from your provider, we parse for a valid email (our primary user identifier) in the following attributes in the provided order:

1.  1\.

    emails - primary:true or first element of the email list.

Making sure that a valid and unique email is passed on either of those two attributes to ThousandEyes is key to creation of a new user through SCIM.

Providers that supply a SCIM application usually provide a template where values can be mapped from the local database to what will be sent through SCIM. As an example, here is a basic structure of a SCIM 1.1 call template:

"urn:scim:schemas:core:1.0"

"username": "{$PROVIDER\\\_DB\\\_FIELD\\\_TO\\\_BE\\\_MAPPED\\\_TO\\\_USERNAME}",

"formatted": "{$PROVIDER\\\_DB\\\_FIELD\\\_TO\\\_BE\\\_MAPPED\\\_TO\\\_NAME}"

"value": "{$PROVIDER\\\_DB\\\_FIELD\\\_TO\\\_BE\\\_MAPPED\\\_TO\\\_EMAIL}",

"externalId": "{$PROVIDER\\\_SUPPLIED\\\_EXTERNAL\\\_ID",

### Microsoft Azure Active Directory <a href="#microsoft-azure-active-directory" id="microsoft-azure-active-directory"></a>

Microsoft Azure Active Directory and ThousandEyes can be configured to automatically provision and de-provision user accounts. The procedure is illustrated in

[this tutorial](https://docs.microsoft.com/en-us/azure/active-directory/saas-apps/thousandeyes-provisioning-tutorial)

.
