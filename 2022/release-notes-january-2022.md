# Release Notes: January 2022

#### A Major Update to BrowserBot <a href="#a-major-update-to-browserbot" id="a-major-update-to-browserbot"></a>

In the past few months, we've made some announcements about a new version of BrowserBot coming in the future. Today, we are announcing that this new version, BrowserBot 2, will begin rolling out to Cloud and Enterprise Agents on January 10, 2022.

BrowserBot 2 introduces a containerized runtime environment for page load and transaction tests that is orchestrated using

[Podman](https://podman.io/)

. In doing so, it improves the consistency of browser-based test results and paves the way for new configuration options in page load and transaction tests.

To smoothe your Enterprise Agent update from BrowserBot 1 to BrowserBot 2, consult our

[upgrade guide](https://docs.thousandeyes.com/product-documentation/global-vantage-points/enterprise-agents/upgrading-to-browserbot-2)

.

#### Changes to Endpoint Agent Reports and Dashboards <a href="#changes-to-endpoint-agent-reports-and-dashboards" id="changes-to-endpoint-agent-reports-and-dashboards"></a>

As previously mentioned in the December 12, 2021 changelog, the Endpoint Agents data source for Reports and Dashboards is now broken out into Endpoint Scheduled Tests, Endpoint Browser Sessions, and Endpoint Local Networks in order to more accurately match what is displayed in the **Endpoint Agents > Views**. All existing metrics and widgets will be migrated to support this new structure.

This is a potential breaking change for API v7 users. If you are using the reports or dashboards v7 API and fetching information for Endpoint data, you will need to appropriately update your dataSource and category properties to match these new results as shown below.

| **Data Source**           | **Category**   | **Previous Data Source and Category** |
| ------------------------- | -------------- | ------------------------------------- |
| Endpoint Scheduled Tests  | HTTP Server    | Endpoint - Web HTTP Server            |
| Endpoint Scheduled Tests  | Network        | Endpoint - Network - Agent to Server  |
| Endpoint Scheduled Tests  | System         | Endpoint - Network - Agent to Server  |
| Endpoint Browser Sessions | Visited Pages  | Endpoint - Browser Session - Web      |
| Endpoint Browser Sessions | Network        | Endpoint - Browser Session - Network  |
| Endpoint Browser Sessions | System         | Endpoint - Browser Session - Network  |
| Endpoint Local Networks   | DNS            | Endpoint - Network Topology           |
| Endpoint Local Networks   | Gateway        | Endpoint - Network Topology           |
| Endpoint Local Networks   | Proxy          | Endpoint - Network Topology           |
| Endpoint Local Networks   | System         | Endpoint - Network Topology           |
| Endpoint Local Networks   | VPN            | Endpoint - Network Topology           |
| Endpoint Local Networks   | Network Access | Endpoint - Network Topology           |

#### Application Outages Added to Built-In Dashboard <a href="#application-outages-added-to-built-in-dashboard" id="application-outages-added-to-built-in-dashboard"></a>

The Internet Insights Built-in default dashboard, available to Internet Insights customers in **Dashboards**, now includes widgets that display Application Outages metrics corresponding to each of the already available widgets displaying Network Outages metrics.

#### Manage Quotas with the API <a href="#manage-quotas-with-the-api" id="manage-quotas-with-the-api"></a>

Quotas on Cloud and Enterprise Agent usage can now be viewed and managed via the ThousandEyes API. This includes quota configuration at the organization and account group levels.

Only API users having the 'Edit organization and account group quotas' permission can access the new functionality.

New Cloud Agents have been added to the following locations:

* Previously, when visiting an affected test from Internet Insights Application Outages, the HTTP server layer of the test view was automatically selected. Now, the Path Visualization layer will automatically be selected instead if it is available, as this view shows the context of the application outage.
* An issue was found when Endpoint Agent users with large lists had issues when attempting to filter correctly. This has been resolved. In addition, we have improved the user experience by removing redundant search boxes for filters with a small range of static options in Agent Settings. These filters remain in place for larger, dynamic option filled lists.
* Fixed an issue where the ThousandEyes alerting system was incorrectly double-counting a single agent across multiple test rounds when evaluating an alert rule criteria. This condition had been causing false positive alerts when an agent had to exceed a threshold in multiple test rounds, but instead the alert was firing after only one test round.
* An issue was found in the Endpoint API where a NetworkTopology request defaulted to 1 minute rounds, rather than 5 minute as expected. This has been resolved to ensure consistency with the application.
* An issue has been resolved where the configuration of sticky agent alert rules was not properly updating in the UI. Previously, when a customer was selecting "the same" agents to evaluate an alert against, the configuration was correctly saving in the backend and being evaluated correctly, but the UI would incorrectly revert back to the "any" agents selection.
* An intermittent UI issue where the time series widget tooltip in a report or dashboard was incorrectly showing a 0 value for data has been resolved for new widgets, and those that have their configuration settings updated. **Note:** If the issue still persists for you, you will need to update your cache by changing any value for the affected widget in **Widget Settings** (for example, "Group By") to a different value, and then back to the original value. This should clear the incorrect data from the cache and resolve the issue.

New Cloud Agents have been added to the following locations:

* Cincinnati, OH, USA (IPv6)
* Osaka, Japan (NTT) (IPv6)
* Application logos are now displayed in the Internet Insights Overview for application outages.
* Users that do not have the "Edit Own Reports" or "Edit Own Dashboard Templates" permissions will no longer see the **Add Another Widget** option during widget configuration.
* Users that do not have the "Edit dashboard templates for all users in an account group" or the "Edit reports for all users in account group" permission will no longer see the **Add Another Widget** option for reports and dashboards that they don't own.
