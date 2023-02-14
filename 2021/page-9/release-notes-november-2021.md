# Release Notes: November 2021

#### CentOS 8.x End of Installation Support <a href="#centos-8.x-end-of-installation-support" id="centos-8.x-end-of-installation-support"></a>

The CentOS 8.1, 8.2, 8.3, and 8.4 operating systems have now transitioned into the **End of Installation Support** lifecycle phase. New installations of Enterprise Agents on these operating systems will no longer be supported.

Support for existing Enterprise Agents running on CentOS 8.1 systems will end on November 30th, 2021, while support for agents running on CentOS 8.2, 8.3, and 8.4 systems will end on December 31st, 2021.

After those dates, the operating systems will transition into the **End of Support** phase, in preparation for **End of Life**.

If you need assistance migrating to a supported operating system, contact ThousandEyes Customer Engineering.

#### Announcing Internet Insights Application Outages <a href="#announcing-internet-insights-application-outages" id="announcing-internet-insights-application-outages"></a>

ThousandEyes announced Application Outages availability on November 9th. Application Outages expands Internet Insights – the first ever collectively powered global view of Internet health – to give you visibility into outages affecting the top SaaS applications you rely on.

Application Outages brings the following new capabilities to ThousandEyes Internet Insights:

* **Overview** screen: See both Application Outages and Network Outages on a color-coded map display.
*
  * Select **Network Outages** or **Application Outages**
  * Cross-layer visualization shows you what type of outage is occuring: network, application, or both.
  * Error Types tell you the type of errors encountered in the outage.
* **Catalog Settings** screen: New SaaS type packages add more than 75 top application providers.

Application Outages data is available across the ThousandEyes platform: within snapshots, dashboard and reports, as well as outage alerts and alerts API. All of these capabilities leverage ThousandEyes' collective network intelligence using real data, not sentiment.

ThousandEyes has added a new view to simplify Endpoint Agent troubleshooting. This view gives you the ability to search for a specific agent and view all the information related to its scheduled tests, local networks, and browser session data.

For full documentation of this new view, see

[Agent Views](https://docs.thousandeyes.com/product-documentation/end-user-monitoring/viewing-data/single-agent-view)

.

Initially, this view is an opt-in feature. To access it, contact ThousandEyes Customer Engineering.

You can now edit tests assigned to multiple Enterprise Agents simultaneously. In **Cloud & Enterprise Agents > Agent Settings**, select multiple agents; then use the new **Edit Tests** option to edit the set of tests assigned to these agents.

#### Updated Dashboards and Reports Caching Mechanism <a href="#updated-dashboards-and-reports-caching-mechanism" id="updated-dashboards-and-reports-caching-mechanism"></a>

The caching mechanism for dashboards and reports has been updated to improve end-to-end performance. As part of this change, the cache time has been increased to 30 minutes. This will result in a delay in updated dashboards and reports when you change the ownership of a test to a different account or organization ID.

For example, if the test ownership moves from Account Group A to Account Group B, this change will only be reflected in your dashboard or report when the cache is updated - meaning there is a maximum potential delay of 30 minutes.

#### New Version of the Enterprise Agent Docker Image <a href="#new-version-of-the-enterprise-agent-docker-image" id="new-version-of-the-enterprise-agent-docker-image"></a>

A new version of the Enterprise Agent Docker image (0.14-1635966276) is released that includes important changes for future versions of BrowserBot. This version allows you to inspect your Docker Enterprise Agents' image versions via the **Agents Settings** page and plan an upgrade as necessary.

#### Change to the Agent ID Data Type in Web Transaction Scripts <a href="#change-to-the-agent-id-data-type-in-web-transaction-scripts" id="change-to-the-agent-id-data-type-in-web-transaction-scripts"></a>

The JavaScript data type of the `agentId` field, provided by the `agent` module, will change from Number to String in BrowserBot version 1.172.0 onwards. This change allows the Transaction scripting sandbox to accommodate agent IDs that are too large for the JavaScript Number type to represent.

New Cloud Agents have been added to the following locations:

* Chengdu, China (Alibaba cn-chengdu)
* Dublin, Ireland (IPv6) (Eircom)
* Guangzhou, China (Alibaba cn-guangzhou)
* Heyuan, China (Alibaba cn-heyuan)
* Manila, Philippines (Alibaba ap-southeast-6)
* Rio de Janeiro, Brazil (IPv6)
* Ulanqab, China (Alibaba cn-wulanchabu)

#### Deletion of Transaction Data from the ThousandEyes Platform <a href="#deletion-of-transaction-data-from-the-thousandeyes-platform" id="deletion-of-transaction-data-from-the-thousandeyes-platform"></a>

#### Deprecated and Removed Features <a href="#deprecated-and-removed-features" id="deprecated-and-removed-features"></a>

* BrowserBot is no longer supported for Enterprise Agents deployed on Amazon Linux. New Enterprise Agent installations using `install_thousandeyes.sh` will not be able to install BrowserBot on Amazon Linux. Existing Enterprise Agents will not be impacted immediately, though they may fail to upgrade to future versions of BrowserBot.
* The **Keep browser cache between tests** agent setting has been deprecated. The setting will be visible, toggle-able, and respected by Enterprise Agents with the current BrowserBot version, but the setting will not be available in future releases. When the next version of BrowserBot is released, the setting will be removed from the **Agent Settings** page, and BrowserBot will reset the browser cache between all test rounds unconditionally.
* An issue was found where **/v6/endpoint-agents** API calls did not return the **createdTime** field. This has now been fixed.
* An issue was found on macOS where TCP tests that run over certain VPN clients could cause the network interfaces to stop functioning. This issue has been reported to Apple, and the issue trigger is now avoided by ThousandEyes.
*   Previously, path trace alerts were triggered incorrectly for the following scenarios:

    * The alert condition was to trigger in event of path trace being incomplete. However, the alerts were triggered for tests with path trace completed.
    * The IP addresses provided were in the pre-defined range, yet the alerts were triggered.

    These have now been fixed.
