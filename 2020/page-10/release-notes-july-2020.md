# Release Notes: July 2020

BrowserBot 1.132, which is used by Cloud and Enterprise Agents to conduct page load and transaction tests, includes an upgrade of the te-chromium browser from version 68 to version 80. Users may observe changes in test behavior due to the browser upgrade.

Red Hat Enterprise Linux and CentOS environments now require java-1.8.0-openjdk rather than java-1.7..0-openjdk.

Debian-based agents are not affected by this update as they already use java-1.8.0-openjdk.

#### TLS Subject Name Indication for HTTPS Endpoints <a href="#tls-subject-name-indication-for-https-endpoints" id="tls-subject-name-indication-for-https-endpoints"></a>

Webhooks using HTTPS endpoints now require that the TLS SNI matches one of the webserver certificate's subject alternative names (SANs). ThousandEyes will reach out to customers that we believe will be directly impacted by this change.

#### Custom Static Key-Value Pairs Added to Webhooks <a href="#custom-static-key-value-pairs-added-to-webhooks" id="custom-static-key-value-pairs-added-to-webhooks"></a>

Custom static key-value pairs can now be added to the webhook payload as part of the **Alert Key** in the **Body** section of a supported webhook. These custom payloads can only be used on the Cloud or Enterprise Agent alert type, and will be specific to the selected alert rules. This change also adds two new fields to the webhook payload:

* **testLabels**: The test label name and ID.
* **testTargetsDescription**: The description of the test target as defined in the test configuration.

In addition, the **Authorization Code** grant type has been added to the OAuth workflow for webhooks.

#### In Session Path Trace Mode for Network Agent to Agent Tests <a href="#in-session-path-trace-mode-for-network-agent-to-agent-tests" id="in-session-path-trace-mode-for-network-agent-to-agent-tests"></a>

In order to better support Palo Alto and Juniper firewalls in the path visualization, ThousandEyes has added the capability to perform a path trace "in session" within an agent to agent test. This initiates a TCP session with the target server, and sends path trace packets within that session.

The new option can be configured by selecting the **In Session** checkbox on the **Basic Configuration** page of the test, under the **Path Trace Mode** setting:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-013816dd950a6f5bf0d46d8677d2784002715903%2Frelease-notes\_2020-07-10\_feature-in-session-path-trace-mode.png?alt=media)

#### Disabled Tests Excluded from Test Table Widget by Default <a href="#disabled-tests-excluded-from-test-table-widget-by-default" id="disabled-tests-excluded-from-test-table-widget-by-default"></a>

The **Test Table** widget has been updated to exclude disabled tests by default. Additionally, a checkbox option has been added to the widget configuration that allows users to include disabled tests in the Test Table widget if needed.

#### Transaction Test Sleep Button <a href="#transaction-test-sleep-button" id="transaction-test-sleep-button"></a>

A new button has been added to the script editor in the transaction test settings that will add a sleep command to the transaction script where the cursor is positioned.

* An issue occurred when an Endpoint Agent user tried to access a share link immediately after creating it. In some instances, this would result in the user seeing gaps in the data, as they were viewing the share link before all the data had been indexed. This issue has been resolved.
* An issue occurred where some Endpoint Agents connected via WiFi showed no wireless information in the **Local Networks** views. This has been resolved.
* Previously, the best-match logic used when searching the Internet Insights catalog on the **Catalog Settings** page resulted in unexpected results when searching for short terms (for example, _ISP_). This has been resolved.
* When configuring Internet Insights outage alert rules, in some instances, the validation errors did not provide enough information to identify the field that did not validate. This has been resolved.
* An issue occurred where many transaction tests would periodically appear to complete successfully (reporting a full waterfall and duration), but end up reporting as having timed out. This was caused by a step in the inter-test setup running over the allocated duration, which counted against the user's configured test timeout time. This has been corrected.

An issue was found where changing the alert conditions on an existing alert rule inadvertently removed all of the assigned tests from the alert rule. This issue has been fixed.

#### Endpoint Agents: Higher Number of Scheduled Tests Per Agent <a href="#endpoint-agents-higher-number-of-scheduled-tests-per-agent" id="endpoint-agents-higher-number-of-scheduled-tests-per-agent"></a>

You can now configure up to 10 scheduled tests per Endpoint Agent. This higher limit applies to both Endpoint Agent and Endpoint Agent Pulse.

#### Expandable Editor for Transaction Scripts <a href="#expandable-editor-for-transaction-scripts" id="expandable-editor-for-transaction-scripts"></a>

When you edit a transaction script, you can now expand the editor window, for a more ergonomic coding experience.

#### BGP Widgets without Filters <a href="#bgp-widgets-without-filters" id="bgp-widgets-without-filters"></a>

When you create a report or dashboard widget that uses BGP data and does not use filters, you are now asked to confirm that you want to render the data. This change is made to improve performance when a widget selects a large data set.

This change impacts existing widgets as well as new widgets, but it does not impact existing snapshots.

#### Cloud Agents with IPv6 Support <a href="#cloud-agents-with-ipv6-support" id="cloud-agents-with-ipv6-support"></a>

The following Cloud Agent locations now have IPv6 support:

* Changing the alert conditions on an existing alert rule inadvertently removed the assigned tests from the alert rule. This issue has been resolved.
* In Agent Settings, when you sort the list by **Last Contact** in ascending order, the list now displays disabled agents last.
* An issue sometimes occurred in Internet Insights where the **Select All** checkboxes in filters could reach a selected state without all options being selected. This issue has been resolved.
* In some rare cases, the Endpoint Agent failed to check in when connected over VPN and when a specific HTTP error code had been returned for previous connection requests. This issue has been resolved. With this fix, the Endpoint Agent is now always able to check in when there is a clear Internet connection (VPN or otherwise).
* Previously, some transaction tests could time out spuriously on certain agents without any apparent cause. ThousandEyes has determined that the root cause of the issue was variability in certain phases of transaction test setup, and has modified BrowserBot to account for time differently, such that these spurious timeouts cease.
