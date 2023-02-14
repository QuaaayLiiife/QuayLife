# Release Notes: August 2022

#### DNS Issues with Cloud Agents in China <a href="#dns-issues-with-cloud-agents-in-china" id="dns-issues-with-cloud-agents-in-china"></a>

At 8:00 UTC time on July 11, 2022, certain Cloud Agents in China began experiencing high packet loss to both configured DNS resolvers. This is representative of conditions that occur in this geographic region. DNS resolution also affected the ability to submit Cloud Agent data to the ThousandEyes Platform.

Between July 13, 2022 at 00:40 UTC and July 13, 2022 at 05:40 UTC, the Cloud Agent operations team took action to enable data submission by updating the DNS resolver for affected locations to **114.114.114.114**, which is a DNS resolver in China Unicom's ASN. This change enabled data collected to be successfully submitted to the ThousandEyes platform.

An expected side-effect of this change is that certain tests' DNS resolution behavior may have changed due to using different resolvers. Our product and engineering teams continually assess DNS performance in China and from their tests, they found the most reliable DNS open resolver is aliDNS (223.6.6.6). This is an anycast solution, so we expect good reliability from it moving forward, using **223.6.6.6** as a primary and **114.114.114.114** as a secondary DNS resolver for the following Cloud Agents in China:

* Beijing, China (China Mobile)
* Beijing, China (China Telecom)
* Beijing, China (China Unicom)
* Changsha, China (China Mobile)
* Chengdu, China (China Mobile)
* Chongqing, China (China Mobile)
* Dalian, China (China Unicom)
* Guangzhou, China (China Mobile)
* Guangzhou, China (China Unicom)
* Jinan, China (China Unicom)
* Ningbo, China (China Mobile)
* Shanghai, China (China Mobile)
* Shanghai, China (China Telecom)
* Shanghai, China (China Unicom)
* Shenyang, China (China Unicom)
* Shenzhen, China (China Mobile)
* Shenzhen, China (China Unicom)
* Shijiazhuang, China (China Unicom)
* Tianjin, China (China Mobile)
* Wenzhou, China (China Telecom)
* Wuhan, China (China Telecom)
* Xi'an, China (China Telecom)
* Zhengzhou, China (China Mobile)

This change took place on the 25th of July, 2022 at 16:00 UTC.

#### Endpoint Automated Session Tests Snapshots <a href="#endpoint-automated-session-tests-snapshots" id="endpoint-automated-session-tests-snapshots"></a>

Automated Session Tests from Endpoint Agents can now be included in Endpoint Snapshots. Together with Scheduled Tests, Browser Sessions, and Local Network, you will be able to save a snapshot carrying the necessary information related to the specific set of tests that you have defined. In addition, you can still define the data range, the anonymization of the data that identifies users, and whether you want to generate the link to share it with third-parties.

#### Endpoint Agent NPCAP Library Upgrade to Version 1.55 <a href="#endpoint-agent-npcap-library-upgrade-to-version-1.55" id="endpoint-agent-npcap-library-upgrade-to-version-1.55"></a>

The NPCAP library on the Endpoint Agent client for Windows will be upgraded to version 1.55 on September 17, 2022. This library is required by users to leverage TCP network tests. The manual upgrade for testing is available now. You can learn more about this upgrade and how to test it

