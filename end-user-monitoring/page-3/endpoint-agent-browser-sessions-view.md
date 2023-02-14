# Endpoint Agent Browser Sessions View

Data collected by an Endpoint Agent from either browsing webpages within domains listed under a monitoring profile from a monitored network, or from manually triggering a recording session, is displayed in the **Browser Sessions** view under **Endpoint Agents > Views** for that account group.

This article provides an overview of the **Browser Sessions** view.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-76d43d2345329a3a10f7525a4ce93d0df158bc8e%2Fproduct-documentation\_endpoint-agent\_endpoint-agent-browser-sessions-view-1.png?alt=media)

Browser Sessions Visited Pages View

The **Browser Sessions** view can be broken into three sections:

* The **Views** list contains a list of all available views for Endpoint Agents. This includes the **Browser Sessions** view outlined in this article.

The sections below outline the primary and secondary sections of the view.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-fed6e8a5ebeae5fe9f8ce8f591a16d8e798d3b6c%2Fproduct-documentation\_endpoint-agent\_endpoint-agent-browser-sessions-view-2.png?alt=media)

The **Snapshot Selector** is a drop-down menu of all saved Endpoint Agent snapshots. For more information on snapshots, see

[Endpoint Agent Test Snapshots](https://docs.thousandeyes.com/product-documentation/tests/sharing-test-data#endpoint-agent-test-snapshots)

.

The **Global Filters** are a set of dynamic drop-down menus that allow users to drill down into the data presented in the **Browser Sessions** view. These filters allow users to configure which agents they see data from, as well as specify details including which destinations, gateways, and VPN vendors to focus on.

The **Metric Selector** is a drop-down menu that lists the available metrics to display in the timeline.

The **Timeline** is the primary focus of all Endpoint Agent views. It shows test data from the last 30 days, or the length of time the test has been enabled (whichever is the lesser value). The data shown on the timeline can be manipulated by selecting the time range shortcuts, by clicking within the timeline to select a particular round of data, or by highlighting a range within the timeline, using the **Time Range Selector**.

The **Time Range Selector** allows users to customize the window the **Timeline** focuses on, by moving the highlighted section to the desired date, and increasing/reducing the size of the highlighted time range as necessary. This area of focus can be between 24 hours and 14 days long.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-70d8f5bc9adc90603fc8d69b3aaa3c5ce151d7cc%2Fproduct-documentation\_endpoint-agent\_endpoint-agent-browser-sessions-view-3.png?alt=media)

The **Overview** provides the average user experience score for the specified round of data.

The **Detailed Metrics** tabs are a dynamic set of additional views that provide users with varying perspectives on the same data, allowing them to navigate through and dive into the data in the way that best suits their needs. These views include:

* The **Pages** tab is a table view of all the visited sites for the specified round of data.
* The **Sessions** tab is a table view of all user sessions for the specified round of data.
* The **Map** tab displays the geolocation of each of the agents, and the relevant collected metrics.
* The **Table** tab provides a detailed breakdown of the metrics collected per agent for the selected time interval.

The **Path Visualization** view allows you to visualize the layer 3 hop-by-hop topology from the source Endpoint Agent to the test target, to identify problem areas in both the private and public network infrastructure.
