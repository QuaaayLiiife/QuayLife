# Release Notes: March 2022

#### Changes to Dynamic Baselines <a href="#changes-to-dynamic-baselines" id="changes-to-dynamic-baselines"></a>

We are in the process of improving our dynamic baselining functionality for alert rules. Part of this improvement is simplifying the configuration process and ensuring that our alerts are firing on real issues and not false positives.

In order to do this, we are removing the option to select a sliding window for your dynamic baseline. Dynamic baselines will be based on a 24-hour period. If a user selects a dynamic alert rule based on a standard deviation, this standard deviation will always be based on a 3-hour period. You will still be able to select a percentage, standard deviation, or absolute value above the dynamic baseline in order to trigger an alert.

For the time being, all existing alert rules will maintain their existing configuration. However, if a user attempts to create a new alert rule or edit an existing alert rule with dynamic baselines, this new 24-hour baseline and 3-hour standard deviation will be required.

30 days after the release of this feature (approximately March 30), we will migrate all alert rules to this new configuration. No customer action is required.

New Cloud Agents have been added to the following locations:

* Charlotte, NC, USA (IPv6)
* Cleveland, OH, USA (IPv6)
* Geneva, Switzerland (IPv6)
* Nashville, TN, USA (IPv6)
* Pittsburgh, PA, USA (IPv6)

The ThousandEyes private BGP collectors listed below will be retired on March 30th, 2022 at 18:00 UTC, and all private BGP monitors currently associated with these collectors will be removed.

| BGP Collector           | IPv4            | IPv6                  |
| ----------------------- | --------------- | --------------------- |
| bgpc1.thousandeyes.com  | 192.150.160.138 | 2620:c2:4000:128::138 |
| bgpc2.thousandeyes.com  | 192.150.160.135 | 2620:c2:4000:128::135 |
| bgpc3.thousandeyes.com  | 192.150.160.136 | 2620:c2:4000:128::136 |
| bgpc4.thousandeyes.com  | 192.150.160.137 | 2620:c2:4000:128::137 |
| bgpc5.thousandeyes.com  | 192.150.160.139 | 2620:c2:4000:128::139 |
| bgpc6.thousandeyes.com  | 192.150.160.140 | 2620:c2:4000:128::140 |
| bgpc7.thousandeyes.com  | 192.150.160.144 | 2620:c2:4000:128::144 |
| bgpc8.thousandeyes.com  | 192.150.160.145 | 2620:c2:4000:128::145 |
| bgpc9.thousandeyes.com  | 192.150.160.146 | 2620:c2:4000:128::146 |
| bgpc10.thousandeyes.com | 192.150.160.147 | 2620:c2:4000:128::147 |
| bgpc11.thousandeyes.com | 192.150.160.148 | 2620:c2:4000:128::148 |
| bgpc12.thousandeyes.com | 192.150.160.149 | 2620:c2:4000:128::149 |
| bgpc13.thousandeyes.com | 192.150.160.150 | 2620:c2:4000:128::150 |
| bgpc14.thousandeyes.com | 192.150.160.151 | 2620:c2:4000:128::151 |
| bgpc15.thousandeyes.com | 192.150.160.152 | 2620:c2:4000:128::152 |
| bgpc16.thousandeyes.com | 192.150.160.153 | 2620:c2:4000:128::153 |
| bgpc17.thousandeyes.com | 192.150.160.154 | 2620:c2:4000:128::154 |
| bgpc18.thousandeyes.com | 192.150.160.155 | 2620:c2:4000:128::155 |

If you are currently using the private BGP collectors above, you should have received multiple emails starting in December 2021 with instructions on how to update your configuration to peer with our new BGP collectors. If you did not receive the emails or need help making the change,

