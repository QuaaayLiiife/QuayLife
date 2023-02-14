# Release Notes: February 2021

#### Export Transaction Tests with the ThousandEyes Recorder <a href="#export-transaction-tests-with-the-thousandeyes-recorder" id="export-transaction-tests-with-the-thousandeyes-recorder"></a>

The ThousandEyes Recorder now supports exporting transaction tests and synchronizing credentials to the ThousandEyes platform. For more information, see

[ThousandEyes Recorder](https://docs.thousandeyes.com/product-documentation/tests/thousandeyes-recorder)

.

#### GlobalProtect VPN Support <a href="#globalprotect-vpn-support" id="globalprotect-vpn-support"></a>

Endpoint Agent VPN support for Palo Alto's GlobalProtect VPN is now available to all customers. For more information, see

[Endpoint Agent VPN Support](https://docs.thousandeyes.com/product-documentation/endpoint-agent/endpoint-agent-vpn-support)

.

* An issue was found where cleared alerts were still showing in the alert list, despite the error condition no longer being met. This was caused by the addition of several BGP monitors and the associated missing data collection of these monitors, and has now been resolved.
* An issue was found where the ability to add a custom webhook payload was visible for non-supported alert types. This functionality is now only visible within the supported Cloud and Enterprise Agent alert webhooks.
* An issue was found where a timeseries widget showed no data when it was included in a downloaded report PDF. This has been fixed.

#### Incorrect IP Address in Infrastructure Changes Documentation <a href="#incorrect-ip-address-in-infrastructure-changes-documentation" id="incorrect-ip-address-in-infrastructure-changes-documentation"></a>

A typo was found in the

[ThousandEyes Infrastructure Changes](https://docs.thousandeyes.com/product-documentation/enterprise-agents/thousandeyes-infrastructure-changes)

list of IP addresses to use in allowing connections to **api.thousandeyes.com**. The document has now been updated to reflect the correct IP address (13.248.200.34).

#### Endpoint Agent Settings Redesign <a href="#endpoint-agent-settings-redesign" id="endpoint-agent-settings-redesign"></a>

The **Agent Settings**, **Test Settings**, and **Agent Labels** sections of the ThousandEyes application for Endpoint Agents have undergone a substantial redesign. The following sections outline the major changes that have been made.

* Agent specific settings are now displayed in a modal, rather than inline:
  * Added a list of labels applied to the agent.
  * Added a timeline of the number of tests allocated to the agent on a **Time Series** graph.
  * Added a list of all scheduled tests associated with the agent.
  * Hid the Agent's details to streamline the UI.
* Users can now add filters for any of the device attributes (including username, or users who are members of a label etc).
* Added a **Last Modified** column to the table.
* Agent usernames are now displayed beneath the agent name.
* Agent labels have a new, condensed, icon. Hovering over the icon will display a list of the labels.
* Individual test settings are now opened in a modal, rather than in-line.
* The following new columns have been added to the table:
  * **Last Modified**: Last time this test was edited.
  * **Assigned Agents (24h)**: The number of agents assigned to the test in the last 24 hours.
* The enabled/disabled option is now a switch.
* Tests can now be assigned to **All Agents**, one or more labels, or one or more specific agents. Additional filters have been added to support this feature:
  * You can now filter by **Assignment Type**, **Agent Label**, and by **Agent**.
* Updated the **Time Series** graph that shows the number of agents assigned and running the test.
* Added a list of all agents assigned and running the test.
* The **Show/Hide Details** option now opens/closes an additional panel that includes the **Last Modified**, **Labels** and **Views Enabled for this Test** information.
* The **Add New Label** form is now a side panel, rather than a floating modal.
* Agent labels are now displayed as tags rather than circles.
* The **24 hour** time series now includes:
  * All agents matching the label's definition.
  * The agents that are available and also have not exceeded the number of tests running.

#### Endpoint Agent Data Support <a href="#endpoint-agent-data-support" id="endpoint-agent-data-support"></a>

From February 23 2021, the Endpoint data API will support 30 days of retention. If you require more than 30 days, our Reports and Dashboards have a data retention of 90 days. For more information, see the

[Reports](https://docs.thousandeyes.com/product-documentation/reports/working-with-reports)

and

[Dashboards](https://docs.thousandeyes.com/product-documentation/thousandeyes-basics/working-with-the-dashboard)

documentation.

New Cloud Agents have been added to the following locations:

* Quebec City, Canada (IPv6)
* Cape Town, South Africa (IPv6)
* Previously, a 404 error was presented when visiting a snapshot link while it was still being generated. This has now been updated to a progress indicator so that users are aware that the snapshot is still being generated.
* In some circumstances, double counting of Endpoint Agents occurred when an Endpoint Agent was transferred between users or account groups. The calculation has been updated to reduce the chance of overage notifications when the effective number of agents is still below the organization's subscription amount.
* An issue was found where the scale of the color grid widget was not resetting to **auto** after clearing the field of any values. This has been resolved.
* In rare cases, the CSV download option was not working on a subset of select reports. This has been fixed.
* An issue was found where the ability to show overall mean on a time series widget was not selectable during configuration and only selectable after a widget was saved. This has been corrected.
* An issue was found with the timeline where the y-axis was not showing the correct scale when updating the selected metric. This has been fixed.
* An issue was found where multiple IP addresses appeared when specifying a static IPv4 address. This has been resolved.
* An issue was found where agent updates would fail if NTLM/Kerberos authenticated proxies were being used. This has been fixed.
