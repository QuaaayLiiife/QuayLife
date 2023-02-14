# Working with Account Settings

The

[**Account Settings** screen](https://app.thousandeyes.com/settings/account/)

provides a management interface for various aspects of your ThousandEyes account, such as your user settings and contact information. You can also manage information about your organization, its users, and account groups. To access your account settings, click **Account Settings** on the lefthand side menu.

The **Account Settings** screen's submenus are separated into multiple tabs. You might not see all the tabs and their contents, depending on your permissions. For example, users with the _Organization Admin_ role see the **Users** tab, which displays information about users in each account group within the organization. Users with the _Account Admin_ role also see a **Users** tab, but are limited to seeing only those users in the account groups they are assigned to.

The

[**Profile** tab](https://app.thousandeyes.com/settings/account/?section=profile)

displays information about the user's organization(s), account groups(s) and assigned roles within those account groups. Here, users can modify their own username and email address (used for login to the ThousandEyes platform), change their password, and set their preferred timezone for the web interface.

**Updating Your Email Address**

If you need to update the email address you use for login to the ThousandEyes platform, do the following:

1.  1\.

    In the **Email** field, type the new email address.
2.  3\.

    In both the new and the old email addresses, confirm the change.

    The update takes effect only when confirmation is received from _both_ email addresses. Until then, the user can still log in from the previous email address.

Note that this dual-confirmation approach applies whether you are interacting with the ThousandEyes user management via the ThousandEyes web UI, via the ThousandEyes API, or via SCIM.

Each user's password must be at least 8 characters in length, and must contain at least 3 of the following types of characters:

If the user is a member of more than one account group (in one or in multiple organizations), they can select their **Login Account Group**. This determines into which account group the user is placed upon login. Once logged in, users can switch between account groups with the **Current Account Group** selector in the User menu, as described in

[Switching Account Groups](broken-reference)

.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-92214f7c20b682f1beb98e86d1079368d700579c%2Fproduct-documentation\_user-management\_working-with-account-settings-1.png?alt=media)

For users with

[API access](https://developer.thousandeyes.com/v6/#/authentication)

enabled (i.e., users with the _API Access_ permission), the **User API Tokens** section is visible, containing the API authentication tokens:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-6adb62fb3ba6198d782f27a9b8d77a129bab9574%2Fproduct-documentation\_user-management\_working-with-account-settings-2.png?alt=media)

A user with the _View roles_ permission will be able to see the

[**Roles** tab](https://app.thousandeyes.com/settings/account/?section=roles)

containing a table of all security Roles defined within the organization (1) and permissions associated with each Role (2):

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-c82a45f690d02e1dc13b3cbbee127af1e44ffc2a%2Fproduct-documentation\_user-management\_working-with-account-settings-3.png?alt=media)

The extensive list of permissions can be narrowed down by using the search bar (3). New roles can be defined by either clicking the **Add New Role** button (4) or by cloning one of the existing roles by clicking the

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-5db22c47bdfed2631e8eacf268a5eb6b0b111d5a%2Fproduct-documentation\_user-management\_working-with-account-settings-4.png?alt=media)

icon under its name.

The

[**Users** tab](https://app.thousandeyes.com/settings/account/?section=users)

is visible for users having the _View all users_ permission. As the name suggests, this section allows general user management:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-53677d589016420f4551c0b03e44ac02350e34b2%2Fproduct-documentation\_user-management\_working-with-account-settings-5.png?alt=media)

Clicking on any entry in the table expands it and presents management options for the user's name, email address and account group associations, not unlike what each user sees in their **Profile** tab:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-443759727695baf02b7e4fdeddd879e9fef9906d%2Fproduct-documentation\_user-management\_working-with-account-settings-6.png?alt=media)

At the top, the **Add New Users** button opens a similar dialog, displayed in the figure below. This dialog has one additional feature - multiple users can be created in one step, with identical account group and role associations. To create multiple users in one step, simply add multiple email addresses into the **Emails** field. You can add multiple emails by either pressing the **Enter** key after each email address is typed in, or by pasting a comma-separated list of email addresses into the field:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-7349c043068e55c2e261e8d466a2dde36867a313%2Fproduct-documentation\_user-management\_working-with-account-settings-7.png?alt=media)

