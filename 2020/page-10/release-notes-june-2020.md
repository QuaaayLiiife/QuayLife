# Release Notes: June 2020

The COVID-19 virus is putting a huge strain on IT and network teams all around the world. To assist with managing your end-user experience, ThousandEyes is offering free access to our End User Monitoring until July 31, 2020. If this is of interest to you, reach out soon — enrollment for this offer ends on June 30, 2020. For more information, please see our

[blog](https://blog.thousandeyes.com/helping-support-remote-workers-irregular-operations/)

or

[contact](https://www.thousandeyes.com/remote?utm\_source=Release-Notes\&utm\_medium=Textlink\&utm\_campaign=Helping-Support-Remote-Workers-Irregular-Operations)

the ThousandEyes team.

ThousandEyes has expanded our Enterprise Agent deployment options to include support for Raspberry Pi 4. A new download option is now available, along with installation instructions, on the **Agent Settings** page.

Browser-based tests are not supported when running an Enterprise Agent on Raspberry Pi 4.

#### New Features and Enhancements <a href="#new-features-and-enhancements" id="new-features-and-enhancements"></a>

**Cloud and Enterprise Agents**

**Updated Agent Statistics Tab**

The **Agent Statistics** tab in the **Agent Settings** view has been revamped to provide per test contribution to agent utilization. The tab now includes the host account group, test type, average utilization, and max utilization of each test to provide greater context.

In addition, agent uptime and utilization metrics are available over a longer time period (up to 30 days).

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-f401eb7fbed0932995294389372cd33b6de50989%2Frelease-notes\_2020-05-12\_feature-cea-statistics-1-2.png?alt=media)

* The location filter on the Internet Insights **Views** page has been updated. Locations are now grouped by area and country, allowing users to search more effectively.

#### Deprecated and Removed Features <a href="#deprecated-and-removed-features" id="deprecated-and-removed-features"></a>

ThousandEyes is deprecating the voice call test type on August 31, 2020.

Voice call tests simulate a full Voice over Internet Protocol (VoIP) call sequence, starting with the session initiation using the Session Initiation Protocol (SIP), and then the voice data transmission using the Real-time Transport Protocol (RTP) between one or more ThousandEyes agents and a target agent, acting as the VoIP user agents (or the call endpoints).

A voice call test can be migrated to separate SIP and RTP tests without incurring additional unit consumption. For more information about SIP and RTP test configuration, see

[SIP Server Test Settings](https://github.com/thousandeyes/docs/blob/prod/product-documentation/tests/sip-server-test-settings.md)

and

[RTP Stream Test Settings](https://github.com/thousandeyes/docs/blob/prod/product-documentation/tests/rtp-stream-test-settings.md)

. Contact support for more information.

**Cloud and Enterprise Agents**

* An issue occurred where device views would become unresponsive when navigating from the **Alerts List** page, or from alert notification emails. This has been resolved.
* Under certain conditions, the certification path displayed was not the certification path used by the test's TLS connection. The way the certificate chain is shown in the **Response Details** panel has been changed to show the more commonly used certificate chain in the case of cross-signed certificates.
* An issue in the **Test Settings** page was found where the bypass list configured in proxy settings would bleed across the test settings box if there were greater than 4 entries. This has been resolved.
* An issue was found in **Device** views where the "interface" filter selection did not auto-populate all available options a user would typically be able to select. This has been fixed.
* An issue occurred where inconsistent times were displayed on report widgets based on the users timezone. This has been updated to accurately reflect the time regardless of timezone.
* In rare production circumstances, a previously identified and fixed issue that resulted in a report snapshot being emailed twice instead of once would reappear. Additional checks have been added to ensure the issue is now resolved.
* An issue with test table widgets existed where user-created labels were not showing up as filterable options. This has been corrected.
* The color grid widget filter option was not working properly, and has been fixed.
* An issue occurred where the filter values selector for individual widgets was enabled before a metric was selected. The filter values selector is now only available when a metric has been selected.
* An error occurred that resulted in an agent being displayed multiple times in a filter. This has been resolved.
* An issue occurred where Endpoint Agents without data reported as 100% data loss in dashboards. This has been resolved.
* A race condition prevented setting changes from being applied to some Endpoint Agent tests. This has been resolved.
* An issue occurred where changing the Endpoint Agent network topology view grouping could cause the web UI to hang. This has been resolved.
* An error occurred when clicking the "Show Network Topology of this Agent" link for an Endpoint Agent that resulted in a perpetual loading icon. This has been resolved.
* An issue occurred where an error was displayed when attempting to modify a label. This has been fixed.
* We have resolved an issue in Internet Insights where in some cases, when creating an outage alert rule, the "Catalog Providers" dropdown menu had a blank entry.
* An issue causing animations on the Internet Insights Overview page to occasionally consume 100% CPU has been resolved.

The COVID-19 virus is putting a huge strain on IT and network teams all around the world. To assist with managing your end-user experience, ThousandEyes is offering free access to our End User Monitoring until July 31, 2020. If this is of interest to you, reach out soon — enrollment for this offer ends on June 30, 2020. For more information, please see our

[blog](https://blog.thousandeyes.com/helping-support-remote-workers-irregular-operations/)

or

[contact](https://www.thousandeyes.com/remote?utm\_source=Release-Notes\&utm\_medium=Textlink\&utm\_campaign=Helping-Support-Remote-Workers-Irregular-Operations)

the ThousandEyes team.

#### New Features and Enhancements <a href="#new-features-and-enhancements-1" id="new-features-and-enhancements-1"></a>

* Previously, the scheduled tests assigned to an agent were randomly selected from the list of pre-assigned tests. Now, tests containing a label that matches specifically to an agent are prioritized ahead of all other tests when they are assigned execution slots.
* The URL and network target can now be edited in the **Scheduled Test Settings** form when you edit a test.
* Reachable VPN nodes are now displayed on the path visualizations created for scheduled tests.
* Endpoint Agent browser session alerts are now supported in the **Alert Grid** and **Alert List** widgets.
* An issue occurred where the **Markers** filter was showing duplicate markers if a saved event shared the same name as the test it was created from. This duplication has been resolved.
* An issue occurred that caused public dashboards and reports to be deleted when the original creator was deleted from the platform. Dashboards and reports now remain within the appropriate account group even when a user is deleted.
* An issue caused embedded links to be deleted when a user updated a dashboard or a report through the API. This has been resolved.
* In some instances, the **Download** button for report snapshots was grayed out and non-functional. This has been resolved.
* An issue in the registration process caused the process to abort when it encountered network errors. This has been resolved.
* The **Headers** link was missing under the **Response code** column in the **Table** view for Endpoint Agent HTTP server tests. It is now displayed correctly.
* An issue sometimes occurred where the **Affected Tests** filter in Internet Insights would display a "loading" animation indefinitely and the test list would never complete loading. This issue has been resolved.

The COVID-19 virus is putting a huge strain on IT and network teams all around the world. To assist with managing your end-user experience, ThousandEyes is offering free access to our End User Monitoring until July 31, 2020. If this is of interest to you, reach out soon — enrollment for this offer ends on June 30, 2020. For more information, please see our

[blog](https://blog.thousandeyes.com/helping-support-remote-workers-irregular-operations/)

or

[contact](https://www.thousandeyes.com/remote?utm\_source=Release-Notes\&utm\_medium=Textlink\&utm\_campaign=Helping-Support-Remote-Workers-Irregular-Operations)

the ThousandEyes team.

#### New Features and Enhancements <a href="#new-features-and-enhancements-2" id="new-features-and-enhancements-2"></a>

*   The default BGP alert rule has been updated to fire when 10% of monitors have less than 100% reachability.

    **Note**: This change will be applied moving forward and retroactively, but will only impact the default BGP alert rules that have not been updated by a customer.

    **Note**: These changes will occur in sequence; initially, the change will be made for new rules, and then in the next couple of weeks, the changes will be made retroactively.
* Transaction scripts can now contain up to 200 defined markers.
* The **Waterfall** tab now includes a **Show More** link for when there are more than 10 markers to display.
*   The number and ID of affected tests reported in outage alerts are now available via the alerts API. See

    [v7 API documentation](https://developer.thousandeyes.com/v7/)

    .
* Added more specific tooltip titles to the metrics displayed in the timeline for Endpoint Agent local networks.
* An issue occurred with the v7 Dashboard API that was allowing users to create, update, or delete dashboards using the **GET** method instead of the appropriate HTTP method **POST**. This has been fixed.
* An issue was found where gaps could appear between the page bars shown in the **Waterfall** view when browser-based tests targeted certain pages. This was caused by missing start/end time requests for those pages, and has been resolved.
* An issue occurred where transaction tests would periodically appear to complete successfully (reporting a full waterfall and duration), but would also report as having timed out. This was caused by part of the inter-test setup overrunning its allocated duration, and counting against the user's configured test timeout. This has been resolved.
* An error occurred when transaction scripts that used the **waitForDownload()** function were configured to use an HTTP proxy. In these circumstances, the test would fail. This was caused by the way **waitForDownload()** had been implemented, and has been resolved.
* An error occurred when transaction scripts were configured to use an HTTP proxy where the proxy would receive periodic HTTP requests on port 9999 that were not intended to leave the agent. This was caused by the way the **waitForDownload()** function had been implemented, and has been resolved.
* Previously, the outage swimlane tooltip would sometimes cover the Internet Insights **Views** timeline selection, making it difficult to click on the timeline. The tooltip positioning has been changed and the issue is now resolved.
* An issue occurred that required users to have the **View alert rules** permission in order to view the Endpoint Agent **Views** and **Test Settings** pages. This has been resolved.
* An issue occurred where agents remained disabled after a customer's trial period was extended. This has been corrected.
