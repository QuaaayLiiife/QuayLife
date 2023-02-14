# Alert Rule Severity

When you create an alert rule, you must set a _severity_ for it. When the rule is triggered, the severity level of the resulting alert is displayed both in the ThousandEyes UI and in any notifications that you have configured, such as email.

Alert severity is a **static property**. That is, once an alert has been triggered, its severity level cannot be raised or lowered. If the conditions that triggered the alert (such as the number of locations impacted) change, the alert's severity does not change.

An alert rule can have one of the following severity levels:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-66790eb61ab937af3ca9adb0a8a98e0a9d74d78d%2Falert-severity-1.png?alt=media)

To set the severity level for a new alert rule, use the **Severity** field in the **Add New Alert Rule** dialog:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-15a04e7f62909e9806eeda6d4853a90effc61a43%2Falert-severity-2.png?alt=media)

By default, alert rules are configured with the severity **Info**. If you have existing alert rules that predate this feature, they will be assigned the default **Info** severity. You can change this default to the severity level that suits your organization's needs.

### Changing an Alert Rule's Severity <a href="#changing-an-alert-rules-severity" id="changing-an-alert-rules-severity"></a>

If you change the severity of an alert rule that has current triggered alerts, those alerts maintain their original severity level. The alerts listed in **Alerts > Alert List > Active Alerts** and **Alerts > Alert List > Alert History** maintain severity that was assigned to them when they were triggered. After you change the severity of an alert rule, future alerts will have the new severity level.
