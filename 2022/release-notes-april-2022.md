# Release Notes: April 2022

You can now set a severity level for your alerts and alert rules. An alert's severity is shown both in the ThousandEyes UI and in any notifications that you have configured, such as email.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-66790eb61ab937af3ca9adb0a8a98e0a9d74d78d%2Falert-severity-1.png?alt=media)

If you have existing alert rules that predate this feature, they will be assigned the default **Info** severity. You can change this default to the severity level that suits your organization's needs.

New Cloud Agents have been added to the following locations:

* Indore, India (JIO) (IPv6)
* Irvine, CA, USA (Century Link)
* Irvine, CA, USA (Century Link) (IPv6)
* Phoenix, AZ, USA (CenturyLink)
* Phoenix, AZ, USA (CenturyLink) (IPv6)
* Phoenix, AZ, USA (Cox) (IPv6)
* During a DNS trace test, it is possible that a non-authoritative answer is received from a server in the path. Previously, we returned a general error message in this situation. Now, a more descriptive error message similar to "ERROR: Received non-authoritative response (AA flag not set) to query for www.example.com. A" is returned.

#### 2022-04-18 General Bug Fixes <a href="#2022-04-18-general-bug-fixes" id="2022-04-18-general-bug-fixes"></a>

* An issue was found where, in some edge cases, Endpoint Agents were able to fire alerts after the organization that they were associated to had been disabled. This has been resolved.
* An issue was found where the alert count wasn't being passed correctly via the report and dashboard APIs, and was instead always returning a 'No Data' response. This has been fixed, and the APIs now pass the correct number of alerts present in the appropriate widget.
* An issue has been resolved that was preventing the Endpoint Agents drill down filter from loading in report and dashboard widgets.

**2022-04-18 Endpoint Agent Client version 1.108.2 Bug Fixes**

* An issue has been resolved where the Endpoint Agent was generating test data for an application after disabling the corresponding automated session test.

New Cloud Agents have been added to the following locations:

* New Delhi, India (JIO) (IPv6)

#### Additional Dynamic Baseline Metrics <a href="#additional-dynamic-baseline-metrics" id="additional-dynamic-baseline-metrics"></a>

Additional metrics have been added to our dynamic baseline alerting capabilities:

*
  * Agent-to-server - Latency
*
  * FTP server - SSL negotiation time
  * HTTP server - Connect time
  * HTTP server – Receive time
  * HTTP server – SSL negotiation time
  * Page load - Page load time
  * Page load - Response time

#### 2022-04-26 General Bug Fixes <a href="#2022-04-26-general-bug-fixes" id="2022-04-26-general-bug-fixes"></a>

* An issue has been resolved that was preventing customers from downloading a PDF or CSV of a report if an individual widget wasn't fully configured. Customers can now download a PDF or CSV even with widgets that are not fully configured.
* An issue has been resolved where, in some cases, the Internet Insights provider selector did not alphabetize the list of available providers.
* An issue has been resolved that, in rare cases, prevented the correct sorting of values in descending or ascending order in our stacked bar chart widget for reports and dashboards.

#### Kazan, Russia Cloud Agent Decommission <a href="#kazan-russia-cloud-agent-decommission" id="kazan-russia-cloud-agent-decommission"></a>

The ThousandEyes Cloud Agent in Kazan, Russia is currently unavailable.

At this time we have no estimate for when this Cloud Agent will return to operation. If you need help transferring your tests to other agents, contact

\[email protected]

. The nearest available agents are:
