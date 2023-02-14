# Dashboard Widgets

This page describes each of the dashboard widgets available within the ThousandEyes platform. See

[Examples of Widgets](broken-reference)

for the configuration options for each widget type.

A _widget type_ refers to a category of widgets. For example, live status widgets includes the Agent Status and Alert List widgets.

The table below summarizes the widgets available for ThousandEyes dashboards, grouped by widget type.

| Widget Type: | Live Status                                                                                                                                                    |
| ------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Alert List   | A look at the alerts that were active during the configured time period.                                                                                       |
| Tests        | A 12-hour, live display a list of tests configured in your account group for a one stop glance at high level test health. Grayed-out rows show disabled tests. |
| Agent Status | A live look at the status of your enterprise or endpoint agents to give you an idea of overall agent health.                                                   |

| Widget Type: | Breakdown                                                                                                                                                                                                                                                                                          |
| ------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Stacked Bar  | Provides horizontal histogram bars with multiple values, which are useful for composite metric data (such as HTTP response or fetch time) and for comparing values between multiple tests, or comparing values on a per-country basis. Bars can be oriented horizontally or vertically as columns. |
| Grouped Bar  | Represents multiple values as single bars in a group of bars. Bars can be oriented horizontally or vertically as columns.                                                                                                                                                                          |
| Pie          | Similar to stacked bar chart widgets, representing multiple values as proportionally sized segments of a pie.                                                                                                                                                                                      |

| Widget Type:       | Data Summary                                                                                                                                                                                                                                                             |
| ------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Table              | Allows a breakdown of numbers by rows and columns. Either rows or columns can list by test, country, continent, or data source (agents or BGP monitors) or the aggregate of those ("All").                                                                               |
| Multi-Metric Table | Can have columns with different metrics, rather than a single metric for the entire table.                                                                                                                                                                               |
| Number             | One or more cards, each card displays a single scalar quantity, such as an average of packets lost or page load times, or a number of alerts.                                                                                                                            |
| Color Grid         | Displays an array of colored cards, where each card's color depends on the configured color scale, with red representing errors or poor target test performance, green signifying good test performance, and shades in between indicating various levels of degradation. |

| Widget Type:     | Time Series                                                                                                                                                                                                                                                                                                                                                                                                |
| ---------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Line             | Line plots with time on the horizontal axis, and the selected quantity on the vertical axis.                                                                                                                                                                                                                                                                                                               |
| Stacked Area     | Line plots with time on the horizontal axis, and the selected quantities on the vertical axis. They are used similarly to stacked bar charts but showing values over time. Useful when looking at increases in overall response timing, error counts, and other components. Use the stacked area chart in place of where you're using stacked bar charts today, to show a progression of values over time. |
| Box and Whiskers | Plot data values versus time on the horizontal axis, with the vertical axis displaying the median, minimum and maximum data points per time value, along with a bar for the range of values represented by the second and third quartiles.                                                                                                                                                                 |

| Widget Type: | Maps                                                                                                                                                                                                |
| ------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Map          | Displays data on a world map, based on location of the testing systems (agents or BGP monitors). Data can be displayed per country, per continent, or per agent (if a non-BGP metric is displayed). |

Each widget has custom options for data sources, filters, and similar, as shown below.

| Widget Type: | Live Status                                                                                                                                                    |
| ------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Alert List   | Alert Types are BGP Routing, Cloud & Enterprise Agents, Devices, Endpoint Agents. Beneath these you can select ThousandEyes test types.                        |
| Tests        | Search your own tests by ThousandEyes test name, or exclude tests by name.                                                                                     |
| Agent Status | Choose from agents that you own, either endpoint agents or enterprise agents. (No option to see status of cloud agents, as those are managed by ThousandEyes.) |

| Widget Type: | Breakdown                                                                                                                                                                          |
| ------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Stacked Bar  | Data sources: Cloud & Enterprise Agents, Endpoint browser sessions, or Endpoint scheduled tests.                                                                                   |
| Grouped Bar  | Data sources: Alerts, CEA, Devices, Endpoint browser sessions, Endpoint local networks, Endpoint scheduled tests, Endpoint automated session tests, Internet Insights, or Routing. |
| Pie          | Data sources: Cloud & Enterprise Agents, Endpoint browser sessions, or Endpoint scheduled tests.                                                                                   |

| Widget Type:       | Data Summary                                                                                                                                                                       |
| ------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Table              | Data sources: Alerts, CEA, Devices, Endpoint browser sessions, Endpoint local networks, Endpoint scheduled tests, Endpoint automated session tests, Internet Insights, or Routing. |
| Multi-Metric Table | You can choose properties, but not data sources.                                                                                                                                   |
| Number             | Data sources: Alerts, CEA, Devices, Endpoint browser sessions, Endpoint local networks, Endpoint scheduled tests, Endpoint automated session tests, Internet Insights, or Routing. |
| Color Grid         | Data sources: Alerts, CEA, Devices, Endpoint browser sessions, Endpoint local networks, Endpoint scheduled tests, Endpoint automated session tests, Internet Insights, or Routing. |

| Widget Type:     | Time Series                                                                                                                                                                        |
| ---------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Line             | Data sources: Alerts, CEA, Devices, Endpoint browser sessions, Endpoint local networks, Endpoint scheduled tests, Endpoint automated session tests, Internet Insights, or Routing. |
| Stacked Area     | Data sources: Cloud & Enterprise Agents, Endpoint browser sessions, or Endpoint scheduled tests.                                                                                   |
| Box and Whiskers | Data sources: Alerts, CEA, Devices, Endpoint browser sessions, Endpoint local networks, Endpoint scheduled tests, Endpoint automated session tests, Internet Insights, or Routing. |

| Widget Type: | Maps                                                                                                                                                                               |
| ------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Map          | Data sources: Alerts, CEA, Devices, Endpoint browser sessions, Endpoint local networks, Endpoint scheduled tests, Endpoint automated session tests, Internet Insights, or Routing. |

The remainder of this page contains a more in-depth description of what each widget does, shows an illustrated example of each type of dashboard widget, and explains the configuration options for each widget.

To bring up the widget configuration screen, click the gear icon next to the widget displayed in a dashboard. For adding a new widget, click **+ Add Widget** in the dashboard where you want to add it, select the widget type, and the configuration screen will appear.

Live Status widgets include Alert List, Tests, and Agent Status.

The Alert List widget displays alerts that are currently active or were recently cleared within the configured period of time:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-6ecc0067eb2cf04cc15a7df8f7d030f2781e62c7%2Fproduct-documentation\_thousandeyes-basics\_working-with-the-dashboard-1.png?alt=media)

The Alert List widget includes the following columns:

* Active alerts display a red dot on the left-hand side.
* The alert duration displays in orange on the right.
* **Alert Rule** references the alert rule, associated with the test, that triggered the alert.
* **Alert Type** refers to the ThousandEyes test type. For example “Web - Transaction” refers to transaction tests, which are part of the Web layer or family of tests.
* If you click the link in the **Alert Source** column, you see the results view of the test that generated the alert.
*   Click the **View All Alerts** link in the top right-hand corner of the widget to open the

    [Alerts > Alert List](https://app.thousandeyes.com/alerts/list/active)

    view, where you can see all your alerts.

For further information about ThousandEyes alerting capabilities, see

[Alerts](https://docs.thousandeyes.com/product-documentation/alerts)

.

**Alert List Widget Configuration**

The Alert List widget configuration is shown below.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-6a8648c6a79e2a15331f73b66784eb4a9c534648%2Fdashboard-alert-list-widget-config.png?alt=media)

**Alert Type:** Configure the types of alerts to show. Various combinations can be configured, from BGP Routing, Cloud and Enterprise Agents, Devices, and Endpoint Agent classes of alert types.

**Limit to:** Number of alerts to show. If the amount of alerts to show exceeds the configured limit, a **Show more alerts** link is provided.

**Active within:** Limit the age of alerts shown. Only alerts that are currently active, or were active during the outlined period, are shown by the widget. The currently active alerts are listed first.

**Filters:** Additional filters can be configured to narrow down displayed alerts, by specific Tests, Labels, Agents, Alert rules, etc.

The Tests dashboard widget displays a list of tests as follows:

* Tests configured in your account group
* Tests shared to your account group via the Live Share feature
* Grayed-out rows indicating disabled tests

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-80cf08d9c1276bde3d41c143fe39426da55ecb04%2Fproduct-documentation\_thousandeyes-basics\_working-with-the-dashboard-2.png?alt=media)

Each test lists the name, the test type, the test's alert status, and a 12-hour trend graph of key metrics relevant to that test type. The Tests widget only shows test data for cloud and enterprise agents. It doesn’t show data from endpoint agents, devices, or BGP monitors.

1.  1\.

    _Header bar_ – Click a column name to sort the list of results by that column, or to toggle sort order between ascending and descending alphabetical order.
2.  2\.

    _Alert status_ – Shows red for an alert that is currently running, or green for a healthy test. No color indicates either that no alert rules are assigned to the test, or that alerts are disabled on the test.
3.  3\.

    _Test name hyperlink_ – Click to open the results page for that test. For a test type with multiple views, the default view opens.
4.  4\.

    _Trending values_ – Default metrics for each test type, using values collected over the trailing 12 hours. Navigate to any test round by clicking on the desired point on the graph.
5.  5\.

    _Current values_ – Default metrics for each test type, showing the most recent set of values collected when the page was last refreshed.
6.  6\.

    _Test configuration_ – Click to open the test's configuration page. The gear icon appears when you mouse over the row.

**Tests Widget Configuration**

The Test widget configuration is shown below.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-c502beb543e515d27df36e222244ac591c682e70%2Fdashboard-tests-widget-config.png?alt=media)

**Filter all/any:** Enter one or more filter criteria. Filter criteria will be displayed when you place focus on the text field. With "all" the filter displays matches of the criteria that meet all the criteria in the text field. With "any" the filter displays matches if any of the criteria are met. For example, two Test Name criteria of "ThousandEyes" and "Support" would match the tests "My ThousandEyes", "ThousandEyes Support site" and "Linux support website" if the selection were "any". If the selection were "all", then the match would only be "ThousandEyes Support site".

**Exclude all/any:** Identical to Filter all/any above, except matches cause exclusion from display in the widget.

**Data Suppression:** Check a box to enable a data exclusion filter.

* _Exclude Disabled tests:_ Omit tests that have been disabled. This is on by default.

The Agent Status widget is a global map that displays enterprise or endpoint agents that belong to your account group or have been shared with your account group, and whether those agents are online, offline, or disabled:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-a792f9521770eabdcd197b31ee7fdd15bf1cea0a%2Fproduct-documentation\_thousandeyes-basics\_working-with-the-dashboard-3.png?alt=media)

Enterprise Agent Status widgets display Enterprise Agents on a world map, using the agent's IP address with the ThousandEyes geolocation database, or manually configured geographical information to place the agent in the correct location on the map.

Agent locations are determined using:

* The IP address, using the ThousandEyes geolocation database
* Manually configured geographical information using the **Country** and **Region** settings on an agent (which override geolocation).

If the agent’s exact location cannot be determined:

* The agent is placed in the correct country if possible
* If no information is available, the agent is shown in a neutral location on the map

Each circle on the map displays a number if more than one agent is in that location. The color indicates the status of the agent:

* **Green:** Indicates an agent with up-to-date data uploads.
* **Red:** Indicates an agent which has not uploaded data in the current round.
* **Yellow:** Indicates a mix of agents that are and are not current in their data uploads.
* **Clear**: Indicates a disabled agent.

A summary legend of online, offline, and disabled agents displays in the upper-left corner. In the upper-right corner of the widget, zoom-in (**+**), zoom-out (**-**) and 100% zoom controls are available.

When you mouse over an agent dot, a tooltip displays the names and private and public IP addresses of the Enterprise Agents in that location - or names and host OS information for Endpoint Agents. If you click the name of an agent, the agent's configuration opens in the corresponding **Agent Settings** page.

**Agent Status Widget Configuration**

The Agent Status widget configuration is shown below.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-3f398ea735956a3fbea4f9b019fb41a029b504a2%2Fproduct-documentation\_thousandeyes-basics\_customizing-your-dashboard-8.png?alt=media)

**Agents**: This selector allows the widget to display either Enterprise Agents or Endpoint Agents.

**Show:** **Owned Agents** displays only those agents that belong to the user's current account group (i.e., agents installed using the account group's token). **All Assigned Agents** (Enterprise Agents only) displays owned agents, plus any agents shared to your account group from another account group in your organization.

**Filter:** Allows for the selection of specific agents or account groups.

Breakdown widgets include Stacked Bar, Grouped Bar, and Pie.

The Stacked Bar dashboard widget is useful for composite metric data (such as HTTP response or fetch time) and for comparing values between multiple tests or on a per-country basis. Bars can also be oriented vertically as columns.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-ace9ec8122f0f752188715d7a58bafe162f767f9%2Fdashboard-stacked-bar-widget-example.png?alt=media)

**Stacked Bar Widget Configuration**

The Stacked Bar widget configuration is shown below.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-7c76ea0be3f5d9ff563686fcf27d2c0e64b2054a%2Fdashboard-stacked-bar-widget-config.png?alt=media)

Stacked bar chart widgets have the following settings:

**Data Source:** The data source indicates which platform service will be referenced within the widget. Current options include:

* **Alerts:** Data is obtained from Platform alerts
* **Cloud and Enterprise Agents:** Data is obtained from scheduled tests performed by Cloud and Enterprise Agents
* **Devices:** Data is obtained from device-layer reporting
* **Routing:** Data is obtained from BGP tests

**Category:** The category choices depend on the **Data Source** selected. For example, if you select Cloud and Enterprise Agents as the data source, the Category drop-down shows you a subset of the ThousandEyes test type categories, for example Web - Transaction or Web - Page Load.

**Metric:** Options for metrics depend on the test type chosen in the previous **Category** selection. For example, in the Stacked Bar dashboard widget configuration, the metrics that you can choose from (Response Time, Total Fetch Time and Total Error Count) are each themselves composites of other metrics found in an HTTP Server test.

To continue with the example, suppose that you want your Stacked Bar widget to display the Response Time metric for all your HTTP server tests. Response Time consists of four distinct sub-metrics that are part of the HTTP server test: DNS resolution time, connect time, SSL time and wait time. In this dashboard widget, all of these four metrics are presented in a single stacked bar.

**Measure:** A statistical measurement. **Measure** types available depend on the **Metric** setting, and will be one or more of the following:

* _% positive (Total Error Count only):_ The percentage of measurements with non-zero error counts.
* _% zero_ (Total Error Count only): The percentage of measurements with error counts equal to zero.
* _nth Percentile:_ The value of the metric that contains n% of the measurements. When "nth Percentile" is selected, a text box will appear, allowing you to specify an integer for the percentile value from 1 to 99. 98% is the default. For example, a 98th Percentile whose value is 500 ms for a **Metric** of "Response Time" would indicate that 98% of the measurements of the response time were between 0 and 500 ms.
* _Maximum:_ The maximum value in the set of measurements, such as the response times of an HTTP Server test over the time period of the dashboard.
* _Minimum:_ The minimum value in the set of measurements, such as the response times of a HTTP Server test over the time period of the dashboard.
* _Mean:_ The value of the arithmetic mean (i.e. average) of the measurements. For example, a **Mean** of 50 ms for a **Metric** of "Response Time" would indicate that the average value of the response time in the reporting period was 50 ms.
* _Median:_ The value of the median measurement. For example, a **Median** of 50 ms for a **Metric** of "Response Time" would indicate that the value of 50 ms is the middle value in the range of all values of the response time in the reporting period.
* _Standard Deviation:_ The population standard deviation of a set of measurements, such as the response times, over the time period of the dashboard.
* _Total (Total Error Count only)_: The total number of errors in the reporting period.

**X-Axis** or **Y-Axis:** Arrange the data into bars by the following criteria, and orient the label(s) on the axis displayed :

* _All:_ Produces a single bar with all data.
* _Agent:_ Produces bars for each agent.
* _Continents:_ Produces bars for each continent/continental region (North America, Europe/EMEA, Asia/APAC, etc...).
* _Countries:_ Produces bars for each country.
* _Test:_ Produces bars for each test.
* _Test Labels:_ Each test label has its own bar.
* _Sources:_ Produces dedicated bars for each source.
* _Visited Sites:_ Each visited site has its own bar.
* _Private Networks:_ Each private network has its own bar.
* _User:_ Each user has its own bar.
* _Connection:_ Each connection gets a dedicated bar.
* _Network:_ Produces bars for each network.
* _Domain:_ Each visited domain has its own bar.
* _Location:_ Each location would have a dedicated bar.
* _Endpoint Agent Labels:_ A separate bar is produced for each Endpoint Agent label.
* _Endpoint Tests:_ Each Endpoint test has its own bar.
* _Devices:_ Each device is dedicated a bar on graph.
* _Interfaces:_ Device interfaces would have dedicated bars.
* _Device Types:_ Separate bars produced for each type of device.
* _Interface Types:_ Each interface type would have dedicated bars.

Either **X-Axis** or **Y-Axis** is displayed, based on the **Orientation** selected.

**Orientation:** This toggle icon controls the orientation of the bars, either horizontal or vertical. Selecting horizontal or vertical orientation sets the associated pull-down menu label to **X-Axis** or **Y-Axis.**

**Sort By:** For charts containing multiple bars, the Sort By setting will determine in what order the bars appear. That is, the value of the Sort By setting is applied to the value in the X-Axis/Y-Axis setting.

* _Default (Highest):_ Sort bars optimally, based on the settings for **Metric** and **Show Comparison**. The metric that is optimal for your settings is shown in parentheses.
* _Alphabetical:_ Sort bars by ascending alphabetical order.
* _Alphabetical (Reverse):_ Sort bars by ascending alphabetical order.
* _Highest:_ Sort bars by highest value first.
* _Lowest:_ Sort bars by lowest value first.

**Fixed Time Span:** When checked, a date selector will appear, allowing selection of a range of days different than the one specified for the entire dashboard. The widget will display data in that range unless the **Global Time Overide** option is selected.

**Limit To:** When checked, the chart will display at most the number of groups you set in the selector. When more groups exist than are displayed, the **Sort By** order determines which rows are displayed.

**Sources:** Filter on names of tests or agents that will provide the data to the dashboard. To filter by both tests and agents, click the **+** icon to the right of the pull-down menu.

**Drill Down** lets you add multiple filters for Agents, Agent Labels, Tests, Test Labels, and Servers.

**Example Stacked Bar Chart Widget**

Below is an example of a configured stacked bar chart widget and the resulting output.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-a10d08f4f1a6f2c20ebf018bf0336793f2378fae%2Fproduct-documentation\_reports\_working-with-reports-20.png?alt=media)

1.  1\.

    The configured widget visualizes mean Response Time for HTTP Server tests based on Cloud and Enterprise Agents.
2.  2\.

    Graph is configured to be oriented to extend from left to right with Y axis as Servers sorted alphabetically.
3.  3\.

    This widget is visualizing 4 out of 149 available HTTP server tests.

The Grouped Bar dashboard widget represents multiple values as single bars in a group of bars.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-d3d44e844124c8fbb8347a45495b7cd07fb3a9cb%2Fdashboard-grouped-bar-widget-example.png?alt=media)

**Grouped Bar Widget Configuration**

The Grouped Bar widget configuration is shown below.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-b13ca3994ba5e20975ab4776926a9c908e4bf084%2Fdashboard-grouped-bar-widget-config.png?alt=media)

Grouped bar chart widgets have the following settings:

**Data Source:** The data source indicates which platform service will be referenced within the widget. Current options include:

* Alerts: Data is obtained from Platform alerts
* Cloud and Enterprise Agents: Data is obtained from scheduled tests performed by Cloud and Enterprise Agents
* Devices: Data is obtained from device-layer reporting
* Endpoint Browser Sessions: Data is obtained from endpoint agent browser sessions
* Endpoint Local Networks: Data is obtained from endpoint agent local networks
* Endpoint Scheduled Tests: Data is obtained from endpoint agent scheduled tests
* Endpoint Automated Session Tests: Data is obtained from endpoint automated session tests
* Internet Insights: Data is obtained from Internet Insights collective intelligence
* Routing: Data is obtained from BGP tests

**Category:** The category options depend on the **Data Source** selected.

**Metric:** Options for metrics depend on the previous **Category** selection. All of the ThousandEyes Data Sources have their own metrics. For example, if you choose Cloud and Enterprise Agents as the Data Source, the Category would show test types.

To continue the example, if we choose Cloud and Enterprise Agents as the Data Source, and Agent-to-Server as the Category, the agent-to-server tests have five metrics: Available Bandwidth, Capacity, Jitter, Latency and Packet Loss. In addition to each of the ThousandEyes test types, alerts also have metrics. For more information on ThousandEyes metrics, see

