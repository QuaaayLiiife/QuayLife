# Release Notes: November 2022

In preparation for providing support for using IPv6 for agent communication between Enterprise Agents and the ThousandEyes Cloud, we will be adding IPv6 addresses as new AAAA records to our existing public production endpoints.

For the ThousandEyes package repositories, IPv6 will be used on platforms that preference IPv6 if you have a dual-stack configuration. All other agent communications are controlled by a flag in the Enterprise Agent configuration and should not be disrupted.

#### Endpoint Agent ASN Support <a href="#endpoint-agent-asn-support" id="endpoint-agent-asn-support"></a>

ASN information is often very useful while troubleshooting a network issue. Having to look for the specific IP range related to a particular ISP always slows down all the network-related tasks. In order to make all these processes simpler, we have introduced support for ASN information in various parts of the Endpoint Agent:

* You can now filter agents by their ASN in the **Agent Settings** table. This way, you can identify the agents that are connecting from a specific ASN (ISP).
* Similar filtering has been added to agent labels. You can now associate a label with an ASN by searching for the AS by name or number.
* You can now filter test views by agent ASN, which lets you easily identify the test data that is specifically related to the agents associated with the ISP affected by the outage.
* Two new grouping options have been added to the **Path Visualization** tab. You can now group by both agent ASN and interface ASN, and identify whether an issue is related to a specific AS, as well as the affected agents.

#### Multi-Interface Support for Cisco Catalyst 9000 Switches <a href="#multi-interface-support-for-cisco-catalyst-9000-switches" id="multi-interface-support-for-cisco-catalyst-9000-switches"></a>

ThousandEyes now supports configuring multiple interfaces on Cisco Catalyst devices, allowing a single Cisco Enterprise Agent to access multiple virtual networks, instead of deploying separate agents for each virtual network. This will benefit the SD-WAN users who want to measure performance across each WAN circuit.

#### Content Subscription Updates <a href="#content-subscription-updates" id="content-subscription-updates"></a>

ThousandEyes has updated its content subscription categories for product documentation. All existing subscriptions will be transferred to the new categories, and no action is required from customers.

* New ThousandEyes Documentation

New Cloud Agents have been added to the following locations:

* Ahmedabad, India (Vodafone Idea)
* Ahmedabad, India (Vodafone Idea) (IPv6)
* Ashburn, VA (CenturyLink) (IPv6)
* Los Angeles, CA (Cox) (IPv6)
* Paris, France (Orange) (IPv6)
* Seattle, WA (CenturyLink) (IPv6)
* An issue that caused certain hover panels in Internet Insights to display beyond the edge of the screen has been resolved.
* Cloud and Enterprise Agents: Fixed an issue where agent proxy information was displayed incorrectly in **Views** when a proxy is not used.
* Cloud and Enterprise Agents: Fixed an issue in the API that prevented the **contentRegex** property from being reset to empty in an HTTP server test.
* Dashboard: Fixed an issue where the Color Grid widget was using the wrong scale colors for Endpoint Agent automated session tests.
* Enterprise Agents: An issue that prevented custom appliances from detecting network interfaces in NUC11 physical appliances has been resolved.
* Revenue Platform: Fixed an issue in the usage consumption calculator that showed inaccurate unit consumption that did not match what users saw when creating tests. This issue occurred specifically with agent-to-agent tests.
* Fixed an issue where alerts were triggered incorrectly during an active alert suppression window.
* An issue has been resolved that impacted the reliability of NAT traversal while executing agent-to-agent tests against Webex Cloud Agents.

#### New Advanced Settings for Page Load and Transaction Tests <a href="#new-advanced-settings-for-page-load-and-transaction-tests" id="new-advanced-settings-for-page-load-and-transaction-tests"></a>

Additional advanced settings have been added for configuring page load and transaction tests:

* **Exclude Domains and Object URLs:** Users can now block requests to specific domains and object URLs. This excludes objects that are not important to the performance of your web page, or ensure third party tracking software is unaffected by your browser synthetic tests.
* **Disable Screenshots:** Users can now disable screenshots in a test.
* **Set Browser Language:** You can now set the browser language for your page load and transaction tests to verify the various language versions of your website or application.
* **Set Page Loading Strategy:** Some transaction tests have high timeouts because they need to wait for large assets to load in the browser before the next synthetic action can take place. Users can now adjust the page loading strategy so that synthetic actions are not delayed by non-critical assets. This lowers both the total necessary timeout length needed, and the variability in transaction time metrics.
* **Emulate Microphone and Camera Input:** This feature allows you to emulate a camera and microphone for web applications that require camera/microphone input.
* **Allow Geolocation From Agent Vantage Point:** This feature provides the geolocation of your agent for applications that require geolocation input.
