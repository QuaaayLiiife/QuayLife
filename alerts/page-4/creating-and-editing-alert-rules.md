# Creating and Editing Alert Rules

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-e12f66f21f93d4f65b5d8f04fec5c8f2f0dc1ee0%2Fproduct-documentation\_alerts\_creating-and-editing-alert-rules-1.png?alt=media)

From the tabs at the top of the page, select the desired alert source:

* Cloud and Enterprise Agents

Then click **Add New Alert Rule**. The **Add New Alert Rule** panel appears, displaying the **Settings** tab.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-a487b30d1962c6f3b0ffe72e21257c9f70110e80%2Falerts\_new-alert-rule.png?alt=media)

* **Alert Type**: Select the test layer and test type for this alert rule.
* **Rule Name**: Specify a name for the alert rule.
* **Compatible Test Types**: As you select the test layer in the **Alert Type** field, this area displays the test types to which this alert rule can be assigned.

Use the **Settings** tab to configure the conditions that must be met to trigger this alert rule, and to assign the alert rule to tests and agents. The fields on this tab vary depending on the source of the data; the image above displays the options for **Cloud and Enterprise Agents** tab.

* **Tests**: A drop-down menu listing the all the tests set up in your account group. Select one or more tests to assign them to this alert rule.
* **Agents**: Select the agents to which you will assign this alert rule. The options are:
  * **All agents**: All agents will be assigned this alert rule.
  * **All agents except**: All agents will be assigned this alert rule except for the ones selected.
  * **Specific agents**: Only the selected agents will receive this alert rule.
* **Alert Conditions**: The alert conditions that must be met in order to trigger this alert rule. The available alert conditions vary depending on the test type you have specified.

Use the **Notifications** tab to configure the methods by which users are notified when an alert rule is triggered.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-9345f506e4431243010cfd7fb69b448f4dfc1b82%2Fproduct-documentation\_alerts\_creating-and-editing-alert-rules-3.png?alt=media)

1.  1\.

    **Send emails to:** email addresses that receive the alert notification.
2.  2\.

    **Edit emails:** create or edit an email address which can then be added to the **Send emails to** field.
3.  3\.

    **Send an email when alert clears:** if checked, an email is sent when the alert rule is no longer triggered.
4.  4\.

    **Add message:** an optional field for text that will be sent in the body of the alert email. Note that greater than ">" and less than "<" characters are not allowed in this field.
5.  5\.

    **Webhooks:** Webhooks-enabled web services that receive the alert notification.
6.  6\.

    **Edit webhooks:** create or edit

    [webhooks](broken-reference)

    that can then be added to the Webhooks **Send Notifications to** field.
7.  7\.

    **Integrations:** integrations that should receive the alert notification.
8.  8\.

    **Edit Integrations:** create or edit an integration that can then be added to the Integrations **Send Notifications to** field. Currently, ThousandEyes offers integrations for

    [AppDynamics](broken-reference)

    ,

    [PagerDuty](broken-reference)

    ,

    [Slack](broken-reference)

    and

    [ServiceNow](broken-reference)

    .
