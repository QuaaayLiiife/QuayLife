# Release Notes: March 2020

The COVID-19 virus is putting a huge strain on IT and network teams all around the world. To help with the increased surge of remote workers, we at ThousandEyes are offering our Endpoint Agent product, free of charge. For more information, please see our

[blog](https://blog.thousandeyes.com/helping-support-remote-workers-irregular-operations/)

or

[contact](https://www.thousandeyes.com/remote?utm\_source=Release-Notes\&utm\_medium=Textlink\&utm\_campaign=Helping-Support-Remote-Workers-Irregular-Operations)

the ThousandEyes team.

In an upcoming release, ThousandEyes will upgrade the version of Chromium used by browser-based tests (Page Load, Transaction \[Classic], and Transaction tests) from version 68 to version 79. As part of this upgrade, Flash will no longer be supported, and any Page Load, Transaction (Classic), or Transaction test that depends on Flash is unlikely to continue working.

#### New Features and Enhancements <a href="#new-features-and-enhancements" id="new-features-and-enhancements"></a>

When you create a report or a dashboard, you can now exclude data that was captured during a configured alert suppression window. This change should improve the reliability of ThousandEyes reports and dashboards, as they will not include data on planned downtime or maintenance windows.

The **Reports** page now includes the **Color Grid** widget. This widget has identical functionality to that of the **Color Grid** widget found in the **Dashboards** page.

The message that the Alert List widget displays when there are no active alerts has been updated from **No Data** to **No Alert Activity**. The previous message implied that the account had never had any alerts; the new message indicates that there are currently no alerts.

On the **Overview** page, the default time range is now 60 minutes. The previous default range was 10 minutes, which led to confusion if there was no data within that period. With a longer default range, you should more easily see the overall health of your users’ experience.

On the **Usage and Billing** page, projections have been updated and should no longer result in discrepancies when compared to the **Test Settings** page.

#### Deprecated and Removed Features <a href="#deprecated-and-removed-features" id="deprecated-and-removed-features"></a>

**Alert Notifications for HipChat**

As announced earlier, ThousandEyes has ended support for alert notifications with HipChat. The ThousandEyes Support team has worked with affected customers, and HipChat integrations have been removed.

* In order to better support tests that have a large number of traces, the Path Visualization view now uses a different method for pagination. Pagination is now based on the total number of traces in the visualization, rather than on the number of source agents. The new pagination provides faster rendering of the Path Visualization.
*   When an alert notification included a link to see a BGP test view, the link resulted in the following error:

    `The given server isn’t valid for the current state.`

    The error has been resolved.
* On the **Reports** page, when data in the table widget was grouped by agent label, an empty column was created. This issue has been fixed.
* When an agent label was deleted, tests that were attached to that label could not be enabled or disabled with the **Enabled** checkbox. You can now enable and disable these tests

The COVID-19 virus is putting a huge strain on IT and network teams all around the world. To help with the increased surge of remote workers, we at ThousandEyes are offering our Endpoint Agent product, free of charge. For more information, please see our

[blog](https://blog.thousandeyes.com/helping-support-remote-workers-irregular-operations/)

or

[contact](https://www.thousandeyes.com/remote?utm\_source=Release-Notes\&utm\_medium=Textlink\&utm\_campaign=Helping-Support-Remote-Workers-Irregular-Operations)

the ThousandEyes team.

​

[status.thousandeyes.com](https://status.thousandeyes.com/)

is a unified service for monitoring health statistics, viewing announcements, and managing notification subscriptions. ThousandEyes platform and Cloud Agent announcements, traditionally posted at success.thousandeyes.com, will now be posted at status.thousandeyes.com.

Users may now choose from email, SMS, or RSS notification. Due to new subscription options, all previous notification subscriptions will not be carried over to this new service. We encourage users to

[sign up and select their preferred notification options](https://status.thousandeyes.com/)

as soon as possible. Notifications from our legacy platform will be discontinued on April 30th.

Our support team is available to answer any questions via our in-application chat or \[email protected]

In an upcoming release, ThousandEyes will upgrade the version of Chromium used by browser-based tests (page load, transaction \[classic], and transaction tests) from version 68 to version 79. As part of this upgrade, Flash will no longer be supported, and any page load, transaction (classic), or transaction test that depends on Flash is unlikely to continue working.

#### New Features and Enhancements <a href="#new-features-and-enhancements-1" id="new-features-and-enhancements-1"></a>

For users who are implementing SD-WAN at their branches, a key need is the ability to measure performance across each WAN circuit. Currently, SD-WAN policies determine which WAN circuit is preferred for traffic that originates from the agent. Allowing the ability to select the interface and IP address for agent traffic allows users to direct agent traffic to across a particular WAN circuit.

You can now configure additional network interfaces for the ThousandEyes Virtual Appliance, and select which interface should be used for each test. Alternatively, you can also configure additional IP addresses for an existing interface. For a detailed guide, see this

[ThousandEyes Knowledge Base article](https://success.thousandeyes.com/PublicArticlePage?articleIdParam=kA02R000000UL9tSAG\_Enterprise-Agent-Interface-Selection)

.

To configure which interface should be used for a test, go to **Cloud & Enterprise Agents > Test Settings**:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-2ccf5107ecc88b88ee1b9d6f59c88a09c9b4a951%2Fwhats-new\_changelog-1.png?alt=media)

**Alerts Based on System Metrics**

For Endpoint Agents, you can now configure alerts to be triggered based on system metrics (CPU and memory). These system-metrics alerts are included in the Alert List page and in notifications in the same way as other alert types.

**TCP and TLS Connections in Transaction Scripts**

Transaction script users can now use **import net** from '**thousandeyes**', in order to take advantage of the helper methods connect(port, **host)** and **connectTls(port, host, options)** for forming raw TCP and TLS connections, respectively.

Note that these methods return promisified sockets, allowing users to **await** on method calls for sending and receiving bytes. Previously, users had to follow a clumsy process of registering and deregistering callbacks from a standard Node.js socket.

**Agent Groupings in the Internet Insights Topology View**

ThousandEyes has improved the way agents are displayed and organized in the Topology view. This change introduces three new agent grouping options:

* Origin Network - Groups agents by their origin network.
* Next Hop Network - Groups agents by the network in the next hop.
* Agent - Lists agents (sorted by the number of affected tests).

If Internet Insights does not have enough information about an agent to display details, it includes that agent in the Other Networks grouping.

**New Path Visualization Probing Mode**

In certain customer environments, middleboxes like Palo Alto and Juniper firewalls interfere with the way the ThousandEyes platform collects path trace metrics, leading to incomplete path information. In order to better support such scenarios, ThousandEyes has added the capability to perform path trace "in session", which first initiates a TCP session with the target server and sends path trace packets within that TCP session. For tests with Network metrics, the new option is configured in the Advanced Settings of the test, using the Path Trace Mode setting. Select the **In Session** checkbox:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-19e64281fd8f600f834f95648566698d6a00df17%2Fwhats-new\_changelog-2.png?alt=media)

This capability has been added to the ThousandEyes API as well, in a new test object field called **pathTraceMode**.

* Slack integrations used the default Slack channel, rather than the one specified in the configuration. The system has now been changed so that it now sends alerts to the specified channel.
* In the Recorder IDE, when you click Insert Markers, the system now inserts a **markers.start( )…markers.stop( )** block, instead of a call to **markers.set( )**. The new block is designed to clarify the start/stop nature of the calls. **markers.set( )** is still supported as before.
* A bug has been fixed that caused the Box-and-Whiskers widget to display incorrect data.
* On the Dashboards page, the Alert List widget was not automatically updating the relative start time of active alerts when the dashboard was refreshed.
* On Windows, the Chrome browser extension component of Endpoint Agent in some cases incorrectly reported a status of inactive. ThousandEyes has fixed this issue by more accurately determining the extension's status: rather than being based on installation alone, the extension's status is now based on whether it is communicating with the backend.
* An issue has been fixed that prevented the transfer of disabled tests to a different account group if an organization was close to its usage limit.