[ThousandEyes Metrics: What Do Your Results Mean?](https://docs.thousandeyes.com/product-documentation/thousandeyes-basics/thousandeyes-metrics-what-do-your-results-mean)

​

**Measure:** A statistical measurement. **Measure** types available depend on the **Metric** setting, and will be one or more of the following:

* _% positive:_ The percentage of measurements greater than zero. For example, the percentage of time when a Network alert was active.
* _% zero:_ The percentage of measurements equal to zero. For example, the percentage of time when a Network alert was active.
* _nth Percentile:_ The value of the metric that contains n% of the measurements. When "nth Percentile" is selected, a text box will appear, allowing you to specify an integer for the percentile value from 1 to 99. 98% is the default. For example, a 98th Percentile whose value is 500 ms for a **Metric** of "Response Time" would indicate that 98% of the measurements of the response time were between 0 and 500 ms.
* _Maximum:_ The maximum value in the set of measurements, such as the response times of an HTTP Server test over the time period of the dashboard.
* _Minimum:_ The minimum value in the set of measurements, such as the response times of a HTTP Server test over the time period of the dashboard.
* _Mean:_ The value of the arithmetic mean (i.e. average) of the measurements. For example, a **Mean** of 50 ms for a **Metric** of "Latency" for one or more Network tests would indicate that the average value of the latency in the reporting period was 50 ms.
* _Median:_ The value of the median measurement. For example, a **Median** of 50 ms for a **Metric** of "Latency" for one or more Network tests would indicate that the value of 50 ms is the middle value in the range of all values of the latency in the reporting period.
* _Standard Deviation:_ The population standard deviation of a set of measurements, such as the response times, over the time period of the dashboard.
* _Total:_ The total number of measurements. For example, a **Metric** set to "Alerts" and **Tests** set to a HTTP Server test indicate the total number of HTTP Server alerts received in the reporting period.

**Axis:** Arrange the data into bars by the following criteria, and orient the label(s) on the axis displayed :

* _All:_ Produces a single bar with all data.
* _Source:_ Produces bars for each source of data (test or agent).
* _Continents:_ Produces bars for each continent/continental region (North America, Europe/EMEA, Asia/APAC, etc...).
* _Countries:_ Produces bars for each country.
* _Test:_ Produces bars for each test.
* _Test Labels:_ Each test label has its own bar.
* _Sources:_ Produces dedicated bars for each source.
* _Visited Sites:_ Each visited site has its own bar.
* _Private Networks:_ Each private network has its own bar.
* _User:_ Each user has its own bar.
* _Connection:_ Each connection gets a dedicated bar.
* _Network:_ Produces bars for each network.
* _Domain:_ Each visited domain has its own bar.
* _Location:_ Each location would have a dedicated bar.
* _Endpoint Agent Labels:_ A separate bar is produced for each Endpoint Agent label.
* _Endpoint Tests:_ Each Endpoint test has its own bar.
* _Devices:_ Each device is dedicated a bar on graph.
* _Interfaces:_ Device interfaces would have dedicated bars.
* _Device Types:_ Separate bars produced for each type of device.
* _Interface Types:_ Each interface type would have dedicated bars.

Either **X-Axis** or **Y-Axis** is displayed, based on the **Orientation** selected.

**Orientation:** The orientation of the bars--either horizontal or vertical. Selecting horizontal or vertical orientation sets the associated pull-down menu label to **X-Axis** or **Y-Axis.**

**Group By:** One or more sets of bars are produced for each of the values in the **Axis** setting, based on the value of the Group By setting. The available settings will be among the following:

* _All:_ All data aggregated into one bar
* _Test:_ Data from all sources and tests are aggregated together into a single line.
* _Source:_ Data from all tests or agents are given their own bars.
* _Continents:_ Data are aggregated by continent. A chart line is displayed for each continent that has data from at least one source.
* _Countries:_ Data are aggregated by country. A chart line is displayed for each country that has data from at least one source.
* _Test Labels:_ Data from each test label is aggregated into a single line.
* _Sources:_ Data from each source is aggregated into a single line.
* _Agent Labels:_ Data from each agent label is aggregated into a single line.
* _Servers:_ Data aggregated based on servers in a single line.
* _Visited Sites:_ Endpoint Data from each visited site is aggregated into a single line.
* _Private Networks:_ Data from each private network is aggregated into a single line.
* _Users:_ Data is aggregated based on user into a single line.
* _Platforms:_ Data from each platform Windows/Mac is aggregated into a single line.
* _Connections:_ Data for each connection is aggregated into a single line.
* _Networks:_ Data aggregated based on networks into a single line.
* _Domains:_ Data aggregated based on visited domain into a single line.
* _Endpoint Agent Labels:_ Data from each Endpoint Agent label is aggregated into a single line.
* _Device:_ Data from each device is aggregated into a single line.
* _Device Types:_ Data from each type of device is aggregated into a single line.
* _Interfaces:_ Data from each device interface is aggregated into a single line.
* _Interface Types:_ Data from each device interface type is aggregated into a single line.

**Sort By:** For charts containing multiple bars, the Sort By setting will determine in what order the bars appear. That is, the value of the Sort By setting is applied to the value in the X-Axis/Y-Axis setting.

* _Default:_ Sort bars optimally, based on the settings for **Metric** and **Show Comparison**. The metric that is optimal for your settings is shown in parentheses.
* _Alphabetical:_ Sort bars by ascending alphabetical order.
* _Alphabetical (Reverse):_ Sort bars by ascending alphabetical order.
* _Highest:_ Sort bars by highest value first.
* _Lowest:_ Sort bars by lowest value first.

**Fixed Time Span:** When checked, a date selector will appear, allowing selection of a range of days different than the one specified for the entire dashboard. The widget will display data in that range unless the **Global Time Overide** option is selected.

**Limit To:** When checked, the chart will display at most the number of groups you set in the selector. When more groups exist than are displayed, the **Sort By** order determines which rows are displayed.

**Sources:** Filter on names of tests or agents that will provide the data to the dashboard. To filter by both tests and agents, click the **+** icon to the right of the pull-down menu.

**Example Grouped Bar Chart Widget**

Below is an example of a configured grouped bar chart widget and the resulting output.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-9a0fea7bdb47158f9aa872fefa81aac73572fe2a%2Fproduct-documentation\_reports\_working-with-reports-22.png?alt=media)

1.  1\.

    The chart is configured to visualize Mean Receive Time from HTTP Server tests based on Cloud and Enterprise Agents.
2.  2\.

    Graph is configured to extend horizontally with Servers as Y axis grouped by agent labels and sorted in a descending order.
3.  3\.

    Widget is configured to visualize 5 out of 149 tests.

Pie widgets represent multiple values as proportionally sized segments of a pie.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-38db5d00c51bade743cde6261da3d84a867cff3b%2Fdashboard-pie-widget-example.png?alt=media)

**Pie Chart Widget Configuration**

The Pie Chart widget configuration is shown below.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-22f4ea1d12a00e48632de42f680e65e2f5ed058d%2Fdashboard-pie-widget-config.png?alt=media)

Pie chart widgets have the following settings:

**Data Source:** The data source indicates which platform service will be referenced within the widget. Current options include:

* Cloud and Enterprise Agents: Data is obtained from scheduled tests performed by Cloud and Enterprise Agents
* Endpoint Browser Sessions: Data is obtained from endpoint agent browser sessions
* Endpoint Local Networks: Data is obtained from endpoint agent local networks
* Endpoint Scheduled Tests: Data is obtained from endpoint agent scheduled tests
* Internet Insights: Data is obtained from Internet Insights collective intelligence

**Category:** The category choices depend on the **Data Source** selected.

**Metric:** The metric choices depend on the **Category** selected. If we select Cloud and Enterprise Agents as the Data Source and Web - HTTP server as the Category, the metrics you can choose from for the Pie Chart widget are (Response Time, Total Error Count and Total Fetch Time) are composites of metrics found in an HTTP server test.

To continue the example, Response Time consists of four distinct metrics from the HTTP server test: DNS resolution time, connect time, SSL time and wait time. Each of the four metrics are presented in a single pie chart. For more information on ThousandEyes metrics, see

[ThousandEyes Metrics: What Do Your Results Mean?](https://docs.thousandeyes.com/product-documentation/thousandeyes-basics/thousandeyes-metrics-what-do-your-results-mean)

​

**Measure:** A statistical measurement. **Measure** types available depend on the **Metric** setting, and will be one or more of the following:

* _% positive:_ The percentage of measurements greater than zero. For example, the percentage of time when a Network alert was active.
* _% zero:_ The percentage of measurements equal to zero. For example, the percentage of time when a Network alert was active.
* _nth Percentile:_ The value of the metric that contains n% of the measurements. When "nth Percentile" is selected, a text box will appear, allowing you to specify an integer for the percentile value from 1 to 99. 98% is the default. For example, a 98th Percentile whose value is 500 ms for a **Metric** of "Response Time" would indicate that 98% of the measurements of the response time were between 0 and 500 ms.
* _Maximum:_ The maximum value in the set of measurements, such as the response times of an HTTP Server test over the time period of the dashboard.
* _Minimum:_ The minimum value in the set of measurements, such as the response times of a HTTP Server test over the time period of the dashboard.
* _Mean:_ The value of the arithmetic mean (i.e. average) of the measurements. For example, a **Mean** of 50 ms for a **Metric** of "Latency" for one or more Network tests would indicate that the average value of the latency in the reporting period was 50 ms.
* _Median:_ The value of the median measurement. For example, a **Median** of 50 ms for a **Metric** of "Latency" for one or more Network tests would indicate that the value of 50 ms is the middle value in the range of all values of the latency in the reporting period.
* _Standard Deviation:_ The population standard deviation of a set of measurements, such as the response times, over the time period of the dashboard.
* _Total:_ The total number of measurements. For example, a **Metric** set to "Alerts" and **Tests** set to a HTTP Server test indicate the total number of HTTP Server alerts received in the reporting period.

**Group By:** One or more pie charts are produced based on the value of the Group By setting. The available settings will be among the following:

* _All:_ All data aggregated into one pie chart.
* _Agent:_ Data from all agents are aggregated into a single pie chart.
* _Continents:_ Data are aggregated by continent. A pie chart is displayed for each continent that has data from at least one test.
* _Countries:_ Data are aggregated by country. A pie chart is displayed for each country that has data from at least one test.
* _Test:_ Data from all tests are aggregated into a single pie chart.
* _All:_ Group all the data as a single chart.
* _Test Labels:_ Data from all associated test labels are aggregated in a single pie chart.
* _Sources:_ Data from each source is given their own pie charts.
* _Agent Labels:_ Data from each agent label is given its own pie chart.
* _Servers:_ Data aggregated based on servers. Each server would have a dedicated pie chart.
* _Visited Sites:_ Endpoint Data from each visited site is given its own pie chart.
* _Private Networks:_ Data from each private network is given its own pie chart.
* _Users:_ Data is aggregated based on user, each user gets their own pie chart.
* _Platforms:_ Data from each platform Windows/Mac is given its own pie chart.
* _Connections:_ Data for each connection is given its own pie chart.
* _Networks:_ Data aggregated based on networks, each network gets its own pie chart.
* _Domains:_ Data aggregated based on visited domain, each domain would have a dedicated pie chart.
* _Endpoint Agent Labels:_ Data from each Endpoint Agent label gets its own pie chart.
* _Device:_ Data from each device is given its own pie chart.
* _Device Types:_ Data from each type of device is given its own pie chart.
* _Interfaces:_ Data from each device interface is given its own pie chart.
* _Interface Types:_ Data from each device interface type is given its own pie chart.

**Filter:** Names of tests or agents that will be the source of the data to the dashboard. To filter by both tests and agents, click the **+** icon to the right of the pull-down menu.

Below is an example of a configured pie chart widget and the resulting output.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-d1e8db6e9c8375533994c82b4edb6625b38ad3cc%2Fproduct-documentation\_reports\_working-with-reports-24.png?alt=media)