As shown in the previous figure (the expanded user entry figure above), each user can be a member of multiple account groups. In each account group, the user can have more than one role assigned. The permission list granted to the user within each account group is a union of permissions across all roles assigned to the user in that account group. For example, if the user has the Account Admin and Regular User roles, they will have the combined permissions of both roles.

For users with the _View all account groups_ permission, the

[**Account Groups** tab](https://app.thousandeyes.com/settings/account/?section=accountgroups)

will be visible. This tab displays all

[account group](<../../.gitbook/assets/what is an account group>)

defined in the organization, along with the number of users and

[Enterprise Agents](https://docs.thousandeyes.com/product-documentation/global-vantage-points/enterprise-agents/)

present in each account group. Users with the _Edit all account groups_ permission can add, manage and delete account groups:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-8696f3be715ff3f93440d703fe2facc67348e733%2Fproduct-documentation\_user-management\_working-with-account-settings-8.png?alt=media)

Expanding a row in the **Account Groups** table displays the account group's details and allows changes to the account group's name. The

[account group token](https://docs.thousandeyes.com/product-documentation/global-vantage-points/enterprise-agents/installing/where-can-i-get-the-account-group-token)

is also displayed for users to copy when installing Enterprise Agents.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-c2929e6ef8d8d1dea319351d93dbedd24d8b45f6%2Fproduct-documentation\_user-management\_working-with-account-settings-9-2.png?alt=media)

An account group's Enterprise Agents can be displayed in the **Enterprise Agents** drop-down. Enterprise Agents available to the current account group are displayed with checked boxes. Agents from other account groups can be checked to make them available to this account group or can be unchecked to remove them from the current account group. A checked and greyed out entry indicates an agent for which the current account group is the primary account group (i.e., the agent was created with the current account group's token) and thus cannot be deselected:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-b8e207527db8b434265ba84c69df9a91e31b377d%2Fproduct-documentation\_user-management\_working-with-account-settings-10.png?alt=media)

See

[What Is an Account Group?](<../../.gitbook/assets/what is an account group>)

for further information about account groups and why having multiple account groups might be useful for you.

As explained above, each user can have access to more than one account group. Those account groups can even span across multiple organizations. Additionally, users with the Organization Admin role (or similar) have access to all account group defined within the organization. This allows the user to view tests, shares, reports and agents assigned to each of the account groups belonging to the organization.

To change the current account group context, click on the

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-4be4a2c52ee326a95244a179a1d56616d27b7ee3%2Fproduct-documentation\_user-management\_working-with-account-settings-11.png?alt=media)

icon in the upper right corner of the ThousandEyes platform and expand the **Current Account Group** drop-down menu. This will allow you to switch into another account group context.

The following figure on the left shows the currently active context of the "QA PROD" account group (1). The figure on the right shows the expanded drop-down listing all account groups available to the user, from multiple organizations (2). Below the ThousandEyes Support Organization (in gray) is the "ThousandEyes Support" (3) account group. Under the ThousandEyes Internal Organization there are 4 other account groups. In this example QA PROD is listed in another organization further up in the menu selection:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-8b4008978adb3739d6e0764a3e6b91b039ca4b70%2Fproduct-documentation\_user-management\_working-with-account-settings-12.png?alt=media)

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-a013607ecc7a8209dacbf414a00603a13b40d2b9%2Fproduct-documentation\_user-management\_working-with-account-settings-13.png?alt=media)

The

[**Usage** tab](https://app.thousandeyes.com/settings/account/?section=organization)

shows settings for Plan Usage and Cloud Agent Units. This tab is only accessible by organization administrators - relevant permissions are _View billing_, _View organization usage_, and _View security & authentication settings_:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-adc85c1ea61ec7fc678c0e5f57bce89b79aff8de%2Fproduct-documentation\_user-management\_working-with-account-settings-14\_v2.png?alt=media)

