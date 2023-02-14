# Release Notes: February 2020

#### New Features and Enhancements <a href="#new-features-and-enhancements" id="new-features-and-enhancements"></a>

ThousandEyes has updated the **Topology** view to improve how destination interfaces are displayed and organized. A new IP Prefix grouping option has been added. This allows users to filter the Destination view, so that only nodes with IP prefixes are shown.

In addition, nodes that do not have enough information to display are now grouped as “Other Destination(s)” in the **Topology** View.

Endpoint Agent users can now trigger instant tests, allowing them to run one-time queries, validate test configuration, and troubleshoot problems, without waiting for a scheduled test to run.

System metrics are now included in Endpoint Agent scheduled tests, network tests, and browser sessions. These metrics (including CPU load and memory consumption) provide a more comprehensive overview of the state of the end-user’s machine when the test was run, allowing for a clearer understanding of test results and data.

The ThousandEyes API (version 7) now includes the new Dashboard API. Users can create, update, delete, and read dashboards, as well as retrieve data from dashboard widgets. For more information, see the

[Developer documentation](https://developer.thousandeyes.com/v7/dashboards/)

.

#### Deprecated and Removed Features <a href="#deprecated-and-removed-features" id="deprecated-and-removed-features"></a>

**Alert Notifications for HipChat**

In early March, ThousandEyes is ending support for alert notifications with HipChat. The ThousandEyes Support team will be reaching out to customers that use the integration, to assist with transitioning to other notification channels.

* A change in authentication requirements resulted in the ThousandEyes Virtual Appliance (TEVA) diagnostics page displaying a warning that the ThousandEyes collector was unreachable, despite it working as expected. This error has been resolved.
*   An error occurred during some new Endpoint Agent installations, resulting in the following error message:

    `“Recording is not enabled for this page at this time on Endpoint Agent”`

    This was caused by an issue with how monitored networks were configured and has been corrected. The Endpoint Agent Extension is now able to initiate recordings before setting up monitored networks.
* An issue occurred in the Proxy Settings tab, where a user’s configuration changes were not fully rolled back after clicking Cancel. This has been resolved.

Once a year, our entire company gathers together in the San Francisco Bay Area in order to set the organization's priorities and cadence for the year that follows. This year, the event will occur during the week of March 1st, 2020.

In order to allow all team members to participate, our chat and telephone-based support hours will be reduced to 12 hours per day, from 6am to 6pm Pacific Standard Time, starting Sunday March 1st. We'll still have a team on call during the off-hours, but will be operating with reduced response times. We will resume 24-hour coverage beginning on March 8th.

See this

[article](https://success.thousandeyes.com/PublicArticlePage?articleIdParam=kA02R000000UKh1SAG\_Reduced-Support-Coverage-March-1st-to-March-8th-PST-2020)

for more information, or contact either your account manager or our support team.

#### New Features and Enhancements <a href="#new-features-and-enhancements-1" id="new-features-and-enhancements-1"></a>

ThousandEyes users can now monitor and interact with arbitrary API endpoints from within a transaction script (for example, making HTTP requests and initiating TCP and TLS connections directly from the transaction scripts’ execution environment). This allows users to implement transaction testing in a number of new ways, including:

* Surrounding a fetch HTTP request with markers to measure the responsiveness of an API endpoint.
* Testing arbitrary and proprietary network protocols.
* Making POST calls directly to an API endpoint.
* Mixing API calls and browser commands to, for example, create a resource via API and then view its data through the web application's frontend.
* Using an API endpoint to generate an ephemeral access token for use in a transaction test.

New Endpoint Agent labels can now be created when running an Instant Test with additional changes.

1.  1\.

    From the **Test** view, open the **Run Now** drop-down menu and click **With changes**.

    ​

    ![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-03f69d3efbcddcaedebe4f80bcd167860ff6be4c%2Fwhats-new\_changelog-3.png?alt=media)

    ​
2.  2\.

    Open the **Agent Label** dropdown menu.

The **Add New Label** panel will now open.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-809b6b61b28c4bb73d177f2447a6a205e9f9b424%2Fwhats-new\_changelog-4.png?alt=media)

The Developer API now exposes the ability to create, run, and re-run Endpoint Agent Instant Tests. In addition, users can list the existing set of Endpoint Agent labels, as well as create new ones.

#### Deprecated and Removed Features <a href="#deprecated-and-removed-features-1" id="deprecated-and-removed-features-1"></a>

**Alert Notifications for HipChat**

In early March, ThousandEyes is ending support for alert notifications with HipChat. The ThousandEyes Support team will be reaching out to customers that use the integration, to assist with transitioning to other notification channels.

* Previously, customers were unable to select or copy the text of the **Target URL** visible in browser-based test views. This issue has been fixed.
* An issue occurred when viewing transaction test data, where timeline marker selections could be reset when selecting a different set of agents, or by changing between test layers. Marker selection stickiness has been improved to resolve this issue.
* A change to te-sandboxd prevented Red Hat Enterprise Linux (RHEL) agents from running transaction tests. This was the result of RHEL-specific behavior that caused a filesystem to be mounted with insufficient permissions. Customers running te-browserbot version 1.116 or later should no longer experience this issue.
* An issue occurred when customers ran page load or transaction tests on sites that made asynchronous HTTP requests, that resulted in BrowserBot failing to detect and collect those requests. This caused the tests to be omitted from the waterfall test view. The issue has been resolved.
* For some categories of transaction test failures, BrowserBot would fail to collect a browser final screenshot. This issue has been resolved.
* An issue would sometimes occur where the table view for transaction test data would contain a row that simultaneously said “zero errors” and showed no error icon, but had no entry for “transaction time”. This was caused by a UI rendering bug, and both tests and errors now display correctly.
* Previously, the ThousandEyes API for transaction tests returned broken links for network metrics and for path visualization. The correct links are now returned.
* Issues were found in the UI design for the transaction waterfall view that resulted in the view becoming illegible or unusable in certain circumstances. The design has been refined, and these issues should no longer occur.
* Previously, NTLM was not selectable in the settings for the HTTP server portion of a transaction test. This has been corrected.
* When configuring the Color Grid widget, if the **SIP Availability** metric was selected, the tile colors would not accurately affect the color scale selections. This has been fixed, and the tile colors now display as expected.
* A visual error resulted in tests using agents in Hong Kong and Singapore not highlighting the two countries correctly in the **Geomap** widget. This has been resolved.
* An issue occurred where Endpoint Agent cached objects were marked as “Object incomplete” as they did not have content size information. This has now been resolved.
* An issue with authentication tokens resulted in Endpoint Agent shared links not working for newly created accounts. This was caused by the token not being generated upon account creation, resulting in potential race conditions that impacted the share links. Tokens are now generated upon account creation, resolving the issue.
* An error occurred that prevented color changes to Endpoint Agent labels from being saved if the color was the only change made. This has now been resolved.