1.  1\.

    The widget is configured to visualize Mean Page Load Time of Browser Sessions - Web collected by Endpoint Agents.
2.  2\.

    Group By field is set to Networks and as a result data from each network is visualized as a separate pie chart.
3.  3\.

    The data is not filtered and as a result all available data is visualized.

Data Summary widgets include Table, Multi-Metric Table, Number, and Color Grid.

The Table widget shows a breakdown of numbers by rows and columns.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-938a6bfdd4b232b8cda688b04b7565d00e278fd8%2Fdashboard-table-widget-example.png?alt=media)

**Table Widget Configuration**

The Table widget configuration is shown below.

![](https://github.com/thousandeyes/docs/blob/prod/.gitbook/assets/dashboard-table-widget-config.png)

Table widgets have the following settings:

**Data Source:** The data source indicates which platform service will be referenced within the widget. Current options include:

* Alerts: Data is obtained from Platform alerts
* Cloud and Enterprise Agents: Data is obtained from scheduled tests performed by Cloud and Enterprise Agents
* Devices: Data is obtained from device-layer reporting
* Endpoint Browser Sessions: Data is obtained from endpoint agent browser sessions
* Endpoint Local Networks: Data is obtained from endpoint agent local networks
* Endpoint Scheduled Tests: Data is obtained from endpoint agent scheduled tests
* Endpoint Automated Session Tests: Data is obtained from endpoint automated session tests
* Internet Insights: Data is obtained from Internet Insights collective intelligence
* Routing: Data is obtained from BGP tests

**Category:** The category choices depend on the **Data Source** selected.

\***Metric:** Options for metrics depend on the test type chosen in the previous **Category** selection. For example, agent-to-server tests have five metrics: Available Bandwidth, Capacity, Jitter, Latency and Packet Loss. In addition to each of the ThousandEyes test types, alerts also have metrics. For more information on ThousandEyes metrics, see

[ThousandEyes Metrics: What Do Your Results Mean?](https://docs.thousandeyes.com/product-documentation/thousandeyes-basics/thousandeyes-metrics-what-do-your-results-mean)

Depending on your choice of **Metric**, the names of the widget settings may change, or additional settings may appear. For example, selecting any of the alerts metrics will result in the Alert Rules setting appearing in the widget.

**Measure:** A statistical measurement. **Measure** types available depend on the **Metric** setting, and will be one or more of the following:

* _% positive:_ The percentage of measurements greater than zero. For example, the percentage of time when a Network alert was active.
* _% zero:_ The percentage of measurements equal to zero. For example, the percentage of time when a Network alert was active.
* Maximum: The maximum value in the set of measurements, such as the latency times of a Network test over the time period of the dashboard.
* Minimum: The minimum value in the set of measurements, such as the latency times of a Network test over the time period of the dashboard.
* _nth Percentile:_ The value of the metric that contains n% of the measurements. When "nth Percentile" is selected, a text box will appear, allowing you to specify an integer for the percentile value from 1 to 99. 98% is the default. For example, a 98th Percentile whose value is 500 ms for a **Metric** of "Response Time" would indicate that 98% of the measurements of the response time were between 0 and 500 ms.
* _Mean:_ The value of the arithmetic mean (i.e. average) of the measurements. For example, a **Mean** of 50 ms for a **Metric** of "Latency" for one or more Network tests would indicate that the average value of the latency in the reporting period was 50 ms.
* _Median:_ The value of the median measurement. For example, a **Median** of 50 ms for a **Metric** of "Latency" for one or more Network tests would indicate that the value of 50 ms is the middle value in the range of all values of the latency in the reporting period.
* _Total:_ The total number of measurements. For example, a **Metric** set to "Alerts" and **Tests** set to a HTTP Server test indicate the total number of HTTP Server alerts received in the reporting period.
* _Active Time:_ The amount of time an alert rule was active. (Alerts metrics only)
* _Inactive time:_ The amount of time an alert rule was inactive. (Alerts metrics only)

**Show Comparison to Previous Timespan:** When checked, the dashboard displays the difference between the current data set and a past data set, shown as an additional row of cells below the principle row, with the comparison numbers in red or green along with an up-arrow or down-arrow indicating a numerical increase or decrease. The combination of color and arrow direction changes based on the metric setting. For some settings of metric, a numeric increase is a change for the better and thus is rendered in green. For other metrics a numeric increase is a change for the worse and rendered in red. For some metrics, the situation may be ambiguous; those metrics are rendered in grey font without accompanying arrows.

"N/A" is displayed in place of the comparison numbers when sufficient data is not currently available for a comparison (such as when a test is first configured but hasn't accumulated a full timespan of data). A "-" (single dash) is displayed in place of the comparison numbers when no data is present and will not ever be present, such as when a test error prevented a round of data collection.

By default, the timespan of the past data set is the timespan prior to the current data set's time span, which is specified by the **From** and **To** fields of the dashboard's date and time selector. If the **Fixed Time Span** box is checked, then the timespans of the data sets are specified by the **Fixed Time Span** setting's date selector.

**Fixed Time Span:** When checked, a date selector will appear, allowing selection of a range of days different than the one specified for the entire dashboard. The widget will display data in that range unless the **Global Time Overide** option is selected.

**Limit To:** When checked, the table rows will display at most the number you set in the selector. When more rows exist than are displayed, the **Sort By** order determines which rows are displayed.

* _Agent:_ Data from all agents are aggregated by agent. A row is displayed for each agent that has data from at least one test.
* _All:_ Data from all sources are aggregated into a single row.
* _Continents:_ Data from all sources are aggregated by continent. A row is displayed for each continent that has data from at least one source.
* _Countries:_ Data from all sources are aggregated by country. A row is displayed for each country that has data from at least one source.
* _Test:_ Data from all tests are given their own rows.
* _Test Labels:_ Data from all test labels are given their own rows.
* _Agent Labels:_ Data from all agents aggregated based on agent labels.
* _Agent:_ Data from all agents are aggregated by agent. A column is displayed for each agent that has data from at least one test.
* _All:_ Data from all sources are aggregated into a single column.
* _Continents:_ Data are aggregated by continent. A column is displayed for each continent that has data from at least one source.
* _Countries:_ Data are aggregated by country. A column is displayed for each country that has data from at least one source.
* _Test:_ Data from all sources are aggregated by test. A column is displayed for each test that has data from at least one source.

**Sort By:** For tables containing multiple rows, the Sort By setting will determine in what order the rows appear. That is, the value of the Sort By setting is applied to the value in the Rows setting.

* _Default:_ Sort rows optimally, based on the settings for **Metric** and **Show Comparison**. The metric that is optimal for your settings is shown in parentheses.
* _Alphabetical:_ Sort rows by ascending alphabetical order.
* _Alphabetical (Reverse):_ Sort rows by ascending alphabetical order.
* _Greatest Decrease:_ Sort rows by greatest decrease between current and past measurements of a row's **Metric** value. This setting is meaningful only when the **Show Comparison** box is checked.
* _Greatest Increase:_ Sort rows by greatest increase between current and past measurements of a row's **Metric** value. This setting is meaningful only when the **Show Comparison** box is checked.
* _Highest:_ Sort rows by highest value first.
* _Lowest:_ Sort rows by lowest value first.

**Tests:** Names of tests that will provide the data to the dashboard. Select one or more tests that are appropriate for your selection of **Metric** setting (e.g. if the **Metric** is Packet Loss, select one or more Network tests or tests with included Network metrics; if the metric is Availability, select a Web test, etc..)

**Sources:** Filter the sources from which the data will be taken. This setting's name and the corresponding column heading change once the **Metric** is set, and will be one of the following:

* _Alert Rules:_ If the **Metric** is a Network, Web, DNS or Voice test or alert metric, a list of alert rules.
* _Agents:_ If the **Metric** is a Network, Web, DNS or Voice test or alert metric, a list of Cloud and Enterprise Agents.
* _Agent Labels:_ If the **Metric** is a Network, Web, DNS or Voice test or alert metric, a list of Cloud and Enterprise Agent labels (Built-in or Custom)
* _Tests:_ For any **Metric**, a list of tests.
* _Test Labels:_ For any **Metric**, a list of test labels (Built-in or Custom).
* _Monitors:_ If the **Metric** is a BGP test or alert, a list of ThousandEyes BGP monitors.

Below is an example of a configured table widget and the resulting output.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-cd3f98900b1565f4b02118661fae7bbff09036d7%2Fproduct-documentation\_reports\_working-with-reports-13.png?alt=media)

1.  1\.

    The configuration shows Cloud and Enterprise Agents set as data source, with latency of agent to agent tests set as a reported metric for the table. The widget is set to visualize Standard Deviation of a latency metric in the source-to-target direction.
2.  2\.

    Data is set to visualize with tests forming the Rows and agent forming the columns. Rows are sorted by a reported value, in the ascending order.
3.  3\.

    The filter is set to include 2 of 189 available agent to agent tests. The “+” icon can be used to put on additional filters.

#### Multi-Metric Table Widget <a href="#multi-metric-table-widget" id="multi-metric-table-widget"></a>

The Multi-Metric Table can have columns with different metrics, rather than a single metric for the entire table.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-dcd393a109af2313377ef199cb5f5a2b679c3c7f%2Fdashboard-multi-metric-table-widget-example.png?alt=media)

**Multi-Metric Table Widget Configuration**

The Multi-Metric Table widget configuration is shown below.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-8a648597687e9faff90fd2ae8bdc69ac499acc3f%2Fdashboard-multi-metric-table-widget-config.png?alt=media)

