# Release Notes: June 2022

New Cloud Agents have been added to the following locations:

* Antwerp, Belgium (Telenet Belgacom)
* Antwerp, Belgium (Telenet Belgacom) (IPv6)
* Buffalo, New York, USA (IPv6)
* Liege, Belgium (Telenet Belgacom)
* Liege, Belgium (Telenet Belgacom) (IPv6)
* Sydney, Australia (Optus)
* Sydney, Australia (Optus) (IPv6)

#### New Alerter Engine for Network Outage Alerts <a href="#new-alerter-engine-for-network-outage-alerts" id="new-alerter-engine-for-network-outage-alerts"></a>

Internet Insights Network Outage alerts are being migrated to a new alerts engine, which is shared with Application Outage alerts. As part of the migration, the behavior of the Network Outage alerts `Affected Interfaces` condition will be updated to match the behavior of the Application Outages alerts `Affected Servers` condition (selecting a specific set of tests will filter but not reduce the size of the set of interfaces reported in the Network Outage alert).

#### Updated VMware Support for ThousandEyes Virtual Appliance <a href="#updated-vmware-support-for-thousandeyes-virtual-appliance" id="updated-vmware-support-for-thousandeyes-virtual-appliance"></a>

The OVF package included in the ThousandEyes Virtual Appliance has been updated to remove support for end-of-life releases of VMware ESXi and to update the OVF specified VM hardware version to version 13.

* Previously, ThousandEyes assumed that Internet Explorer was present by default on all Windows devices. This is no longer the case, and from Endpoint Agent client v1.119.0 and later, we now explicitly probe for this when displaying the supported browser icons on Windows OS.
* An issue was found where the incorrect assignment of network labels in Endpoint Agents resulted in tests not running as expected. This has been resolved.
* An issue was resolved that caused Endpoint Agents to be assigned the incorrect geolocation for a small set of IP addresses.
* An issue was found where some alert webhook payloads were not correctly sending test labels associated with the test that triggered an alert. This has been resolved.
* An issue was found with the ThousandEyes PagerDuty integration where the alert severity values were not correctly mapped to the PagerDuty `Severity` field. This has been resolved.
* Previously, Endpoint Agent users would see a mismatch between the millisecond value they selected in their Scheduled Test alert rule configuration versus what was being displayed in the UI. This was purely a visual bug, as the alert rule configuration was still capturing the correct millisecond value entered by the customer and alerting appropriately, and has been resolved.
* An issue that allowed the creation of Endpoint Agent labels with invalid machine IDs through the API has been resolved. Extra validation has been added in the API to make sure only consistent labels can be created.
* An issue where the Enterprise Agent repeatedly failed to run after being restarted, if there wasn't enough disk space available, has been resolved.

**Endpoint Agent Client v. 1.119.1 Bug Fixes**

* Previously, an issue resulted in Windows 11 devices being identified as Windows 10 by the Endpoint Agent client. This has been resolved.

#### Japanese Language Support <a href="#japanese-language-support" id="japanese-language-support"></a>

New Cloud Agents have been added to the following locations:

* Melbourne, Australia (Optus)
* Melbourne, Australia (Optus) (IPv6)
* Melbourne, Australia (Telstra)
* Melbourne, Australia (Telstra) (IPv6)
* Sydney, Australia (Telstra)
* Sydney, Australia (Telstra) (IPv6)

A new Webex Cloud Agent have been added to the following location:

* The visualization of Endpoint Agent Browsers Sessions when the visited page is cached has been improved. It will now explicitly show that the connection was cached in the page details and, as a result, the path visualization won't show any network nodes (for example, **Connection**, **VPN**, or **Proxy**) between the agent and the destination. This way, users will no longer be confused by seeing network metrics for requests that didn't go through the network.
* Enterprise Agents will now report the underlying ICMP error when agents are unable to connect in agent to agent tests.
* An issue that was not allowing customers to define Endpoint Agent HTTP server tests with **Customer Headers** longer than 1024 characters has been resolved. The limit has been extended and up to 3000 characters is now supported.
* An issue was found where Endpoint Agent labels could not be created or updated if they contained non-latin characters. This issue has been resolved, and non-latin characters can be used as expected.
* An issue was found with the **endpoint-data/user-sessions** API endpoint where it was provided with a "pages\[next]" element when no more data was available. This has been resolved.
* An issue has been resolved where log messages were not generated in the activity log when Endpoint Agent scheduled tests were modified by internal operations (for example, tests being disabled as there were no agents associated with it).
