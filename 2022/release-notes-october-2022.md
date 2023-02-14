# Release Notes: October 2022

#### The Verify SSL Certificate Setting Now Applies Consistently to Page Load and Transaction Tests <a href="#the-verify-ssl-certificate-setting-now-applies-consistently-to-page-load-and-transaction-tests" id="the-verify-ssl-certificate-setting-now-applies-consistently-to-page-load-and-transaction-tests"></a>

In **Cloud & Enterprise Agents > Test Settings > Advanced Settings**, the **Verify SSL certificate** field now applies to both the HTTP view and the page load or transaction view in page load and transaction tests.

Previously, the **Verify SSL certificate** setting for these test types did not apply for the entire test, but held for the HTTP server view only. As a workaround, customers had to configure the agent-level settings.

As part of this change, starting **December 6, 2022**, we will begin deprecating the agent-level option at **Cloud & Enterprise Agents > Enterprise Agents > Agent Settings > **_**agent-name**_** > Verify SSL certificates for browser tests**.

In cases where the test-level option is de-selected but the agent-level option is _not_ de-selected, the ThousandEyes platform will continue to apply the agent-level setting until December 6, 2022.

After that date, all web-layer tests will follow the configuration you have set in **Test Settings**. The agent-level setting will be removed.

Most browser-based tests will not require changes. But if your page load and transaction tests have SSL verification disabled, review your configuration and use the test-level setting going forward.

#### Reports and Dashboards Are Now Merged <a href="#reports-and-dashboards-are-now-merged" id="reports-and-dashboards-are-now-merged"></a>

Reports and dashboards have now been merged into a single function. **Reports** has been removed from our lefthand navigation and all functionality has been consolidated into our **Dashboards** page. To find your previous reports, you can filter in the dashboard selector on **Migrated Reports**.

#### Endpoint Agent Views Enhancements <a href="#endpoint-agent-views-enhancements" id="endpoint-agent-views-enhancements"></a>

The Endpoint Agent View dashboard has been enhanced in order to make troubleshooting easier. These updates include:

* Improvements have been made to the search function for agents. In addition to agent name, you can now search by username, hostname, and IP addresses (both public and private).
* The tooltip for wireless information within the Network Access row will now show all the information related to the wireless information (i.e., SSID, Channel, Phy Mode) to make it easier to correlate data when troubleshooting issues related to it.

We have improved how our v6 and v7 dashboard APIs work as it relates to the time range specified in the API request. If the user provides a time range (from and to) in their API request to get widget data, the API will now return data for that time range. If the user does not provide a time range in the API request, the request will use the dashboard's **defaultTimespan** if **globalOverride** is set to true. If **globalOverride** is set to false, then the API will return data for the individual widget time settings set by the user or the default time range (1 day) if no value is set for the individual widget. The user can change **defaultTimespan** and **globalOverride** values using the UI or the **dashboardupdate** endpoint of the v7 API.

#### Endpoint Agent Scheduled Test Support for Custom Webhooks <a href="#endpoint-agent-scheduled-test-support-for-custom-webhooks" id="endpoint-agent-scheduled-test-support-for-custom-webhooks"></a>

Our custom webhooks now support Endpoint Scheduled Test alert types. You can now create custom webhooks and attach them to any Endpoint Scheduled Test alert rule. We have also improved the **Alert Rules** page under **Alerts**. As we continue to scale out the types of alert rules supported, we have added a specific alert type group selector when assigning alert rules for an integration.

New Cloud Agents have been added to the following locations:

* Ahmedabad, India (Bharti Airtel)
* Ahmedabad, India (Bharti Airtel) (IPv6)
* Dubai, UAE (AWS me-central-1)
* Jakarta, Indonesia (IPv6)
* New Delhi, India (Vodafone Idea)
* New Delhi, India (Vodafone Idea) (IPv6)
* St. John's, Canada (IPv6)
* Yogyakarta, Indonesia (IPv6)
* Device Discovery now correctly shows an error message when a newly discovered device is a duplicate of a monitored device.
* An issue that caused the browser back button to not work as expected on the Internet Insights Overview page has been resolved.
* An alert rules issue for Devices, that prevented the interface selection dropdown from correctly appearing in account groups with large numbers of monitored interfaces, has been resolved.
* An issue that was temporarily preventing our EU region customers from accessing the "Integrations" page in product has been resolved.

#### Automated Session Test Support in Dashboards <a href="#automated-session-test-support-in-dashboards" id="automated-session-test-support-in-dashboards"></a>

Automated session test data can now be used to generate dashboards. In particular, you can now use the data from both Network (Jitter, Loss, Latency, TCP Connection Count, VPN Loss, VPN Latency) and System (CPU and Memory Load) metrics together with the standard measures (Mean, Median, Average, Maximum, Minimum, nth Percentile, and Standard Deviation).

AST data is only available in the Grouped Bar, Table, Multimetric table, Number, Color Grid, Line, and Box and Whiskers widgets.

#### Endpoint Agent Views Enhancements <a href="#endpoint-agent-views-enhancements-1" id="endpoint-agent-views-enhancements-1"></a>

Endpoint Agent **Views**, the screen that shows all the results related to Endpoint Agent tests, has been improved in order to make troubleshooting tasks easier:

* The type of connection (Ethernet/Wireless), SSID and channel information has been added to the table of the **Network** tabs for scheduled and automated session tests. This way, you can easily correlate issues related to the quality of the wireless connection.
* We have added a new filter option on the **Views** page that allows users to define a filter for different network metrics (i.e., jitter, latency, packet loss, VPN latency, and VPN packet loss) to, for example, identify all the agents with latency over a threshold. This aims to make the identification of agents affected by a specific metric easier.
* Two new buttons have been added to allow you to easily select agents and automatically create a filter for the whole view or specifically for the pathview. This aims to help you in your troubleshooting workflow. By consulting the **Network > Table** tab, you could identify the set of agents that are affected by a specific issue. However, you could not easily select and filter them to focus on the data related to the affected agents.
* A new grouping option has been added to the **Table** tab for automated session tests. Unlike other types of tests, a single automated session test might target many different destinations (IP addresses) within the same test (Webex). To make the identification of the specific destinations affected by an incident easier, we now provide the ability to group tests by agent and also by agent and IP addresses.

#### Manage Dashboards via Labels <a href="#manage-dashboards-via-labels" id="manage-dashboards-via-labels"></a>

You can now create, edit, and manage dashboards via a labeling system. You can create custom labels and assign them to specific dashboards, either via the dashboard selector or via the **Dashboard Details** page for a specific dashboard. You can then filter based on the created labels when using the dashboard selector for easy access to you favorite dashboards.

* We have slightly changed the behavior of our custom webhook testing functionality. Previously, the **Test Status** of an integration would not change from **Success** to **Untested** if a user made a change to an existing webhook that had successfully been tested. Now, if a user makes a change to the custom webhook form, except for changing the name of the webhook, the status will be changed to **Untested** until a user again successfully tests the integration.

New Cloud Agents have been added to the following locations:

* Chennai, India (Bharti Airtel)
* Chennai, India (Bharti Airtel) (IPv6)
* Los Angeles, CA, USA (CenturyLink) (IPv6)
* Los Angeles, CA, USA (Charter) (IPv6)
* New Delhi, India (Bharti Airtel)
* New Delhi, India (Bharti Airtel) (IPv6)
* San Jose, CA, USA (CenturyLink) (IPv6)
* San Jose, CA, USA (Cox) (IPv6)
* St. John's, Canada (IPv6)