The multi-metric table widget's **Rows** tab has the following settings:

**Rows:** Select the property that will be used for the rows in the table. Rows will be one of the following:

* _All:_ Any property that is relevant to the criteria in the Column(s) tab(s) will be used as a row.
* _Tests:_ Tests relevant to the criteria in the Column(s) tab(s) will be used as a row.
* _Test Labels:_ Test labels relevant to the criteria in the Column(s) tab(s) will be used as a row.
* _Agents:_ Agents relevant to the criteria in the Column(s) tab(s) will be used as a row.
* _Monitors:_ Monitors relevant to the criteria in the Column(s) tab(s) will be used as a row.
* _Agent Labels:_ Agent labels relevant to the criteria in the Column(s) tab(s) will be used as a row.
* _Servers:_ Servers relevant to the criteria in the Column(s) tab(s) will be used as a row.
* _Countries:_ Servers relevant to the criteria in the Column(s) tab(s) will be used as a row.
* _Continents:_ Continents relevant to the criteria in the Column(s) tab(s) will be used as a row.

**Sort By:** For tables containing multiple rows, the **Sort By** setting determines in what order the rows appear. That is, the value of the **Sort By** setting is applied to the value in the **Rows** setting.

* _Default:_ Sort rows optimally, based on the settings for **Metric** and **Show Comparison**. The **Metric** that is used for each column shows the column's **Measure** in parentheses.
* _Alphabetical:_ Sort rows by ascending alphabetical order.
* _Alphabetical (Reverse):_ Sort rows by ascending alphabetical order.
* _Greatest Decrease:_ Sort rows by greatest decrease between current and past measurements of a row's **Metric** value. This setting is meaningful only when the **Show Comparison** box is checked.
* _Greatest Increase:_ Sort rows by greatest increase between current and past measurements of a row's **Metric** value. This setting is meaningful only when the **Show Comparison** box is checked.
* _Highest:_ Sort rows by highest value first.
* _Lowest:_ Sort rows by lowest value first.

**Show Comparison to Previous Timespan:** When checked, the dashboard displays the difference between the current data set and a past data set, shown as an additional value in the cells below the principle value, with the comparison numbers in red or green along with an up-arrow or down-arrow indicating a numerical increase or decrease. The combination of color and arrow direction changes based on the metric setting. For some settings of metric, a numeric increase is a change for the better and thus is rendered in green. For other metrics a numeric increase is a change for the worse and rendered in red. For some metrics, the situation may be ambiguous; those metrics are rendered in grey font without accompanying arrows.

"N/A" is displayed in place of the comparison numbers when sufficient data is not currently available for a comparison (such as when a test is first configured but hasn't accumulated a full timespan of data). A "-" (single dash) is displayed in place of the comparison numbers when no data is present and will not ever be present, such as when a test error prevented a round of data collection.

By default, the timespan of the past data set is the timespan prior to the current data set's time span, which is specified by the **From** and **To** fields of the dashboard's date and time selector. If the **Fixed Time Span** box is checked, then the timespans of the data sets are specified by the **Fixed Time Span** setting's date selector.

**Fixed Time Span:** When checked, a date selector will appear, allowing selection of a range of days different than the one specified for the entire dashboard. The widget will display data in that range unless the **Global Time Overide** option is selected.

**Limit To:** When checked, the table rows will display at most the number you set in the selector. When more rows exist than are displayed, the **Sort By** order determines which rows are displayed.

**Sources:** Filter sources from which the data will be taken. This setting's name and the corresponding column heading change once the **Metric** is set, and will be one of the following:

* _Alert Rules:_ If the **Metric** is a Network, Web, DNS or Voice test or alert metric, a list of alert rules.
* _Agents:_ If the **Metric** is a Network, Web, DNS or Voice test or alert metric, a list of Cloud and Enterprise Agents.
* _Agent Labels:_ If the **Metric** is a Network, Web, DNS or Voice test or alert metric, a list of Cloud and Enterprise Agent labels (Built-in or Custom)
* _Tests:_ For any **Metric**, a list of tests.
* _Test Labels:_ For any **Metric**, a list of test labels (Built-in or Custom).
* _Monitors:_ If the **Metric** is a BGP test or alert, a list of ThousandEyes BGP monitors.
* _Servers:_ For any Metric, a list of servers being tested.
* _Location:_ For any Metric, a list of locations being tested.

The multi-metric table widget's Columns tabs have the following settings:

**Metric:** Each type of ThousandEyes test has its own metrics. For example, agent-to-server tests have five metrics: Available Bandwidth, Capacity, Jitter, Latency and Packet Loss. In addition to each of the ThousandEyes test types, alerts also have metrics. For more information on ThousandEyes metrics, see

[ThousandEyes Metrics: What Do Your Results Mean?](https://docs.thousandeyes.com/product-documentation/thousandeyes-basics/thousandeyes-metrics-what-do-your-results-mean)

Depending on your choice of **Metric**, the names of the widget settings may change, or additional settings may appear. For example, selecting any of the alerts metrics will result in the Alert Rules setting appearing in the widget.

**Measure:** A statistical measurement. **Measure** types available depend on the **Metric** setting, and will be one or more of the following:

* _% positive:_ The percentage of measurements greater than zero. For example, the percentage of time when a Network alert was active.
* _% zero:_ The percentage of measurements equal to zero. For example, the percentage of time when a Network alert was active.
* Maximum: The maximum value in the set of measurements, such as the latency times of a Network test over the time period of the dashboard.
* Minimum: The minimum value in the set of measurements, such as the latency times of a Network test over the time period of the dashboard.
* _nth Percentile:_ The value of the metric that contains n% of the measurements. When "nth Percentile" is selected, a text box will appear, allowing you to specify an integer for the percentile value from 1 to 99. 98% is the default. For example, a 98th Percentile whose value is 500 ms for a **Metric** of "Response Time" would indicate that 98% of the measurements of the response time were between 0 and 500 ms.
* _Mean:_ The value of the arithmetic mean (i.e. average) of the measurements. For example, a **Mean** of 50 ms for a **Metric** of "Latency" for one or more Network tests would indicate that the average value of the latency in the reporting period was 50 ms.
* _Median:_ The value of the median measurement. For example, a **Median** of 50 ms for a **Metric** of "Latency" for one or more Network tests would indicate that the value of 50 ms is the middle value in the range of all values of the latency in the reporting period.
* _Total:_ The total number of measurements. For example, a **Metric** set to "Alerts" and **Tests** set to a HTTP Server test indicate the total number of HTTP Server alerts received in the reporting period.
* _Active Time:_ The amount of time an alert rule was active. (Alerts metrics only)
* _Inactive time:_ The amount of time an alert rule was inactive. (Alerts metrics only)

To add a column, click on the **Add New Column** link. To delete a column, click the tab of the column you wish to delete, then click the **X** in the column's header.

**Example Multi-Metric Table Widget**

Below is an example of a configured multi-metric table widget entitled “HTTP Server statistics” and the resulting output.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-b00413b7e8c61fbab539784a4314ece6d3d43644%2Fproduct-documentation\_reports\_working-with-reports-16.png?alt=media)

The **Rows** setting is set to "Tests", indicating that the table's rows will be individual test names, and the **Sources** is set to filter on "Tests", where 3 tests of 241 are selected, creating a two-row table with the first column containing those two selected tests. Column 1 has "Availability" selected as the **Metric** and "Mean" as the **Measure**. Each test row will display the mean of availability in the first column. Column 2 has "Response Time" selected as the **Metric** and "Maximum" as the **Measure**. Each test row will display the largest of all response time values in the round, in the second column.

Sort by is set to "Default (Tests)", meaning that the sorting order of the rows will be the default (the first column that's set by the **Rows**). The dark switch with the white up-arrow indicates that the value of the **Sort by** field will be sorted from low to high, alphabetically in this case. The **Show Comparison** box is checked, producing the second, lower set of numbers along with up or down arrows to indicate whether the value rose or dropped, and a color code to indicate whether that rise or drop is an improving change from the previous period (green), a degrading change (red) or is ambiguous (gray). **Fixed Time Span** is unchecked, indicating that the dashboard uses the time frame that is set at the top of the Dashboards page. Limit To is set to 2 rows, thereby preventing one of the three tests from being displayed.

The Number widget can show one or more cards, each card displaying a single scalar quantity, such as an average of packets lost or page load times, or the total number of alerts.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-6ec5fc8db2b17da31f559f519335a2ace721cb8a%2Fdashboard-number-widget-example.png?alt=media)

**Number Widget Configuration**

The Number widget configuration is shown below.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-6c587ddbe5b7878d1edc365bede1d94095f3b23c%2Fdashboard-number-widget-config.png?alt=media)

Number widgets have the following settings:

**Data Source:** The data source indicates which platform service will be referenced within the widget. Current options include:

* Alerts: Data is obtained from platform alerts
* Cloud and Enterprise Agents: Data is obtained from scheduled tests performed by Cloud and Enterprise Agents
* Devices: Data is obtained from device-layer reporting
* Endpoint Agents: Data is obtained from scheduled tests, automated session tests, and monitored domain metrics
* Routing: Data is obtained from BGP tests

**Metric:** Each type of ThousandEyes test has its own metrics. For example, agent-to-server tests have five metrics: Available Bandwidth, Capacity, Jitter, Latency and Packet Loss. In addition to each of the ThousandEyes test types, _Alerts_ is also a category of choices for metrics. For more information on ThousandEyes metrics, see

