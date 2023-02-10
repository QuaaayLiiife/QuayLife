# Using the Page Load View

When you create and run a page load test, you can see the test data under **Cloud & Enterprise Agents > Views**. Select your page load test as the Current Test at the top of the view window to gain access to the following views:

* BGP Route Visualization (note that all Network views are optional)

This article focuses solely on the Page Load view. For general information on the ThousandEyes standard view layout, see

[Getting Started with Views](https://docs.thousandeyes.com/product-documentation/getting-started/getting-started-with-views)

.

This article contains screenshot views and instructions that reference “Classic” test views. ThousandEyes is in the process of introducing multi-service views that combine multiple test views into one multi-service view. See

[Multi-Service Views](https://docs.thousandeyes.com/product-documentation/internet-and-wan-monitoring/tests/multi-service-views)

for more information.

The top of the Page Load view shows a timeline similar to other views, with a time period slider below. The only **Metric** available is Page Load Time. Use the **Agent** selector to choose a specific Cloud or Enterprise Agent.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-7562a771fedf6ff13eea7adb07b77c4abf754b5a%2Fpage-load-view-001-first-load-timeline-top.png?alt=media)

The example above shows test results for a page load test for **slate.com**, a popular online news magazine, using multiple agents in different locations.

* Without an agent selected, the timeline shows the average page load time, calculated from all of this test’s agent locations.
* Scroll down in the Page Load view window to see the **Map**, **Table**, and **Waterfall** tabs displayed beneath the timeline.

When you have a specific Cloud or Enterprise Agent selected in the Page Load view, the timeline shows page load time for that agent, charted against the average page load times across all agents, as shown below.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-85a6ead049ca2bfb6b8f620865759739292b9ced%2Fpage-load-view-002-timeline-agent-selected.png?alt=media)

The **Map** tab as shown below displays a global map showing all of the agents that are running the test, with a Details panel to summarize data and any error messages reported by the agents. The color of the agents shown on the map, as well as the bar graphs, indicates the speed relative to the test duration, as specified by the **Timeout** parameter in the **Advanced Settings** tab for the test configuration in **Cloud & Enterprise Agents > Test Settings**. Anything shown in red indicates that the test timed out from the indicated agent. Redirect time is taken into account when determining total page load time.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-82bf814f684e266ed9f9ca972e17fb2b861c9dfd%2Fpage-load-view-003-map-all-agents.png?alt=media)

To view data from a specific agent in the details panel, click an agent icon in the map, or use the Agent selector at the top of the screen. To select an agent directly from the map, click the agent’s icon in the map. The image below shows the Page Load **Map** tab with one agent selected.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-bf6ca93af8f84b873370a3276a6e08ea0c5669c8%2Fpage-load-view-004-map-one-agent-selected.png?alt=media)

On the **Map** tab for the Page Load view, if no agent is selected, you will see average load times for both Document Object Model (DOM) load and page load, in bar graph and numeric form.

* If one or more agents have not yet reported data for the current test round, for example a page load timeout, you’ll see a warning message in the Details panel.
* It is possible for a test to obtain a DOM load time but not a page load time, if the test times out. If the test obtains a DOM load time but no page load time from one or more agents, the DOM load time is incorporated into the average DOM load.
* If the test obtains a DOM load time but no page load time, the DOM load time is displayed.

If one agent is selected, either on the **Map** tab itself or using the Agents drop-down at the top of the window, the Map tab for the Page Load view shows the actual DOM load and page load times for the last test round reported by that agent.

### Page Load View, Table Tab <a href="#page-load-view-table-tab" id="page-load-view-table-tab"></a>

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-1e4eae49bf2d8b44b159e2879b254a6db14e33d9%2Fpage-load-view-005-table-tab.png?alt=media)

The **Table** tab as shown above displays agent data including:

* Agent name (click an entry to select that one agent)
* Date and time of the last data data collection cycle for that agent
* Wire size (size prior to any decompression on the receiver/client)

### Page Load View, Waterfall Tab Summary <a href="#page-load-view-waterfall-tab-summary" id="page-load-view-waterfall-tab-summary"></a>

The **Waterfall** tab shows how a browser interacts with each object on the target page, including the order in which each object loads. Below is an example of what the **Waterfall** tab looks like for the page load test, before selecting any agents:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-0c6095557894a59e4a382daa418da4e16149f890%2Fpage-load-view-006-waterfall-no-agent-by-domain.png?alt=media)

On the **Waterfall** tab for the Page Load view:

* **Breakdown by Domain or Provider**: Use the toggle button to view data by domain or by provider for bytes received, throughput, and total response rime. This can be helpful when you are troubleshooting a slow page load that is dependent on components from other domains.
* **Summary averages**: When no agent is selected, this panel shows average bytes received, throughput, and response time.

When a single agent is selected, the summary on the Waterfall tab shows the throughput and response time for the selected test round, for the selected agent, as shown below.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-c3b02b1747fd466db02d9b26d810caf55c62a7a6%2Fpage-load-view-007-waterfall-summary-one-agent.png?alt=media)

### Waterfall Details for Page Load View <a href="#waterfall-details-for-page-load-view" id="waterfall-details-for-page-load-view"></a>

Waterfall details as shown below are only available when you have an agent selected. You can select an agent by clicking a location on the **Map** tab, clicking an agent on the **Table** tab, or by choosing an agent from the **Agent** drop-down at the top of the screen.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-b45db9fe236d47b74860175281aed65fdb3dc020%2Fpage-load-view-008-page-load-waterfall-detail.png?alt=media)

The image below shows how to hover over an item in the **Object** column to see, for that object:

* URL used to fetch the object
* HTTP method, for example GET
* Target IP used to fetch the object
* Response code, for example "200 OK"
* Content type, for example "application/javascript" or "text/html"
* Protocol, for example "HTTP 2.0"
* Pop-out icon, click to load the object in a new browser window

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-41244fce60c2a4de0b68a8faa8f5754525939f85%2Fpage-load-view-009-waterfall-object-detail.png?alt=media)

Click a link in the **Headers** column to display a dialog showing the HTTP request and response headers, as shown below.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-402c650b66fa117cf63060e7cab2e6c600db7c8f%2Fpage-load-view-010-request-response-header.png?alt=media)

Hover over an object's total load time in the **Waterfall** column as shown below, to see a breakdown of the load time by connect phase, for example Blocked, DNS, Connect, SSL, Send, Receive.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-fe7a88eb29f9470e801b15c0cd9563a13fabbe25%2Fpage-load-view-011-object-load-time-detail.png?alt=media)

If an object shown on the Waterfall indicates an error, you can open it directly by clicking the pop-out icon to the right of the name of the object, as shown below.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-d00ce6c61d027046883cb99cbe7c02ae17b6fbd2%2Fpage-load-view-012-object-load-error-detail.png?alt=media)
