# Getting Started with Account Setup

This section helps you learn about configuring your account as an administrator, securing user access, and planning usage - as well as tracking account activities.

Every ThousandEyes user belongs to an _organization_, which represents the customer's billing entity. Any licenses you purchase apply to your entire organization and are shared by account groups. An _account group_ is an entity internal to your organization that divides it into functional groups. For detailed information about account groups, see

[What Is an Account Group](https://docs.thousandeyes.com/product-documentation/user-management/account-groups/what-is-an-account-group)

.

Account groups divide users, tests, agents, dashboards, alert rules, and many other elements of the ThousandEyes platform. Account groups are a way to create an independent instance within an organization, for security or functional purposes.

For example, Organization A can be divided into account groups for IT, NetOps, and DevOps. Each department uses the ThousandEyes platform within their own account group. While billing is shared, the users in one account group cannot access other account groups' data (unless it is specifically shared across account groups).

A user can belong to multiple account groups and can switch between them without re-authentication. In the example below, "Super User" has access to three account groups in the "ThousandEyes Internal" organization, and is currently logged into the “Engineering” account group:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-9554f2ba377984b690c4cc24e650377271fb2abd%2F1.png?alt=media)

a user named Super User is a member of three account groups

It's best to plan in advance how you will use account groups based on your corporate structure. There is no limit on the number of account groups you can add.

To create account groups in the ThousandEyes platform, go to **Account Settings > Users and Roles > Account Groups**.

When you add new users to the platform, you must assign each one to an account group and a _role_. The ThousandEyes platform provides a