[ThousandEyes Metrics: What Do Your Results Mean?](https://docs.thousandeyes.com/product-documentation/thousandeyes-basics/thousandeyes-metrics-what-do-your-results-mean)

​

**Measure:** A statistical measurement. **Measure** choices available depend on the **Metric** setting, but will come from the following list:

* _% positive:_ The percentage of measurements greater than zero. For example, the percentage of time when a Network alert was active.
* _% zero:_ The percentage of measurements equal to zero. For example, the percentage of time when a Network alert was active.
* _Maximum:_ The maximum value in the set of measurements, such as the latency times of a Network test over the time period of the dashboard.
* _Minimum:_ The minimum value in the set of measurements, such as the latency times of a Network test over the time period of the dashboard.
* _Standard Deviation:_ The population standard deviation of a set of measurements, such as the latency times of a Network test over the time period of the dashboard.
* _nth Percentile:_ The value of the metric that contains n% of the measurements. When "nth Percentile" is selected, a text box will appear, allowing you to specify an integer for the percentile value from 1 to 99. 98% is the default. For example, a 98th Percentile whose value is 500 ms for a **Metric** of "Response Time" would indicate that 98% of the measurements of the response time were from 0 to 500 ms.
* _Mean:_ The value of the arithmetic mean (i.e. average) of the measurements. For example, a **Mean** of 50 ms for a **Metric** of "Latency" for one or more Network tests would indicate that the average value of the latency in the reporting period was 50 ms.
* _Median:_ The value of the median measurement. For example, a **Median** of 50 ms for a **Metric** of "Latency" for one or more Network tests would indicate that the value of 50 ms is the middle value in the range of all values of the latency in the reporting period.
* _Total:_ The total number of measurements. For example, a **Metric** set to "Alerts" and **Tests** set to a HTTP server test indicate the total number of HTTP server alerts received in the reporting period.
* _Active Time:_ The amount of time an alert rule was active. (Alerts metrics only)
* _Inactive time:_ The amount of time an alert rule was inactive. (Alerts metrics only)

**Show Comparison to Previous Timespan:** When checked, the dashboard displays the difference between the current data set and the previous data set of the same length as the reporting interval. The comparison numbers are shown as an additional row of cells below the principle row, in red or green font color along with an up-arrow or down-arrow indicating a numerical increase or decrease. The combination of color and arrow direction changes based on the metric setting. For some settings of metric, a numeric increase is a change for the better and thus is rendered in green. For other metrics a numeric increase is a change for the worse and rendered in red. For some metrics, the situation may be ambiguous; those metrics are rendered in grey font.

"N/A" is displayed in place of the comparison numbers when sufficient data from the previous reporting interval is not currently available for a comparison (such as when a test is first configured but hasn't accumulated a full timespan of data). A "-" (single dash) is displayed in place of the comparison numbers when no data is present and will not ever be present, such as when a agent is not assigned to the test.

By default, the timespan of the past data set is the timespan prior to the current data set's time span, which is specified by the **From** and **To** fields of the dashboard's date and time selector. If the **Fixed Time Span** box is checked, then the timespans of the data sets are specified by the **Fixed Time Span** setting's date selector.

**Fixed Time Span:** When checked, a date selector will appear, allowing selection of a range of days different than the one specified for the entire dashboard. The widget will display data in that range unless the **Global Time Overide** option is selected.

**Card Description:** For number widgets, each number is contained on a card, which can be given its own description which will appear in the number box when viewing the dashboard. Configuration of this setting is optional.

**Tests:** Names of tests that will provide the data to the dashboard. Select one or more tests that is appropriate to your **Metric** setting (e.g. if the **Metric** is Packet Loss, select one or more Network tests or tests with included Network metric; if the **Metric** is Response Time, select an HTTP Server or Page Load test).

**Sources:** Filter sources from which the data will be taken. The column heading changes based on which **Metric** is set, and will be one of the following:

* _Alert Rules:_ If the **Metric** is a Network, Web, DNS or Voice test or alert metric, a list of alert rules.
* _Agents:_ If the **Metric** is a Network, Web, DNS or Voice test or alert metric, a list of Cloud and Enterprise Agents.
* _Agent Labels:_ If the **Metric** is a Network, Web, DNS or Voice test or alert metric, a list of Cloud and Enterprise Agent labels (Built-in or Custom).
* _Tests:_ For any **Metric**, a list of tests.
* _Test Labels:_ For any **Metric**, a list of test labels (Built-in or Custom).
* _Monitors:_ If the **Metric** is a BGP test or alert, a list of ThousandEyes BGP monitors.

Below is an example of a configured number widget and the resulting dashboard output.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-b9a41cba508e1ec6db587e7209c6d666932f6b15%2Fproduct-documentation\_reports\_working-with-reports-11.png?alt=media)

The configuration shows the widget configured with three numbers:

1.  1\.

    Maximum Packet Loss for selected agent-to-server test.
2.  2\.

    Total number of alerts triggered across all tests.
3.  3\.

    Maximum Packet Loss observed by Endpoint Agents across all browser sessions.

The Color Grid widget shows an array of colored cards, where each card's color depends on a configured scale.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-a6abb20f2825e019e8ca2cb27b208a4f84b727e9%2Fdashboard-color-grid-widget-example.png?alt=media)

**Color Grid Widget Configuration**

The Color Grid widget configuration is shown below.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-309de413b981900f5ee0b3ca5bd157b617cba64e%2Fdashboard-color-grid-widget-config.png?alt=media)

**Data Source:** The data source indicates which platform service will be referenced within the widget. The current options include:

* Alerts: Data is obtained from Platform Alerts
* Cloud & Enterprise Agents: Data is obtained from Scheduled Tests performed by Cloud & Enterprise Agents
* Devices: Data is obtained from Device Layer reporting
* Endpoint Agents: Data is obtained from Scheduled Tests, Automated Session Tests, and Monitored Domain metrics
* Routing: Data is obtained from BGP tests

**Category:** The category options depend on the **Data Source** selected.

**Metric:** Options for metrics depend on the test type chosen in the previous **Category** selection. Each type of ThousandEyes Data Source has its own metrics. For example, Cloud and Enterprise Agents data from agent-to-server tests have five metrics: Available Bandwidth, Capacity, Jitter, Latency, and Packet Loss. In addition to each of the ThousandEyes test types, alerts also have metrics. For more information on ThousandEyes metrics, see

[ThousandMetrics: what do your results mean?](https://docs.thousandeyes.com/product-documentation/thousandeyes-basics/thousandeyes-metrics-what-do-your-results-mean)

.

**Measure:** A statistical measurement. Measure types available depend on the Metric setting and will be one or more of the following:

* _% positive:_ The percentage of measurements greater than zero. For example, the percentage of time when a Network alert was active.
* _% zero:_ The percentage of measurements equal to zero. For example, the percentage of time when a Network alert was active.
* _Maximum:_ The maximum value in the set of measurements, such as the latency times of a Network test over the time period of the report.
* _Minimum:_ The minimum value in the set of measurements, such as the latency times of a Network test over the time period of the report.
* _nth Percentile:_ The value of the Metric which contains n% of the measurements. When "nth Percentile" is selected, a text box will appear, allowing you to specify an integer for the percentile value from 1 to 99. 98% is the default. For example, a 98th Percentile whose value is 500 ms for a **Metric** of "Response Time" would indicate that 98% of the measurements of the response time were between 0 and 500 ms.
* _Mean:_ The value of the arithmetic mean (i.e. average) of the measurements. For example, a **Mean** of 50 ms for a **Metric** of "Latency" for one or more Network tests would indicate that the average value of the latency in the reporting period was 50 ms.
* _Median:_ The value of the median measurement. For example, a **Median** of 50 ms for a **Metric** of "Latency" for one or more Network tests would indicate that the value of 50 ms is the middle value in the range of all values of the latency in the reporting period.
* _Total:_ The total number of measurements. For example, a **Metric** set to "Alerts" and **Tests** set to a HTTP Server test indicate the total number of HTTP Server alerts received in the reporting period.
* _Active Time:_ The amount of time an Alert Rule(s) was active. (Alerts Metrics only).
* _Inactive time:_ The amount of time an Alert Rule(s) was inactive. (Alerts Metrics only).
* _Standard Deviation:_ The population standard deviation of a set of measurements, such as the latency times of a Network test over the time period of the report.
* _All:_ Data from all sources are aggregated into a single card.
* _Test:_ Data from all tests are given their own card based on group cards configuration.
* _Test Labels:_ Data from all test labels configured in **Settings > Labels** are given their own card based on group cards configuration.
* _Agents:_ Data from all agents are given their own card based on group cards configuration.
* _Agent Labels:_ Data from all agent labels configured in **Settings > Labels** are given their own card based on group cards configuration.
* _Servers:_ Data from all Target servers are given their own card, and the card is displayed for each Target server.
* _Continents:_ Data from all sources are aggregated by continent. A card is displayed for each continent that has data from at least one source.
* _Countries:_ Data from all sources are aggregated by country. A card is displayed for each country that has data from at least one source.
* _All:_ Data from all sources are grouped by **Cards** drop-down menu configuration.
* _Test:_ Data from sources configured in Cards are grouped by Test name.
* _Test Labels:_ Data from sources configured in Cards are grouped by Test Labels.
* _Agents:_ Data from sources configured in Cards are grouped by Agent name.
* _Agent Labels:_ Data from sources configured in Cards are grouped by Agent Labels name.
* _Servers:_ Data from sources configured in Cards are grouped by Target Servers name.
* _Continents:_ Data from sources configured in Cards are grouped and aggregated by Continent.
* _Countries:_ Data from sources configured in Cards are grouped and aggregated by Country.

**Sort Cards By:** For cards displayed in multiple rows, the **Sort By** setting will determine in what order the cards appear. That is, the value of the **Sort Cards By** setting is applied to the value in the **Cards** setting:

* _Alphabetical:_ Sort rows by ascending alphabetical order.
* _Alphabetical (Reverse):_ Sort rows by descending alphabetical order.
* _Value:_ Sort rows by highest value first.
* _Value (Reverse):_ Sort rows by lowest value first.

**Time Span:** Select a number of minutes, hours, or days. The widget displays data for the time span configured in Time setting.

**Scale:** Select a number range on how cards will be colored. Select the maximum metric value for a card to be colored green and the minimum metric value for a card to be colored red.

**Columns:** Select a number of group of cards displayed per column, the dashboard can allocate up to two columns on the widget.

**Limit To:** When checked, the cards in a group will be displayed up to the number you set in the selector. When more cards exist than are displayed, the **Sort Cards By** order determines which cards are displayed.

**Color Grid Widget Example**

The Color Grid widget displays an array of cards, where each card's color is determined by comparing the card's value to a predefined scale. Here is an example Color Grid widget showing data collected over the last six hours by two tests, with each test having 16 agents assigned to it:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-20dfd33ff1236c9e892d1d2f9fdaac62535c0e5d%2Fproduct-documentation\_thousandeyes-basics\_working-with-the-dashboard-6.png?alt=media)

The following remarks about this widget's configuration will explain why the data is displayed the way it is:

1.  1\.

    Cards visualize the `Median` value of the `Total Time` metric of the `Web - HTTP Server` tests running on `Cloud & Enterprise Agents`.
2.  2\.

    The `Agents` value is selected in the **Cards** drop-down menu makes each card display data from a specific agent.
