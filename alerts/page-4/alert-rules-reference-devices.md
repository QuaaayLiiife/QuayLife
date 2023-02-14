# Alert Rules Reference: Devices

This section assumes that you have gone through the

[device discovery process](https://docs.thousandeyes.com/product-documentation/device-layer/discovering-device-layer-devices)

, and are using the ThousandEyes platform to monitor one or more devices.

Once ThousandEyes is monitoring devices, you may want to configure alerts based on device-layer data.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-92d00b5f9e163bd43b14cad3b23741ead9e867b6%2Falerts\_new-alert-rule-devices.png?alt=media)

The sections below describe the fields on **Add New Alert Rule** screen.

* **Alert Type**: Select **Device** or **Interface**.
* **Rule Name**: Give the alert rule a human-readable name that makes sense for your implementation of ThousandEyes.
* **Devices**: Select the devices that this alert rule should apply to. After you click the dropdown, you can search for devices by name.
* **Alert Conditions**: Set the alert conditions that must be met in order to trigger this alert rule. The available alert conditions vary depending on the alert type you have specified.

On this tab, you configure which people or services will receive notifications when the alert rule is triggered.

*
  * **Send emails to**: Click the dropdown, then use the search box to find and select the email addresses that will receive alert notifications for this alert rule.
  * **Edit external emails**: \[Optional] Click to add new email addresses, or remove listed email addresses. When you add a new email address here, it is included in the list in the **Email > Send emails to** field.
  * **Send an email when the alert clears**: \[Optional] Select this checkbox if you want the recipient to be notified when the alert is resolved.
  * **Add message**: \[Optional] You can write a custom message to be included in the email body of the alert notification. Note that the greater-than (**>**) and less-than (**<**) characters are not allowed in this field.
*
  * **Send notifications to**: Click the dropdown, then use the search box to find and select the webhook-enabled services that will receive alert notifications for this alert rule.
  * **Edit webhooks**: \[Optional] Click to add a new webhook, or to edit or delete existing webhooks. When you add a new webhook here, it is included in the list in the **Webhooks > Send notifications to** field.
*
  * **Send notifications to**: Click the dropdown, then use the search box to find and select the integration that will receive alert notifications for this alert rule.
  * **Edit integrations**: \[Optional] Click to add a new integration, or to edit or delete existing integrations. When you add a new integration here, it is included in the list in the **Integrations > Send notifications to** field.
