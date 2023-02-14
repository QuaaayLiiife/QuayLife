# Release Notes: October 2020

The digital certificates for **app.thousandeyes.com** and **downloads.thousandeyes.com**, which were previously issued by the DigiCert certificate authority, will be replaced with certificates from the QuoVadis certificate authority on October 13th, 2020. The replacement certificates will use certificate chains with larger key lengths (4096 bits) than the current certificate chain (2048 bits).

Customers who access these servers with clients (browsers, file transfer utilities, custom programs) that use older cryptographic libraries which cannot support 4096-bit key lengths should update their clients. Customers who use supported browsers or other current clients do not need to take any action.

#### New ISP for Paris Cloud Agent <a href="#new-isp-for-paris-cloud-agent" id="new-isp-for-paris-cloud-agent"></a>

Due to a change in service provider, customers with tests assigned to the Cloud Agent in Paris, France will observe a corresponding change in path-visualization and source IP.

We do not anticipate downtime or impact on test performance. The Cloud Agent ID used within the ThousandEyes API will remain unchanged.

#### Cloud Agents with IPv6 Support <a href="#cloud-agents-with-ipv6-support" id="cloud-agents-with-ipv6-support"></a>

The following Cloud Agent locations now have IPv6 support:

You can now gather network data and path-visualization data about proxy servers.

In the past, if your target was behind a proxy, your ThousandEyes tests would not collect network data. Workarounds existed (adding the target to the proxy's bypass list, or creating separate agent-to-server tests to the proxy), but these were cumbersome to configure. And with the popularity of cloud proxy solutions such as Zscaler, Netskope, and Palo Alto Networks, you may want to understand network health to the cloud proxy.

With the ability to run network tests to the proxy, you can more easily correlate data between the application and network layers. The new ThousandEyes proxy capabilities allow you to see

* A visualization of the network path to the proxy

To explore the new proxy metrics:

1.  1\.

    Go to **Cloud & Enterprise Agents > Test Settings**.
2.  2\.

    Select or create an HTTP, page load, or transaction test.
3.  3\.

    On the **Advanced Settings** tab, find the **Proxy Settings** section.
4.  4\.

    Select **Perform network measurements to the proxy**.

    ​

    ![](https://github.com/thousandeyes/docs/blob/prod/.gitbook/assets/whats-new\_changelog\_proxy\_settings.png)

    ​

#### Endpoint Agent Support for VPN Metrics <a href="#endpoint-agent-support-for-vpn-metrics" id="endpoint-agent-support-for-vpn-metrics"></a>

Several improvements have been made to how Endpoint VPN data is visualized:

* VPN loss and VPN latency metrics have been added to the **Scheduled Tests**, **Browser Sessions**, and **Local Networks** views.
* The following filters have been added to Endpoint Agent Settings and Endpoint Agent labels:
  * VPN Vendor: The VPN vendor.
  * VPN Gateway IP address: The public IP Address of the VPN gateway/server.
  * VPN Client Address: The private IP via which clients route packets to the VPN tunnel.
  * VPN Client Network: The private network that the VPN client belongs to.

The old **VPN Address** label filter is still supported, but is marked for deprecation. This label filter is only relevant for filtering data in the views. In **Browser Sessions**, it will return pages that were accessed through a VPN where the gateway IP address is equal to the filter value. In **Local Networks > Network Access**, it will return probes to the VPN server where the gateway IP address of the VPN is equal to the filter value.

It will be fully removed from the product in a future release.

#### X11 Server Package No Longer Mandatory <a href="#x11-server-package-no-longer-mandatory" id="x11-server-package-no-longer-mandatory"></a>

From **te-browserbot** version 1.146 and later, installation of an X11 server (via the **te-xvfb** package) is no longer mandatory. Existing Enterprise Agents will continue to have **te-xvfb** installed, unless users take action to remove the package. New Enterprise Agents will have the package installed by default, but this can be avoided using one of the following processes:

* For Linux package installations: **install\_thousandeyes.sh** now has a new command-line flag to skip te-xvfb package installation.
* For Docker installations: Users may create new images based on the official ThousandEyes image that run `apt remove te-xvfb`.
* For TEVA installations: Users may unlock their appliances and run `apt remove te-xvfb`.

While it is now optional, users are still encouraged to keep the **te-xvfb** package installed. Some page load and transaction test configurations require starting Chromium without the **--headless** flag, and these situations will require **te-xvfb**.

#### New ISP for Dublin IPv6 Cloud Agent <a href="#new-isp-for-dublin-ipv6-cloud-agent" id="new-isp-for-dublin-ipv6-cloud-agent"></a>

Due to a change in service provider, customers with tests assigned to the IPv6 Cloud Agent in Dublin, Ireland will observe a corresponding change in path-visualization and source IP. The Cloud Agent ID used within the ThousandEyes API will remain unchanged. The new IPV6 IP is: 2001:4d40:4003::/48.

#### Endpoint Agent API Updates <a href="#endpoint-agent-api-updates" id="endpoint-agent-api-updates"></a>

* Endpoint Agent labels can now be updated via the API.
* Users can now create Endpoint Agent scheduled tests via the API.
* Previously, the **Account group list** API endpoint would only return the **organizationName** if the user was associated with multiple organizations. This has been changed, and the **organizationName** will now always be included.
* The **Import from JS File** button in **Transaction Test Settings** has been replaced with a **Create New** dropdown menu. This dropdown retains the option to choose a local file to import, but also provides a selection of predefined template scripts. Clicking on an option will update the editor with the contents of the selected template script.
* An issue was found where duplicate alerts were inadvertently being created, causing one of the alerts to fail to clear after resolution of the issue. This has been resolved.
* An issue was found where updating proxy configuration would refresh disabled tasks, causing them to continue to run despite being disabled. This has been resolved. .
* An issue was found where Cloud and Enterprise Agents reported no data on the **Map** view, even if data was being reported as expected. This has been resolved.

#### Endpoint Agent Integration with the Pulse Secure VPN <a href="#endpoint-agent-integration-with-the-pulse-secure-vpn" id="endpoint-agent-integration-with-the-pulse-secure-vpn"></a>

The Endpoint Agent now integrates with the Pulse Secure VPN, providing end-to-end visibility of network nodes and metrics for traffic that traverses the network. When present, the client will populate the **VPN Vendor** attribute visible in Endpoint Agent views and filters.

#### Credential-less Device Discovery <a href="#credential-less-device-discovery" id="credential-less-device-discovery"></a>

Device discoveries now report devices that failed discovery due to a lack of working credentials. The **Edit Device** modal has also been updated to show the used credentials on the device, and provide users with easy access to new credential creation:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-9afbe1cf4486d5d63c987c05e05ac3991a321ee0%2Fwhats-new\_changelog\_device-discovery-1.png?alt=media)

#### Hard Limit Added for BGP Data Requests <a href="#hard-limit-added-for-bgp-data-requests" id="hard-limit-added-for-bgp-data-requests"></a>

A hard limit of 700 (for example, 50 tests over 14 days, or 100 tests over 7 days) has been added to improve performance when a report or dashboard widget is created with a large BGP data set (either due to no applied filters or too large of a time span). Users are now asked to either apply a BGP test or monitor filter, or to reduce the time span in order to render the data, if it would otherwise exceed the hard limit.

#### Internet Insights Alert Rules Update <a href="#internet-insights-alert-rules-update" id="internet-insights-alert-rules-update"></a>

The Internet Insights alert rules functionality has been updated for when both **Catalog Providers** and **Affected Tests** are set to **Any**. Previously, this configuration would only trigger if a customer test was impacted by an outage. The configuration has now been updated to trigger if a subscribed provider is impacted, in addition to if a customer test is affected by an outage in a subscribed provider.

To alert on outages affecting only customer tests (including in providers the customer is not subscribed to), customers should set **Affected Tests** to **Specific**, and select all tests, or the specific set of tests you want the rule to match.

This change has been made to all existing alert rules.

* In order to simplify test selection in Cloud and Enterprise Agent views, saved events have been removed from the test selector. Saved events can be accessed from the **Sharing > Saved Events** page in the main menu.
* An issue was found where path trace data was not appearing in Endpoint Agent sharelinks. This has been resolved.

#### Updated Reports and Dashboards User Interface <a href="#updated-reports-and-dashboards-user-interface" id="updated-reports-and-dashboards-user-interface"></a>

ThousandEyes has updated the reports and dashboards user interface, widget icons, and workflow to substantially improve user experience, and ensure that widget addition and configuration is as streamlined as possible:

* Widgets can now be added by clicking the **+ Add Widget** button to open the **Add a Widget** panel, and then either selecting a widget to configure, or by dragging it to the desired location in the report or dashboard.
* The **Add a Widget** side panel is now movable and minimizable, allowing users to review how the added widget looks before saving.
* Changes to a widget can be previewed before saving. Clicking **Cancel** will revert the widget to its pre-configuration state, while clicking **Save** will confirm the new configuration.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-b9a41cba508e1ec6db587e7209c6d666932f6b15%2Fproduct-documentation\_reports\_working-with-reports-11.png?alt=media)

