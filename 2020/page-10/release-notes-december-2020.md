# Release Notes: December 2020

#### New Device Layer Metric Features <a href="#new-device-layer-metric-features" id="new-device-layer-metric-features"></a>

Three new metrics have been added for the Device layer to improve topology highlighting and surfacing of device-based issues. The new metrics are:

* Interfaces with State Changes

As part of this update, metric selection above the timeline is now decoupled from highlighting options in the Device topology views (similar to standard test views).

#### Proxy Metrics Alert Conditions <a href="#proxy-metrics-alert-conditions" id="proxy-metrics-alert-conditions"></a>

**Proxy Loss**, **Proxy Jitter**, and **Proxy Latency** have been added as alert conditions for agent to server alerts.

#### Proxy Metrics API Support <a href="#proxy-metrics-api-support" id="proxy-metrics-api-support"></a>

**Proxy Loss**, **Proxy Jitter**, and **Proxy Latency** have been added to the ThousandEyes API under the **/v6/net/metrics/{testId}** endpoint.

* A bug was found that prevented the bulk transfer of Endpoint Agent ownership from one account group to another. This has been resolved.
* A bug was found that resulted in an infinite page load spinning icon when opening the Endpoint Agent **Local Networks** view. This has been resolved.
* On newly installed Endpoint Agents, the presence of the Cisco AnyConnect VPN client was not detected after startup. This was due to a configuration error, and has been resolved.
* A bug was found where Endpoint Agent tests were run but the results were not submitted. This was caused by how timeouts were handled across redirects, and has been resolved.
* An issue was found where the **Number Card** report widget would not save configuration changes. This has been corrected.
* An issue that resulted in **Multi-Metric Table** widgets incorrectly showing the 98th percentile value regardless of how the widget was configured has been fixed.
* An issue was found where the **Response Code** metric was showing up on active alerts in the **Metrics at Alert Start** column, even though they weren't part of the triggered error condition. This has been corrected.
* A path visualization issue resulted in the proxy icon not displaying properly when there was a loop at the proxy. This has been resolved.
* A database replication issue caused device discovery on some devices to fail. This has been fixed.
* An issue was found where, in some cases when an HTTP redirect was involved, the certificate chain was not being presented in the HTTP server response details. This has been resolved.
* An NTP issue prevented customers from deploying ThousandEyes agents using the new appliance type based on Ubuntu 18.04 LTS. This issue has been resolved.

Please review the features below that we are retiring on March 1st, 2021.

#### Classic Transaction Tests <a href="#classic-transaction-tests" id="classic-transaction-tests"></a>

ThousandEyes will end support for classic transaction tests after March 1st, 2021. Classic test data will remain available for test views, API requests, and reports in accordance with our data retention policies. Customers may use saved events to retain test data beyond our

[standard retention timelines](https://docs.thousandeyes.com/product-documentation/tests/retaining-data-beyond-the-90-day-limit)

.

#### New Selectable Widget Metrics <a href="#new-selectable-widget-metrics" id="new-selectable-widget-metrics"></a>

**Page DOM Load Time** and **Page Load Time** are now selectable widget metrics in reports and dashboards for the transaction metric type. A user can group their data by the individual pages identified in their transaction test.

* Previously, queries to **https://api.thousandeyes.com/v7/endpoint-data/tests/net/metrics/** returned **100% loss** when ICMP measurements were blocked. This has been updated - queries now return the **ErrorDetails** field.
* To improve user experience when there are a large number of white nodes in an Endpoint Agent path visualization, these white nodes will now be grouped together when there are three or more consecutively.
* Previously, if there was a DNS failure when resolving the target of a scheduled test, no network scheduled test datapoints would be uploaded to the backend. In this case the agent would appear as if it didn't participate at all running scheduled tests at those rounds. Failed scheduled tests ping and pathtrace datapoints are now generated if the name resolution to the target failed.
* A display formatting error in the Endpointn Agent **Browser Sessions** network table was found that made the values inconsistent with those shown in the path visualization. This has been resolved.
* An issue that caused the loading spinner icon to not disappear when an Endpoint Agent page request completed has been fixed.
* The screen placement of the **Agent Filter** dropdown menu prevented some agents from being selectable. This issue has been resolved.
* An issue that caused ICMP blocked traffic to trigger browser session alerts on packet loss has been resolved.
* An issue that caused scheduled snapshots with the **Number Card** widget to be displayed incorrectly has been fixed.
* An issue was found where throughput metrics were being collected for agent-to-agent tests, but were not a selectable metric on the timeline. This has been resolved.
* In cases where an agent used a proxy but was told to go directly to the target by the PAC file, the Target IP address was incorrectly displayed as the proxy IP address. This has been resolved.
* In rare circumstances, a BGP alert rule would still show as triggered even though the rule had been deleted. This has been resolved.
* In rare instances, an alert was fired after 1 round when the associated alert rule specified multiple rounds were required to fire the alert. This error has been corrected.

#### Deprecated and Removed Features <a href="#deprecated-and-removed-features" id="deprecated-and-removed-features"></a>

On March 15th, 2021, the DNS+ test type will be removed from the ThousandEyes product.

Previously, DNS+ tests, including DNS+ server latency tests and DNS+ domain tests, leveraged open DNS resolvers to gather DNS record availability information and nameserver performance. However, due to the transient nature of open resolvers on the internet, maintaining and discovering a global list of resolvers has become operationally difficult.

​

[DNS server tests](https://docs.thousandeyes.com/product-documentation/thousandeyes-basics/using-the-dns-server-view)

can be used to test against public and common ISP resolvers using our

[Cloud Agent](https://www.thousandeyes.com/product/cloud-agents)

vantage points around the world. Used in conjunction with alert rules for the **Mappings** metric, DNS server tests can monitor DNS servers for use cases such as cache poisoning.

Other DNS test types, including DNS trace tests and DNSSEC tests will also remain supported.

After March 15th, customers will no longer be able to create new DNS+ tests, and any existing DNS+ tests and snapshots will be deleted. For more information, contact your account team or

[ThousandEyes support](https://docs.thousandeyes.com/product-documentation/getting-started/getting-support-from-thousandeyes)

.
