# Using the Dashboard

The figure below shows one of the ThousandEyes built-in dashboards:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-a1319855b049a45d63afbf0d1dfe20f638e577e1%2Fdashboard-with-callouts.png?alt=media)

* Use the selector to choose one of the dashboards shared within your account group, or private dashboards you've created for yourself.
* Displays time since the current dashboard was last refreshed.
* Click the **+ Add Widget** button to add new widgets to the current dashboard.

The **Dashboards** page is the starting point when you log in to the ThousandEyes platform. You can see live status dashboards that show a specific time period, and also schedule and share point-in-time snapshots of a dashboard. Data from tests and Internet Insights can be organized into highly customized layouts, presented numerically or in tables or graphs, and sent via email to users.

The **Dashboards** page is configured to refresh every two minutes. Displaying the Dashboard page prevents the user from being logged out due to inactivity, making it suitable for kiosk or operations-center displays.

### Using the Dashboard Controls <a href="#using-the-dashboard-controls" id="using-the-dashboard-controls"></a>

You can use the dashboard controls to adjust the display or to make changes to dashboards, as shown below.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-bcf7e4a10a5a3d1e667d8abbac135bd490d4177c%2Fdashboard-controls.png?alt=media)

* Refresh countdown shows when dashboard refresh will occur. It’s every 2 minutes.
* Choose a time interval to view. Time range options are last 1 hour to last 60 days. You can also look back at a period of 90 days in a fixed time view.
* Toggle to override fixed interval settings in dashboard widget configurations.
*   Use the **+ Add Widget** button to add a new widget to the current dashboard. See

    [Using the Widget Controls](broken-reference)

    for information on how to edit existing widgets.
* Click the ellipsis button to reveal a dropdown menu with the following options:
  * **Create New Dashboard** creates a new blank dashboard to be named and populated with widgets.
  * **Duplicate Dashboard** creates a copy of the current dashboard.
  * **Edit Dashboard** opens a side modal where you can configure the dashboard title, description, and sharing options within the organization's account groups.
  * **Delete Dashboard** deletes the currently viewed dashboard.

You’ll need permission to edit the dashboard in order to create, duplicate, or delete a dashboard. You can’t change the built-in dashboards.

### Using the Widget Controls <a href="#using-the-widget-controls" id="using-the-widget-controls"></a>

Each widget on the dashboard includes a set of controls as well, as shown below.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-4b3f2353ceb51673fcdc1c4bc738ececdd76c436%2Fdashboard-widget-controls.png?alt=media)

### Render Limits on Dashboards <a href="#render-limits-on-dashboards" id="render-limits-on-dashboards"></a>

When you add a dashboard or dashboard widget that uses a large data set, you are asked to either apply a test filter, or reduce the time span in order to render the data.

Currently, the ThousandEyes platform applies _soft_ or _hard_ limits to the following widget types:

* Widgets that use the Cloud and Enterprise Agent data set.
* Widgets that use the Device data set.
* Widgets that use the BGP data set.
* Widgets that use the Endpoint Agent data set.
* Widgets that include an excessive number of lines of data.

When you reach the soft limit, the app offers you the option to click **Render Anyway** and load the widget. This does not guarantee that the widget will load, as it could still exceed the hard limit. When you reach the hard limit, you cannot load the widget without the modifications below.

#### Widgets with Cloud and Enterprise Agent Data <a href="#widgets-with-cloud-and-enterprise-agent-data" id="widgets-with-cloud-and-enterprise-agent-data"></a>

*   The hard limit applies to widgets that query more than 1,000,000 data points. Because the data point total is based on the number of tests in the widget, the number of agents running those tests, and the timespan of the widget, this data point limit is difficult to quantify. If you hit this hard limit, we suggest you reduce the number of tests or lower the timespan of the widget.

    ![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-8821631b511e5e855415553318acf39704c4e832%2Fproduct-documentation\_reports\_working-with-reports-38.PNG?alt=media)
*   The hard limit applies to widgets that query more than 2,000,000 data points. Because the data point total is based on the number of devices in the widget, the number of interfaces on those devices, and the timespan of the widget, this data point limit is difficult to quantify. If you hit this hard limit, we suggest you reduce the number of devices or lower the timespan of the widget.

    ![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-ed211384a78602e872dd3d36f0e7390e8bd2c0dd%2Fproduct-documentation\_reports\_working-with-reports-37.png?alt=media)
* The soft limit applies to all widgets that do not use filters.
*   The hard limit applies to widgets that go beyond a multiplicative factor of 700 for tests and days. For example, if you have 100 tests and 7 days worth of data, this is the upper bound of the hard limit. If you have 50 tests and 14 days worth of data, this is the upper bound of the hard limit.

    ![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-8e90d5047a17fa8c29ebfca3280fe2b0b74da3a8%2Fproduct-documentation\_reports\_working-with-reports-33.png?alt=media)

#### Widgets With an Excessive Number of Lines of Data <a href="#widgets-with-an-excessive-number-of-lines-of-data" id="widgets-with-an-excessive-number-of-lines-of-data"></a>

*   The soft limit applies to time series, bar chart, and box-and-whiskers widgets with more than 30 lines.

    ![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-fecaecda746b96840f437614df588563bfaa3c98%2Fproduct-documentation\_reports\_working-with-reports-34.png?alt=media)
* The hard limit applies to time series, bar chart, and box-and-whiskers widgets with more than 100 lines. To remove the limit, apply a filter that reduces the line numbers to fewer than 100.
