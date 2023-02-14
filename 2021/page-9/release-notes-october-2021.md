# Release Notes: October 2021

#### Agent Alert Notifications Update <a href="#agent-alert-notifications-update" id="agent-alert-notifications-update"></a>

We have made several updates to our agent alert notifications in order to match our existing notification patterns for other alert types.

Agent alert email notifications have been updated to match our other notification types. They now include:

Slack notifications will now include:

* **Agent Alert triggered for agent**

PagerDuty notifications will now include:

Webhook notification will now include:

The following changes have also been made:

* **AGENT\_ALERT\_NOTIFICATION\_TRIGGER** has been changed to **ALERT\_NOTIFICATION\_TRIGGER**.
* **AGENT\_ALERT\_NOTIFICATION\_CLEAR** has been changed to **ALERT\_NOTIFICATION\_CLEAR**.

#### Alerting Platform Updates <a href="#alerting-platform-updates" id="alerting-platform-updates"></a>

Over the next several weeks, our alerting platform will be updated to change the way we treat Enterprise Agents that are not reporting data.

Previously, a triggered alert would not clear, even if all violating/triggering agents had cleared the condition, if **m** or more agents were not reporting data (where **m** = the number of agents required to trigger an alert). For example, if an alert rule was set up to alert if two agents were violating a condition, the triggered alert would not clear if two or more agents did not report data, even if the previously violating agents were now cleared.

With the coming change, Enterprise Agents that do not send data to our system will now be treated as **not** violating the alert condition. Triggered alerts will now clear when violating/triggering agents have cleared the condition, even if **m** or more agents are not reporting data (where **m** = the number of agents required to trigger an alert). For example, if an alert rule was set up to alert if two agents are violating a condition, the alert will clear if less than two agents are violating the condition, even if two or more agents are not reporting data.

#### Cisco Nexus Switch Support for Enterprise Agents <a href="#cisco-nexus-switch-support-for-enterprise-agents" id="cisco-nexus-switch-support-for-enterprise-agents"></a>

ThousandEyes now supports installing Enterprise Agents on Cisco Nexus 9000 series switches.

For more information on the system requirements, see the

[Support Matrix](https://docs.thousandeyes.com/product-documentation/global-vantage-points/enterprise-agents/installing/cisco-devices#support-matrix)

.

#### Snapshot Scaling and Performance Improvements <a href="#snapshot-scaling-and-performance-improvements" id="snapshot-scaling-and-performance-improvements"></a>

As part of our performance and scaling improvements, Endpoint Agent snapshot data will be migrated to a new data platform. Whilst our migration project is in progress, snapshots that include **Local Network** data will be limited to a maximum of 12 hour windows.

In the Endpoint Agents **Instant Test** view, the current view in the left hand navigation bar is now described as **Instant Tests** rather than as **Scheduled Tests**. This is now also the case when saving snapshots of instant tests.

#### Deprecated and Removed Features <a href="#deprecated-and-removed-features" id="deprecated-and-removed-features"></a>

The **Organization** filter in reports and dashboards widgets has been deprecated. This change only affects widgets that are configured with an **Endpoint Agents > Browser Sessions** metric that also filter by organizations. The filter will automatically be migrated to a **Network** filter in all affected widgets. No action is required.

* Previously, some macOS edge cases could result in the Endpoint Agent name not reflecting the correct hostname of the device. We have improved the way the Endpoint Agent obtains the hostname to eliminate these edge cases.
* An issue was found where Endpoint Agent instant tests were breaking for accounts with long account names. This was caused by base64 encoding by default adding a new line character for names longer than 80 characters, and has been resolved.
* The Endpoint Agent now shows traffic that has been configured in Zscaler Client Connect to bypass the VPN tunnel as going directly to the Internet in the path visualisation.
* The Endpoint Agent now shows overlay network nodes for network tests using ICMP, when ZScaler Internet Access is used with tunnel version 2.0.

#### Path Trace Alert Display Change <a href="#path-trace-alert-display-change" id="path-trace-alert-display-change"></a>

As a result of migrating path trace metrics to our new alerter architecture, the display of alert data has changed:

*   When you set up an alert rule on any indexed hop condition from the destination direction, the hop index now displays the alert value from the source, rather than the destination.

    Old alerter: Hop #1 from destination: (DSCP: Best Effort (DSCP 0))

    New alerter: Path Trace #1: (Hop #18: (DSCP: Best Effort (DSCP 0)))
*   All alerting conditions with "No Hops" or "MPLS Label is empty" expressions will display the triggering condition as "No Hops: Path Violates Alerting Condition" instead of the specific rule expression.

    Old alerter: Path Trace #1 - No Hop meets: rDNS in \["thousandeyes.com"]

    New alerter: Path Trace #1: (No Hops: Path Violates Alerting Condition)

#### Notifications for Device Data Alerts and Device Status Alerts <a href="#notifications-for-device-data-alerts-and-device-status-alerts" id="notifications-for-device-data-alerts-and-device-status-alerts"></a>

We have moved our device alert notifications to our standard notifier platform. This has resulted in the changes described below.

We recommend that you review the changes to see if any of your configured notifications are affected.

**Device Data Alert Notifications**

*
  * The webhook payload now includes both **alert** and **deviceAlert** as JSON keys. Moving forward, you should migrate to using just the **alert** JSON key, as the **deviceAlert** JSON key is now deprecated and will eventually be removed.
  * A permalink to the **Device Topology** page is now included in the webhook.
  * Date fields are timezone-converted dates instead of Epoch seconds timestamps.
*
  * **Device Name** is no longer in the title of the Slack message.
  * **Device Name** is added as a new field for the body of the Slack message.
*
  * The column header for interfaces is now **Interface** instead of **Interface name**.
*
  * Most custom detail field names are now in plain English rather than raw variable names.
  * **Alert Rule** and **Rule Expression** are now merged into one field instead of separate fields.
  * **Type**, **No. of Interfaces**, and **Permalink** have been added as new fields.
  * **Interface Name** has been removed from the incident title.

**Device Status Alert Notifications**

*
  * The webhook payload now includes both **alert** and **deviceAlert** as JSON keys. Moving forward, you should migrate to using just the **alert** JSON key, as the **deviceAlert** JSON key is now deprecated and will eventually be removed.
  * A permalink to the **Device Topology** page is now included.
  * Date fields are timezone-converted dates instead of Epoch seconds timestamps.
  * A **dateEnd** field has been added.
*
  * Rule expression is combined with rule name as the value for **Alert Rule**.
*
  * The original email format contained links to devices for which a particular notification rule was triggered. The new email now gives a summary of all the devices that were triggered, with details such as alert ID, rule, and start date.
  * The new email includes the summary header and adds headers and brief information for each device.
*
  * **Alert Rule** and **Rule Expression** are now merged into the **Alert Rule** field.
  * Alert type and permalink have been added as new fields.
  * Most custom detail field names are now in plain English rather than raw variable names
  * The header and summary in PagerDuty now only include the rule name.

#### New Webhook Timezone Variables <a href="#new-webhook-timezone-variables" id="new-webhook-timezone-variables"></a>

Two new variables have been added for ThousandEyes webhook payloads to replace the existing variables **dateStart** and **dateEnd**. Previously, the alert **dateStart** and **dateEnd** variables were based on the organization's timezone, but did not include a timezone identifier:

"dateStart": "2021-10-19 17:42:00",

The new variables, **dateStartZoned** and **dateEndZoned**, include the time zone associated with the time of the alert trigger, as well as the alert clear.

Example for UTC timezone:

"dateStartZoned": "2021-10-19 17:42:00 UTC",

"dateEndZoned": "2021-10-19 17:47:39 UTC",

The timezone is shown explicitly, based on your organization’s time zone setting. If your organization’s timezone is Eastern Daylight Time, the payload looks like this:

"dateStartZoned": "2021-10-19 15:20:00 EDT",

In order to preserve current integrations, the existing **dateStart** and **dateEnd** variables will be maintained. However, these variables will eventually be removed. We ask that every customer begin to use the new variables moving forward.

#### Deprecated and Removed Features <a href="#deprecated-and-removed-features-1" id="deprecated-and-removed-features-1"></a>

**Endpoint Agent Windows 7 Support**

Fixed a bug where instant tests were broken for long account names. This had been caused by base64 encoding, which by default was adding a newline character for names longer than 80 characters.