[here](https://docs.thousandeyes.com/product-documentation/global-vantage-points/endpoint-agents/installing/npcap-upgrade)

.

New Cloud Agents have been added to the following locations:

* Antwerp, Belgium (Proximus) (IPv4)
* Antwerp, Belgium (Proximus) (IPv6)
* Bangkok, Thailand (Alibaba ap-southeast-7)
* Gävle, Sweden (Azure swedencentral)
* Jakarta, Indonesia (AWS ap-southeast-3)
* Jersey City, NJ, USA (IPv4)
* Jersey City, NJ, USA (IPv6)
* Madrid, Spain (GCP europe-southwest1)
* Midlothian, TX, USA (GCP us-south1)
* Milan, Italy (GCP europe-west8)
* New Albany, OH, USA (GCP us-east5)
* Paris, France (GCP europe-west9)
* Phoenix, AZ, USA (Azure westus3)
* Santiago de Chile, Chile (GCP southamerica-west1)
* Seoul, South Korea (Alibaba ap-northeast-2)
* Tokyo, Japan (NTT) (IPv4)
* Tokyo, Japan (NTT) (IPv6)
* An issue was identified when migrating Endpoint labels to the new system. A small subset of customers had an additional set of labels created incorrectly. These labels were removed and did not cause any service impact.

#### Multi-Region Cloud Support <a href="#multi-region-cloud-support" id="multi-region-cloud-support"></a>

ThousandEyes is pleased to announce the general availability of our EU region data centers. With this release, customers based in the EMEA region will have the option to onboard to our EU region, which will enhance the performance, scalability, and resilience of the ThousandEyes platform, and allow customers to address any regulatory concerns they have that require SaaS or Cloud services to be based in the EU.

If you would like to understand more about this announcement, see the

[Multi-Region Cloud Support](https://docs.thousandeyes.com/product-documentation/user-management/thousandeyes-multi-region-cloud-support)

documentation, or reach out to your account team's Customer Success Manager.

#### BrowserBot v2 Release Complete for All Cloud and Enterprise Agents <a href="#browserbot-v2-release-complete-for-all-cloud-and-enterprise-agents" id="browserbot-v2-release-complete-for-all-cloud-and-enterprise-agents"></a>

All BrowserBot agents with auto-upgrade enabled have been upgraded to version 2.5.7+ to leverage the new BrowserBot containerized architecture that uses Podman. This improves security and sets the foundation for future browser test capabilities.

As mentioned in the

[November 2021 Release Notes](https://docs.thousandeyes.com/archived-release-notes/2021/2021-11-release-notes#deprecated-features)

, the **keep browser cache between tests** option has been removed, and these page load and transaction tests will reset the browser cache between all browser test rounds. This option is no longer available from the **Agent Settings** page, in BrowserBot starting from v2, and is no longer functional via the API.

Amazon Linux 2 will also no longer be supported by BrowserBot starting with v2 onwards.

#### Dashboard and Reports Parity Now Available <a href="#dashboard-and-reports-parity-now-available" id="dashboard-and-reports-parity-now-available"></a>

We have added several new features to our dashboard page in order to ensure parity between our dashboard and reports objects, with the goal of de-commissioning our reports page entirely in 30 days. All of your existing reports will now be available in the dashboard page and we strongly encourage you to stop using reports and only use dashboards moving forward.

For parity's sake, with our dashboards, you can now:

1.  1\.

    Download your dashboard and widget data into a CSV or as a PDF.
2.  2\.

    Create or schedule a snapshot of your dashboards.
3.  3\.

    Save an individual widget as an image.
4.  4\.

    Add a detailed description to a dashboard in the administration page of the dashboard.
5.  5\.

    View and edit all of your existing reports in the dashboard page.

We have also added a few new features as we work towards merging the two objects:

1.  1\.

    We have updated our dashboard selector to now match the look and feel of our test selector. You can better filter based on sharing permissions and built-in dashboards.
2.  2\.

    You can now override the individual widget time selections and apply a consistent time selection to all widgets in a dashboard.
3.  3\.

    We have added a spinning timer to let you know when your data will be refreshed.

Note that the live action dashboard widgets (alert list, alert grid, test table, and agent status) cannot be viewed in a fixed timespan. Additionally, the test table widget will always only display data on a 12-hour running period, the alert grid widget will always only show data on a 24-hour running period, and the agent status widget will always show a live status of the agents displayed.

#### New Endpoint Agent Reinstallation <a href="#new-endpoint-agent-reinstallation" id="new-endpoint-agent-reinstallation"></a>

Previously, when you reinstalled an Endpoint Agent on a device, the agent was registered as an entirely new agent in ThousandEyes. As a result, apart from perhaps seeing agents with duplicate names, you also had their data disjointed between the new and the old agent, making it very difficult to correlate the historical data between them.

With the new reinstallation key included in the agent installation process, ThousandEyes will automatically check whether there is an existing agent with the same hostname, and consolidate their data into a single one. The detailed reinstallation procedure can be found

[here](https://docs.thousandeyes.com/product-documentation/global-vantage-points/endpoint-agents/installing/re-install-the-endpoint-agent)

.

#### Agent Interfaces Information Now Available in the Endpoint API <a href="#agent-interfaces-information-now-available-in-the-endpoint-api" id="agent-interfaces-information-now-available-in-the-endpoint-api"></a>

The Endpoint API now includes all the agent interfaces' information in the Endpoint Agent API endpoints. In particular, you can now obtain all the available information that ThousandEyes has about the agent interfaces (for example, interface name, IP address, gateway, link speed, BSSID, SSID, and PHY mode).

New Cloud Agents have been added to the following locations:

* Liege, Belgium (Proximus)
* Liege, Belgium (Proximus) (IPv6)
* Mumbai, India (Vodafone Idea)
* Mumbai, India (Vodafone Idea) (IPv6)
* An issue was found that was resetting the **Assigned Agents (24h)** field in the **Test Settings** page from the Endpoint dashboard when a scheduled test was saved. The issue has been resolved and the field now shows the correct value.
* An issue was found where changing between nodes that were labelled with **IP Address** and **ASN** would not immediately take effect in the path visualization of the Endpoint Views dashboard. This has been resolved.
* An issue was found where we were incorrectly showing a 24 hour timespan in our report download PDFs, even though the data represented was for a different timespan. This was a simple header mistake, as the data was showing correctly based on the desired configuration, and has been resolved.
* An error in our v6 reports API was sending an incorrect value for **dataComponentID** in our response. This lead to customers then requesting the incorrect **dataComponentID** and receiving a 404 response from our API. This issue has been resolved.
* An issue that was incorrectly showing the alert severity of some Endpoint alert rules as _Info_, even though they were assigned different severity values in their alert rule configuration, has been resolved.

We are happy to announce general availability of our new custom webhooks feature! You can find custom webhooks under the **Alerts > Integrations** menu. With custom webhooks, you can

* Ingest our alert webhook into any third-party system that supports incoming webhooks, including Cisco Webex, Microsoft Teams, and Splunk.
* Define the structure of the webhook payload to your liking, including fully customizable headers, URL query parameters, and JSON payload.
* Add static key : value pairs or dynamic variables based on your needs to any portion of the webhook payload.

This feature is currently available only for our Cloud and Enterprise Agent alerts and only supported via the ThousandEyes UI. API and additional alert type support will come in the near future. You can read more about this feature in our

[documentation](https://docs.thousandeyes.com/product-documentation/alerts/integrations/webhooks/custom-webhooks)

.

#### BrowserBot v2.6 Release - Upgrading Chromium to v97 <a href="#browserbot-v2.6-release-upgrading-chromium-to-v97" id="browserbot-v2.6-release-upgrading-chromium-to-v97"></a>

BrowserBot v2.6.0+ provides an upgrade to the Chrome browser used in the BrowserBot agent to run page load and transaction tests.

With the conclusion of the

[BrowserBot Early Track Program](https://docs.thousandeyes.com/whats-new/changelog#browserbot-early-track-program)

, all BrowserBot agents are being upgraded to v2.6+ with Chromium v97, quickly followed by an upgrade to the Recorder IDE. This change will improve IDE stability for macOS devices, and will enable additional features for browser tests from Chrome.

We've identified 3 edge cases where the scripting syntax has changed between Chromium v80 (prior to BrowserBot v2.6.0) and Chromium v97 (BrowserBot v2.6.0 and after):

* After an iframe is destroyed, Selenium WebDriver will no longer switch to the default content automatically.
* HTML elements with an area of zero are no longer clickable.
* shadowRoot no longer returns a WebElement.

We have reached out to all identified customers affected by these script changes. Contact ThousandEyes Support if you need additional assistance.

#### Public Snapshots to be Deleted <a href="#public-snapshots-to-be-deleted" id="public-snapshots-to-be-deleted"></a>

Over the next few months, we will be removing access to public snapshots that were made available via link sharing and that have not been accessed in over 365 days. This is part of our broader strategy to ensure a strong security posture for our customers. You will still be able to access these snapshots in the ThousandEyes platform, just not via the publicly accessible URL. After this change, these snapshots will be accessible as private snapshots, under **Sharing > Saved Events**.

We also plan to eventually delete any public snapshots that have not been accessed in 365 days entirely from the platform. If you don't want public snapshots affected by this change to be auto-deleted, you should access them to reset the time count since last access.

Both of these changes will impact all test snapshots, Endpoint Agent snapshots, Internet Insights snapshots, device snapshots, and report snapshots that have link sharing enabled and are available via a public URL. There is no action required on your part. In the future, we will introduce the option for you to define, at the time of snapshot creation, how long you want the snapshot to be active.

#### Open Beta: Full Application Support for Auto-Detect Configuration for Endpoint Agents Using Automated Session Tests <a href="#open-beta-full-application-support-for-auto-detect-configuration-for-endpoint-agents-using-automated" id="open-beta-full-application-support-for-auto-detect-configuration-for-endpoint-agents-using-automated"></a>

The new auto-detect feature, currently in open Beta, now provides full support for all AST applications (i.e,. Webex, Zoom, and MS Teams).

Auto-detect is a new feature that allows you to automatically select the best configuration to monitor the selected application in ASTs, making the monitoring of applications with your Endpoint Agents much easier.

When configuring an automated session test within the **Endpoint Agents > Tests Settings** dashboard, you will now see an auto-detect option under **Protocol**, which will automatically select the most reachable protocol for the selected application.

In order for auto-detect configuration to work correctly, you must have the TCP driver installed.

#### Round-Robin Aware Utilization Rebalancing <a href="#round-robin-aware-utilization-rebalancing" id="round-robin-aware-utilization-rebalancing"></a>

We've made a change in how we rebalance tests in agent clusters when round-robin is enabled, to take into account test sub-intervals. This change improves the reliability of round-robin enabled tests and improves balancing of tests across agent clusters.

New Cloud Agents have been added to the following locations:

* Cordoba, Argentina (IPv6)
* Osaka, Japan (KDDI) (IPv4)
* Oskaka, Japan (KDDI) (IPv6)
* Seoul, South Korea (LG Telecom)
* Singapore (Singtel) (IPv6)
* An issue that affects agent-to-agent tests conducted from the ThousandEyes Virtual Appliance (TEVA) in environments where the originating agent has IPv6 disabled in the kernel has been resolved. This issue would have impacted any TEVAs deployed that had IPv6 disabled in the kernel at boot-time, but would not have impacted TEVAs that had no IPv6 interface available, where a fallback would have already occurred.
* We have added validation to both our classic and custom webhooks that prevents users from sending webhooks to private IP addresses.