3.  3\.

    Cards are grouped by `Tests`, meaning data from each test is displayed as a separate group of cards.
4.  4\.

    The configured **Scale** values determine card colors. Cards will be green when their value is lower than 200 ms. The color will progressively turn to red when the card's value approaches 270 ms.
5.  5\.

    Display two columns of card groups per row.

Time Series widgets include Line, Stacked Area, and Box-and-Whiskers.

The Line widget shows time along the horizontal axis, and the selected quantity on the vertical axis. You can overlay several quantities or have separate charts for each, one beneath the other.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-c80405e414f6a270a157cc9574b23f9067840c55%2Fdashboard-line-widget-example.png?alt=media)

**Line Widget Configuration**

The Line widget configuration is shown below.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-aabca3a166fe731adc566ed6cb1183dbfe54f6d7%2Fdashboard-line-widget-config.png?alt=media)

Line widgets have the following settings:

**Data Source:** The data source indicates which platform service will be referenced within the widget. Current options include:

* Alerts: Data is obtained from Platform alerts
* Cloud and Enterprise Agents: Data is obtained from scheduled tests performed by Cloud and Enterprise Agents
* Devices: Data is obtained from device-layer reporting
* Endpoint Agents: Data is obtained from scheduled tests, automated session tests, and monitored domain metrics
* Routing: Data is obtained from BGP tests

**Category:** The category choices depend on the **Data Source** selected.

**Metric:** Options for metrics depend on the test type chosen in the previous **Category** selection. Each type of ThousandEyes test has its own metrics. For example, agent-to-server tests have five metrics: Available Bandwidth, Capacity, Jitter, Latency and Packet Loss. In addition to each of the ThousandEyes test types, alerts also have metrics. For more information on ThousandEyes metrics, see

[ThousandEyes Metrics: What Do Your Results Mean?](https://docs.thousandeyes.com/product-documentation/thousandeyes-basics/thousandeyes-metrics-what-do-your-results-mean)

​

**Measure:** A statistical measurement. **Measure** types available depend on the **Metric** setting, and will be one or more of the following:

* _% positive:_ The percentage of measurements greater than zero. For example, the percentage of time when a Network alert was active.
* _% zero:_ The percentage of measurements equal to zero. For example, the percentage of time when a Network alert was active.
* _Maximum:_ The maximum value in the set of measurements, such as the response times of an HTTP Server test in a test round.
* _Minimum:_ The minimum value in the set of measurements, such as the response times of an HTTP Server test in a test round.
* _nth Percentile:_ The value of the metric that contains n% of the measurements. When "nth Percentile" is selected, a text box will appear, allowing you to specify an integer for the percentile value from 1 to 99. 98% is the default. For example, a 98th Percentile whose value is 500 ms for a **Metric** of "Response Time" would indicate that 98% of the measurements of the response time were between 0 and 500 ms.
* _Mean:_ The value of the arithmetic mean (i.e. average) of the measurements. For example, a **Mean** of 50 ms for a **Metric** of "Latency" for one or more Network tests would indicate that the average value of the latency in the reporting period was 50 ms.
* _Median:_ The value of the median measurement. For example, a **Median** of 50 ms for a **Metric** of "Latency" for one or more Network tests would indicate that the value of 50 ms is the middle value in the range of all values of the latency in the reporting period.
* _Total:_ The total number of measurements. For example, a **Metric** set to "Alerts" and **Tests** set to a HTTP Server test indicate the total number of HTTP Server alerts received in the reporting period.
* _Active Time:_ The amount of time an alert rule was active. (Alerts metrics only)
* _Inactive time:_ The amount of time an alert rule was inactive. (Alerts metrics only)

**One Chart per Line:** When checked, the widget will create a chart for each member of the setting specified in the **Group By** column. For example, if **Group By** is set to "Agent", then a chart will be created for each agent, rather than one chart graphing all of the lines.

**Fixed Time Span:** When checked, a date selector will appear, allowing selection of a range of days different than the one specified for the entire dashboard. The widget will display data in that range unless the **Global Time Overide** option is selected.

* _Single Line:_ Data from all sources and tests are aggregated together into a single line.
* _Test:_ Data from all sources and tests are aggregated together into a single line.
* _Agent:_ Data from all agents are given their own chart lines.
* _Continents:_ Data are aggregated by continent. A chart line is displayed for each continent that has data from at least one source.
* _Countries:_ Data are aggregated by country. A chart line is displayed for each country that has data from at least one source.
* _None:_ Data are not aggregated.
* _All:_ Group all the data as a single chart line.
* _Test Labels:_ Data from each test label is given their own chart lines.
* _Sources:_ Data from each source is given their own lines on chart.
* _Agent Labels:_ Data from each agent label is given their own chart lines.
* _Servers:_ Data aggregated based on servers. Each server has a dedicated chart line.
* _Visited Sites:_ Endpoint Data from each visited site is given their own chart lines.
* _Private Networks:_ Data from each private network is given their own lines on chart.
* _Users:_ Data is aggregated based on user, each user gets their own chart lines.
* _Platforms:_ Data from each platform Windows/Mac is given their own chart lines.
* _Connections:_ Data for each connection is given their own lines on chart.
* _Networks:_ Data aggregated based on networks, each network gets their own chart lines.
* _Domains:_ Data aggregated based on visited domain, each domain would have a dedicated chart line.
* _Endpoint Agent Labels:_ Data from each Endpoint Agent label gets its own line on the chart.
* _Device:_ Data from each device is given their own chart lines.
* _Device Types:_ Data from each type of device is given their own chart lines.
* _Interfaces:_ Data from each device interface is given their own chart lines.
* _Interface Types:_ Data from each device interface type is given their own chart lines.

**Note:** If the Group By field's setting is the same as the Source field type (e.g. Group By is "Test" and Source type is "Test", Group By is "Countries" and Source type is "Countries", or Group By is "Monitors" and the Source type is "Monitors"), the Source field takes precedence.

For example, if Group By is "Countries" and Source type is "Tests", then all selected tests will have their data grouped by all countries found from those tests' results. Each country will have its own graph. However, if Group By is "Countries" and Source type is "Countries", then only those countries selected in the Source selector will have their own graph.

**Tests:** Names of tests that will provide the data to the dashboard. Based on your selection of **Metric** setting, the Tests menu will display only those tests that are relevant (e.g. if the **Metric** is Packet Loss, the Test menu displays Network tests and other tests that use an included Network test; if the metric is Availability, the Test menu displays a Web test, etc.).

**Sources:** Filter sources from which the data will be taken. The selections change based on which **Metric** is set, and will be one of the following:

* _Alert Rules:_ If the **Metric** is a Network, Web, DNS or Voice test or alert metric, a list of alert rules.
* _Agents:_ If the **Metric** is a Network, Web, DNS or Voice test or alert metric, a list of Cloud and Enterprise Agents.
* _Agent Labels:_ If the **Metric** is a Network, Web, DNS or Voice test or alert metric, a list of Cloud and Enterprise Agent labels (Built-in or Custom).
* _Tests:_ For any **Metric**, a list of tests.
* _Test Labels:_ For any **Metric**, a list of test labels (Built-in or Custom).
* _Monitors:_ If the **Metric** is a BGP test or alert, a list of ThousandEyes BGP monitors.

Below is an example of a configured time series widget and the resulting output.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-789a7df5f670046c77cefd0b47a2c8e39e837be2%2Fproduct-documentation\_reports\_working-with-reports-18.png?alt=media)

1.  1\.

    The above widget visualizes Maximum Packet Loss detected by an agent-to-server test. Data Source is configured to Cloud and Enterprise Agents.
2.  2\.

    The data is aggregated by agent, resulting in each agent's data rendered on an indivudual chart line.
3.  3\.

    “One Chart per Line” checkbox results in each line being rendered in a separate chart.
4.  4\.

    Configured to visualize data from 1 of 189 available tests.

Stacked Area widgets are used similarly to the Stacked Bar widget, except Stacked Area shows values over time. Useful when looking at increases in overall response timing, error counts, and other components, to show a progression of values over time.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-86bf78e74d1ab6f85e97761e51a57b5f99c0a452%2Fdashboard-stacked-area-widget-example.png?alt=media)

**Stacked Area Widget Configuration**

The Stacked Area widget configuration is shown below.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-d10feacc2eec2310fe5b97ee14793c5989f31309%2Fdashboard-stacked-area-widget-config.png?alt=media)

The Box-and-Whiskers widget is a convenient way of visually displaying a data distribution including key values such as: average, median, maximum, and minimum. It can also be useful for detecting outliers, as well as showing how tightly the data grouped.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-25d171d4271a169d614d561a62fe9c7bd2834381%2Fdashboard-box-and-whiskers-widget-example-2.png?alt=media)

**Box-and-Whiskers Widget Configuration**

The Box and Whiskers widget configuration is shown below.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-6eb6268a2912493c74d894ab2d110f57802b7135%2Fdashboard-box-and-whiskers-widget-config.png?alt=media)

Box-and-whiskers widgets have the following settings:

**Data Source:** The data source indicates which platform service will be referenced within the widget. Current options include:

* Alerts: Data is obtained from Platform alerts
* Cloud and Enterprise Agents: Data is obtained from scheduled tests performed by Cloud and Enterprise Agents
* Devices: Data is obtained from device-layer reporting
* Endpoint Browser Sessions: Data is obtained from endpoint agent browser sessions
* Endpoint Local Networks: Data is obtained from endpoint agent local networks
* Endpoint Scheduled Tests: Data is obtained from endpoint agent scheduled tests
* Endpoint Automated Session Tests: Data is obtained from endpoint automated session tests
* Internet Insights: Data is obtained from Internet Insights collective intelligence
* Routing: Data is obtained from BGP tests

**Category:** The category choices depend on the **Data Source** selected.

**Metric:** Options for metrics depend on the previous **Category** selection. All of the ThousandEyes Data Sources have their own metrics. For example, agent-to-server tests have five metrics: Available Bandwidth, Capacity, Jitter, Latency and Packet Loss. In addition to each of the ThousandEyes test types, alerts is also a category of choices for metrics. For more information on ThousandEyes metrics, see

