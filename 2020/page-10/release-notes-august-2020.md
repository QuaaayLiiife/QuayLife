# Release Notes: August 2020

#### Disable Global Credential Retrieval <a href="#disable-global-credential-retrieval" id="disable-global-credential-retrieval"></a>

ThousandEyes has added the ability to disable viewing of stored transaction test credentials by any user, regardless of permissions.

Previously, any user with the **View sensitive data in web transaction scripts** permission (including, by default, an **Organization Admin** or **Account Admin** user) was able to reveal stored credential values in the **Credentials Repository**.

Users with the **Edit security and authentication settings** permission (by default, only those in the **Organization Admin** role) can now select a new **Disable global credential retrieval** checkbox to override the **View sensitive data in web transaction scripts** permission, and disallow user credential access via the web app and the API.

To configure the new option:

1.  1\.

    Navigate to **Account Settings > Organization Settings > Security and Authentication**.
2.  2\.

    Scroll down to the **Credentials Repository** section, and select **Disable global credential retrieval**:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-41529ab18eca7150d7faba1308349d93ae0da06f%2Frelease-notes\_2020-08-04\_feature-disable-global-credential-retrieval-1.png?alt=media)

Changes to the **Disable global credential retrieval** setting are logged under **Account Settings > Activity Log**.

* An issue occurred on the **Scheduled Tests** view for Endpoint Agents, where the settings displayed when hovering over an agent label were inconsistent with the agent's settings. This has been resolved.
* An error occurred when validating the proxy setting URL for Endpoint Agents. This has been resolved, and now any URL can be used as the PAC URL target.
* In some instances, the **Download** button for report snapshots wasn't working. This has been resolved.

#### Browser-Based Test Frequency Increased <a href="#browser-based-test-frequency-increased" id="browser-based-test-frequency-increased"></a>

ThousandEyes now allows customers to configure higher-frequency browser-based tests:

* Page load test intervals can now be reduced to one minute.
* Transaction test intervals can now be reduced to two minutes.

#### Exclude Cloud Agents with Local Problems from Reports and Dashboards <a href="#exclude-cloud-agents-with-local-problems-from-reports-and-dashboards" id="exclude-cloud-agents-with-local-problems-from-reports-and-dashboards"></a>

Data from Cloud Agents with local problems can now be excluded from report and dashboard widgets by clicking the **Exclude Data from Cloud Agents with Local Problems** checkbox in the widget's configuration.

#### AppDynamics Alert Integration Support <a href="#appdynamics-alert-integration-support" id="appdynamics-alert-integration-support"></a>

AppDynamics is now supported as an alert integration type for all Cloud and Enterprise Agent and BGP alert data sources. For more information, see

[AppDynamics Integration](https://docs.thousandeyes.com/product-documentation/alerts/integrations/appdynamics-integration)

.

#### Endpoint Agent Alerts Added to Alert Grid Widget <a href="#endpoint-agent-alerts-added-to-alert-grid-widget" id="endpoint-agent-alerts-added-to-alert-grid-widget"></a>

The following Endpoint Agent scheduled test alerts are now available in the **Alert Grid** widget:

#### Additional Filter Options Added <a href="#additional-filter-options-added" id="additional-filter-options-added"></a>

Two new filter options are now available when searching for interfaces or devices:

* The **IP Address** filter uses the mapped IP address to find associated interfaces and devices.
* The **Test** filter allows customers to find interfaces and devices that were traversed by the selected test(s) over the last 30 days.
*   An issue was found where the estimated usage for BGP tests was not calculated correctly for the current and next billing cycles. This has been resolved.

    **Important**: The actual BGP test usage was still captured and reported correctly.
* An issue was found where the loss, jitter, and latency for an Endpoint Agent network connection displayed inconsistent data if the connection had failed. The loss would show 9%, while the jitter and latency were shown to be < 1ms. This has been resolved, and the correct values are now displayed if the connection fails.
* An issue was found where Endpoint Agent browser session tests were not gathering network information when a proxy server was part of the network. This has been resolved.
* An error was found where a log entry was incorrectly referencing an "unsupported device". The correct system error is now logged instead.
* An issue was found where Endpoint Agents running macOS 10.9 were not reporting wireless information. This has been resolved.
* In some instances, the **Download** button for report snapshots was not working. This has been fixed.
* An issue occurred when creating a report snapshot with the v7 API, where the incorrect time range was shown in the UI when compared to the inputted request. This has been fixed.
