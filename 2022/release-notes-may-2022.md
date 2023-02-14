# Release Notes: May 2022

#### ThousandEyes Recorder IDE v1.3.0 <a href="#thousandeyes-recorder-ide-v1.3.0" id="thousandeyes-recorder-ide-v1.3.0"></a>

Transaction scripting through the Recorder IDE now supports the ability to make API requests through a proxy by using **fetch()** and an HTTP proxy agent. To learn more, see the

[documentation](https://docs.thousandeyes.com/product-documentation/browser-synthetics/transaction-tests/api-monitoring/node-fetch-module#proxy-support-for-api-monitoring)

and examples in the

[scripting repository](https://github.com/thousandeyes/transaction-scripting-examples/tree/master/API-transaction-scripts)

.

This version also resolves the issue where the Recorder IDE for Windows was not cleaning up `scoped_dir` files in the **temp** directory after running a test round in the IDE.

#### Additional Dynamic Baseline Metrics <a href="#additional-dynamic-baseline-metrics" id="additional-dynamic-baseline-metrics"></a>

Additional metrics have been added to our dynamic baseline alerting capabilities:

* Web – FTP Server – Connect Time
* Web – FTP Server – FTP Negotiation Time
* Web – FTP Server – Response Time
* Web – FTP Server – Transfer Time
* Web – FTP Server – Wait Time
* Voice – Sip Server – Connect Time
* Voice – Sip Server – Invite Time
* Voice – Sip Server – Options Time
* Voice – Sip Server – Register Time
* Voice – Sip Server – Response Time
* Voice – Sip Server – Wait Time
* Network – Agent to Server – Jitter
* Network – Agent to Agent – Jitter
* Network – Agent to Server – Proxy Jitter
* Network – Agent to Server – Proxy Latency

#### Enhanced API Output to Support Automated Solutions <a href="#enhanced-api-output-to-support-automated-solutions" id="enhanced-api-output-to-support-automated-solutions"></a>

For Enterprise Agents, we have added a new element to the output of the agent status in the ThousandEyes API that contains a hash of the interfaces available to that agent, with the IPs assigned to those interfaces. This allows customers building automation to deterministically select which IP and interface combination should be used for testing. For situations where the unordered nature of the IP Addresses element is an issue, this presents a better path.

* The Endpoint Agent API now allows customers to extract end-to-end metrics, path visualization, and detailed path trace from specific automated session tests.

#### New and Updated Cloud Agents <a href="#new-and-updated-cloud-agents" id="new-and-updated-cloud-agents"></a>

New Cloud Agents have been added to the following locations:

* Riyadh, Saudi Arabia (IPv6)
* Seoul, South Korea (IPv4)

In addition, the following Cloud Agent locations been renamed:

New Webex Cloud Agents have been added to the following locations:

#### 2022-05-12 General Bug Fixes <a href="#2022-05-12-general-bug-fixes" id="2022-05-12-general-bug-fixes"></a>

* For automated session tests, an issue has been resolved that was causing inconsistencies in the aggregated metrics for the path view. Customers can now see consistent data (packet loss, latency, jitter) along the different hops of the path view.
* Fixed an issue that displayed empty graphs for VPN metrics when no data was collected. Customers will only see graphs with VPN metrics in the Endpoint Agent views when meaningful data is obtained.
* Fixed an issue that was duplicating the system proxy in the path visualization of browser session tests.
* Fixed an issue in the Dashboards API (v6), where the ThousandEyes built-in dashboards were not being returned as part of the response payload.
* Fixed an issue where the Dashboards dropdown list was incorrectly showing in alphabetical order instead of by **last seen**.
* An issue has been resolved in the visualization of BGP path changes which caused a path that was withdrawn and re-announced within the same round to be incorrectly rendered as withdrawn only.

**2022-05-12 Endpoint Agent Client Version 1.117.0 Bug Fixes**

* An issue has been resolved that would occur on a network change event, which caused the Endpoint Agent to stop running automated session tests until the tests were updated or the agent was restarted.
* Fixed an issue where the Endpoint Agent was not running automated session tests for the whole duration of a meeting.
* An issue was found where the CPU metrics (CPU, memory) were not being collected for cases where the Local Network probe failed or completed too quickly. This has been resolved.

New Cloud Agents have been added to the following locations:

* Jakarta, Indonesia (Biznet)
* Jakarta, Indonesia (Biznet) (IPv6)
* Little Rock, AR, USA (IPv6)
* Singapore (Star Internet)
* Singapore (Star Internet) (IPv6)
* Singapore (MobileOne) (IPv6)
* We have added three additional metrics to our dynamic baseline alerts:
  * Web - Page Load – DOM Load Time
  * Voice – RTP Stream – Packet Delay Variation
  * Web - Transaction - Transaction Time
* Customers can now see the calculated baseline over the last 24 hours, for all triggered dynamic baseline alerts on the alert list page, via a tooltip. This tooltip will show each dynamic metric, its baseline over the last 24 hours, and if used, its standard deviation over the last 3 hours. This will help customers better understand why a dynamic alert has been triggered and get a sense of their stable performance over the last 24 hours.
* The Endpoint Agent API now allows customers to create scheduled tests for a much wider variety of labels. In the past, a scheduled test was only able to target a single Endpoint Agent label. You can now target all agents, a list of labels, or a specific set of agents. As a result of this change, we expect the **groupId** attribute to be deprecated when ThousandEyes releases v7 of the public API in the future.
* The certificate used for signing the Endpoint binaries and installer releases has changed from "ThousandEyes, Inc." to "CISCO SYSTEMS, INC."
* We have resolved a memory leak in the Enterprise Agent that would result in unbounded memory usage when monitoring SNMP devices that use SNMPv3 authentication.
* Fixed an issue in our report and dashboard widgets where we incorrectly showed the number of tests associated with a widget when the "Alerts" data source was selected as a filter. The widgets were incorrectly including deleted tests in the filter.
* Fixed an issue where the Dashboards drop down list was incorrectly showing in alphabetical order instead of by last seen.
* Fixed an issue that sent users to an invalid URL of a deleted dashboard if the dashboard was set as default and then deleted. Now when a default dashboard is deleted, the default setting is also removed and users will be sent to our built-in dashboards before selecting a new default.
* An issue has been fixed in the Enterprise Agent which would produce incorrect interface metrics when monitoring large numbers of interfaces.
* We have fixed an issue in the Enterprise Agent that would result in incorrect throughput measurements being reported in agent-to-agent tests.
* Fixed a bug that was incorrectly showing tests assigned to an agent in the **Agent Settings** tab.
* Fixed a bug that was not properly updating the test configuration of an agent, in cases where no tests were currently assigned to the agent. Agents are now correctly updated, even if no tests are running on the agent.
