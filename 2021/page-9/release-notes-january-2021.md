# Release Notes: January 2021

#### Install Browser Extensions with the Endpoint Agent Installer <a href="#install-browser-extensions-with-the-endpoint-agent-installer" id="install-browser-extensions-with-the-endpoint-agent-installer"></a>

Endpoint Agent users can opt-in to install the Google Chrome and Microsoft Edge browser extensions alongside the Endpoint Agent, either:

If you opt not to install the extensions as part of the Endpoint Agent installer process, you can still install them separately. See

[Install the Browser Extension](https://docs.thousandeyes.com/product-documentation/endpoint-agent/install/install-the-browser-extension)

.

From April 2021, the installation of the Google Chrome and Microsoft Edge extensions will be automatic and will no longer be opt-in.

On the **Feature Selection** page of the installer wizard, open the drop-down menu for the desired extension, and select the relevant option.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-f60c0a4644da12016b2563326bae65c192644a79%2Fwhats-new\_changelog\_endpoint-installer-1.png?alt=media)

Users can install one or both of the extensions as necessary.

Once you have configured the extensions, click **Next** to continue the installation wizard.

To install the extensions via the command-line, add the relevant flags shown in the examples below:

* Google Chrome extension: `msiexec.exe /i <path_to_msi> /quiet /norestart ADDLOCAL="ChromeExtension"`
* Microsoft Edge extension: `msiexec.exe /i <path_to_msi> /quiet /norestart ADDLOCAL="EdgeExtension"`
* Both extensions: `msiexec.exe /i <path_to_msi> /quiet /norestart ADDLOCAL="ChromeExtension,EdgeExtension"`

An update has been made to the snapshot sharing modal. To generate a URL link for the snapshot, click the **Share** button:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-acdfbf8a6f00eecb69a2b440e716fbe3af45cc76%2Fwhats-new\_changelog\_sharing-snapshot-2.png?alt=media)

A URL link for the snapshot will then be generated:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-96aeb3b1412ba7af03f4b5e63e443beace86abed%2Fwhats-new\_changelog\_sharing-snapshot-1-2.png?alt=media)

New IPv6 Cloud Agents have been added to the following locations:

In addition, the Tokyo, Japan IPv6 Cloud Agent has a new provider (NTT).

* The Endpoint Agent error messages shown when the machine has connectivity issues or the wrong content-length header have been improved, and split into two more specific error messages:
* “Content-Length header is invalid or has been corrupted”.
* "The user’s internet connectivity was interrupted”.
* The timezone is now included in downloaded report PDFs to avoid timeline confusion.
* An error occurred where the clicking on **Show only this agent for entire view** in an Endpoint Agent scheduled test table would not activate the **Details for agent** state when switching to the **Map** tab. This has been fixed.
* An error was found where the Endpoint Agent would stop listening for the response to ping messages for a few milliseconds before the ICMP response was received. This issue has been resolved.
* Previously, targets without RDNS entries would incorrectly be resolved to their authoritative server's name. These targets are now only displayed as IP addresses.
* An issue was fixed where the **DOM Load Time** metric for transaction tests was incidentally showing pages with 0 data points.
* An issue occurred where incorrect color coding was used in agent to agent tests, resulting in available metrics appearing to be unavailable. This has been resolved.

Multi-service views allow ThousandEyes users to build a more comprehensive view of their environment by combining multiple test views into one multi-service view. For more information, see

[Multi-Service Views](https://docs.thousandeyes.com/product-documentation/tests/multi-service-views)

.

#### Device Layer RFC 7860 Support <a href="#device-layer-rfc-7860-support" id="device-layer-rfc-7860-support"></a>

The SNMPv3 authentication protocol options for device credentials have been expanded to include support for RFC 7860 protocols:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-480ab68b1b770aed5a334277ccf8a94bb85b9d52%2Fwhats-new\_changelog\_rfc-7860-1.png?alt=media)

#### Resolved Outdated BGP Alerts <a href="#resolved-outdated-bgp-alerts" id="resolved-outdated-bgp-alerts"></a>

In October 2020, ThousandEyes migrated backend BGP services. Some BGP alerts that were active during this migration failed to resolve.

Active BGP alerts created on or before 2020-10-20 will be resolved by the ThousandEyes operations team. Resolved alerts will still appear within an account group's alert history. If the post resolution state of a BGP test triggers an assigned alert rule, a new alert will be created.

#### API Support for Interface Selection <a href="#api-support-for-interface-selection" id="api-support-for-interface-selection"></a>

Tests can now be created, updated, and deleted with the `sourceIPAddress` attribute for Endpoint Agent interface selection via the API. The `sourceIPAddress` attribute can be specified in the "Agents" list to define a particular sourceIPAddress to be used.

New Cloud Agents have been added to the following locations:

* Cape Town, South Africa (AWS af-south-1) (IPv4)
* Spokane, WA (IPv4 and IPv6)
* Two minor enhancements have been made to how the installation status of an Endpoint Agent browser extension is displayed:
  * Previously, only one extension was considered when returning filter results. Now, all extensions are checked when filtering by browser extension status.
  * The **Not installed** status now denotes that at least one supported browser does not have a ThousandEyes extension installed (this includes instances where no supported browsers are installed).
* The headers for some page elements in the Endpoint Agent **Browser Sessions > Waterfall** view were found to be missing, and have now been restored.
* An issue was found where the UI hint text stated that Endpoint Agents could be searched for on the **Agent Settings** page by both the agent name and the hostname. This was incorrect, as only the agent name was considered by the search function. This has been fixed, and users can now search by either agent name or hostname as expected.
* A display issue that caused some Endpoint Agent path visualization nodes to be displayed backwards (from right to left) has been resolved.
* An issue was found where the minimum path MTU in the path visualization agent tooltip was inaccurately shown as "-1". This has been resolved.
