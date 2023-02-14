# Release Notes: March 2021

#### Improved Performance for Dashboards and Reports <a href="#improved-performance-for-dashboards-and-reports" id="improved-performance-for-dashboards-and-reports"></a>

The ThousandEyes reporting and dashboard platform is moving to a new backend data store to provide a faster and more responsive customer experience. The first data sources moving to this new data store are Endpoint Agent sources for Web - HTTP server, Network - agent-to-server, and network topology. The hard limits that have been applied to these data sources will gradually be removed over time as we move towards a 90-day retention period in our new data store.

Starting today, there will be no hard limits applied to data requests from January 23rd, 2021 onward. Any dashboard or reporting requests for data before January 23rd, 2021, will be met with the same hard limits currently in place for endpoint data. For more information on these hard limits, see

[the product documentation](https://docs.thousandeyes.com/product-documentation/reports/working-with-reports#render-limit)

.

#### Enterprise Agent on Cisco Catalyst 9300 <a href="#enterprise-agent-on-cisco-catalyst-9300" id="enterprise-agent-on-cisco-catalyst-9300"></a>

As of this release, customers with Cisco Catalyst 9300 switches running IOS-XE 17.3.3 can deploy our Enterprise Agent on the Catalyst 9300 natively - that is, without using an SSD.

As part of this effort, we've also redesigned the **Add New Enterprise Agent** modal:

* Cisco deployment types are now shown in a separate **Cisco Application Hosting** tab.
* The account group token now appears at the top of the tab, to make it easier to find and copy during agent installation.

#### End-of-Life for Transaction (Classic) Tests <a href="#end-of-life-for-transaction-classic-tests" id="end-of-life-for-transaction-classic-tests"></a>

​

[As previously announced](https://docs.thousandeyes.com/whats-new/changelog#classic-transaction-tests)

, ThousandEyes has ended support for classic transaction tests as of March 1st, 2021. Classic transactions tests can no longer be created, enabled, or run as instant tests.

Classic test data will remain available for test views, API requests, and reports in accordance with our

[data retention policies](https://docs.thousandeyes.com/product-documentation/tests/how-long-does-thousandeyes-retain-customer-data)

.

#### End of Internet Explorer 11 Support <a href="#end-of-internet-explorer-11-support" id="end-of-internet-explorer-11-support"></a>

Effective March 30, 2021, ThousandEyes will cease support for Internet Explorer 11 for https://app.thousandeyes.com. Support for all other browsers remains unchanged.

#### API V7 Properties Now Use Enum Names <a href="#api-v7-properties-now-use-enum-names" id="api-v7-properties-now-use-enum-names"></a>

In v7 of the Dashboards API and Reports API, the JSON that is returned now refers to all **dataSource**, **direction**, **filters**, **metric**, **measure**, and **metricGroup** values using an all-caps, snake-cased literal, rather than the display name shown in the ThousandEyes platform's UI. The API will continue to accept display names in JSON when posting, but will use enum names in the JSON that is returned from requests.

This change is only for v7 of the API.

**Note:** v7 of the ThousandEyes API is in preview status, and is subject to change.

For example, before this change, the response JSON might read as follows:

"dataSource": "Cloud & Enterprise Agents",

"metricGroup": "Network - Agent to Agent",

"direction": "Both Directions",

After this change, the same JSON response will read as follows:

"dataSource": "CLOUD\_AND\_ENTERPRISE\_AGENTS",

"metricGroup": "AGENT\_TO\_AGENT",

"direction": "BIDIRECTIONAL",

"metric": "ONE\_WAY\_NET\_LOSS\_BIDIRECTIONAL",

In the past, the default BGP alert rule was automatically selected and attached to higher-level network, web, DNS, and voice tests when they were created. With this release, the default BGP alert rule is no longer automatically applied to the following test types:

* Network - Agent-to-server

This change **does not affect any existing tests** that have this alert rule.

**Note:** This change applies to _any_ BGP alert rules that are designated in your system as default. To see which BGP alert rules you have designated as default, go to **Alerts > Alert Rules > BGP Routing** and see the selections in the **Default** column.

For new tests of the above types, you can still select the default BGP alert rule manually and apply it to these tests if you wish. For any new BGP tests you create, the default BGP alert rule is still automatically applied.

*   For cases where a machine has multiple users, the Endpoint Agent's **Agent Details** list now displays an icon next to each user name, to show the status of the browser extension for this user.

    ​

    ![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-04ae50f7e6a5e59f3f39d0a4052d1646673593c2%2Fwhats-new\_changelog\_epa-multiple-users.png?alt=media)

    ​
* Fixes around deleting an Endpoint Agent:
  * Deleted Endpoint Agents now only appear in the \*\*Agent Labels\*\* filter options dropdown list if they have been previously selected in the label. A deleted agent can be recovered for a seven-day period after deletion. If a deleted agent was included in a label and is within its seven-day recovery period, it may appear in the \*\*Agent Labels\*\* list.
  * When you perform a bulk-delete operation of Endpoint Agents, the list of agents is now updated correctly. Previously, in some cases deleted agents could still be shown, or search results were incorrectly filtered.
  * Endpoint Agents that were deleted more than one week ago are no longer displayed.
* An issue was fixed in which some BGP alert rules were not triggering when an unexpected covered prefix was advertised, despite the alert rule being set up to trigger for this condition.
* An erroneous error message was presented when a user generated a DNS server sharelink from the Network Overview layer of a DNS server test. Although the sharelink captured the relevant test data, the error message was misleading. This issue has been fixed.
* An issue was fixed in which the colors on the color grid widget were not accurately reflecting the scale selected by the user.
* Certain strings in report and dashboard widgets were being incorrectly and inconsistently truncated. This issue has been fixed.
* An intermittent issue was fixed in which an embedded alert grid widget was not redirecting users to the the correct URL when they clicked an alert.
* For Endpoint Agents, the path visualization for local networks now correctly displays the \*\*Avg. Response\*\* metric on hops and the \*\*Delay\*\* metric on links.

#### Deprecated and Removed Features <a href="#deprecated-and-removed-features" id="deprecated-and-removed-features"></a>

As of March 15, 2021, the DNS+ test type has been removed from the ThousandEyes product. DNS+ tests can no longer be created, and any existing DNS+ tests and snapshots are in the process of being deleted. For more information, contact your account team or ThousandEyes support.

* An Endpoint Agent IP address was wrongly identified as being located in the United Kingdom, rather than in Japan, by our geolocation data provider. This issue has been resolved with our provider, and the correct data should be present in the product from March 19, 2021.
