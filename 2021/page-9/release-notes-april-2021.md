# Release Notes: April 2021

#### Browser Extensions Installed by Default <a href="#browser-extensions-installed-by-default" id="browser-extensions-installed-by-default"></a>

Starting April, 2021, the Google Chrome and Microsoft Edge browser extensions are installed by default in new installations of Endpoint Agent on Windows endpoints. Users can opt-out of the installation as part of the Endpoint Agent installer process.

If you opt not to install the extensions as part of the Endpoint Agent installer process, you can still install them separately. See

[Install the Browser Extension](https://docs.thousandeyes.com/product-documentation/endpoint-agent/install/install-the-browser-extension)

.

#### Endpoint Agent Zscaler Internet Access Support <a href="#endpoint-agent-zscaler-internet-access-support" id="endpoint-agent-zscaler-internet-access-support"></a>

The ThousandEyes Endpoint Agent is now able to identify the presence of Zscaler Internet Access (ZIA) on customer machines allowing us to gather metrics and performance measurements for traffic transiting the Zscaler network. Metrics and measurements are displayed in the UI in the same way as other supported VPN providers. Some ZIA deployment models may not be fully supported. For more information see

[Endpoint Agent VPN Support](https://docs.thousandeyes.com/product-documentation/endpoint-agent/endpoint-agent-vpn-support)

.

ThousandEyes has introduced a new image for its Docker Enterprise Agents that attaches an anonymous Docker volume to each container running the Enterprise Agent. This change supports a future enhancement that will improve the consistency and performance of browser-based tests.

* The endpoint scheduled test table now displays a dash rather than 0% loss if the loss is in fact null, which may happen if ICMP measurements could not be completed.
* The ThousandEyes Endpoint API has been extended to allow existing agent labels to be updated.
* The API /endpoint-agents now correctly respects the "deleted" flag when returning a list of agents. By default this flag is false - only non-deleted agents are returned.
* The Endpoint Agent basic service set identifiers (BSSID) table now shows a list of all of the BSSIDs detected in a test round.
* The location of the Endpoint Agent is no longer updated if insufficient WiFi data is obtained from the end user machine, to avoid occasional "flapping" between agent locations that occurred due to operating system inconsistencies in obtaining the WiFi data used for obtaining geolocation data.
* In cases where the speed score cannot be calculated due to an error gathering data for the page, the experience score is now set to **0** rather than **-**.
* The default widget time on reports has been updated from 7 days to 1 day. This value can still manually be changed by the customer at the report level or the individual widget level.

#### Deprecated and Removed Features <a href="#deprecated-and-removed-features" id="deprecated-and-removed-features"></a>

**Internet Explorer 11 Support**

Effective March 30, ThousandEyes will cease support for Internet Explorer 11 for https://app.thousandeyes.com. Support for all other browsers remains unchanged.

* Fixed an improper handling of an aborted request that could result in an occasional failure to display an Endpoint Agent Path Visualisation.
* An issue was found where creating an Endpoint agent scheduled test via the API could throw a 500 Internal Server Error. This has been resolved.
* An issue occurred where our third-party provider of geolocation data was wrongly assigning an IP address to a location in the UK rather than in New York City, USA. This is now resolved.
* An edge case was found where, when an Endpoint alert rule was applied to a scheduled test, the test would show the assigned rule, but the alert rule would show 0 assigned tests. This issue has been resolved.
* API endpoint /v6/endpoint-data/user-sessions no longer returns 500 when only the "from" field is specified. In this case, the end date of the query will default to the current time.
* API endpoint /v6/endpoint-data/network-topology no longer returns 500 when specifying only the "from" field is specified. In this case, the end date of the query will default to the current time.
* Previously, unresolved VPN overlay targets were displayed on the path visualization as 0.0.0.0, which was misleading. This has been corrected, and they are no longer displayed.
* An issue was found where a deleted Endpoint Pulse Agent was still being returned in API calls. This has been resolved.
* Previously, an issue occurred where a combination of filters was interpreted as OR rather than AND. The path visualisation agent filter now correctly filters the list of agents.
* Previously, it was possible to see different colours when clicking a group to expand it versus when you applied the equivalent filter manually. The path visualisation now shows consistent colours for groups.
* In a small number of cases, test data was not collected as scheduled tests data points were discarded if the tests couldn’t finish within their expected time bounds. Data points are no longer discarded in this case.
* Fixed an issue where the interactive Endpoint Agent Windows installer could fail installing a COM component and return an error "There is a problem with this Windows installer package."
* Fixed an issue where a handful of no longer valid BGP alerts were incorrectly being included in reporting and dashboarding widgets due to an incorrect clear time on the alerts.
* An issue was found where enterprise agents running shared tests were not showing up as a filter option in the shared to account group while using dashboards and reports. This has been resolved.
* An issue was found where the hard render limits put in place for report and dashboard widgets were not transparent to users in our multi-metric table widget. Previously, if a multi-metric table request was too large, we would simply say "No Data." We have now added a tooltip that explains that the data cannot be rendered because the request is too large.
*   Fixed an issue that prevented test labels from being used in reports and dashboards in relation to our BGP hard render limits. A user can now select a test label and the hard render limit calculation will correctly apply. For more information on our render limits, see

    [Working with Reports](https://docs.thousandeyes.com/product-documentation/dashboards-and-reports)

    .
* Fixed an issue that occurred when a user tried to deselect a filter selection in a dashboard or report widget and the filter inadvertently closed instead of letting the user deselect multiple options at a time.
* Fixed an issue where a small number of users with the correct edit permissions were not able to edit existing alert rules.

#### Dashboard and Report Hard Render Limit <a href="#dashboard-and-report-hard-render-limit" id="dashboard-and-report-hard-render-limit"></a>

We have placed a hard render limit on our Cloud and Enterprise and Device data as it relates to our dashboards and reports. Widgets that have a high number of tests, a large number of agents running those tests, and long timespans may hit this hard render limit. For more information, see

[Working with Reports](https://docs.thousandeyes.com/product-documentation/dashboards-and-reports)

.

#### Update to Activity Log for Transaction Tests <a href="#update-to-activity-log-for-transaction-tests" id="update-to-activity-log-for-transaction-tests"></a>

The Activity Log now provides the option to display more details related to "create" and "update" events for transaction tests. For these events, a **View Change** button is displayed in the event row. This button opens a modal that provides a diff showing any transaction script changes. A separate tab shows any credential selection changes for the test.

#### Webhook Alert Notification Improvements <a href="#webhook-alert-notification-improvements" id="webhook-alert-notification-improvements"></a>

We have made several updates to our webhook alert notifications around outage alerts:

* The **link** field has been removed, and replaced by the **permalink** field. The link field will remain for the time being, but will eventually be removed. ThousandEyes recommends using the **permalink** field going forward.
* The **ruleAid** field has now been added to all alert types that use the new notifier. Previously, it was only included in outage alerts.
* A **dateEnd** field has been added.
* A **type** field has been added.
* The **ruleRefId** field has been removed.

**Transfer Endpoint Agents with the API**

Endpoint Agents can now be transferred in bulk via the public API. Users can upload a CSV file containing the **agentId**, the source account and the target account. For large transfers (several thousands of agents) it may take a few minutes for the UI to show the agents as transferring.

We've redesigned the look of test labels for scheduled tests.

* Fixed an issue where a small number of alerts were being inadvertently suppressed due to faulty "agents with local problems" logic in our backend system.
* Fixed a UI bug where the system was not rendering error messages correctly around OAuth authentication for our webhook integrations. Previously, clicking **Add New Webhook** would close the modal dialog even if the save operation failed. This issue has been fixed to ensure the proper error message is shown before a webhook is saved.
* Fixed an issue where the alerter system was not correctly updating alert configurations based on updates to IP prefix subnet ranges. This impacted a very small number of customers and all spurious alerts have been cleared.
* In **Views > Scheduled Tests > Table**, an agent that appeared when no filters were applied would not be displayed when filtered by agent using its own name. This was because we were only considering agents that submitted data for the round if a filter was applied. This is now fixed.
* Fixed an issue where, when a report based on Internet Insights metrics had a duration set to 12 hours or less, some widgets displayed "No Data" instead of the expected 0 outages.

#### ThousandEyes Recorder for Windows Auto Updates <a href="#thousandeyes-recorder-for-windows-auto-updates" id="thousandeyes-recorder-for-windows-auto-updates"></a>

The ThousandEyes Recorder IDE for Windows will be signed by "Cisco Systems, Inc" from version 1.0.5 onwards. Customers running version 1.0.4 will be able to auto-update without issue.

Customers running version 1.0.3 or earlier may need to reinstall the IDE to upgrade to version 1.0.5.

The latest version of the IDE is always linked from the **Test Settings** page when the transaction test option is chosen.

#### Changes to the te-browserbot Package's Dependencies <a href="#changes-to-the-te-browserbot-packages-dependencies" id="changes-to-the-te-browserbot-packages-dependencies"></a>

In the coming weeks, ThousandEyes will add `te-podman` as a dependency of the `te-browserbot` package. This package is required for page load and transaction tests, and will be automatically installed.

`te-podman` is a wrapper of the

[Podman package](https://podman.io/)

. If your Enterprise Agents have existing installations of Podman, this dependency may cause conflicts. We suggest removing Podman before installing this new version of BrowserBot.

#### AppDynamics Integration for Cloud and Enterprise Agent Test Data <a href="#appdynamics-integration-for-cloud-and-enterprise-agent-test-data" id="appdynamics-integration-for-cloud-and-enterprise-agent-test-data"></a>

Joint ThousandEyes and AppDynamics customers can now ingest ThousandEyes Cloud and Enterprise test data directly into their AppDynamics Dash Studio instance as either a number card widget or a time series widget. For more information, see

[ThousandEyes Integration with AppDynamics](https://docs.appdynamics.com/display/PRO21/ThousandEyes+Integration+with+AppDynamics)

.

#### Endpoint Agent TCP Support <a href="#endpoint-agent-tcp-support" id="endpoint-agent-tcp-support"></a>

The Endpoint Agent now allows scheduled tests to be executed using TCP as well as ICMP protocols. This is available in Endpoint Agent version 1.75.0 and above. For more information, see

[Endpoint Agent TCP Support](https://docs.thousandeyes.com/product-documentation/global-vantage-points/endpoint-agents/endpoint-agent-tcp-support)

.

* The average response time per hop is now shown in the **Endpoint Agents > Views > Local Networks** view.
* The Endpoint Agent API response now includes DNS server test ping data instead of ICMP ping data for DNS probes. This avoids cases where no ICMP data was available for DNS probes.
* Agent-to-server network tests can now be created and read with DSCP parameters (**dscp** and **dscpId**) when using the API.
* Previously, some of the advanced settings options for shared tests were selectable. This gave users the impression that those settings could be modified within the shared account group, which is incorrect. All test settings options are now unselectable to ensure users are aware that shared tests cannot be edited from the shared account group.
* The SNMP timeout and number of retry attempts for device availability SNMP requests has been increased to account for devices with high CPU utilization that either take a long time (over 2 seconds) for an SNMP or may ignore the SNMP request altogther.
* Endpoint network topologies can now be grouped by interface. The available options to group by are **IP Address**, **Network**, **Network & Location** and **Location**.
* An edge case was found when using the Endpoint Agent public API to get test data, where if there was exactly 1000 data points returned, the next page URL for pagination was not set. This has been resolved.
* An issue was found that caused attempts to create Endpoint Agent snapshots with a date range of more than 12 hours to fail. This has been resolved, and snapshots can now be created with a date range of up to 2 days.
* An issue was found where the hop slider in a multi-service path visualization view was not showing every hop, even when the slider was set to show maximum hops. This has been resolved.
* An issue was found where the traceroute style output in the path visualization layer showed the test target IP address instead of the terminating hop's IP address. This has been resolved.
* An issue was found that caused sorting Enterprise Agents by **Utilization** to incorrectly sort the list of agents. This has been fixed.
* An issue was found that caused test names that included '<' or '>' to be incorrectly rejected due to a silent validation error. This has been corrected.