[role-based access control (RBAC) model](https://docs.thousandeyes.com/product-documentation/user-management/rbac/role-based-access-control-explained)

, in which users' roles determine what they can do within the platform. The administrator can opt for the default, built-in roles, or can create custom roles.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-655b66b889ebccbcada07d805d35114ebed1913c%2F2.png?alt=media)

assigning a user to a role

The built-in roles are _Organization Admin_, _Account Admin_, and _Regular User_:

* The Organization Admin role has full permissions including managing usage, users, and account groups. We suggest reserving this role for a limited number of administrators who are fully trained in ThousandEyes account setup.
* The Regular User role is for read-only-access users, and carries no administrative permissions.
* Users who need an access level between Organization Admin and Regular User can hold the Account Admin role.

Alternatively, you can build a custom role by selecting the desired

[permissions sets](https://docs.thousandeyes.com/product-documentation/user-management/rbac/role-based-access-control-explained#roles-and-permissions-table)

.

To create a custom role, you must have the **Edit roles** permission.

When you create a new role, you can use it in any account group within the organization. While users with the Organization Admin role automatically have access to all account groups, non-Organization Admin users must be assigned a role for each account group they belong to.

To create a custom role, go to **Account Settings > Users and Roles > Roles**. Keep in mind the following guidelines:

*   Reserve management permissions for administrators only.

    ![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-ca02d931718092dee75883c1caa542ac3c67b14b%2F3.png?alt=media)

    list of management permissions
*   Make sure every user can view

    [snapshots](https://docs.thousandeyes.com/product-documentation/dashboards/dashboard-shares-snapshots)

    for collaboration.

    ![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-93bc547e3270b9d1caf33b54926bf388fb45cbcb%2F4.png?alt=media)

    permissions for snapshots
*   If you plan to use

    [SSO](https://docs.thousandeyes.com/product-documentation/user-management/sso)

    , the **Login via Single Sign-On** permission is required.

    ![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-e609da406c6e409f60c9364d91a00013354c28f3%2F5.png?alt=media)
*

    ![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-1cb14fbbb0cff5bc558eb48ad5195aaf4b94556c%2F6.png?alt=media)

    permissions for credentials-repo access
*   If you plan to create or use

    [integrations](https://docs.thousandeyes.com/product-documentation/integration-guides)

    and

    [webhooks](https://docs.thousandeyes.com/product-documentation/alerts/integrations/webhooks)

    , the accounts for those services must have API access.

    ![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-1b8cfc434915f81581db3e88613c2ea9a97651c3%2F7.png?alt=media)

    permissions for API access

Reducing login to one set of credentials improves enterprise security. ThousandEyes supports SAML 2.0-based single sign-on (SSO) so you can follow your organization's security policies. Before you invest time in manually provisioning new users, we suggest that you check whether your directory service supports SAML 2.0 and SCIM provisioning.

In addition, with any identity provider (IdP) that supports System for Cross-domain Identity Management (SCIM) provisioning, user accounts can be auto-provisioned via your IdP. Manually provisioning and deprovisioning user accounts for every SaaS application costs your IT team enormous time and effort. A common security issue is terminated users who can continue to use a SaaS application using the same password. You can avoid these issues by using SCIM auto-deprovisioning users' accounts when their access is removed from the IdP. In addition, ThousandEyes will automatically benefit from enhanced security, like multifactor authentication (MFA) that the IdP provides.

We highly recommend you consider enabling SSO before onboarding any users. To make setup easier, we provide runbooks for the major IdPs:

If your IdP is not listed above, see

[this guide](https://docs.thousandeyes.com/product-documentation/user-management/sso/how-to-configure-single-sign-on-with-metadata)

for a general configuration that works for any IdP. If your system supports loading XML metadata, we recommend using ThousandEyes metadata, which can be downloaded from https://app.thousandeyes.com/saml-metadata for your service provider configuration. For IdP configuration, we support static configuration, metadata import, as well as dynamic configuration that parses the IdP’s public URL.

To start setting up SSO, go to **Account Settings > Organization Settings > Security and Authentication**.

Before you save your SSO configuration, use the **Run Single Sign-On Test** button to test it. Make sure the test passes before you save the configuration; otherwise, it will impact existing users' ability to log in.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-69a59d8f44d7f950123b37033bf62f4dab799421%2F8.png?alt=media)

screen for setting up SSO

ThousandEyes customers commit to an annual contract that can include the following forms of subscription:

* Units for Cloud and Enterprise Agent tests
* Internet Insights packages

You can view your subscriptions at **Account Settings > Usage and Billing**.

The **Plan Usage** section shows your monthly subscription status, including:

* Billing period (the date when monthly usage is reset)
* Usage included in your plan
* Units and licenses used to date
* For units, the projected usage by the end of the billing cycle

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-b40f3edbb9eb0553edc1beb4560a7aeb7bb084d3%2F9.png?alt=media)

plan usage tab showing units used and projected

In the above customer’s example, their billing cycle begins on the 14th of every month, and their usage is not exceeding the limit at this point, especially for units. As unused units do not roll over from month to month, we would suggest that this customer should add tests to consume more units.

Units are calculated based on the test's type, interval, and timeout, and on the number and type of ThousandEyes agents running the test. As a SaaS solution, ThousandEyes provides a usage-based billing model, which means that every running test uses units.

You can break usage down by account group, test type, or individual test. The **Used** versus **Projected** labels can provide easy guidance about which account group, test type, or individual test consumes the most units, and whether your current usage will exceed the set limit by the end of the billing cycle.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-b697cd9c8501449e07e9b46ad6d5997627373d34%2F10.png?alt=media)

As ThousandEyes admins, you aim to keep your organization's usage below the monthly allowance. ThousandEyes offers three ways to help you prevent overages:

*   Use the calculator to estimate unit consumption. The

    [ThousandEyes calculator](https://app.thousandeyes.com/calculator/)

    automatically pulls your organization's current test settings and calculates the monthly total. It allows you to overwrite tests' interval, timeout, number of agents, and the number of tests as you calculate usage.

    To avoid unexpected unit consumption, we highly recommend you run the calculator when you change existing test settings or create new tests.
*   Set a usage quota on account groups. For every account group, you can set a usage quota to guard against unwanted overages. Quotas can be set by percent of your total plan or by number of units.

    To create a usage quota, go to **Account Settings > Usage and Billing > Quotas**.

    ![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-11acba59d4b261fe4f8f6b71e122fa8655a8be5d%2F12.png?alt=media)

    screen for creating usage quotas

    When the projected units in the current billing cycle exceeds the quota, users see a warning message and are prevented from saving test configurations that consume more units. For times when you need to run more tests, we recommend you expand your unit capacity.

To remain within your contracted usage, we recommend the following:

* Make sure your test's intervals, agents, and timeouts match your business needs.
* Don’t add use cases without also adding adding capacity.
* Use the calculator before making changes.

### Auditing Account Activity <a href="#auditing-account-activity" id="auditing-account-activity"></a>

ThousandEyes offers a live platform shared by multiple concurrent users. There is no version-control method that allows administrators to revert a user's configuration changes to a previous point in time. Every save action is final, so should be made with due consideration.

Instead, we offer the

[activity log](https://docs.thousandeyes.com/product-documentation/user-management/user-activity/working-with-the-activity-log)

that exposes UI actions made by all users. For each action, the log provides details of the account group, user, component, and a description. You can download the logs for up to two years' activity, for audit purposes.

In addition to its uses for transaction details, you can use the activity log to measure the adoption of the ThousandEyes platform in your organization. For example, the activity log shows which users you have added to the platform have then activated their accounts. To view the activity log, go to **Account Settings > Activity Log**. For detailed information, see

[Working with the Activity Log](https://docs.thousandeyes.com/product-documentation/user-management/user-activity/working-with-the-activity-log)

.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-24be67e72d9fcc1ba9787b96e696f93826d62e8f%2F13.png?alt=media)
