# Release Notes: July 2022

#### Microsoft Azure Support for Enterprise Agents <a href="#microsoft-azure-support-for-enterprise-agents" id="microsoft-azure-support-for-enterprise-agents"></a>

#### Continuous Monitoring for One-Minute Interval Tests <a href="#continuous-monitoring-for-one-minute-interval-tests" id="continuous-monitoring-for-one-minute-interval-tests"></a>

Previously, the ThousandEyes platform sent 50 packets in a burst at the start of a one-minute interval network test. This resulted in ThousandEyes potentially missing intermittent blips that lasted a few seconds. These blips were sometimes caught by black-box tools, resulting in confusion for customers.

With this release, customers can configure ThousandEyes to send one packet per second over the full duration of a network test. Packet loss is calculated as an average over the minute, and jitter and latency calculations have also been updated to match the new capability. In addition, we've added a sparkline visualization to show exactly when a packet drop occurred during your test.

This feature is specific to network tests, and is currently only available to agent-to-server network tests with one-minute intervals.

To configure continuous monitoring:

1.  1\.

    Log into the ThousandEyes web application using a user with permission to modify tests.
2.  2\.

    Navigate to **Test Settings**.
3.  3\.

    Select the desired test, either by scrolling through the list or using the text search field.

    ![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-e2d4a4437e0a61a410f0a6f03acf5b52284c0152%2Fchangelog\_packet-spreading-1.png?alt=media)

    ​
4.  4\.

    Navigate to the **Advanced Settings** tab.
5.  5\.

    Select the **Perform network measurements in 1-second intervals** checkbox.

    ![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-df1b875c6a12fae43eec2b7e7b0ad8931064dd19%2Fchangelog\_packet-spreading-2.png?alt=media)

    ​

The screenshot below shows how the data looks with continuous monitoring enabled, using a test with packet loss:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-b7e51569c2dad256682be66fcf8a6063d7e55747%2Fchangelog\_packet-spreading-3.png?alt=media)

#### Auto-Detect Now in Open Beta for Endpoint Agents Using Automated Session Tests for Microsoft Teams <a href="#auto-detect-now-in-open-beta-for-endpoint-agents-using-automated-session-tests-for-microsoft-teams" id="auto-detect-now-in-open-beta-for-endpoint-agents-using-automated-session-tests-for-microsoft-teams"></a>

The auto-detect feature is now in open Beta for Endpoint Agent users, focused on Microsoft Teams.

Previously, when configuring automated session tests (ASTs), it has been difficult for customers to know what the best test configuration was to monitor a specific application. This was especially true if targeting an application that ran hundreds of nodes spread around the globe and that were accessed through different scenarios (for example, different locations, different network configurations, etc).

In order to make the configuration of ASTs easier, ThousandEyes has developed a new feature that will allow you to select an "auto-detect" protocol configuration that will automatically select the best configuration to monitor the selected application.

In order for the auto-detect configuration to work correctly, the TCP driver should be installed. This is because some configurations may rely on TCP.

When configuring an AST within the ThousandEyes dashboard, you will now see an **Auto-detect** option under protocol, which will automatically select the most reachable protocol for the selected application.

#### Enhanced Priorities for Endpoint Tests <a href="#enhanced-priorities-for-endpoint-tests" id="enhanced-priorities-for-endpoint-tests"></a>

Previously, the priority of a test to be executed on an Endpoint Agent followed a simple priority line. The 10-slot limit per agent first focused on tests where the agent was selected within the **Specific Agents** field. After that, the tests applied to a specific **Label** were selected. Finally, if there were still available slots for an agent, the tests that were configured for **All Agents** were executed.

In order to provide you more flexibility on the prioritization of the tests, you can give priority to tests, both in the creation of a test or directly in the **Tests Settings** dashboard. Prioritized tests will now be selected over non-prioritized tests, each of them internally following the previous simple priority line (i.e., Specific Agents > Labels > All Agents).

We have enhanced the definition of Endpoint Agent labels. In particular, you can now define whether a label _includes or does not include_ agents that match the following filters:

In addition, you can now use wildcards (i.e., \*) within the **SSID**, **Username** and **Hostname** fields in order to define the desired target (e.g., **Hostname** in "SF-\*").

New Cloud Agents have been added to the following locations:

* Durban, South Africa (IPv6)

A new Webex Cloud Agent has been added to the following location:

* We have changed our **Report Snapshot** email subject from `Report - 'Snapshot Name'` to `Snapshot - 'Snapshot Name'` in order to remain future-proof with upcoming changes to our reporting and dashboarding structure.
* You can now modify interface groups via the API, providing parity with the current solution in our product UI.
* Activity logs are now generated when Endpoint Agent tests are created using the API, in the same way that they are when tests are created in the UI.
* An issue was resolved where a link to fetch more data on some Endpoint API endpoints was provided even when no more data was available.
* An issue with our v6 Integrations API that was preventing users from using the **.json** format has been resolved. When a customer used **.json**, we were incorrectly sending back a 404 error. This has been corrected and you can use the **.json** format in our v6 Integrations API as expected.
* An issue that was preventing users from duplicating our built-in dashboards has been resolved.
* An issue that was preventing the update of the Endpoint Agent usage after deleting Endpoint Agents has been resolved. You will now see that as soon as an agent is deleted, the Endpoint Agent usage is reduced.
* An issue where users without the "Can add or modify tests to consume over 100% resources" permission were able to configure tests that increased the organisation's usage above the purchased subscription amount has been resolved.
* An issue was resolved where some Internet Insights customers did not have the default Application Outage alert rule, which should have been created automatically at provisioning. This has been corrected, and impacted customers will now begin receiving these alerts.
* An issue was resolved that was preventing Network Outage alerts from clearing in production. Alerts should now clear as expected.

#### Endpoint Agent Metrics for Dashboards and Reports <a href="#endpoint-agent-metrics-for-dashboards-and-reports" id="endpoint-agent-metrics-for-dashboards-and-reports"></a>

Our dashboards and reports now support additional metrics, filters, and group bys for Endpoint Agent browser sessions and scheduled tests.

#### New Agent Status Settings for the Endpoint Agent <a href="#new-agent-status-settings-for-the-endpoint-agent" id="new-agent-status-settings-for-the-endpoint-agent"></a>

Efficiently managing hundreds or thousands of Endpoint Agent licenses is not simple. In order to make the maintenance process easier, the Endpoint Agent now includes the new **Agent Status Settings**. This new feature provides you with a set of configuration options to automatically manage the status of Endpoint Agents. In particular, these options allow you to configure the number of days after which the agents can be automatically disabled, deleted, or re-enabled. After the initial configuration, the system will periodically evaluate the conditions defined on the agents' statuses and notify you with any change in the Activity Log.

* The usability of the agent selection within Endpoint Agent labels has been improved. In particular, a 'deleted' filter in the drop-down agent list has been added. You can use this filter to find all agents that have been deleted from the platform.
* An issue has been resolved where the Endpoint Agent label search function was not allowing for the correct search results.
* An issue in the ThousandEyes Enterprise Agent that occurred when the agent was configured with link local IPv6 addresses only and the target of a test was an IPv6 address has been corrected.
* An issue was found where the link to download the Endpoint Agent was not properly generating when the “Allow anyone with the link to download” option was enabled. This has been resolved.
* An issue was resolved in Internet Insights where, when switching from the Network Outage layer to Application Outages, the alerts swimlane was not updated. This would only occur when the "Affected Test" metric was selected and would result in Network Outage alerts appearing in the Application Outages alerts swimlane.
* Fixed an issue where alert suppression windows of shared tests were incorrectly being applied to multiple account groups, instead of the account group that created and assigned the alert suppression window. Moving forward, any alert suppression window applied to a shared test will only suppress alerts in the same account group as the alert suppression window.
* An issue was found that was preventing users from downloading a PDF or CSV of a report when accessing the download link through the notification icon in the header of the product. This has been resolved.
* An issue was resolved that was preventing users from creating a browser session alert rule with an underscore in the domain. Customers can now set alert rules for a specific visited site with a custom domain including an underscore.
* An issue was resolved with our built-in reports where we were incorrectly rendering the top ten tests in specific widgets and showing a "Render Anyway" message. The top ten tests for each widget now show as expected when loading the report.
* An issue was resolved where our report PDF downloads were incorrectly showing "Generated by null" instead of showing the specific user that generated the PDF.

#### BrowserBot Early Track Program <a href="#browserbot-early-track-program" id="browserbot-early-track-program"></a>

From July 26th - August 8th, 2022, Enterprise Agents that have already been enrolled in the BrowserBot Early Track Program will receive Browserbot v2.6.0, which will include the Chromium v97 upgrade. For teams using Cloud Agents for browser-based tests, two Cloud Agents will also have BrowserBot upgraded to Chromium v97 for testing page load and transaction tests. These Cloud Agents are:

After the conclusion of the Early Track Program, all Cloud and Enterprise Agents will be upgraded to BrowserBot v2.6.0 with Chromium v97 during the week of August 8th, 2022.