As part of this update, the **Manage Widgets** section has been removed.

For more information on working with reports and dashboards, see:

#### Internet Insights Reports and Dashboards Support <a href="#internet-insights-reports-and-dashboards-support" id="internet-insights-reports-and-dashboards-support"></a>

Internet Insights customers can now add widgets to reports and dashboards to leverage Internet Insights network outage metrics. The network outage metrics provided are:

* **Affected Tests**: Test data within your organization that is affected by outages.
* **Interfaces**: Interface data affected by outages.
* **Locations**: Location data affected by outages.
* **Outages**: Overall outage data.

Widgets built on Internet Insights metrics can apply the following filter conditions: **Catalog Provider, Outage Scope, and Network**; **Interface Location and Interface IP Address**; **Affected Test and Affected Domain**; and **Server Location, Server Prefix, and Server Network**.

To add a widget with Internet Insights metrics:

1.  1\.

    In **Reports** or **Dashboards**, click **+ Add Widget** and select a supported widget.
2.  2\.

    Select **Internet Insights** as the datasource.
3.  3\.

    Select **Network Outages** as the category.
4.  4\.

    Select a metric and measure (and filters if desired).

Internet Insights metrics are not available for use with the **Stacked** widget types (**Stacked Bar**, **Stacked Area**, and **Pie**).

#### New Pre-Built Dashboard for Internet Insights <a href="#new-pre-built-dashboard-for-internet-insights" id="new-pre-built-dashboard-for-internet-insights"></a>

A new pre-built dashboard that captures weekly and monthly outage trends has been added for Internet Insights customers. The dashboard, called **Internet Insights Built-In**, also provides an up-to-date view of the most impacted tests, locations, and providers.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-620de348606288ae00628afd1573ec3dbfcec699%2Fwhats-new\_changelog\_internet-insights-dashboard-1.png?alt=media)

The default dashboard can be duplicated and used as a starting point for building custom dashboards.
