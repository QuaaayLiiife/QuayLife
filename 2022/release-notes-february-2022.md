# Release Notes: February 2022

* In order to improve our user experience, the drag icon and the administrative icons on dashboard and report widgets are now only displayed on hover, instead of by default. Additionally, customers can now tab through the administrative icons with keyboard controls.
* In **Endpoint Agents > Agent Views**, when there is no agent to display, the "Getting Starting with Endpoint Agents" page is now displayed.
* For Endpoint Agent path visualization, in order to better represent an unknown number of hops between the penultimate node displayed in the pathtrace and the destination, we now display the following between the penultimate node and the destination:
  * **?** when the pathtrace reached the destination.
  * **x** when the pathtrace did not reach the destination.
* An issue was resolved that caused HTTP 500 errors to be thrown for a user when they tried to delete their default dashboard.
* An issue was resolved where the Endpoint Agent Browser Sessions view displayed a blank window when viewing agent-specific browser session data, rather than the relevant data for the agent accessing those websites.
* An issue was found in device-layer monitoring, where a device was submitting interface discard metrics, but was not unresponsive to device status calls that the Enterprise Agent was making to the device. This resulted in a discrepancy in Device Layer views where the interface discard metrics were displayed on the timeline, but not in the **Table** view. This has been resolved by allowing the interface metrics to be displayed in the table, but noting to users that the interface status is "Unknown".
* An issue has been resolved that caused some values to incorrectly show as "No Data" rather than "O" in Snapshot report widgets.
* An Endpoint Agent installation issue that prevented installation on macOS if Google Chrome or Microsoft Edge were not installed has been resolved.
* An issue was found where the "Go to views" option in the **Endpoint Agent > Test Settings** page was not displayed for users with the "Regular User" role. This has been resolved.
* An issue where an Endpoint Agent TCP test could show jitter and latency values despite 100% packet loss has been resolved. This occurred because in SACK mode, the round-trip times from the TCP handshake counted towards the reported latency values.
* An issue was resolved where dashboard and report widgets incorrectly showed no data when an agent label filter that only included Cloud Agents was selected.
* Several BGP alerts that were stuck in a triggered state due to stale BGP monitors have been cleared.

ThousandEyes now supports installing Enterprise Agents on Intel NUC 11 devices. For more information on installation processes and hardware requirements, see

[Installing a Physical Appliance](https://docs.thousandeyes.com/product-documentation/global-vantage-points/enterprise-agents/installing/installing-a-physical-appliance#intel-nuc)

.

**Intel NUC 8 No Longer Supported**

Intel NUC 8th generation and older devices are no longer supported. For assistance with upgrading, contact ThousandEyes Support.

#### Support for 100 KB Transaction Scripts <a href="#support-for-100-kb-transaction-scripts" id="support-for-100-kb-transaction-scripts"></a>

Transaction test users can now author scripts that are up to 100,000 characters long (approximately 100 KB). Previously the limit was 64,000 characters.

#### Report Server IPs for Connection Errors <a href="#report-server-ips-for-connection-errors" id="report-server-ips-for-connection-errors"></a>

ThousandEyes now reports server IPs in cases that observe HTTP failures during the TCP connection phase. Also, for failures detected at Layer 4, the server IP is set to the last attempted last IP. This IP can be one of following:

* the network test target URL
* or one of the IPs that failed to connect on the last redirect.

New Cloud Agents have been added to the following locations:

* Ahmedabad, India (JIO) (IPv6)
* Hyderabad, India (JIO) (IPv6)
* Wan Chai, Hong Kong (IPv6)
* For Endpoint Agent path visualization, in order to better represent an unknown number of hops between the penultimate node displayed in the path trace and the destination, we now display the following between the penultimate node and the destination:
  * **?** when the pathtrace reached the destination.
  * **x** when the pathtrace did not reach the destination.
* An issue was found in the Endpoint API where the pagination of result sets for user sessions was incorrect. This has now been fixed and made consistent with other data types.
* Fixed an issue where the Alerts API was not responding with the **Agent Name** in the Agent array section of the response.