[contact ThousandEyes Customer Engineering](https://docs.thousandeyes.com/product-documentation/getting-started/getting-support-from-thousandeyes#ways-to-contact-customer-engineering)

.

* Fixed an issue where our alerter was incorrectly using the page load test interval for HTTP test data when a page load test was executed, although these intervals can be set up independently. This was causing alerts to fire incorrectly due to an incorrect round count.
* We upgraded the Endpoint Agent client to support changes in how WiFi metrics are exposed in macOS 12 devices. \[Endpoint Agent client version 1.100.0]
* Fixed an issue with the 1.99 Endpoint Agent client release, which had led to some customers observing increases in latency metrics when running TCP tests (but not ICMP tests). This issue is resolved in the 1.100 release. \[Endpoint Agent client version 1.100.0]
* Fixed an error in calculating the link delay between two nodes on the local network visualization. The link delay is now correctly calculated and displayed as **delay(hop) - delay(hop-1)**.

#### Provider Labels for Internet Insights <a href="#provider-labels-for-internet-insights" id="provider-labels-for-internet-insights"></a>

ThousandEyes provider labels are now available for use with Internet Insights. Customers can label providers (including by region), and use these labels to customize the Internet Insights overview, views, alerts, dashboards and reports, as well as track and maintain labels within catalog settings.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-6307b262194269902a83cc588dd36c5854a0a1be%2Fwhats\_new-changelog\_2022-03-15\_01.png?alt=media)

#### Improved Snapshot Experience for Reports <a href="#improved-snapshot-experience-for-reports" id="improved-snapshot-experience-for-reports"></a>

The snapshot and download experience for ThousandEyes reports has been improved. Snapshot options can now be accessed via the **Camera** button on the top configuration bar in **Reports**. This will allow you to create a snapshot, as well as view all the most recent snapshots in your account group and all of the related snapshots to the selected report.

In addition, we have moved the **Download** button to the top configuration bar in **Reports**.

* The **Dashboard** object in v6 of the publicly facing API can now be accessed by customers:
  * **GET /dashboards**: Returns object with list of dashboards available for the user.
  * **GET /dashboards/{dashboardId}**: Returns object with the requested dashboard ID.
  * **GET /dashboards/{dashboardId}/{widgetId}**: Returns object with dashboard widget data for requested widget and dashboard ID.
  * **POST /dashboards/{dashboardId}/delete**: Deletes the given dashboard.
* Improved the documentation for the Endpoint Agent update label API to include descriptions of the **endpointAgents** structure.
* A new column, called **Data Type**, has been added to the provider coverage map in the Internet Insights **Catalog Settings > Packages and Catalog Settings > Providers** tab so that customers can distinguish whether individual covered providers in the catalog will appear in network or application outages.
* The **Test Table** widget search box is now always visible in the widget, and has moved to the left hand side, to the right of the widget title.
* An issue that caused the **Alert List** widget to not populate configuration options correctly has been resolved.
* Previously, the **Last Contact** column of the **Device Settings** table was incorrectly displaying the time the last connection attempt was made, instead of the time the device was last seen online. This has been resolved. In addition, the last contact attempt information has been added to the **Device Details** side bar.
* An issue was found where Endpoint snapshots were missing page load and response times after a data migration to a higher-performance data store. This was resolved and all relevant data is now available.
* An issue that prevented data being loaded in the **Local Network** view when Endpoint Agent tests had larger numbers of Endpoint Agents in the path visualization has been resolved.
* An issue was found where some Endpoint Agent time periods were incorrectly displayed as "01:00" during winter, specifically for the Brazil/Sao Paulo timezone. This has been resolved.
* An issue where alerts were incorrectly fired during an active alert suppression window has been resolved.
* An issue where the public IP visible in the Web UI did not match the **sourceAddr** attribute in the user sessions list API when network traffic is proxied has been resolved.
* An issue was found where a focus handling issue on the Endpoint Agent Scheduled Tests view caused the drop-down selection list of scheduled tests to disappear when scrolling through the list using the scrollbar. This has been fixed.
* An issue was found in the Endpoint Agent Browser Sessions view, where a **Connection Failed** error message was displayed when showing results for a visited site, if the network traffic was proxied on the server side. This has been corrected.

