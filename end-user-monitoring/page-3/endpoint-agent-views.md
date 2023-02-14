# Endpoint Agent Views

This article provides an overview of the **Agent Views** view. This view enables users to search for an agent and display all the information related to scheduled tests, automated session tests, local networks, and browser session data for that agent.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-4074f083ff430d66e18a645e98b904a476b0d65d%2Fproduct-documentation\_end-user-monitoring\_viewing-data\_single-agent-view-1.png?alt=media\&token=ecefe027-270f-452a-856f-361ce11a05e9)

The **Agent Views** view can be broken into two sections:

*   The

    [**Agent Performance**](broken-reference)

    section, which includes detailed information related to the agent's local networks, scheduled tests, automated session tests, and browser sessions.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-f2e6768ebc409df672f0990d1f9d946b505f94e3%2Fproduct-documentation\_end-user-monitoring\_viewing-data\_single-agent-view-2.png?alt=media\&token=f9e32a9b-aab4-4ebf-86df-7b018a255f88)

The **Agent Details** section provides detailed information about the selected agent, such as its **Hostname**, **Location**, **Agent Version**, **Users**, and **Labels**.

The **Search** field assists you to find the desired agent. You can perform the search using the following parameters:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-29f7aaa81f8483a82e9eb9e0d4cbb8cf4684647d%2Fproduct-documentation\_end-user-monitoring\_viewing-data\_single-agent-view-11.png?alt=media)

The **Timeline Range Selector** allows you to customize the time window that the timeline focuses on. You can select the time range as a **Relative Time Interval** or a **Fixed Time Interval**. By default, this field is set to **Relative Time Interval** and **Last 24 hours**.

This section displays all the information related to scheduled tests, local networks, and browser session data for the selected agent.

This section displays the local network and wireless access connectivity for the selected agent over the chosen time period.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-c270cf7819d7cbac1df6dda097eb7e66651d2726%2Fproduct-documentation\_end-user-monitoring\_viewing-data\_single-agent-view-3.png?alt=media\&token=2ae428b6-feea-4346-8a68-48e7dd9944c1)

The left hand side lists all the major components associated with the local networks and their metrics for the time range selected. You can customize these components and metrics from the **Metrics** dropdown menu. The values displayed for each metric are the average values for the selected time range. The timeline adjacent to each metric displays the complete data for the selected time range. Hover over the timeline to see the local network data for a particular time in the specified range. You can click a given round on the timeline to view the main

[Endpoint Agent Local Networks View](broken-reference)

. This view opens on the same round and metric, filtered by the specific agent.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-6d37adb83059b9defebaeb34c325da64c2ec5183%2Fproduct-documentation\_end-user-monitoring\_viewing-data\_single-agent-view-12.png?alt=media)

The wireless information (i.e., SSID, Channel, Phy Mode) within the Network Access row is displayed on the tooltip. Hovering over the timeline displays the tooltip information making it easier to correlate data when troubleshooting issues related to it.

This section displays the data for the Web and Network scheduled tests.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-9fd32c7944e6f7889d4a5428ddfe1893dd4a4445%2Fproduct-documentation\_end-user-monitoring\_viewing-data\_single-agent-view-4.png?alt=media\&token=36561f08-b296-4319-9ba3-b6111e904d02)

The left hand side lists all the scheduled tests associated with the selected agent and their metrics for the time range selected. Use the **Metric** dropdown menu to toggle between **Web** and **Network** layers, and among the metrics available for those layers. By default, the data displayed is for the Network layer and the default metric selected is **Loss**.

The values displayed for each metric are the average values for the selected time range. The timeline adjacent to each metric displays the complete data for the selected time range. Hover over the timeline to see the data from the scheduled test for a particular time. This view supports pagination, and you can customize the number of tests to be displayed by using the **Show** dropdown menu.

You can click a given round on the timeline to view the main

[Endpoint Agent Scheduled Tests View](broken-reference)

. This view opens on the same round and metric, filtered by the specific agent.

This section displays the data for the Endpoint Agent's automated session tests.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-3286d887b4ed456a698c1dea04e929de6ccc0473%2Fproduct-documentation\_end-user-monitoring\_viewing-data\_single-agent-view-7.png?alt=media)

The left hand side lists all the automated session tests associated with the selected agent and their metrics for the time range selected. Use the **Metric** dropdown menu to select the desired metrics. By default, the default metric selected is **Loss**.

The values displayed for each metric are the average values for the selected time range. The timeline adjacent to each metric displays the complete data for the selected time range. Hover over the timeline to see the data from the automated session test for a particular time. This view supports pagination, and you can customize the number of tests to be displayed by using the **Show** dropdown menu.

This section displays the data for the Endpoint Agent's browser sessions.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-99be7c7cbdb65dff127887497fd7cfabad0d5ae3%2Fproduct-documentation\_end-user-monitoring\_viewing-data\_single-agent-view-5.png?alt=media\&token=683d8530-93e2-4d3f-9a26-424512739287)

The left hand side lists all the browser sessions associated with the selected agent and their metrics for the time range selected. Use the **Metric** dropdown menu to toggle between **Web** and **Network** layers, and among the metrics available for those layers. By default, the data displayed is for the Web layer and the default metric selected is **Response Time**.

The values displayed for each metric are the average values for the selected time range. The timeline adjacent to each metric displays the complete data for the selected time range. Hover over the timeline to see the browser session data for a particular time. This view supports pagination, and you can customize the number of tests to be displayed by using the **Show** dropdown menu.