The **Plan Usage** section provides an overview of all aspects of Unit and license consumption:

1.  1\.

    **Units**: Shows the current usage (solid green bar), additional projected usage until the end of the current billing cycle (dashed green/white bar) and the remainder of the planned/purchased capacity.
2.  2\.

    **Endpoint Agent Licenses**: The number of Endpoint Agents currently enabled and the number of purchased licenses in the plan.
3.  3\.

    You can select between showing consumption details of **Cloud Agent Units** or **Enterprise Agent Units**. The **Enterprise Agent Units** option is only visible to organizations on a metered billing model.
4.  4\.

    Control the breakdown table content by choosing to show your consumption by **Account Group**, by **Test Type** or by individual **Test**.

If you have any questions regarding your usage numbers, contact your ThousandEyes account manager or the Customer Engineering team via

\[email protected]

.

An organization owner can delete their organization. To delete your organization:

1.  1\.

    Log in to the ThousandEyes platform.
2.  3\.

    In the **Organization Deletion** section, click **Delete**.

The

[**Billing** tab](https://app.thousandeyes.com/settings/account/?section=billing)

shows current billing information for your organization. This tab is only accessible by users with the _View billing_ permission:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-bea55a60a516f4f285ecf95a088ecaa6dec3c926%2Fproduct-documentation\_user-management\_working-with-account-settings-15.png?alt=media)

The following sections are visible in this tab:

1.  1\.

    **Plan Details**: The details of your contracted ThousandEyes usage plan.
2.  2\.

    **Billing Address**: The address to be included on the invoices and the email address to which invoices are sent.
3.  3\.

    **Payment Method**: Displays payment information which is sent to a third party provider used by ThousandEyes for credit card processing. This form is a secure element connecting you directly to the third party provider. ThousandEyes never receives the credit card information, but rather obtains an authorization on behalf of the payment processor.
4.  4\.

    **Billing History**: Displays billing information generated over previous billing cycles.

If you have any questions regarding your plan details, contact your ThousandEyes account manager or the Customer Engineering team via

\[email protected]

.

An account group can be limited to a fixed quota of units from here. A user with the _Can assign and edit quota_ permission will be able to see the

[**Quotas** tab](https://app.thousandeyes.com/settings/account/?section=quotas)

:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-e2a9c69e58a5584d0d962e1057e58f27f91442ec%2Fproduct-documentation\_user-management\_working-with-account-settings-16.png?alt=media)

Components of the **Quotas** tab:

1.  1\.

    **Plan**: Total units allocated to an organization per month.
2.  2\.

    **Organization Current Usage Rate**: Current rate at which an organization is utilizing units in their plan. Shown in terms of % of Plan used and units consumed.
3.  3\.

    **Organization Quota**: Total units assigned to an organization. Enabled and value set to total plan by default. Can be toggled depending upon plan of an organization.
4.  4\.

    **Unallocated Usage**: Available units not allocated to any account group.
5.  5\.

    **Account Group**: This column contains names of account groups defined in the organization.
6.  6\.

    **Current Usage Rate**: Current rate at which an account group is utilizing units. Shown in terms of % of Plan and units consumed.
7.  7\.

    **Quota Switch**: Enable/Disable fixed quota of units for an account group.
8.  8\.

    Slider to configure a value for Usage Selector field
9.  9\.

    **Usage Selector**: Amount of units allocated to an account group.
10. 10\.

    Two options are available to configure **Usage Selector** value as below:

    * **Units**: Maximum number of units an account group can use per month.
    * **% of Plan:** Maximum proportion of organization's total units an account group can use per month.

Once you have finished configuring quotas, click **Save Changes** for the changes to take effect.

**Use case #1: I don't want a single account group consuming all my units unexpectedly.**

Configure quota settings for all your account groups. This way none of your account groups will be able to consume all available units, preventing (unintended) increased unit usage in one account group from adversely affecting your other account groups.

**Use case #2: My users are located all over the world. I want to allocate units to users based on regions.**

Create one account group per region. Then configure unit quotas for each region.

