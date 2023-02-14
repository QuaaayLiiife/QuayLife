# Release Notes: August 2021

#### Cisco Catalyst 8000 Router and Integrated Services Routers 4000 Series Support <a href="#cisco-catalyst-8000-router-and-integrated-services-routers-4000-series-support" id="cisco-catalyst-8000-router-and-integrated-services-routers-4000-series-support"></a>

As part of this release, ThousandEyes now supports deploying Enterprise Agents on Cisco Catalyst 8000 series and ISR 4000 series routers. For full support details and installation instructions, see:

#### Browser Test Support for Catalyst 9000 Series Switches <a href="#browser-test-support-for-catalyst-9000-series-switches" id="browser-test-support-for-catalyst-9000-series-switches"></a>

Starting with this agent release, ThousandEyes supports browser tests on Catalyst 9300 and 9400 switches that have an SSD. For more information, see the

[Support Matrix](https://docs.thousandeyes.com/product-documentation/integration-guides/thousandeyes-cisco-integration#support-matrix)

.

#### Agent Identifier Setting in Transaction and Page Load Tests <a href="#agent-identifier-setting-in-transaction-and-page-load-tests" id="agent-identifier-setting-in-transaction-and-page-load-tests"></a>

As transaction and page load tests are run from a ThousandEyes Agent, all HTTP requests for those tests include a custom header, `X-ThousandEyes-Agent: yes`. This header is necessary to identify requests as originating from a ThousandEyes agent.

In certain edge cases (for example, when an agent or test is configured to use a PAC file), the inclusion of this identifying header will trigger a

[CORS policy](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS)

violation for some cross-origin requests.

To circumvent this issue, HTTP requests can alternatively be made identifiable by extending the **User Agent** request header with a specific identifier text. Customers whose transaction or page load tests are affected by cross-origin request failure will be provided with a dropdown labeled "Agent ID Strategy" in the advanced settings for those test types. This dropdown contains two options:

1.  1\.

    **x-thousandeyes-agent Header**: The default selection for transaction and page load tests where the custom header is used as the identifier.
2.  2\.

    **Extend User Agent Header**: Selecting this option will ensure that the problematic custom header is not included in Agent HTTP requests, but also requires that the `(ThousandEyes Agent)` identifier text is included in the User Agent request header. When selected, the User Agent dropdown options will update to display "(TE)" after every option name to signify that this identifier text is appended to the User Agent request header. Whenever the User Agent text input is visible the identifier text will be included at the end of the displayed text. If the identifier text is subsequently modified or removed from the text input while the "Extend User Agent Header" option is selected, the test configuration will not be valid and saving the test configuration will be prevented until the identifier text is restored.

Agents assigned to transaction or page load tests which use the **User Agent** identifier strategy must have:

* a minimum agent version of 1.120.0.
* a minimum Browserbot version of 1.168.0.

The agent and Browerbot version can be seen in the configuration side panel for an agent in **Agent Settings**.

#### Changes to Webapp Session Timeout Duration <a href="#changes-to-webapp-session-timeout-duration" id="changes-to-webapp-session-timeout-duration"></a>

In the coming weeks, ThousandEyes will change the default session timeout duration from indefinite to 30 minutes. This change will patch a security vulnerability, as well as better align the timeout duration with industry best practices.

As part of this change, the **keep\_session\_alive\_on\_auto-update** permission will be automatically removed from all default built-in roles. This change could affect customers that continuously display ThousandEyes dashboards (for example, in Network Operations Centers).

If you would like to preserve the **keep\_session\_alive\_on\_auto-update** permission for certain users within your organization, we recommend that you create a custom role with this permission and assign users in the appropriate account group to that role.

* Previously, HTTP scheduled tests on macOS Endpoint Agents would fail when the "Verify SSL Certificate" flag was off, even if a valid certificate was installed. This has been fixed.
* An issue was found where any data collected while an Endpoint Agent device was connected to mobile broadband may not appear in the Endpoint Agent views. This included scheduled test, browser session, and local network data. This issue has been resolved, and the Endpoint Agent now recognizes when a mobile broadband adapter is used as the primary network interface correctly.
* An issue was found that caused outage alert rules to be shown and selectable in the test settings **Alert Rules** list, despite not having a corresponding test type. The outage alert rules have now been removed from the list.
* The "Country" column header under the "Cloud Agents" tab in agent settings has been updated to "Country and Region" to ensure the column header captures all agents and their associations.
* Added a warning message on the alert list page to provide additional context as to why certain alerts may not be clearing due to lack of data.
* Previously, the datapoint sent to the alerting platform used to include all markers that were present in a script, regardless of if they were present in the actual measurement or not. This changed when we upgraded our alerting platform, which resulted in an issue where the transaction test alert rule expression **Marker \<markerName> is not present** was not being evaluated correctly. This has been fixed.
* A rare case was found where a DNS query performed on a particular test caused an instance on some of our cloud agents to crash. This has been resolved.
* An issue was found that prevented large PDFs from being downloaded. This has been resolved, and customers can now download all reports that can be loaded and rendered in the application as PDFs.
* An issue was found where the "measure" header for Internet Insights data was populated incorrectly for when downloading a CSV file for a report. This has been fixed.
* An issue was found where the "Show in device layer" hyperlink was not correctly redirecting users to the appropriate device layer views from the path visualization. This has been resolved.
* An issue was found where agent uptime was not reported correctly in the **Agent Statistics** tab in agent settings. This was caused by a MySQL error, and has been fixed.
* An issue was found where the Endpoint Agent browser sessions **Waterfall** view was not showing the correct messages when the user hovered over alert messages. This has been resolved.
* An error message is now displayed if the user tries to save a label with the deprecated **VPN Address** attribute.
* A visual error caused labels to be removed from the display when an Endpoint Agent test was saved. This has been fixed.
* Fixed a rare issue that prematurely ended some alert suppression windows, causing alerts to be fired during this suppression.

#### Changes to Webapp Session Timeout Duration <a href="#changes-to-webapp-session-timeout-duration-1" id="changes-to-webapp-session-timeout-duration-1"></a>

In the coming weeks, ThousandEyes will change the default session timeout duration from indefinite to 30 minutes. This change will patch a security vulnerability, as well as better align the timeout duration with industry best practices.

As part of this change, the **keep\_session\_alive\_on\_auto-update** permission will be automatically removed from all default built-in roles. This change could affect customers that continuously display ThousandEyes dashboards (for example, in Network Operations Centers).

If you would like to preserve the **keep\_session\_alive\_on\_auto-update** permission for certain users within your organization, we recommend that you create a custom role with this permission and assign users in the appropriate account group to that role.

#### Endpoint Agent F5 VPN Support for macOS and Windows <a href="#endpoint-agent-f5-vpn-support-for-macos-and-windows" id="endpoint-agent-f5-vpn-support-for-macos-and-windows"></a>

Endpoint Agents now support F5 VPN connections, and run network tests to these virtual networks.

#### New Hostname for ThousandEyes Cloud Service <a href="#new-hostname-for-thousandeyes-cloud-service" id="new-hostname-for-thousandeyes-cloud-service"></a>

As part of our continued efforts to scale our services globally, from this release, new agents will use a different hostname to reach the ThousandEyes cloud service. New agents will now use **registry.agt.thousandeyes.com** when registering for the first time upon boot. Subsequent connections will still use **sc1.thousandeyes.com**.

New Cloud Agents have been added to the following locations:

* Portsmouth, England (IPv6)
* Santiago de Chile, Chile (IPv6)
* Ho Chi Minh City, Vietnam (IPv6)
* Guadalajara, Mexico (Trial) (IPv6)

#### Endpoint Agent UI Performance Improvements <a href="#endpoint-agent-ui-performance-improvements" id="endpoint-agent-ui-performance-improvements"></a>

The Endpoint Agent **Agent Settings** page has been significantly improved for performance. For larger account groups, the **Agent Settings** page should be displayed around 10x faster, while filtering and searching for agents is now up to 50x faster.

* For transaction tests, the default device emulation has been changed from **Desktop Small** to **Desktop Large** to better simulate a real user's environment.
* An agent that has been deleted for 7 days is now removed from the list of assigned agents in the Endpoint Agent proxy settings. This brings this functionality in line with agent labels and scheduled tests, where agents are already removed 7 days after deletion. Agents that have been deleted but are still within the 7 days recovery window are shown with a '(deleted)' note in the list of assigned agents in the Endpoint Agent proxy settings.
* A **Deleted** filter has been added to the Endpoint Agent drop-down list, to improve usability. This filter can be used to show all agents that have been deleted from the platform.
* Previously, creating an existing user through SCIM could result in a runtime error, rather than the more accurate 409 response code. This has been corrected, and users will see a 409 error in this scenario.
* Previously, responses from SCIM endpoints would include an additional element than requested when paging results. This has been resolved to return the exact amount requested.
* An edge case where the Endpoint Agent filter could fail to be displayed above the agent search box in the **Agent Settings** page has been resolved.
* Previously, the list of agents displayed in the **Scheduled Tests** view's agent filter did not include agents that were using **computerName** to identify themselves, and had no unique name set. Agents that use **computerName** as the identifier are now also included.
* The Endpoint node is now correctly colored green when selecting the **CPU / Memory** metric in the Local Networks view.
* Previously, a **system metrics parameters are not available** message was returned when a call was made to **https://api.thousandeyes.com//v6/endpoint-data/tests/web/http-server/{testId}.json**. The correct metrics data is now returned.
* An issue was found where alerts were incorrectly firing during an alert suppression window. This was related to a maintenance window that we created for bootstrapping the configuration for the new alerter, and has been fixed.
* Previously, some alerts were not being cleared after deletion of the alert rule. This was due to a metadata issue that has since been corrected.
