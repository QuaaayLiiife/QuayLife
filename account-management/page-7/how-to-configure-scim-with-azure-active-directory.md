# How to Configure SCIM with Azure Active Directory

You can add, delete, and modify ThousandEyes users using SCIM 2.0- and 1.1-compatible identity providers. This method dramatically decreases the time needed to provision users into ThousandEyes. This article describes how to integrate between the Azure Active Directory (Azure AD) identity provider and ThousandEyes.

* A ThousandEyes account that is assigned a role with the following permissions:
  * Edit users in all account groups
* User provisioning (user account creation)

Azure AD group information or other user attributes cannot be translated into account groups, roles, or any other ThousandEyes structure.

1.  1\.

    To start, log in to Azure AD with this

    [special link](https://ms.portal.azure.com/?Microsoft\_AAD\_IAM\_userProvisioningV2ClientEnabled=false#home)

    . This disables the Azure v2 Provisioning Client, which is not compatible with ThousandEyes SCIM. If you have already set up SSO with Azure AD, skip to step 7.
2.  2\.

    Go to **Azure Active Directory > Enterprise applications > Add an application** and search for **ThousandEyes**. If you are configuring a custom application, skip to step 4.

    ![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-e7dc5d455f67994c5bc05abdf86a3d588a2b5ac7%2Fproduct-documentation\_user-management\_how-to-configure-single-sign-on-with-azure-active-directory-1.png?alt=media)
3.  3\.

    Click the ThousandEyes Enterprise application and **Add**.

    ![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-db80a1d082f58d550e43706c9a92bf2e94050a2b%2Fproduct-documentation\_user-management\_how-to-configure-single-sign-on-with-azure-active-directory-2.png?alt=media)
4.  4\.

    Once you click **Add**, the Enterprise Application opens as below:

    ![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-02c411e147762b3a40039b6c2f353e6118101ae0%2Fproduct-documentation\_user-management\_how-to-configure-single-sign-on-with-azure-active-directory-3.png?alt=media)
5.  5\.

    To assign users can be assigned to the app, use the **Assign users and groups** option.
6.  7\.

    Click **Provisioning** (1) and change the **Provisioning Mode** (2) to **Automatic**.

    ![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-1080af78c514f228abf09905c1b1bf9ecc0e9376%2Fproduct-documentation\_user-management\_how-to-configure-scim-with-azure-active-directory-4.png?alt=media)
7.  8\.

    In the ThousandEyes platform, go to

    [**Account Settings > Users and Roles**](https://app.thousandeyes.com/account-settings/users-roles/?section=profile)

    **> Profile** tab and copy the **OAuth Bearer Token**. In Azure's **Admin Credentials** section, paste the token into the **Secret Token(1)** field and click **Test Connection** (2). The enterprise application tests the token and displays results(3).

    ![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-a09873c2a926aab7019f159ce5438c8b9d90561e%2Fproduct-documentation\_user-management\_how-to-configure-scim-with-azure-active-directory-5.png?alt=media)
8.  9\.

    Expand the **Mappings** section and click **Synchronize Azure Active Directory Users to ThousandEyes** to open the mappings.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-06c0ac51c571ef6b647daa704121ea1e0fc980fa%2Fproduct-documentation\_user-management\_how-to-configure-scim-with-azure-active-directory-6.png?alt=media)

1.  10\.

    Enable provisioning: Check the **Create**, **Update**, and **Delete** checkboxes. Make sure the **Attribute Mappings** match the following table; then click **Save**.

    | **Azure Active Directory Attribute**                         | **ThousandEyes Attribute**    | **Matching Precedence** |
    | ------------------------------------------------------------ | ----------------------------- | ----------------------- |
    | userPrincipalName                                            | userName                      | 1                       |
    | mail                                                         | emails\[type eq "work"].value | ​                       |
    | Switch(\[IsSoftDeleted], , "False", "True", "True", "False") | active                        | ​                       |
    | displayName                                                  | displayName                   | ​                       |

    ![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-2c269600d797997b26477cd310867cbd3da3df92%2Fproduct-documentation\_user-management\_how-to-configure-scim-with-azure-active-directory-6-1.png?alt=media)
2.  11\.

    Enable the **Provisioning Status** (1) radio button, set **Scope** (2) to **Sync only assigned users and groups**, and click **Save**.

    ![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-eb205fe3a2ac6abb19a267adad8534fc72ff928c%2Fproduct-documentation\_user-management\_how-to-configure-scim-with-azure-active-directory-7.png?alt=media)

Once the initial cycle has run, the Current Status section shows results with the number of users that are synchronized with ThousandEyes. This cycle runs once an hour to maintain a sync between Azure AD and ThousandEyes. You can force a cycle by checking **Clear current state and restart synchronization** and then **Save**.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-f790b4c9fe21e8e6626a1aac0b5facae3e3758ab%2Fproduct-documentation\_user-management\_how-to-configure-scim-with-azure-active-directory-8.png?alt=media)

​

To reveal under-the-hood activity, see **View Audit Logs**. This can be a very valuable troubleshooting tool:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-5b15f6053b8d44c238aa44bea69e3e899f7589db%2Fproduct-documentation\_user-management\_how-to-configure-scim-with-azure-active-directory-9.png?alt=media)

​

To see the attribute mappings in action, open the **Modified Properties** tab of an **Import** event:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-2ff6b05beff948f9a3ee929184280d3a6af58ef2%2Fproduct-documentation\_user-management\_how-to-configure-scim-with-azure-active-directory-10.png?alt=media)

​
