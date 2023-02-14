# Endpoint Agents

The ThousandEyes Endpoint Agent is an application that is installed on Windows or macOS machines to collect network- and application-layer performance data when users access specific websites from within monitored networks.

### Introduction to Endpoint Agents <a href="#introduction-to-endpoint-agents" id="introduction-to-endpoint-agents"></a>

Endpoint Agents allow customers to leverage regular end-user desktops and laptops as test devices for measuring internal and external application performance. As Endpoint Agents can be deployed on and off-premise to readily available machines in any location or network, performance measurements can be run from almost every possible user environment.

Deploying Endpoints gives you the ability to identify and diagnose end-user issues in near real-time. Unlike

[Enterprise Agents](https://docs.thousandeyes.com/product-documentation/thousandeyes-basics/working-with-agent-settings)

, Endpoint Agents run natively on Windows and Mac OSX operating systems and can be deployed on mass using standard automated deployment tools. Figure 1 below shows a typical example of deployment locations for Endpoint,

[Enterprise](https://docs.thousandeyes.com/product-documentation/thousandeyes-basics/working-with-agent-settings)

and

[Cloud](https://www.thousandeyes.com/product/cloud-agents)

Agents.

**Figure 1. Example Endpoint, Enterprise and Cloud Agent deployment locations**

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-1cb589604132ba6f6e71baa20dd25d293ef7527e%2Fproduct-documentation\_endpoint-agent\_getting-started-with-endpoint-agent-1.jpg?alt=media)

Endpoint Agents include the following features that are responsible for measuring the application performance:

* **Scheduled Tests** - Scheduled tests run from Endpoint Agents at regularly scheduled intervals. These tests run withour user interaction and can be deployed on Network (agent-to-server tests) and Web (HTTP server tests) layers.
* **Automated Session Tests** - Automated Session Tests are similar to Scheduled Tests but, in addition they allow you to configure an Endpoint Agent to dynamically create tests to IP addresses and ports it detects, when an application opens a connection.
* **Browser Sessions** - Endpoint Agents record in-browser and network performance metrics whenever users navigate to monitored domains from monitored networks.
* **Network Access** - This feature records the performance of the Endpoint's physical wired or wireless connections, gateways, VPNs, proxies, and DNS servers.

You have full control of when and under what conditions the tests (scheduled and automated session) run or Browser Sessions are recorded. For example, a Scheduled Test deployed to a laptop can be switched on or off as it (the laptop) transits through different locations, wireless and wired networks, VPNs and proxies. Similarly, the Browser Session recordings will only occur when the Endpoint Agent is on a specified network and also limited by configured target domains.

All the collected data and metrics are displayed in one intuitive

[Endpoint Agent > Views](https://app.thousandeyes.com/view/endpoint-agent)

page. The Views page separates Scheduled Tests, Automated Session Tests, Browser Sessions and Network Access data by layers and the interactive timeline presents performance data that can be used to rapidly search through historical data. An example of the Views page, the interactive timeline, layers, metrics and filters can be seen in Figure 2 below. With your Endpoint Agent data you can create proactive alerts, email regular feature-rich reports and create highly customizable dashboards. All Endpoint Agent data is available via our

[API](https://developer.thousandeyes.com/v6/endpoint/)

.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-48dbcc4cf700f879149f743a20ee7f55d81d2c02%2Fproduct-documentation\_endpoint-agent\_getting-started-with-endpoint-agent-2.png?alt=media)

There are two types of Endpoint Agents: **Endpoint Agent** and **Endpoint Agent Pulse**. The key difference between the two is that Endpoint Agent Pulse does not include the browser sessions feature. Throughout this article and the subsequent articles, all topics discussed apply to both products unless explicitly mentioned.

This article further explains: where and how to deploy Endpoint Agents, configuration options, how to run tests, end-user tools and experience, how to navigate your way through the UI and the layers of test views, how to create reports and dashboards, how to troubleshoot deployments and operations, managing licenses, user permissions and much more.

### Deploying Endpoint Agents <a href="#deploying-endpoint-agents" id="deploying-endpoint-agents"></a>

Typically, organizations have multiple teams that manage their IT estate so to assist in the deployment and planning stages and to ensure the right teams are involved do check the

[pre-deployment requirements](<../../.gitbook/assets/system requirements>)

. It’s important the teams who manage functions such as software deployments, end-user access control, VPN-access, proxies and anti-virus systems are involved as early as possible, so the Endpoint deployment runs smoothly. Use the following links for detailed instructions on how to install Endpoint Agents.

### Endpoint HTTP proxy support <a href="#endpoint-http-proxy-support" id="endpoint-http-proxy-support"></a>

We currently support the use of HTTP proxies for both types of Endpoint Agents. If you need HTTPS proxy support please contact our

[Customer Engineering Team](https://docs.thousandeyes.com/product-documentation/getting-started/getting-support-from-thousandeyes)

. The network performance from an Endpoint Agent to a proxy will be automatically measured during **Scheduled Tests** or **Browser Sessions** recordings. The network performance tests consist of a hop-by-hop path trace and end-end latency, loss and jitter tests. Network tests are unable to reach the final target when a proxy is in use (Figure 3 below shows a proxy in use and the Network layer tests unable to reach the final target), therefore, all network tests are performed to the proxy instead. If you need network layer performance measurements beyond a proxy then please reach out to the

[Customer Engineering Team](https://docs.thousandeyes.com/product-documentation/getting-started/getting-support-from-thousandeyes)

for assistance.

The proxy used by Browser Sessions is not configurable but automatically detected from the host system. See Figures 3 and 4 below for examples of how we present proxy data.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-f1cf25d36b05c2aec0600d36a42aaa8c992b876b%2Fproduct-documentation\_endpoint-agent\_getting-started-with-endpoint-agent-3.png?alt=media)

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-21dff702a470b4f8cb31954601bb1331b67b89cf%2Fproduct-documentation\_endpoint-agent\_getting-started-with-endpoint-agent-4.png?alt=media)

You can configure and store multiple proxy configurations and apply them to all tests or set a unique per test proxy. The proxy configuration supports static assignments, PAC files and Basic and NTLM proxy authentication methods. To apply a saved proxy configuration for all scheduled tests use the settings on the

[Endpoint Agent > Agent Settings](https://app.thousandeyes.com/endpoint/agent-settings/?section=proxies)

page or for a per test proxy scenario apply a proxy configuration on the

[Endpoint Agent > Test Settings](https://app.thousandeyes.com/endpoint/test-settings/?tab=tests)

page. This was mentioned previously but as a reminder here it is again: we currently only support HTTP proxies and if you need to use Endpoint with an HTTPS proxy get in touch with our

[Customer Engineering Team](https://docs.thousandeyes.com/product-documentation/getting-started/getting-support-from-thousandeyes)

for further assistance.

For detailed instructions on proxy configurations and options see the

[Proxy Configuration](https://docs.thousandeyes.com/product-documentation/endpoint-agent/endpoint-agent-proxy-configuration-for-scheduled-tests)

article. For more details on how to navigate through the Views page to see your proxy measurements head to the Test, Browser Sessions and Network Access Views and metrics section.

We usually ship Endpoint Agent updates every 2 weeks for both the Windows and Mac OSX operating systems. The Endpoint applications have auto-update process that runs at regular intervals to check, download and install package updates. The Chrome browser extension automatically updates whenever a new Endpoint version is published in the Chrome Store. For full details on how the Endpoint Agent update process works see the

[How does the Endpoint Agent work](https://docs.thousandeyes.com/product-documentation/endpoint-agent/how-does-the-endpoint-agent-work)

article.

### Endpoint Agent permissions <a href="#endpoint-agent-permissions" id="endpoint-agent-permissions"></a>

We have several Endpoint related permissions for user and user group management. For full details on how to create custom roles with Endpoint permissions see the

[Role-based Access Control](https://docs.thousandeyes.com/product-documentation/user-management/role-based-access-control-explained)

article.

With the Endpoint Agent licensing model there is no distinction between the two agent types: A single Endpoint Agent license can be used to deploy an Endpoint Enterprise or an Endpoint Pulse Agent.

An Endpoint Agent license allows you to use all Endpoint Agent features such as scheduled tests and browser sessions. All trial accounts receive 25 licenses by default, whereas prepaid organizations must purchase licenses to access the Endpoint Agent.

Endpoint Agents consume licenses upon registration (first run after the installation) into the ThousandEyes platform. If you reach your license limit, all subsequent Endpoint Agents registered are shown as disabled on the

[Endpoint Agents > Agent Settings](https://app.thousandeyes.com/endpoint/agent-settings/?section=agents)

page. The following section explains how to transfer and reclaim licenses. If you need your license plan modified, contact your ThousandEyes Account Manager or the

[Customer Engineering Team](https://docs.thousandeyes.com/product-documentation/getting-started/getting-support-from-thousandeyes)

for further assistance.

#### Viewing, transferring and re-claiming licenses <a href="#viewing-transferring-and-re-claiming-licenses" id="viewing-transferring-and-re-claiming-licenses"></a>

Endpoint Agent licenses are assigned to the organization and can be transferred between your organizations' account-groups. The total number of licenses available in your Plan, Currently Active licenses and licenses used in each Account Group is shown in the Plan Usage, Endpoint Agent Licenses section on the

[Account Settings > Usage and Billing](https://app.thousandeyes.com/account-settings/usage-billing/?section=usage)

page. See Figure 5 below for an example of the Endpoint Agent licensing data shown on the

[Account Settings > Usage and Billing](https://app.thousandeyes.com/account-settings/usage-billing/?section=usage)

page.

To free up a license you can disable an Endpoint Agent or delete it. The **Currently Active** licenses shown on page

[Account Settings > Usage and Billing](https://app.thousandeyes.com/account-settings/usage-billing/?section=usage)

is a tally of all licenses used within a billing cycle. If you disable or delete an Endpoint Agent within a billing cycle the reduction of the **Currently Active** licenses will not appear until the following billing cycle. Removing the Endpoint Agent software package from an end-user machine will not free up a license until it is deleted from the

[Endpoint Agents > Agent Settings](https://app.thousandeyes.com/endpoint/agent-settings/?section=agents)

page.

You can

[automatically manage](<../../.gitbook/assets/manage endpoint agent settings>)

and handle the statuses of the agents to make the optimum use of the available license.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-c140cd33a9ebd2156255a500a034ab15ea5da543%2Fproduct-documentation\_endpoint-agent\_getting-started-with-endpoint-agent-5.png?alt=media)

### Introduction to the Endpoint Agent Capabilities <a href="#introduction-to-the-endpoint-agent-capabilities" id="introduction-to-the-endpoint-agent-capabilities"></a>

Endpoint Agent and Pulse both run web-layer HTTP-server and network-layer Agent-to-Server **Scheduled Tests** types, both test types are IPv4 and IPv6 compatible. Scheduled tests can run at set intervals from a minimum of 1 minute to a maximum of 1 hour. All scheduled tests perform network-layer end-end and path trace tests. If a proxy is being used the network layer tests will target the proxy and not the end target. Scheduled Tests can be configured to run several types of checks against your target e.g. verify SSL, page content or HTTP response codes.

Endpoint Agent in conjunction with its web-browser plugin can be configured to monitor end-users web Browser Sessions automatically or end-users can manually start recording their **Browser Sessions** using their browser extension. When recording Browser Sessions the agent will also perform network-layer end-end and path trace tests and collect Network Access data. For full details on scheduled test configuration options see the

[Creating Scheduled Tests on Endpoint Agents](https://docs.thousandeyes.com/product-documentation/endpoint-agent/creating-scheduled-tests-on-endpoint-agents)

article.

Automated Session Tests collect data from applications that are developed on Unified communications as a service (UCaaS) platform; for example, Webex or Zoom. These tests are dynamic in nature, so they execute only when a user uses an application on their device (therefore, the system and network resources utilization is optimal). The data collected from these tests can be used for troubleshooting issues faced by the user while using the application. For instructions on how to configure and manage the Automated Session Tests see the

[Configuring Automated Session](https://docs.thousandeyes.com/product-documentation/end-user-monitoring/automated-session-test/configure-automated-session-tests)

article.

**Endpoint Agent labels and test distribution and configuration**

Both Endpoint Agent and Endpoint Pulse can run a maximum of 10 Scheduled Tests at a time (however, you can assign more than 10 tests), so your total test capacity increases with the number of Endpoints deployed. You have two options to distribute tests to your Endpoint Agents and both options begin with creating an Agent Label. An Agent Label is simply a named group of Endpoint Agents that all share a common property such as a gateway device, wireless SSID, proxy address, subnet, agent name or IP address. The Agent Label is assigned to a test and as Endpoints match or un-match the label’s criteria the test will be added or removed from Endpoint Agents. The more dynamic the agent property used for the Agent Label criteria the greater the test distribution activity. Some Endpoint properties are static, so it is possible to create Agent Labels with no dynamic test distribution activity. If Endpoints do not check-in for 1 hour, they are removed from the agent label pool. You can learn more about configuring labels,

[here](<../../.gitbook/assets/configure endpoint agent labels>)

.

#### Browser Sessions and settings <a href="#browser-sessions-and-settings" id="browser-sessions-and-settings"></a>

Browser Sessions recordings can be started manually using the browser extension or configured to automatically collect data by specifying groups of Monitored Networks and Target Domains. There is no limit to the number of Browser Sessions you can record. For instructions on how to use the browser extension to manually record a Browser Session see the

[Endpoint Agent end-user experience](https://docs.thousandeyes.com/product-documentation/endpoint-agent/endpoint-agent-end-user-experience)

article and for instructions on configuring automatic Browser Sessions monitoring see the

[Configuring automatic data collection](<../../.gitbook/assets/configure monitored networks and domain sets>)

article.

The Network Access data can be used for troubleshooting errors seen in Browser Sessions recordings or it can be used to proactively track how your Endpoint Agents' local network services are performing. The Network Access layer has two parts, Network Topology and Wireless. Network Topology visualises the devices in use by Endpoint Agents for Browser Session recordings and Wireless displays a table of information about wireless data such as SSID, signal strength, channel and much more. Network Access data is continuously collected whilst an Endpoint Agent is online and on a configured monitored network (

[Browser Session Settings > Monitored Network](https://app.thousandeyes.com/endpoint/browser-session-settings/?section=networks)

). The devices in the Network Access topology include Endpoint Agents' gateway devices, DNS servers and proxy or VPN servers.

### Working with Endpoint Agent Views <a href="#working-with-endpoint-agent-views" id="working-with-endpoint-agent-views"></a>

The

[Endpoint Agent > Views](https://app.thousandeyes.com/view/endpoint-agent)

page has four layers: Scheduled Tests, Automated Session Tests, Browser Sessions, and Network Access. Each layer contains a menu of sub-layers, a timeline, options to display data in tables and data filters. Depending on the Views layer you have selected you also get geographical maps, network topology diagrams, path visualizations and sliders that scroll into view when table data is selected. There is a lot of information being presented in a very organized and easy to follow format. From the current moment in time, the timeline holds up to 31 days of data. If you wish to keep your data for longer than 31 days then you can run a regular Reports or you have the option to create

[Snapshots](https://docs.thousandeyes.com/product-documentation/tests/sharing-test-data)

. Snapshots let you share test data with anyone, regardless of whether they subscribe to the ThousandEyes platform or not.

The following sub-sections contain screenshots and article links, the articles explain how to navigate and leverage the features of the **Views** layers, for example they show you how to select tests, sift through the timeline, select metrics and what your metrics mean, apply filters (e.g. find data on an Endpoint Agent), find proxy performance data, check page load page waterfall data, use the path visualizations, check wireless strength and display session or Visited Page details.

*   Views -

    [Scheduled Tests](https://docs.thousandeyes.com/product-documentation/end-user-monitoring/viewing-data/endpoint-agent-scheduled-tests-view)

    : HTTP Server and Network type tests, Path Visualizations, Maps and Tables

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-103374182916f657683f7bc9701ba8f26e53d560%2Fproduct-documentation\_endpoint-agent\_getting-started-with-endpoint-agent-6.png?alt=media)

If a Visited Page and Session is selected a detailed slide-out window appears.

*   Views -

    [Browser Sessions > Sessions](https://docs.thousandeyes.com/product-documentation/end-user-monitoring/viewing-data/endpoint-agent-views-reference#sessions)

    : Web sessions recorded manually with the browser extension or automatically via a Monitored Network and Domain groupset.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-f8fa0e8eb4bc17e854997d4cb4a5033edf6fcc92%2Fproduct-documentation\_endpoint-agent\_getting-started-with-endpoint-agent-7.png?alt=media)

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-7f04d2c5abe4714d6dc5032e2f4ce01e9fc59223%2Fproduct-documentation\_endpoint-agent\_getting-started-with-endpoint-agent-8.png?alt=media)

**Views, Automated Session Tests**

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-4a45d7edf951ce49d2ded3bc2cc90ec1e21d221c%2Fproduct-documentation\_endpoint-agent\_getting-started-with-endpoint-agent-10.png?alt=media)

### Dashboards for Endpoint Data <a href="#dashboards-for-endpoint-data" id="dashboards-for-endpoint-data"></a>

Dashboards are simple to use and fully customizable to display your Endpoint Agent data in a style suited for your target audience. Dashboards also assist in running on-demand or scheduled to automatically generate reports at regular intervals. Check out these helpful articles on the topics below:

For your Scheduled Tests, you can customize your Alert Rules. Simply put, alerting is configured out of the box to alert you when you need information about tests which are failing. If you need to get more granular or change some of the notification rules, check out the

[How Alerts Work](https://docs.thousandeyes.com/product-documentation/alerts/how-alerts-work)

article for more information on fine-tuning and managing alerts.

You can access the API to consume the results and data captured by an Endpoint Agent. To know more about the Endpoint API articles, follow this

[link](https://developer.thousandeyes.com/v6/)

.

### Endpoint data collection and metrics <a href="#endpoint-data-collection-and-metrics" id="endpoint-data-collection-and-metrics"></a>

The

[Data collected by Endpoint Agent](https://docs.thousandeyes.com/product-documentation/endpoint-agent/data-collected-by-endpoint-agent)

article describes what data is generated and collected when running your Endpoint Agent, Scheduled Tests, Browser Sessions and by the Network Access layer.