#### Introducing Webex Cloud Agents <a href="#introducing-webex-cloud-agents" id="introducing-webex-cloud-agents"></a>

ThousandEyes has now deployed Webex-specific Cloud Agents at the front door of several Webex data centers responsible for serving customer traffic. These agents are available for general use by all ThousandEyes customers and are a tool to better monitor and troubleshoot your Webex performance.

#### Automated Session Testing <a href="#automated-session-testing" id="automated-session-testing"></a>

ThousandEyes has added **automated session tests** to monitor the network performance of selected applications running on end-user machines. Automated session tests are configured and run using ThousandEyes Endpoint Agents. Note that these tests capture information only when the application is running an active session. Initially, the following applications are supported:

Learn more about automated session tests here:

#### Cisco Catalyst 8500 and Cisco ASR 1000 Container Installation Support <a href="#cisco-catalyst-8500-and-cisco-asr-1000-container-installation-support" id="cisco-catalyst-8500-and-cisco-asr-1000-container-installation-support"></a>

The ThousandEyes Enterprise Agent for Cisco Application Hosting now supports the Catalyst 8500 and ASR 1000 routing platforms. See the

[Support Matrix](https://docs.thousandeyes.com/product-documentation/global-vantage-points/enterprise-agents/installing/cisco-devices#support-matrix)

for a complete list of supported agent platforms.

#### Additional Metrics for Dynamic Baselines <a href="#additional-metrics-for-dynamic-baselines" id="additional-metrics-for-dynamic-baselines"></a>

Per our release notes on March 3rd under

[Changes to Dynamic Baselines](broken-reference)

, we have now migrated all existing dynamic baseline alert rules to a 24-hour dynamic baseline. Any rules using standard deviation will now look at a 3-hour window for standard deviation. No customer action is required.

We have also added two additional metrics to our dynamic baseline alerting capability:

New Cloud Agents have been added to the following locations:

* Fort Worth, TX, USA (IPv6)
* Indianapolis, IN, USA (IPv6)
* Milwaukee, WI, USA (IPv6)
* Oklahoma City, OK, USA (IPv6)
* Rotterdam, Netherlands (IPv6)
* Seoul, South Korea (KT Telecom)
* Seoul, South Korea (KT Telecom) (IPv6)
* Seoul, South Korea (SK Telecom)
* Seoul, South Korea (SK Telecom) (IPv6)
* Utrecht, Netherlands (IPv6)
*
  * We have improved the security of the public installer download links for the Endpoint Agent by replacing the current naming scheme (which uses 5-9 lowercase alphabetic characters) with one that uses 40 characters and considers a wider range of possible characters (upper case, lower case and numbers). The old public installer download links will remain valid for a further 28 days, after which they will not be functional.
  * A single account group can now contain up to 50,000 Endpoint agents.
  * A new geo-location algorithm has been deployed to help identify users more accurately, particularly for users connected behind VPNs.
* To improve customer experience when being logged out of the application due to a timeout, the ThousandEyes platform will now redirect the browser to the ThousandEyes login page automatically. Previously, the platform would require the user to click the **OK** button on a popup before being redirected to the login page in order to reauthenticate.
* Fixed an issue where some BGP origin verification alerts were not firing appropriately, due to a mismatch in the active vs. inactive state of the monitored prefix in the ThousandEyes control plane. This has been corrected.
* Fixed an issue with test labels in alert rules, where the alert webhook was incorrectly sending additional test labels via the JSON payload that were not associated with the alert or test.
* Fixed an issue in the sankey diagram on the Application Outages view, **Topology** tab. Previously, the link hover-panel in Internet Insights Application Outages displayed information in the context of _all_ tests seen by the agent group. This has been corrected to display information only for the affected tests seen by the agent group.
