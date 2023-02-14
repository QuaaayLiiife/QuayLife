# Release Notes: April 2020

The COVID-19 virus is putting a huge strain on IT and network teams all around the world. To help with the increased surge of remote workers, we at ThousandEyes are offering our Endpoint Agent product, free of charge. For more information, please see our

[blog](https://blog.thousandeyes.com/helping-support-remote-workers-irregular-operations/)

or

[contact](https://www.thousandeyes.com/remote?utm\_source=Release-Notes\&utm\_medium=Textlink\&utm\_campaign=Helping-Support-Remote-Workers-Irregular-Operations)

the ThousandEyes team.

In the next ThousandEyes release, the Alerts API endpoint will be updated to version 7.

The ThousandEyes API version 7 is currently in preview mode. As this version is subject to change, ThousandEyes recommends customers that are using version 7 revert back to the stable v6 API as soon as possible, unless accessing APIv7-specific endpoints that are not available in v6.

**Migration of Transaction (Classic) Tests**

In the coming weeks, ThousandEyes will be starting a migration plan to help customers migrate their existing transaction (classic) tests to the transaction test type. As part of that migration plan, we will be disabling the ability to create additional transaction (classic) tests from the product on April 30.

ThousandEyes will be working with individual customers as well as making an automated conversion tool available in the coming months to assist with the migration. If you need the ability to create additional transaction (classic) tests after April 30, contact the ThousandEyes support team.

In an upcoming release, ThousandEyes will upgrade the version of Chromium used by browser-based tests (page load, transaction \[classic], and transaction tests) from version 68 to version 79. As part of this upgrade, Flash will no longer be supported, and any page load, transaction (classic), or Transaction test that depends on Flash is unlikely to continue working.

**End of Installation Support for Red Hat Enterprise Linux and CentOS versions 7.4 and 7.5**

As of this release, new customers will be required to deploy enterprise agents on Red Hat Enterprise Linux and CentOS versions 7.6 and later. RHEL and CentOS versions 7.4 and 7.5 have now been placed in the end of support lifecycle. ThousandEyes will be reaching out to customers to ensure there is time to upgrade.

ThousandEyes recommends that customers upgrade to the latest RHEL 7 minor version (version 7.7).

**Warning:** Red Hat Enterprise Linux 8 is not currently supported. Do not upgrade to RHEL 8.x.

**New Documentation Platform**

ThousandEyes is excited to announce that we will soon be launching a new website for product documentation. This is the first stage in our efforts to provide users with an improved content experience.

More information will be included in future release notes as we get closer to launch.

#### New Features and Enhancements <a href="#new-features-and-enhancements" id="new-features-and-enhancements"></a>

Previously, reports and dashboards that were shared across account groups were tagged as “Shared by Me”. This has been updated to “Shared”.

* In previous releases, editing the direction for Agent to Agent alert rules was not possible. This has now been corrected, and the direction can now be configured.
* An issue occurred for some Enterprise Agent users where BrowserBot was attempting to reuse Chromium browsers across multiple test rounds, and not resetting Chromium’s connection pools. This resulted in inconsistent transaction test results, and has been resolved.
* Previously, XmlHttpRequests (“fetch()” requests, asynchronous HTTP requests, or XHR requests) requests that occurred during page load or transaction tests were not collected by BrowserBot, and not displayed in the waterfall view. This has been corrected.
* An issue occurred when users selected or deselected credentials in the transaction test settings view, where unrelated credentials could toggle as well. This has been resolved.
* Previously, network timings for assets were listed in the API v6 as -1 if the timing datum was not available (for example, if the assets were loaded from the browser’s cache), without context for the value. The API v6 has been updated to indicate on a per-asset basis whether the asset was loaded from the cache, to avoid confusion.
* An inconsistency existed between the timeline and error breakdown for HTTP server views. This was because the timeline used time to first byte (TTFB) errors for the availability metric, while the error breakdown did not. TTFB errors have been removed from the availability metric calculation to correct this inconsistency.
* Previously, the Agent Selector was missing from the "Run now → With changes" Views menu. This has been fixed.
* Previously, public monitors could not be filtered during widget configuration when building a BGP-specific report or dashboard. This has been corrected, and public monitors can now be filtered as expected.
* An issue occurred that prevented some users from duplicating a ThousandEyes built-in report. All reports can now be duplicated as expected.

The COVID-19 virus is putting a huge strain on IT and network teams all around the world. To help with the increased surge of remote workers, we at ThousandEyes are offering our Endpoint Agent product, free of charge. For more information, please see our

[blog](https://blog.thousandeyes.com/helping-support-remote-workers-irregular-operations/)

or

[contact](https://www.thousandeyes.com/remote?utm\_source=Release-Notes\&utm\_medium=Textlink\&utm\_campaign=Helping-Support-Remote-Workers-Irregular-Operations)

the ThousandEyes team.

**Migration of Transaction (Classic) Tests**

In the next release, ThousandEyes will be disabling the ability to create additional transaction (Classic) tests from the product.

ThousandEyes will be working with individual customers as well as making an automated conversion process from within the product console available to assist with the migration process. This tool is expected to be available in May. If you need the ability to create additional transaction (Classic) tests after April 30, contact the ThousandEyes support team.

ThousandEyes now supports installing Enterprise Agents on Amazon Linux 2 operating systems.

**New Documentation Platform**

ThousandEyes is excited to announce that at the end of April, we will be launching a new website for product documentation. This is the first stage in our efforts to provide users with an improved content experience.

#### New Features and Enhancements <a href="#new-features-and-enhancements-1" id="new-features-and-enhancements-1"></a>

The new “sticky agent” feature allows a user to configure alerts that only trigger when the same agent/s meet a specific condition in any number of consecutive rounds.

For example, an alert rule is configured for if the same agent trips a specified threshold in three consecutive rounds. The Atlanta cloud agent trips the rule in round one, the Ashburn cloud agent trips it in round two, and the San Francisco cloud agent trips it in rule three.

In this scenario, the alert rule would not trigger when using sticky agents. Either Atlanta, Ashburn, or San Francisco would need to trip the rule in three consecutive rounds to trigger the alert.

This can be used to configure alerts about the health of the network in a specific agent’s location, to increase confidence in the accuracy of alerts being sent (for example, issues that are seen from the same set of agents across multiple rounds), or to improve the signal to noise ratio by reporting on agent health as opposed to only test health.

**Cloud and Enterprise Agents**

* Improved the warning message that notifies users when an agent set is mixed, as bandwidth measurements are not allowed to run from Cloud Agents.
* The Endpoint agent now supports Microsoft Edge version 79 or higher for collecting browser session metrics. To install the extension:
  1.  1\.

      On the desired endpoint, launch Microsoft Edge.
* The createdTime, lastSeen and version fields are now exposed in the /endpoint-agents API.

Several improvements have been made to how Internet Insights displays outages. Outage event metrics (begin, end, and duration) have been added in the following areas of the UI:

*
  * A purple outage swimlane has been added below the timeline to improve visibility of long outages and outages that cross a five-minute period.
  * A tooltip appears when hovering over events on the swimlane, improving discoverability of individual outages and of when multiple outages occur at the same time.
*
  * In the text displayed while hovering over an affected interface node, a list of outages is now displayed when multiple outages occur at the same time.
*
  * Outage event metrics have been added to the **Table** view.
* In some instances, an issue occurred when a transaction script failed for a reason other than a test timeout that resulted in the error not being reported correctly. This has now been resolved, and detailed error messages should be seen for all failed transaction scripts.
* Previously, there was no option in Transaction test settings to enable following redirects in the HTTP server layer of the test. This has been corrected.
* Fixed an issue that only allowed Latin1 characters in the post body; all UTF-8 characters are now allowed
* Fuzzy searching in the agent selector in test settings has been disabled due to unexpected results.
* DNS Server snapshots that had a server selected were producing an incorrect "Invalid URL parameters" popup. This has been corrected.
* The link to the "Getting Started" videos in the Help & Support dropdown was not loading correctly. This has been fixed.
* Previously, creating a test with a duplicate test name failed with no feedback. The intended error message has been restored.
* An issue occurred when highlighted controls in the Device Topology view were not updating when the selected metric was changed. This has been fixed.
* An issue occurred where organizations with large numbers of Endpoint Agents could not use labels to correctly filter their data in dashboards and reports. This has been resolved.
* Previously, the AlertList widget included DNS+ alerts, but the AlertGrid widget does not. This lead to inconsistencies when looking between the two widgets. DNS+ alerts are now available in the AlertGrid widget.
* Endpoint Agent links inside the map widget were incorrectly pointing to the Enterprise Agent list. This has been resolved.
* An issue occurred when too much data resulted in the browser being unable to render the Path Visualization. This following corrections have been made to resolve this issue:
  * The error message displayed in the UI has been corrected, and now states “The path trace graph is too big, try adding some filters.”
  * The default grouping has been set to “Agents” in all Endpoint Agent view scenarios.
* An issue occurred where Path visualization controllers ( Filter, Group By, and Number of hops etc) were not displayed when there was too much data. This has been resolved.
* An issue occurred in the network topology where trying to apply any filter would result in a spinning wheel and not return any options. This is now fixed.
* An issue that caused the agent label color to revert to gray when the name was edited has been corrected.
* Previously, the Verify Content checkbox stayed enabled after removing specified content when setting up a new test. This is now fixed.
* An issue occurred with some path visualization filters where search options were filtered out and not displayed as they were not on the current pagination page. This issue has been fixed.
* An issue when creating / modifying a test resulted in the custom user agent string disappearing from the UI after saving. This has been fixed.
* The support chat window was not visible on the Endpoint Agents → Overview page. This has been corrected.
* An issue occurred with the Internet Explorer extension where hovering over an element in the browser session waterfall displayed the HTTP method as UNKNOWN. An error message to show that headers for the IE extension are not supported.
* A recent change to the user profile created during registration allowed non UTF-8 characters to be used in a username, causing the username to fail to register. This has been corrected, and only valid UTF-8 characters can now be submitted.
* An error occurred when opening some share links where an incorrect popup error would occur. This has been fixed.
* An issue occurred where clicking the gear icon next to a scheduled test did not filter and expand the scheduled test settings panel. This has been resolved.
* Fixed an issue where Endpoint Agents with connection failures were not showing a severity color.

The COVID-19 virus is putting a huge strain on IT and network teams all around the world. To assist with managing your end-user experience, ThousandEyes is offering free access to our End User Monitoring until July 31, 2020. If this is of interest to you, reach out soon — enrollment for this offer ends on June 30, 2020. For more information, please see our

[blog](https://blog.thousandeyes.com/helping-support-remote-workers-irregular-operations/)

or

[contact](https://www.thousandeyes.com/remote?utm\_source=Release-Notes\&utm\_medium=Textlink\&utm\_campaign=Helping-Support-Remote-Workers-Irregular-Operations)

the ThousandEyes team.

**Migration of Transaction (Classic) Tests**

In the next release, ThousandEyes will be disabling the ability to create additional transaction (Classic) tests from the product.

ThousandEyes will be working with individual customers as well as making an automated conversion process from within the product console available to assist with the migration process. This tool is expected to be available in May. If you need the ability to create additional transaction (Classic) tests after April 30, contact the ThousandEyes support team.

**New Documentation Platform**

ThousandEyes is excited to announce the launch of our new website for product documentation. This is the first stage in our efforts to provide users with an improved content experience.

#### New Features and Enhancements <a href="#new-features-and-enhancements-2" id="new-features-and-enhancements-2"></a>

**Cloud and Enterprise Agents**

**TLS Certificate Expiration and Session Information**

ThousandEyes has introduced the ability to alert on certificate expiration and TLS session information. All existing and new HTTP server tests will now include TLS session information such as the certificate chain, TLS version, and cipher suite negotiated in a new slide-out modal that will also include HTTP request and response headers:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-3a95185e2488b2b9ed22c71122ce5af80a1024be%2Frelease-notes\_2020-04-28\_feature-tls-one.png?alt=media)

In addition to being able to view TLS session information in HTTP Server view, customers can configure alerts for the following new associated metrics:

* Weaker Cipher Suite negotiated

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-d370b65af28cbde3f91c75afcb11019ed21228e4%2Frelease-notes\_2020-04-28\_feature-tls-two.png?alt=media)

Certificate chain and session information have also been added to the _/v6/web/http-server/{testID}?certificates=1_ endpoint. Example output is shown below:

"sslCipher": "ECDHE-RSA-AES128-GCM-SHA256",

"notValidAfter": "2020-06-03 12:00:00",

"notValidBefore": "2018-05-08 00:00:00",

"subjectName": "github.com",

"issuerName": "DigiCert SHA2 Extended Validation Server CA",

"fetchDateInValidCertDateRange": true,

**White Node Collapsing in Path Visualization**

To improve path visualization page performance, instances with three or more consecutive white (star nodes) in the path visualization will be collapsed into a group by default.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-877a6072d714bf1dfba5abbb8b6ea25380879ce1%2Frelease-notes\_2020-04-28\_feature-white-node-one.png?alt=media)

Expanded path visualization after clicking on the grouped number:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-5946765812ae0f969668f24a19d20709cdf61509%2Frelease-notes\_2020-04-28\_feature-white-node-two.png?alt=media)

* Pagination has been added to the dashboard “Test Table” widget.
* The “Shared” dashboard label has been renamed “Shared with others” for dashboards shared across account groups.
* Browser-based tests have been upgraded from Chromium 68 to Chromium 80.
* Forwarding loss can now be shown within Endpoint Agent path trace views.
  * **Important:** This enhancement will be available with the next Client release (currently estimated for May 4th).
* The Agent Settings page is now paginated to improve usability when managing large numbers of Endpoint Agents.
* Added a welcome page to help customers get started with Internet Insights:
  * For subscribers: The content covers key concepts, product areas, and links to existing resources and can be re-launched from the Help menu.
  * For non-subscribers: The Internet Insights navigation menu link now directs users to in-product content instead of opening the product offering page in a new tab.
* Internet Insights outage alert rule names can now be edited.
* The Internet Insights destination network filter has been renamed from "Network" to "Destination Network" in order to make it easier to distinguish from the affected interfaces network filter.

The ThousandEyes v7 API (preview) now includes the an alerts endpoint. For more information, see the

[developer documentation](https://developer.thousandeyes.com/v7/)

.

* The last seen IP address of an Endpoint Agent is now available via the API.
* The Endpoint Agent’s name can now be updated via the API.
* The username associated with an Endpoint Agent is now available via the API.
* ThousandEyes has made a change to the Sharing section that lists the Snapshots and Saved Events available. Specifically, we removed the 'Shared with Me' from the Snapshots, as many customers found it confusing to see snapshots that were shared with members of an organization account, in addition to those that were shared with the individual administrator.

#### Deprecated and Removed Features <a href="#deprecated-and-removed-features" id="deprecated-and-removed-features"></a>

**Temporary Suspension of Mobile Agents**

The ThousandEyes mobile cloud agents introduced in January will be taken offline for the near future in order to make architectural changes that will ensure we provide the best quality data on the optimum networks.

The following agents will be removed on April 30, 2020:

* Chicago, IL (AT\&T Mobile), (T-Mobile), or (Verizon Mobile)
* New York, NY (AT\&T Mobile), (T-Mobile), or (Verizon Mobile)
* Dallas, TX (AT\&T Mobile), (T-Mobile), or (Verizon Mobile)
* Los Angeles, CA (AT\&T Mobile), (T-Mobile), or (Verizon Mobile)
* San Jose, CA (AT\&T Mobile), (T-Mobile), or (Verizon Mobile)

**Adobe Flash Support for Transaction Tests**

Transaction tests no longer support Adobe Flash-based user workflows.

* An issue occurred where there was a difference between the time shown in the dashboard test table widget when compared to the Test view. This was caused by the widget using UTC rather than the local user time, and has been resolved.
* In rare instances, an issue occurred where a report snapshot was emailed twice instead of once. This has been resolved.
* An issue occurred where the "location" filter for Endpoint Agents was presenting either incorrect options or no options at all. This has been fixed.
* Previously, some customers were unable to run Transaction tests on some Enterprise Agents because another process was binding to port 53 on a network interface created by te-sandboxd. A "warn"-level log will now appear in te-sandboxd when this configuration is detected.
* Previously, Transaction tests were not able to perform downloads.waitForDownload() commands in a test that is configured to use an HTTP proxy. This has been resolved.
* Previously, some snapshots of browser-based test data were taking longer than an hour to process. This has been resolved.
* Previously, in Transaction test views, very long marker names could cause their corresponding durations to appear in the wrong place. Layout and styling adjustments have been made to resolve this error.
* An issue occurred where several data points were missing or empty when connecting via a Cisco AnyConnect VPN. This has been resolved.
* Fixed an issue that resulted in an "account mismatch" check misfiring during uninstalls.
* An issue occurred where an instant test would show “Loading” forever if agents were submitting data, but not for the selected metric. This has been resolved.
* An error caused the support chat window to be hidden in some views. This has been fixed.
* An error was caused by the Endpoint Agent link speed being inconsistently calculated. This has been resolved.
