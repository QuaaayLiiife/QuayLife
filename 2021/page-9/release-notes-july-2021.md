# Release Notes: July 2021

#### Simple Install Flow Compliance for PagerDuty Integration <a href="#simple-install-flow-compliance-for-pagerduty-integration" id="simple-install-flow-compliance-for-pagerduty-integration"></a>

All PagerDuty integrations are now compliant with their updated "Simple Install Flow" method for authentication, which can be found here:

[Events Integration](https://developer.pagerduty.com/docs/app-integration-development/events-integration/)

.

This change will allow you to select multiple PagerDuty services to integrate with ThousandEyes. If multiple services are selected on the PagerDuty side, multiple integrations will be created on the ThousandEyes side.

#### Increased Number of Interfaces Supported Per Agent <a href="#increased-number-of-interfaces-supported-per-agent" id="increased-number-of-interfaces-supported-per-agent"></a>

Starting with this release, we have increased the per-agent limit for monitored interfaces to assist in the adoption of monitoring devices using SNMP.

Prior to this release, there was a limit of 4000 interfaces per agent. This required users to deploy additional agents to monitor more interfaces, and thereby more devices using the device layer. The new behavior increases the supported interfaces per agent to around 20,000. The exact number of interfaces supported per agent may depend on local network conditions, and users can leverage the agent utilization information that shows device utilization to gauge the ability to monitor additional interfaces.

* Previously, connection failures could occur when Endpoint Agent TCP network tests were run, because the proxy server port was not taken into account. This has been fixed in Endpoint Agent Client version 1.82.0.
* An issue was found where unexpected network traffic in Endpoint Agent TCP tests resulted in an erroneous calculation of impossibly long delay values from hop 0. This has been resolved in Endpoint Agent Client version 1.82.0 by dropping any incoming packet that we cannot match against a source packet.
* The "Exclude data from Cloud Agents with Local Problems" tooltip in reports and dashboards has been updated to no longer identify the specific agents that are having issues. A generic message is now provided. To view which agents are having issues, see the individual test view for information.
* Alert conditions now appear in alphabetical order when setting up an alert rule, rather than order of creation.
* An issue was found that prevented alerts from being shown correctly in the **Alert List** page. Some alerts were not showing any active location alerts, while some where not populating at all. This has been resolved.
* An issue was found that prevented certain alerts from clearing. This was caused by an ungraceful reset of the alerting platform. The impacted alerts have been cleared, and improvements have been made in order to prevent this from happening again.
* In some cases, the geolocation calculation of an Endpoint Agent could be overwritten by less reliable measurements of location. The accuracy of our calculations has been improved by ensuring we always preserve successful resolutions of RDNS to a specific location.
* An issue was found where Endpoint Agent snapshots with a filter could sometimes take longer to generate than the timeout period configured, resulting in the snapshot failing to be created. The timeout period has been extended to resolve this issue.
* An issue was found in the usage calculation for Endpoint Agent accounts where, when an account was using 0 agents, the usage page incorrectly displayed the last usage. This has been corrected, and 0 Endpoints is now displayed as expected.
* An issue was found in the permissions framework for Endpoint Agents that caused users with the 'View endpoint tests' permission but not the 'View tests' permission to be unable to view Endpoint tests. This has been resolved.

#### API Credentials No Longer Visible <a href="#api-credentials-no-longer-visible" id="api-credentials-no-longer-visible"></a>

As part of ThousandEyes' commitment to improving security within the product, the **OAuth** and **Access Token** fields are no longer visible within the User Profile. Token values are presented when they are initially created, but will not be available afterwards to protect the confidentiality of the information.

* As of Endpoint Agent client version 1.83.0, the Endpoint Agent has been tested and verified against the new Apple M1 chipset. Additionally, the browser extension for Chrome and Edge now declares support for the new mac/arm64 platform.
*   By default, browser extensions are now an opt-in feature during installation. Each extension must be explicitly mentioned in the **ADDLOCAL** section of the **msiexec** command. This change has been made to avoid clashes between the **ExtensionInstallForceList** set at the user-level by group policy versus the **ExtensionInstallForceList** set at the machine level set by the Endpoint Agent. Although multiple levels of policies can exist, Google Chrome only takes into account one policy. See

    [https://support.google.com/chrome/a/answer/9037717?hl=en](https://support.google.com/chrome/a/answer/9037717?hl=en)

    for further details, and

    [Endpoint Agent Installation Reference](https://docs.thousandeyes.com/product-documentation/global-vantage-points/endpoint-agents/installing/endpoint-agent-installation-reference)

    for installation details.

Existing installations of Endpoint Agent will not be affected, as upgrade installs respect the existing settings unless additional command line arguments are used.

* The Internet Insights default alert rule for outages has been renamed the **Default Network Outage Alert Rule**.

New Cloud Agents have been added to the following locations:

* Montevideo, Uruguay (IPv6)
* An issue was found where alerts were either not showing any active location alerts, or not populating at all, preventing them from being correctly displayed on the **Alert List** page. This has been resolved.
* In some rare cases, alert suppression windows would end prematurely, resulting in alerts firing during the intended suppression. This has been resolved.
* An issue was found where shared tests that had previously been disabled in the shared account were triggering alerts. This behavior has been corrected.
* An issue was found where assigning specific agents to a web-transaction test caused alerts to fail to trigger, even if the alert conditions were met. This has been resolved.
* An edge case was found when Cloud Agent vantage points were removed from tests that had an Internet Insights rule attached. In this case, a small subset of Cloud and Enterprise Agent alert rules were disassociated from the tests. This has been fixed.
* Previously, API queries to browser sessions data were not using the **userSessionIds** field correctly. This has been resolved.
* An issue was found in Endpoint Agent label filtering where the text string used was not filtering out all non-matching agents. After the fix, only agents matching the filter text will be displayed.
* In cases where there was an unknown path to a valid destination, the packet loss displayed in the Endpoint Agent path visualization was not consistent with that displayed in the map view. This has been corrected, and the two views now display the same value.
