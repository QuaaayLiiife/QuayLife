# Endpoint Agent Automated Session Tests View

ThousandEyes Endpoint Agents run Automated Session Tests to monitor performance of applications such as Webex, Zoom, etc. These tests are similar to the Scheduled tests but only run the agent-to-server tests.

This article provides an overview of the **Automated Session Tests** view, found within the

[Endpoint Agents > Views](https://app.thousandeyes.com/view/endpoint-agent/)

section of the web application.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-dd650379ee8c02f93f2dbec43debf1c4d406b6d2%2Fproduct-documentation\_end-user-monitoring\_viewing-data\_endpoint-agent-dynamic-app-tests-view-3.png?alt=media)

The **Automated Session Tests** view can be broken into three sections:

* The **Views** list contains a list of all available views for Endpoint Agents. This includes the **Dynamic Application Tests** view outlined in this article.

The sections below outline the primary and secondary sections of the view.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-b4695cddb4b92da36fb913835eda3b31844a2c09%2Fproduct-documentation\_end-user-monitoring\_viewing-data\_endpoint-agent-dynamic-app-tests-view-1.png?alt=media)

The **Snapshot Selector** is a drop-down menu of all saved Endpoint Agent snapshots. For more information on snapshots, see

[Endpoint Agent Test Snapshots](https://docs.thousandeyes.com/product-documentation/tests/sharing-test-data#endpoint-agent-test-snapshots)

.

The **Test Selector** is a drop-down menu of all available tests (including disabled tests). Users can see the current selected test, hide disabled tests, and search for other configured tests.

The **Global Filters** are a set of dynamic drop-down menus that allow users to drill down into the data presented in the **Scheduled Tests** view. These filters allow users to configure which agents they see data from, as well as specify details including which destinations, gateways, and VPN vendors to focus on.

The **Metric Selector** is a drop-down menu that lists the available metrics to display in the timeline.

The **Timeline** is the primary focus of all Endpoint Agent views. It shows test data from the last 30 days, or the length of time the test has been enabled (whichever is the lesser value). The data shown on the timeline can be manipulated by selecting the time range shortcuts, by clicking within the timeline to select a particular round of data, or by highlighting a range within the timeline, using the **Time Range Selector**.

The **Time Range Selector** allows users to customize the window the **Timeline** focuses on, by moving the highlighted section to the desired date, and increasing/reducing the size of the highlighted time range as necessary. This area of focus can be between 24 hours and 14 days long.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-310eb9d51030b3a7ccaaf7834a1f74601d2110da%2Fproduct-documentation\_end-user-monitoring\_viewing-data\_endpoint-agent-dynamic-app-tests-view-2.png?alt=media)

The **Detailed Metrics** tabs are a dynamic set of additional views that provide users with varying perspectives on the same data, allowing them to navigate through and dive into the data in the way that best suits their needs. These views include:

* The **Map** tab displays the geolocation of each of the agents, and the relevant collected metrics.
* The **Table** tab provide a detailed breakdown of the metrics collected per agent for the selected time interval.

The **Path Visualization** view allows you to visualize the layer 3 hop-by-hop topology from the source Endpoint Agent to the test target, to identify problem areas in both the private and public network infrastructure.