[ThousandEyes Metrics: What Do Your Results Mean?](https://docs.thousandeyes.com/product-documentation/thousandeyes-basics/thousandeyes-metrics-what-do-your-results-mean)

​

* _Single Chart:_ Data from all sources and tests are aggregated together into a single plot.
* _Test:_ Data from all tests are aggregated together into a single line.
* _Agent:_ Data from all agents are given their own chart lines.
* _Continents:_ Data are aggregated by continent. A chart line is displayed for each continent that has data from at least one source.
* _Countries:_ Data are aggregated by country. A chart line is displayed for each country that has data from at least one source.
* _None:_ Data are not aggregated.
* _All:_ Group all the data as a single chart.
* _Test Labels:_ Data aggregated based on test labels, each test label gets its own chart.
* _Sources:_ Data from each source is given their own charts.
* _Agent Labels:_ Data from each agent label is given its own chart.
* _Servers:_ Data aggregated based on servers. Each server has a dedicated chart.
* _Visited Sites:_ Endpoint Data from each visited site is given its own chart.
* _Private Networks:_ Data from each private network is given its own chart.
* _Users:_ Data is aggregated based on user, each user gets their own chart.
* _Platforms:_ Data from each platform Windows/Mac is given its own chart.
* _Connections:_ Data for each connection is given its own chart.
* _Networks:_ Data aggregated based on networks, each network gets its own chart.
* _Domains:_ Data aggregated based on visited domain, each domain would have a dedicated chart.
* _Endpoint Agent Labels:_ Data from each Endpoint Agent label gets its own chart.
* _Device:_ Data from each device is given its own chart.
* _Device Types:_ Data from each type of device is given its own chart.
* _Interfaces:_ Data from each device interface is given its own chart.
* _Interface Types:_ Data from each device interface type is given its own chart.

**Note:** If the Group By field's setting is the same as the Source field type (e.g. Group By is "Test" and Source type is "Test", Group By is "Countries" and Source type is "Countries", or Group By is "Monitors" and the Source type is "Monitors") then the Source field takes precedence.

For example, if Group By is "Countries" and Source type is "Tests", then all selected tests will have their data grouped by all countries found from those tests' results. Each country will have its own chart. However, if Group By is "Countries" and Source type is "Countries", then only those countries selected in the Source selector will have their own chart.

**Fixed Time Span:** When checked, a date selector will appear, allowing selection of a range of days different than the one specified for the entire dashboard. The widget will display data in that range unless the **Global Time Overide** option is selected.

**Sources:** Filter sources from which the data will be taken. The selections change based on which **Metric** is set, and will be one of the following:

* _Alert Rules:_ If the **Metric** is a Network, Web, DNS or Voice test or alert metric, a list of alert rules.
* _Agents:_ If the **Metric** is a Network, Web, DNS or Voice test or alert metric, a list of Cloud and Enterprise Agents.
* _Agent Labels:_ If the **Metric** is a Network, Web, DNS or Voice test or alert metric, a list of Cloud and Enterprise Agent labels (Built-in or Custom).
* _Tests:_ For any **Metric**, a list of tests.
* _Test Labels:_ For any **Metric**, a list of test labels (Built-in or Custom).
* _Monitors:_ If the **Metric** is a BGP test or alert, a list of ThousandEyes BGP monitors.

**Scale:** Configure scaling of shown metric. By default, the low end is set to 0. Not available for metrics with non-arbitrary values (i.e. percent metrics).

**Example Box-and-Whiskers Widget**

Below is an example of a configured box-and-whiskers widget entitled and the resulting dashboard output.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-1984b13c510a6b8c8d88edb6698dc1f91eaec313%2Fproduct-documentation\_reports\_working-with-reports-28.png?alt=media)

The configuration shows the widget's metric as “Throughput". The **Group By** selector is set to "Agents", which displays Cloud and Enterprise Agents on the map in their respective locations. The source filter is set to "Tests" and "1 of 188 included", indicating that one test's data is being displayed.

For each time on the horizontal axis, dots representing minimum and maximum values for that round of data are plotted, along with a dot for the median of all values in that round. Additionally, a blue bar starts below the median at the value representing the end of the first quartile of the data, and extends above the median to the value representing the end of the third quartile. Mousing over the points or bars will display a tooltip with the numeric values:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-15c7f98d902ace9809ff15451e0c62de40ccee4b%2Fproduct-documentation\_reports\_working-with-reports-29.png?alt=media)

At 2019-01-27 we see that the data from all agents had the following distribution:

* One quarter of the measurements fell into the range of 8.78 mbps to 42.65 mbps (minimum dot to bottom of the bar)
* One quarter of the measurements fell into the range of 42.65 mbps to 88.18 mbps (bottom of the bar to the median dot)
* One quarter of the measurements fell into the range of 88.18 mbps to 98.67 mbps (median dot to the top of the bar)
* One quarter of the measurements fell into the range of 98.67 mbps to 139.85 mbps (top of the bar to the maximum dot)

Position of the median dot relative to the ends of the bar indicates the spread of the values in the data for the quartile above and below the median.

The Maps widget type includes the Map widget.

The Map widget displays data on a world map, based on location of the testing systems (agents or BGP monitors). Data can be displayed per country, per continent, or per agent (if a non-BGP metric is displayed).

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-623b54b36be7d5631e4703ed9a72d846207e2553%2Fdashboard-map-widget-examples.png?alt=media)

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-3e5c0edaf0890e44cc0e403dd21f1d7ba915ea62%2Fdashboard-map-widget-config.png?alt=media)

Map widgets have the following settings:

**Data Source:** The data source indicates which platform service will be referenced within the widget. Current options include:

* Alerts: Data is obtained from Platform alerts
* Cloud and Enterprise Agents: Data is obtained from scheduled tests performed by Cloud and Enterprise Agents
* Endpoint Browser Sessions: Data is obtained from endpoint agent browser sessions
* Endpoint Local Networks: Data is obtained from endpoint agent local networks
* Endpoint Scheduled Tests: Data is obtained from endpoint agent scheduled tests
* Endpoint Automated Session Tests: Data is obtained from endpoint automated session tests
* Internet Insights: Data is obtained from Internet Insights collective intelligence
* Routing: Data is obtained from BGP tests

**Category:** The category options depend on the **Data Source** selected.

**Metric:** Options for metrics depend on the previous **Category** selection. All of the ThousandEyes Data Sources have their own metrics. For example, agent-to-server tests have five metrics: Available Bandwidth, Capacity, Jitter, Latency and Packet Loss. In addition to each of the ThousandEyes test types, alerts is also a category of choices for metrics. For more information on ThousandEyes metrics, see

[ThousandEyes Metrics: What Do Your Results Mean?](https://docs.thousandeyes.com/product-documentation/thousandeyes-basics/thousandeyes-metrics-what-do-your-results-mean)

​

**Measure:** A statistical measurement. **Measure** choices available depend on the **Metric** setting, but will come from the following list:

* _% positive:_ The percentage of measurements greater than zero. For example, the percentage of time when a Network alert was active.
* _% zero:_ The percentage of measurements equal to zero. For example, the percentage of time when a Network alert was active.
* _Maximum:_ The maximum value in the set of measurements, such as the latency times of a Network test over the time period of the dashboard.
* _Minimum:_ The minimum value in the set of measurements, such as the latency times of a Network test over the time period of the dashboard.
* _Standard Deviation:_ The population standard deviation of a set of measurements, such as the latency times of a Network test over the time period of the dashboard.
* _nth Percentile:_ The value of the metric that contains n% of the measurements. When "nth Percentile" is selected, a text box will appear, allowing you to specify an integer for the percentile value from 1 to 99. 98% is the default. For example, a 98th Percentile whose value is 500 ms for a **Metric** of "Response Time" would indicate that 98% of the measurements of the response time were from 0 to 500 ms.
* _Mean:_ The value of the arithmetic mean (i.e. average) of the measurements. For example, a **Mean** of 50 ms for a **Metric** of "Latency" for one or more Network tests would indicate that the average value of the latency in the reporting period was 50 ms.
* _Median:_ The value of the median measurement. For example, a **Median** of 50 ms for a **Metric** of "Latency" for one or more Network tests would indicate that the value of 50 ms is the middle value in the range of all values of the latency in the reporting period.
* _Total:_ The total number of measurements. For example, a **Metric** set to "Alerts" and **Tests** set to a HTTP Server test indicate the total number of HTTP Server alerts received in the reporting period.
* _Active Time:_ The amount of time an alert rule was active. (Alerts metrics only)
* _Inactive time:_ The amount of time an alert rule was inactive. (Alerts metrics only)

**Group By:** Sets the map widget to display results grouped by:

* _Agent:_ Agents are displayed with circles on the map at their geographic location. Enterprise Agents use the geographic location listed in the agent's row of the Enterprise Agents page (Settings > Enterprise Agents). Agents are colored based on the value of the data, per the colored legend and associated scale from the **Fixed Scale** setting, as described below.
* _Countries:_ Data are aggregated by country. Countries are colored based on the value of the data, per the colored legend and associated scale from the **Fixed Scale** setting, as described below.
* _Continents:_ Data are aggregated by continent. Continents are colored based on the value of the data, per the colored legend and associated scale from the **Fixed Scale** setting, as described below.

**Sort By:** Available only for a **Group By** setting of "Agents". Orders multiple entries in the Tooltips that are displayed when mousing over circles with multiple agents.

* _Default:_ Sort bars optimally, based on the settings for **Metric** and **Show Comparison**. The metric that is optimal for your settings is shown in parentheses.
* _Alphabetical:_ Sort bars by ascending alphabetical order.
* _Alphabetical (Reverse):_ Sort bars by ascending alphabetical order.
* _Highest:_ Sort bars by highest value first.
* _Lowest:_ Sort bars by lowest value first.

**Scale:** Specify the range of values for the colored legend in the map. By default, the low end is set to 0. Not available for metrics with non-arbitrary values (i.e. percent metrics).

**Fixed Time Span:** When checked, a date selector will appear, allowing selection of a range of days different than the one specified for the entire dashboard. The widget will display data in that range unless the **Global Time Overide** option is selected.

**Filter:** Names of tests, agents, or servers that will be the source of the data to the dashboard. To filter by multiple criteria, click the **+** icon to the right of the pull-down menu.

Below is an example of a configured map widget and the resulting output.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-fa57df527536a5059840c8f563b2c4e2e0ef09f8%2Fproduct-documentation\_reports\_working-with-reports-26.png?alt=media)

1.  1\.

    The widget is configured to visualize Mean Packet Loss observed in an agent-to-server tests with Cloud and Enterprise Agents as Data Source.
2.  2\.

    Group By field is set to Countries and hence data is aggregated based on Countries and coloured on the map accordingly.
3.  3\.

    Widget is configured to visualize data from 5 of 189 available tests.

Note in the upper-right corner the magnification selector, which allows you to zoom in or out on the map. Also note in the lower-right corner the colored legend, with a range of the metric (Availability) that starts at 0% and ends at 100%.
