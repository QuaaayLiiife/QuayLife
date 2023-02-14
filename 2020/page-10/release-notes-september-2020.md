# Release Notes: September 2020

#### Infrastructure Relocation and Customer Impact <a href="#infrastructure-relocation-and-customer-impact" id="infrastructure-relocation-and-customer-impact"></a>

By the end of the fourth quarter of 2020, ThousandEyes will complete a relocation of our infrastructure to Amazon Web Services. Some ThousandEyes customers have access control lists (ACLs) or firewall rules which permit Enterprise Agents, Endpoint Agents or other resources to communicate specifically with the ThousandEyes infrastructure. These ACLs/rules will need to be updated with new IP addresses.

Customers who use such ACLs or rules should watch this changelog for future instructions on updating their rules. Additionally, each customer's account mangagement team will will reach out to ensure a smooth transition. In the meantime, feel free to contact

ThousandEyes Customer Engineering

with questions or concerns.

ThousandEyes uses publicly available BGP monitors to provide data for our BGP tests. To achieve a higher granularity of visibility, we have increased the number of public monitor vantage points accessible for tests to 80. For more information on public BGP monitor data and route view collectors, see

[Working with Raw BGP Data](https://github.com/thousandeyes/docs/blob/prod/product-documentation/advanced-troubleshooting/working-with-raw-bgp-data.md)

.

#### Internet Insights Filter Improvements <a href="#internet-insights-filter-improvements" id="internet-insights-filter-improvements"></a>

Several updates have been made to the Internet Insights filters:

* Users can now filter by server location and server prefix, in addition to the existing interface location and interface IP address filters.
* Filters are now applied at an affected interface level, rather than at an outage level.
* A topology filter has been added for the **Server Location** to allow users to filter the topology view by location (for example, by country).

In addition, the **Add a filter** menu has been reorganized to clarify the following options:

* The **Affected Interfaces**, **Destinations**, and **Other** sections are now the **Network**, **Application**, and **Outage** sections respectively.
* The **In Catalog** option has been removed.
* The default outages filter is now **Outage Scope**, and listed under **Outages**.
* The **Catalog Provider** filter has been renamed **Affected Provider**.
* The **Location** and **IP Address** filters in the **Network** section have been renamed as **Interface Location** and **Interface IP Address** to distinguish them from the new server location and server prefix options.
* The **Affected Test** filter has been moved to the **Application** section.
* The **Domain** and **Network** sections have been renamed **Affected Hostname/Domain** and **Server Network** respectively.

Existing snapshots have been updated to include the new filter options and functionality. Depending on the filters selected in the existing snapshot, views may appear to be more narrowly scoped due to interface-level filtering, but the snapshot data is unchanged.

The voice call test type has now been removed. Voice call tests can be migrated to separate SIP and RTP tests without incurring additional unit consumption. For more information about SIP and RTP test configuration, see

[SIP Server Test Settings](https://github.com/thousandeyes/docs/blob/prod/product-documentation/tests/sip-server-test-settings.md)

and

[RTP Stream Test Settings](https://github.com/thousandeyes/docs/blob/prod/product-documentation/tests/rtp-stream-test-settings.md)

. Contact Support for more information.

* An issue was found after adding the render limit pop up notification to reports and dashboard widgets, where if both the render limit notification and the existing BGP size notification were triggered, only one would display. This has been resolved.
* Previously, the Service Now alert integration was incorrectly avaiable for all alert types. This has been corrected, and the alert integration is only visible for the supported alert types: Cloud and Enterprise Agent, BGP, Endpoint, and Internet Insights.

#### Red Hat Enterprise Linux and CentOS 8.x Support <a href="#red-hat-enterprise-linux-and-centos-8.x-support" id="red-hat-enterprise-linux-and-centos-8.x-support"></a>

ThousandEyes now supports installing Enterprise Agents on Red Hat Enterprise Linux (RHEL) and CentOS 8.1+ operating systems.

#### Upgrade to Embedded Widget ID Security <a href="#upgrade-to-embedded-widget-id-security" id="upgrade-to-embedded-widget-id-security"></a>

ThousandEyes has replaced the existing ten-character key that identifies an embedded widget with a 128-bit universally unique identifier (UUID). This change was made to provide additional security to our embedded report and dashboard widgets, and will impact all widgets created from this update onwards.

Existing embedded widgets will not be impacted by the change.

To update an existing widget to use a 128-bit UUID, uncheck the "Allow anyone to embed this widget to external sites" checkbox on the widget's configuration panel, and then re-check it.

#### Platform Health Announcement Updates and status.thousandeyes.com <a href="#platform-health-announcement-updates-and-status.thousandeyes.com" id="platform-health-announcement-updates-and-status.thousandeyes.com"></a>

ThousandEyes platform health announcements through **https://success.thousandeyes.com** will be discontinued on October 15th, 2020. Future health and maintenance announcements will all be made through the new

[https://status.thousandeyes.com](https://status.thousandeyes.com/)

site.

#### Endpoint Agent Data Render Limit for Reports and Dashboards <a href="#endpoint-agent-data-render-limit-for-reports-and-dashboards" id="endpoint-agent-data-render-limit-for-reports-and-dashboards"></a>

To improve performance when a report or dashboard widget is created with a large Endpoint Agent data set (either due to no applied filters or too large of a time span), users are now asked to either apply an endpoint test filter or reduce the time span in order to render the data.

This change impacts existing widgets as well as new widgets, but it does not impact existing snapshots.

* An issue was found in the Browser Sessions Network view where the domain filter drop-down menu incorrectly opens when clicking on a destination domain that has been grouped by domain. This has been resolved.
* An issue was found where the path visualization for an Endpoint Agent scheduled test displayed inconsistent data compared to other views. This has been resolved.
* The Endpoint Agent ping test timeout has been increased from 11 seconds to 15 seconds to resolve a couple of edge cases.
* Several edge cases were found that prevented Endpoint Agents from terminating when requested. These have been resolved.
* An issue was found where changing a Map widget to display in two columns instead of one distorted the widget configuration panel. This has been resolved.
* Previously, users that entered multiple domains when configuring DNS alert rules did not receive an error message if they used an unsupported delimiter. This has been resolved, and customers can now use space and comma delimiters when entering values into the following alert conditions: OriginAsn, NextHopAsn, Prefix, BgpHopAnyAsn, DnsMapping, Domain, ASN, IP, RDNS, and TargetIP.
* An issue was found where the platform treated the same domain name as two separate domains if the capitalization was different. This has been fixed, and capitalization no longer impacts the domain name.

#### Headless Mode for BrowserBot Chromium Browser <a href="#headless-mode-for-browserbot-chromium-browser" id="headless-mode-for-browserbot-chromium-browser"></a>

ThousandEyes' BrowserBot now runs its Chromium browser in headless mode for page load, transaction (classic), and transaction tests. This change was made to remove the dependency on an X11 server and reduce resource utilization on Cloud and Enterprise Agents. In addition, the Chromium browser will now be restarted between test rounds, rather than BrowserBot attempting to reuse the same browser instance across multiple test rounds.

Two test configurations will still result in Chromium launching the browser without headless mode:

* Kerberos is used for HTTP authentication.
* A PAC script URL is used for proxy configuration.

All other configurations will run in headless mode.

A future release will remove te-browserbot's dependency on an X11 server. This release maintains the dependency, but transitions ownership of the X11 server from the te-browserbot package to te-xvfb (a new package added for this purpose). In future releases, te-xvfb will be an optional package.

While this change will not impact most users, two use-cases are known to be impacted:

*   Transaction scripts that use the "Switch to Next Tab" example will need to be updated:

    [switchToNextTab.js](https://github.com/thousandeyes/transaction-scripting-examples/blob/master/examples/switchToNextTab.js)

    ​
* Transaction scripts that use Chromium's in-browser PDF viewer will need to use **downloads.waitForDownload()** to have their script wait for the PDF download to complete.

#### Upload and Download for Transaction Tests <a href="#upload-and-download-for-transaction-tests" id="upload-and-download-for-transaction-tests"></a>

Transaction test users may now use a variety of functions that enable them to generate files for upload to applications under test, and to inspect the contents of files downloaded from the same location.

Users can now import an **uploads** library from the **thousandeyes** module and use the following functions:

* **uploads.generateFile(filename, fileContents)**: Create a file with the given filename and contents, returning a path to the generated file.
* **uploads.generateRandomTextFile(sizeInBytes, filename)**: Create a file of the given size with the given filename, returning a path to the generated file. The generated file will be filled with randomly-generated alphanumeric characters.
* **uploads.generateRandomBinaryFile(sizeInBytes, filename)**: Create a file of the given size with the given filename, returning a path to the generated file. The generated file will be filled with randomly-generated bytes.

Users can import **downloads** from **thousandeyes** and use the following functions:

* **downloads.waitForDownload(filename)**: Return the path of a downloaded file once the download is complete.
* **downloads.getContents(path)**: Return the contents of the specified downloaded file's path.
* **downloads.getSize(path)**: Return the size of the specified downloaded file's path.
* **downloads.getMD5(path)**, **downloads.getSHA1(path)**, and **downloads.getSHA256(path)**: Return the hash of the specified downloaded file's contents.
* **downloads.getPdfTextContents(path)**: Extract all text from a downloaded PDF file. Customers may use this to verify that the contents of a downloaded PDF file match their expectations.

The AppDynamics integration has been updated to provide a more intuitive user experience. We have updated the **AppDynamics Instance URL** field to specify that we are looking for **protocol://hostname:\[port]**, and have added input validation to this field to strip out any unnecessary information. Additionally, we have added a direct link to our AppDynamics integration documentation to the form itself.

* ThousandEyes UI users can now configure whether they want the HTTP layer of page load tests to follow redirects. Previously, this setting was only configurable via the API.
* Calling **markers.start("x")** twice with the same marker value will now cause transaction tests to throw an error.
* Transaction test scripts can now `import { test } from 'thousandeyes'` and call `test.getSettings()` to obtain an object containing certain test settings, including:
  * **timeout**: The test's timeout in seconds.
  * **interval**: The test's interval in seconds.
  * **url**: The test's target URL.
  * **proxy**: An object describing the test's proxy settings.
* Transaction test scripts can now `import { agent } from 'thousandeyes'` and call `agent.getInfo()` to obtain an object describing the agent that is currently executing the script. This object includes the following parameters:
  * **agentName**: The agent's name.
  * **agentId**: A unique identifier for the physical agent.
  * **hostName**: The agent's hostname.
  * **ipAddress**: The agent's public IP address.
  * **isRunningInAgent**: Boolean value determining whether the script is running in the agent or the Recorder IDE.
* User agent strings and window sizes for HTTP, page load, and transaction tests have been updated to include modern and popular mobile devices.
* Added tooltips to describe the reasons why the Endpoint Agent experience score is not displayed when a metric is unavailable in the UI.
* 304 redirects are no longer shown as errors in the **Browser Sessions** view. They also display the **Cached** label in the **Entry Size** column, rather than a warning triangle icon.
* Probes directed at an Endpoint Agent VPN gateway are now sent out via a physical network interface (bypassing the virtual interface), to determine the nodes between the agent and the VPN gateway.
* An issue was found where the "DNS" timing of a request in the **Waterfall** view of page load and transaction tests was beeing added to the "Connect" timing instead. This has been resolved, and now a DNS lookup is only represented in the "DNS" timing.
* An issue was found where the VPN node in the path visualization for Endpoint Agents was not visible when the agent filter was removed. This has been corrected.
* In some cases, transaction tests were found to run longer than their configured timeouts without timing out. This has been resolved, and tests should timeout when intended.
* Previously, different criteria was used to filter out Endpoint Agent data points for the timeline and the round data of a scheduled test's network layer. This sometimes resulted in inconsistencies in the UI, and has been resolved.
* An issue was found where the metrics summary was occasionally not being updated when switching between rounds of data in Endpoint Agent views. This has been resolved.
* An issue was found where the ethernet link speed for very high-speed network interfaces (>= GBit/s network adapters) was incorrectly determined. This has been resolved.
