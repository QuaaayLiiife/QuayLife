# Release Notes: February 2023

#### End of Installation Support for Ubuntu 18.04 LTS (“Bionic”) <a href="#end-of-installation-support-for-ubuntu-18.04-lts-bionic" id="end-of-installation-support-for-ubuntu-18.04-lts-bionic"></a>

Installation support for Ubuntu 18.04 LTS ("Bionic") has now ended. Updated images for the ThousandEyes Virtual Appliance (TEVA), Intel NUC, Raspberry Pi 4, and Docker for Linux have been released based on Ubuntu 20.04 LTS ("Focal"). We have also updated the custom appliance generation to utilize the newest images. From January 31st, 2023 onwards, you will see failures if you attempt to deploy new agents on Ubuntu 18.04 LTS. Please ensure you are using the latest images available for new agent deployments.

We expect to ship a pathway for customers to perform automated in-place upgrades from Ubuntu 18.04 LTS-based appliances to Ubuntu 20.04 LTS by the end of February 2023.

#### Endpoint Agent Client 1.150.1 <a href="#endpoint-agent-client-1.150.1" id="endpoint-agent-client-1.150.1"></a>

**TCP Tests Renamed and On By Default**

We have renamed "TCP Network Tests" to "Extended Network Tests" to better reflect both the current feature and future functionality.

In addition, as previously announced, the default Windows Installer (MSI package) will now include the Extended Network Tests (TCP Tests) by default. This option can be manually deselected during installations or removed with a switch. For more information on Endpoint Agent command line options, see

[Endpoint Agent Installation Reference](https://docs.thousandeyes.com/product-documentation/global-vantage-points/endpoint-agents/installing/endpoint-agent-installation-reference#command-line-options-for-msiexec-msiexec-switches)

.

#### ASN Endpoint Agent Information Available via the Endpoint API <a href="#asn-endpoint-agent-information-available-via-the-endpoint-api" id="asn-endpoint-agent-information-available-via-the-endpoint-api"></a>

The Endpoint API has been extended to include ASN information. Similar to the VPN data, users will now be able to get ASN information in the Agent Details and the Endpoint Test Data API endpoints.

This extension provides users with more information to, for example, identify the ISP a set of agents are connected to via the API. For more information, see the developer documentation related to

[Endpoint Agents](https://developer.thousandeyes.com/v6/endpoint\_agents/)

and

[Endpoint Test Data](https://developer.thousandeyes.com/v6/endpoint\_tests/)

.

The alert ID format was updated from a numeric value to a 128-bit UUID for both new and existing alerts.

This change affects how alerts are identified in the UI, particularly in the alert list and alert history pages. Additionally, the new UUID value will be displayed in the "id" field of APIs and can be used to search for alerts in place of the current "alertId" field.

The numeric ID value will remain visible in dashboards. This value can be used to search for alerts, and the results will contain alerts associated with the new UUID.

Browser session alerts do not currently support the UUID format, and will continue to display the numeric ID.

New Cloud Agents have been added to the following locations:

* Kuala Lumpur, Malaysia (Telekom Malaysia)
* Kuala Lumpur, Malaysia (Telekom Malaysia) (IPv6)
* Saskatoon, Canada (Saskatel)
* Saskatoon, Canada (Saskatel) (IPv6)
* Washington, DC, USA (IPv6)
* The ability to create new AppDynamics integrations and edit the existing AppDynamics integrations will no longer be available in the **Alert Rules** page. To create and edit the AppDynamics integration, use the **Alerts > Integrations** page.

**Agent Level SSL Setting for Browser Tests**

With the addition of the test level setting for SSL verification

[introduced in October, 2022](https://docs.thousandeyes.com/whats-new/changelog#2022-10-06)

, the agent level SSL verification setting has been removed.

* An issue that was preventing some embedded dashboard widgets from properly loading has been resolved.
* An issue was found where an incorrectly colored directional arrow for improving or worsening performance was displayed for some metrics in the test table widget. For example, when **Response Time** was increasing, an upward green arrow was displayed instead of an upward red arrow. This was caused by a bug in the UI, and has been resolved.