**Use case #3: I want to keep my operations team uncapped while limiting units for all other account groups.**

If you have enabled quotas for all your account groups, you can always disable unit quota allocation for a particular account group while leaving other account groups capped.

**Use case #4: I don't know how many units my new account groups will consume, but I don't want them to consume all available units.**

Quotas allocated to your account groups can add up to more than 100% of available units. Configure your new account group(s) with quota allocations below 100% for each individual account group. This enables an early warning about individual account group consuming more units than expected while not immediately affecting your other account groups.

**Use case #5: I've set up account group quotas, the setup is working as expected. How can I make sure my quotas configuration is unchanged?**

Every ThousandEyes user in your account with the _Can assign and edit quota_ permission will be able to adjust quotas. You will need to remove this permission (only available to Organization Admins by default) from all users unauthorized to perform quota allocation changes. You will need to communicate your requirement to other ThousandEyes administrators in your organization. If unexpected changes do happen, you can always inspect the Activity Log for further details.

When the user has at least one of the _View own activity log_, _View activity log for all users in account group_, or _View user activity in all account groups_ permissions, the

[Activity Log](https://app.thousandeyes.com/settings/account/?section=activityLog)

is available showing events that have happened in your ThousandEyes account and is now visible from **Account Settings > Activity Log**:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-dec547d4c0e5a42aba5497a51801b0c42b801b2a%2Fproduct-documentation\_user-management\_working-with-account-settings-17.png?alt=media)

Security & Authentication, SSO setup and Organization Default Time Zone Settings are found under **Account Settings > Organization Settings**:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-14f4e0898d18a78de05084d338f6fff358c8fa1c%2Fproduct-documentation\_user-management\_working-with-account-settings-18.png?alt=media)

#### Security & Authentication Tab <a href="#security-and-authentication-tab" id="security-and-authentication-tab"></a>

The **Security & Authentication** tab provides configuration of the following aspects of your ThousandEyes account:

*   SCIM Settings - To complement the SSO, SCIM-based automatic user provisioning is supported. For further information, see

    [ThousandEyes Support for SCIM](broken-reference)

    .

    ![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-c8d1962ebd58d605722b1f73ea8c1ae58c8043fc%2Fproduct-documentation\_user-management\_working-with-account-settings-19.png?alt=media)
*   Single Sign-On Settings - Including SCIM-based automatic user provisioning.

    ![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-376e2b1f630f1ed03b39dd65da3965cfcb230b71%2Fproduct-documentation\_user-management\_working-with-account-settings-20.png?alt=media)
*   Password Expiration - Policy configuration for users who are allowed to use interactive login.

    ![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-d9695e0c66bbd1ecc7525e2de6a01c1ad32abe48%2Fproduct-documentation\_user-management\_working-with-account-settings-21.png?alt=media)

There is a series of articles available in our documentation describing

[SAML](https://en.wikipedia.org/wiki/Security\_Assertion\_Markup\_Language)

\-based Single Sign-On (SSO) configuration settings. Start with

[How to Configure Single Sign-On: Metadata](<../../.gitbook/assets/how to configure single sign on sso metadata>)

, which contains further links to identity provider-specific SSO setup guides, or use the search feature at the top of this page to find the SSO setup guide for your identity provider (IdP).

To complement the SSO, SCIM-based automatic user provisioning is supported as well. Consult the

[ThousandEyes Support for SCIM](broken-reference)

article for further information.

The **Advanced Settings** tab provides the ability to change the Organization Default Time Zone settings.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-33c2b696aaa3e3c4aedf3d43ae32139ee44c1012%2Fproduct-documentation\_user-management\_working-with-account-settings-22.png?alt=media)

Organization Default Time Zones can be set for two feature groups. Each dropdown groups timezone settings by European, North America, Asia Pacific as well as Global. In the Global grouping, you have the option to set Coordinated Universal Time (UTC)

* Web UI Timezone - In addition to being able to set to UTC, the option to set the timezone to the User’s System’s time is available here.
* Notification & Snapshots Timezone can also be set independently.

The following resources contain further information related to ThousandEyes account management:
