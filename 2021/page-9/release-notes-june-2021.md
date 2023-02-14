# Release Notes: June 2021

#### Changes to the te-browserbot Package's Dependencies <a href="#changes-to-the-te-browserbot-packages-dependencies" id="changes-to-the-te-browserbot-packages-dependencies"></a>

In the coming weeks, ThousandEyes will add

[**te-podman**](https://podman.io/)

as a dependency of the `te-browserbot` package. Podman version 3.1.0 or greater will be required for page load and transaction tests.

If your Enterprise Agent has an existing compatible version of Podman, Browserbot will configure it to execute tests. Otherwise, Podman version 3.1.0 will be downloaded from the ThousandEyes public repositories (or a configured repository with a compatible version of Podman).

New Cloud Agents have been added to the following locations:

* Eindhoven, Netherlands (KPN) (IPv4 and IPv6)
* Kansas City, MO, USA (IPv6)

#### Extended Validation Certificate for Endpoint Agents <a href="#extended-validation-certificate-for-endpoint-agents" id="extended-validation-certificate-for-endpoint-agents"></a>

The Endpoint Agent is now signed with an Extended Validation (EV) certificate. This smooths the installation process by providing immediate reputation with Microsoft SmartScreen in the event that the certificate used to sign the Endpoint Agent installer package is changed (for example, after it expires or is revoked).

This is implemented in Endpoint Agent Client version 1.80.0.

#### Notification Integration Updates <a href="#notification-integration-updates" id="notification-integration-updates"></a>

Several improvements have been made to the alert integration notifications:

* The property name **ID** has been updated to **Alert ID**.
* The **Test Name** has been added to the notification.
* The **URL** or **Server** target has been added to the notification.
* The **Scope** field has been changed to **Number of Agents**.
* Property names have been updated to title case rather than camel case (i.e. **Rule ID** instead of **ruleId**).
* The alert rule expression now appears in the **Alert Rule** field.
* The **Clear Date** value has been removed.
* The word **Triggered** has been added as part of the email subject line for triggered alerts.
* Previously, an alert with the **error matches** or **error does not match** criteria could trigger even if no errors were present. For example, if an alert condition was set that stated "Alert when: error does not match 401", an alert could trigger even if there were no errors, as a 401 error was also not present. We have updated the way we evaluate these two alert criteria to only trigger an alert when at least one actual error is present. If no errors are present, these two alert criteria will not trigger.
* An issue was found where **Metrics at Alert End** was showing as **N/A - Agent Removed from Test** when an Endpoint Agent was removed from a test, after the alert had triggered. The agent is now persisted in the the **Alert List** and **Alert History** page, even if the agent has been removed.
* An issue was found where updating an existing test with Cloud Agents did not immediately reflect the configuration change. This has been fixed.

#### Transaction Alert Metric Reporting Changes <a href="#transaction-alert-metric-reporting-changes" id="transaction-alert-metric-reporting-changes"></a>

As part of our migration to our new alerter infrastructure, we have made a change to the way transaction metrics are reported in our **Alert List** page. We have moved from string text to key value pairs for both **Metrics at Alert Start** and **Metrics at Alert End**. This will be rolled out to 100% of customers over the coming weeks.

#### Chrome Browser Extension Redesign <a href="#chrome-browser-extension-redesign" id="chrome-browser-extension-redesign"></a>

The Google Chrome browser extension has been redesigned so that configuration changes to the set of monitored domains are now received by the extension faster. Previously, these changes were only received when the agent transitioned from an actively recording page or domain to one that was not recorded (or vice versa). Now, configuration changes are received and applied as soon as they are delivered to the agent.

This improvement also fixes inconsistencies in the data display and UI extension status for Windows agents using Microsoft Edge and Internet Explorer.

The **Agent Settings** page now contains an icon to indicate whether an Endpoint Agent is enabled for TCP tests.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-2d93f4a31591e683abe696918468bba0bb752e39%2Fwhats-new\_changelog\_2021-06-28\_01.png?alt=media)

All Mac agents, and all Windows agents with the **npcap** library installed, support TCP, provided the agent is up to date.

* Previously, when an agent received a network change event, it cleared its scheduled test assignments, checked in with the ThousandEyes backend, and waited for new scheduled test assignments. For agents that were unable to connect via websockets, the agent would wait for one minute before polling the backend for its assignments. During this window, the agent would not run scheduled tests, occasionally resulting in short gaps in test data. This window has been decreased to thirty seconds in Endpoint Agent client version **1.81.0** to reduce the chance of this issue occurring.
* Previously, network changes for Zscaler VPNs would cause the list of scheduled tests to be refreshed immediately. However, the network would cycle again before the tests had been run, causing tests to fail. This has been resolved in Endpoint Agent client version **1.81.0** by ignoring rapid changes for up to a five minute period, and the Endpoint Agent is now able to continue testing when running a Zscaler VPN that is cycling frequently between a range of configured IP addresses.
* An issue was found where the list of domains that should bypass the Zscaler tunnel, when used in "tunnel with local proxy" mode, was incorrect, resulting in the path visualization not clearly showing that traffic was bypassing the Zscaler network, as it should. This has been corrected in Endpoint Agent client version **1.81.0**, and the list of domains is now obtained from both the "App profile PAC" and the "Forwarding PAC" files.

New Cloud Agents have been added to the following locations:

* Baltimore, Maryland, USA (IPv6)
* Columbus, Ohio, USA (IPv6)
* Previously, widgets in reports and dashboards would occasionally show the incorrect amount of tests based on the filters selected. We've updated the functionality to only show the number of tests that are expressed in the data point. **Note:** If multiple filters are selected that have overlapping tests, or in instances where a test is deleted after the widget is created, the number shown on the widget may be less than the number of tests selected in an individual filter.
* Added an error message when a user tries to save a dashboard with **<** or **>** as characters in the name to provide more context as to why the dashboard isn't saving (these characters prevent saving due to information security purposes).
* An issue was found where the list of providers for the **Default Outage Alert Rule** was not being correctly updated. This could prevent the rule from triggering, and has been resolved.
* An issue was found where the selected Endpoint Agent "grouping" option in the UI did not persist after navigating somewhere else on the timeline, resulting in the default values overriding the selected ones. This has been fixed.
* An issue was found where customers were unable to access wireless metrics saved events that were older than 30 days. This bug only affected saved events (not public snapshots), and has been resolved.
* An issue was found that caused more informative Endpoint Agent error messages (for example, "The internet connection has been lost") to be displayed as "Other" when a page load fails. This has been corrected, and the full error messages will now be displayed.
* An issue was found where the Y axis for some report and dashboard widgets had a truncated name. This has been fixed.
* An issue was found where the error count metrics in reports and dashboards were incorrectly showing as "No Data", rather than the correct value of "0 Errors". This has been fixed.
* An issue was found where some alerts were triggering incorrectly during customer defined alert suppression windows. This has been resolved.
* An issue was found where alerts were incorrectly firing due to stale test prefix metadata, which was leading to alerts firing on deleted IP prefixes. This has been fixed.
* An issue was found where some report and dashboard widgets were unable to filter by target agent. This has been resolved.
* An issue was found where certain location alerts were presented in the UI as part of the trigger condition that violated the alert condition before the global alert actually triggered. This issue has been fixed. **Note:** This fix changes the behavior of other potential alert trigger instances. As of this release, the only location alerts that will be displayed in the UI at a global alert trigger will be the location alerts active at the time of trigger. This could lead to scenarios where a flapping agent was involved in the evaluation criteria of an alert being fired, but has since cleared before the global alert fires. However, this will only occur if the alert conditions have multiple agents that need to fire multiple times in a row.
