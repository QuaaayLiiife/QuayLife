# Getting Started with Dashboards

Dashboards are powerful tools to visualize your ThousandEyes tests, quickly isolate issues, and see the health of your infrastructure and applications. Before starting, it’s recommended to consider who will use the dashboard, identify the key metrics, and which tests will provide the best visibility.

Unless you are creating a dashboard using Internet Insights or Application Outages as a data source you will need to have tests created and actively running. Also, you can create agent labels and test labels for grouping the data. See

[Working with Test Labels for Agents and Test Groups](https://docs.thousandeyes.com/product-documentation/internet-and-wan-monitoring/tests/working-with-labels-for-agent-and-test-groups)

for more information.

One of the critical features of the ThousandEyes widget is that you can make changes, instantly see what the data will look like, and then decide to save the settings. If the widget is not showing the data that will provide you or your team with the best view you can revert it or continue to test out different filters and settings by updating the data source, metrics, measure, agents, etc. When widgets are aligned and set up with the proper metrics it can drastically improve your ability to troubleshoot and resolve issues in your environment. You can easily position tests showing a side by side inside-out and outside-in view or create a visualization to show you the critical metrics for different circuits and services in one dashboard.

Before you create a dashboard, you should consider who is the end-user and what is the purpose of the dashboard. This information will help you determine which tests from your environment will be used to configure the widgets and which metrics will provide the best visibility into your critical services.

#### Pre-requisites for Creating a Sample Dashboard <a href="#pre-requisites-for-creating-a-sample-dashboard" id="pre-requisites-for-creating-a-sample-dashboard"></a>

We’ll use three different test types for this dashboard but if you don’t have these tests configured in your environment feel free to experiment with others: DNS, Network - Agent to Server and a Web - HTTP Server Test (Note: this could also be a Web - Page Load or Web - Transaction test as these all have Web - HTTP Server metrics). For more information on tests see

[Getting Started with Tests](broken-reference)

.

#### Seven Steps to Create as Sample Dashboard <a href="#seven-steps-to-create-as-sample-dashboard" id="seven-steps-to-create-as-sample-dashboard"></a>

Here's an example of a dashboard once it's completed. It should take between 5-10 minutes to complete based on the below step-by-step instructions:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-263bef030543bfc4d56f54c45dfe1653145fd60b%2Fmy-dashboard-sample.png?alt=media)

#### Step 1: Log in and Create a New Dashboard <a href="#step-1-log-in-and-create-a-new-dashboard" id="step-1-log-in-and-create-a-new-dashboard"></a>

Log in to the ThousandEyes platform and access the Dashboard Menu. you will be directed to a built-in dashboard called ThousandEyes Built-in unless your account group already has created a default dashboard and set it up for your default login account group. To create a new dashboard, click the **“...” Options** or **ellipsis** menu and select **Create New Dashboard**.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-539d7305b925fabd057eaca478f59b918e076fb7%2Fcreate-new-dashboard.png?alt=media)

This opens the **Create New Dashboard** window and settings. For this example, name the dashboard **My Dashboard** and click **Create Dashboard**:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-1f93fd3f558e28689e949ed4e29e3e4e19ff4ad6%2Fcreate-new-dashboard-pane.png?alt=media)

Create New Dashboard Pane

* **Name:** For this example, use **My Dashboard**. Ensure you provide a unique name to your dashboard. Using an existing name prompts the error message: **Name Not Unique** below the dashboard name field.

#### Step 2: Add a Number Widget <a href="#step-2-add-a-number-widget" id="step-2-add-a-number-widget"></a>

You can start to add widgets and make it into a functional view of your tests and metrics. In this case, start with the

[number widget](https://docs.thousandeyes.com/product-documentation/dashboards/dashboard-widgets#number-widget)

to quickly show the overall health of the packet loss, latency, and jitter from your underlying DNS and Web - HTTP Server and Network - Agent to Server test. In the upper right corner of your dashboard click the **+Add Widget** button and the widget pane appears:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-fc68a9d3da2b53ea88dfa50a54e147c9cfd37373%2Fmy-dashboard-add-widget.png?alt=media)

Click or drag the **Number Widget** on to the dashboard causing the number widget configuration pane to appear:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-881ddda04fdb2fdd9a1b9924abfd321523a1efe6%2Fadd-widget-number.png?alt=media)

Add Number - Number Widget

To configure the Number Widget, you need to update so it will start to show useful metric data. Here’s how the first card will look:

**Note:** most of the selections are card specific and the selections will be reflected in the card view which can easily be duplicated and then modified for the other cards.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-286403240871214bfb042d78a1b7430a230f3d5c%2Fedit-number-widget-packet-loss.png?alt=media)

Editing Number Widget - Packet Loss

* **Widget Name:** Network Health
* **Data Source:** Cloud & Enterprise Agents
* **Category:** Network - Agent to Server
* **Measure:** Mean (other selections can be Maximum, Median, Minimum, nth Percentile or Standard 6. Deviation)
* **Drill Down:** Select Tests and individually select your DNS, Network - Agent to Server and Web - HTTP Server Test.

Drill downs can be used as filters, and you can select multiple filters for Agents, Agent Labels, Tests, Test Labels, and Servers.

Click **+Duplicate Card** and update the next card as shown below:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-81e1b0e6b9511a26d8ff62c2615da1a0ec537444%2Fedit-number-widget-latency.png?alt=media)

Editing Number Widget - Latency

Click **+Duplicate Card** and update the next card as shown below:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-41c5edc26e21fcde4551bf228f84016a2b9241b5%2Fedit-number-widget-jitter.png?alt=media)

Editing Number Widget - Jitter

* Click **Save** as you’ve completed your first widget! Your dashboard should look like the below screenshot:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-455ebc3b28970faf5ec7b40fa9cd03666b4ae604%2Fmy-dashboard-number-widget.png?alt=media)

My Dashboard Number Widget

#### Step 3: Add a Color Grid Widget <a href="#step-3-add-a-color-grid-widget" id="step-3-add-a-color-grid-widget"></a>

In the upper right corner of your dashboard click **+ Add Widget** and click the **Color Grid widget**:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-8b34c16ae6aa7ba75fd2a9fc2e0d57cf0d1b03fd%2Fadd-widget-color-grid.png?alt=media)

In this example, you will configure the color widget to show latency for the tests grouped by the agents from where the tests are being performed. This will make it so you can see which location is having an issue with latency. You can learn more about the color grid widget in our

[documentation](https://docs.thousandeyes.com/product-documentation/dashboards/dashboard-widgets#color-grid-widget)

. Update the color widget as shown in the screenshot below:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-7a8f2c507398df5fff0acc4c0ed5e515d19a3432%2Fedit-color-grid-widget-latency.png?alt=media)

Edit Color Grid Widget - Latency

* **Widget Name:** Latency (by Agent)
* **Data Source:** Cloud & Enterprise Agents
* **Category:** Network - Agent to Server
* **Sort Cards By:** Value (Descending)
* **Drilldown:** Select **Tests** and individually select your DNS, Network - Agent to Server and Web - HTTP Server Test.
* Click **Save** and you should see a widget in your dashboard that looks something like the below screenshot:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-52b175c2750ce91365fb99a2cbdf35958ddf6014%2Fmy-dashboard-color-grid-widget.png?alt=media)

My Dashboard - Color Grid Widget

#### Step 4: Add a Stacked Bar Widget <a href="#step-4-add-a-stacked-bar-widget" id="step-4-add-a-stacked-bar-widget"></a>

In the upper right corner of your dashboard click **+ Add Widget** and click the **Stacked Bar widget** from the Breakdown section as shown below:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-840ae3b271e16f459870d46887877bb519608826%2Fadd-widget-stacked-bar.png?alt=media)

Add Widget - Breakdown - Stacked Bar

You can configure the stacked bar chart to show the metrics that make up your HTTP Total Time when it’s measured from your test agents. This will allow you to easily visualize DNS Time, Connect Time, SSL Time, Wait Time and Receive Time. You can find out more about the stacked bar widget in our

[documentation](https://docs.thousandeyes.com/product-documentation/dashboards/dashboard-widgets#stacked-bar-widget)

. Configure the stacked bar chart widget as show in the screenshot below:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-0d97c394b3bcbc3de0e4556187441cc47e1754ca%2Fedit-stacked-bar-widget-http-total-time.png?alt=media)

Edit Stacked Bar Widget - HTTP Total Time

* **Widget Name:** HTTP Total Time (by Agent)
* **Data Source:** Cloud & Enterprise Agents
* **Category:** Web - HTTP Server
* **Y-Axis:** Agents and be sure change the bars to be horizontal for better visibility
* **Drill Down:** Select your Web - HTTP Server (this will work for Web - Page Load and Web - Transaction tests as well)
* Click **Save** and you should see a widget that looks like the below screenshot that clearly breaks down the important metrics that results in your http total time from each agent’s perspective:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-8d8dd25c2187257ce553dccdffc160a31559710f%2Fmy-dashboard-stacked-bar-widget.png?alt=media)

My Dashboard - Stacked Bar Widget

#### Step 5: Add a Time Series Line Widget <a href="#step-5-add-a-time-series-line-widget" id="step-5-add-a-time-series-line-widget"></a>

In the upper right corner of your dashboard click **+ Add Widget** and click the **Line widget** from the Time Series section as shown below:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-f6f0b018b0d9497cd0da27f1ae25da32f112f837%2Fadd-widget-time-series-line.png?alt=media)

Add Widget - Time Series - Line

The time series line widget provides great visibility so you can see changes in any number of metrics over time. In this example you will be able to quickly see if packet loss has changed over the day with any of your tests. Configure the time series line widget as show in the screenshot below:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-98780e2799b94b05e180a22bbc2cea3cb8843f78%2Fedit-time-series-line-widget-packet-loss.png?alt=media)

Edit Time Series Line Widget - Packet Loss

* **Widget Name:** Packet Loss (by Test)
* **Data Source:** Cloud & Enterprise Agents
* **Category:** Network - Agent to Server
* **Drilldown:** Select Tests and individually select your DNS, Network - Agent to Server and Web - HTTP Server Test.
* Click **Save** and you should see a widget like the below screenshot:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-94e62a13884de59c2e8c9e63238d00efd250f0e2%2Fmy-dashboard-time-series-line-widget.png?alt=media)

My Dashboard - Time Series Line Widget

#### Step 6: Add a Live Status Tests Widget <a href="#step-6-add-a-live-status-tests-widget" id="step-6-add-a-live-status-tests-widget"></a>

In the upper right corner of your dashboard click **+ Add Widget** and click the **Tests widget** from the Live Status section as shown below:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-ccb0066ff1fe61024fdbb98f61f9319721ec1ff4%2Fadd-widget-tests.png?alt=media)

Add Widget - Live Status - Tests

The live status test widget provides a powerful visual of your tests and their primary metrics over the last 12 hours in a spark view so you can quickly troubleshoot if an issue spans multiple tests or if there was a change in the metric. It also provides a link to the test, the test settings, and a visual indicator if there is an active alert including a link to the alert. You can find out more about the test widget in our

[documentation](https://docs.thousandeyes.com/product-documentation/dashboards/dashboard-widgets#tests-widget)

. Configure the test widget as shown in the below screenshot:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-8f09100de7e9676ee03da6aadbf1a2438ab4da1d%2Fedit-tests-widget-test-ids.png?alt=media)

Edit Live Status Tests Widget - Test IDs

* **Widget Name:** Google Tests (in this case all the tests are to Google but be sure to use a logical name based off the tests you chose for this example or just use Tests)
* **Data Filter:** Click **any** and select the **Tests IDs** for your DNS, Network - Agent to Server and Web - HTTP Server Test
* Click **Save** and you should see a widget like the screenshot below:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-284490aaefeee1ca39c8a8dff1d550dafc8fc0d6%2Fmy-dashboard-tests-widget.png?alt=media)

My Dashboard - Tests Widget

#### Step 7: Add a Live Status Alert List Widget <a href="#step-7-add-a-live-status-alert-list-widget" id="step-7-add-a-live-status-alert-list-widget"></a>

This is the last widget for this sample dashboard. In the upper right corner of your dashboard click **+ Add Widget** and click the **Alert List widget** from the Live Status section as shown below:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-42e594ab82a8e5c1db297f8b009d6a30c65cfc29%2Fadd-widget-alert-list.png?alt=media)

Add Widget - Live Status - Alert List

The alert list widget will display the alerts as well as their duration and will indicate if they are active. You can find out more about the alert list widget in our

[documentation](https://docs.thousandeyes.com/product-documentation/dashboards/dashboard-widgets#alert-list-widget)

. Configure the alert list widget as shown in the below screenshot:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-6783f7a685fb0f479ba1753fc2b6241f78ff4491%2Fedit-alert-list-widget-tests.png?alt=media)

Edit Live Status Alert List - Tests

* **Drilldown:** Select **Tests** and individually select your DNS, Network - Agent to Server and Web - HTTP Server Test.
* Click **Save** and now you’re all done!

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-c566c51fc2e60fb81dbf14989beb005884156449%2Fmy-dashboard-alert-list-widget.png?alt=media)

My Dashboard - Alert List Widget

### Dashboard Display Settings <a href="#dashboard-display-settings" id="dashboard-display-settings"></a>

Now that you have a dashboard configured, you may want to view it with data for a particular time interval to use it for troubleshooting an outage or visualizing your network or service performance during a specific time range. To accomplish this, click the **Dashboard Time selector** and select the relative time ranges using the quick select options or customize the time range using the fixed time interval as shown in the below screenshot. **Note:** The timeframe of the Live widgets (Tests, Alert list, Map) cannot be updated. After you select your custom time, you must **toggle** the global time override button otherwise the time selection will not be applied.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-916d36959c982e3d509d1d06d659807e00daec64%2Fdashboard-display-settings-time-options.png?alt=media)

Dashboard Display Settings Time Options

* **Relative Time Interval:** These are quick time selections based on the most commonly used time intervals
* **Fixed Time Intervals:** This can be used if you want to select a custom date and time to be reflected in the dashboard widgets.
* **Global Time Override Button:** This must be toggled on for your selection to be applied to the dashboard widgets.

The following is an example using a relative time interval of last 7 days:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-c7ad818cdf6db153620f1951a7fe00ac1f932064%2Fdashboard-display-settings-time-7-day.png?alt=media)

Dashboard Display Settings - Last 7 Days

* **Relative Time Interval:** Last 7 days
* **Global Time Override Button:** Toggle on so you see the blue indicator
* **Widget:** Updated to show the last 7 days

If you’d like to learn more about dashboard display settings please check our

[documentation](https://docs.thousandeyes.com/product-documentation/dashboards/customizing-your-dashboard#configuring-dashboard-display-settings)

.

There are many different reasons you might want to duplicate a dashboard. For example, another team member has created one, but it doesn’t exactly match your needs. You may want to test out some configuration changes but not cause any issues with the existing one that is used for production or maybe there is a new initiative, and you want to leverage what is in use today but customize it to the tests for the new initiative. Dashboards can be duplicated simply by using the upper right “...” options menu or ellipsis and selecting “Duplicate Dashboard” so you can test out and experiment with different configurations. See the screenshot below:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-71c9aff4782280b11bf225798ec3509846993e79%2Fdashboard-duplication-options.png?alt=media)

Dashboard Duplication Options

* Click: **Duplicate Dashboard** and the Duplicate Dashboard pane will appear as shown below:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-1fc1763e5d3d1cd285b3f97c422c66ad4008a86d%2Fdashboard-duplication-name.png?alt=media)

* **Dashboard Name:** You must provide a unique name otherwise you won’t be able to save it.
* Click **Duplicate Dashboard**

### Dashboard Permissions and Labels <a href="#dashboard-permissions-and-labels" id="dashboard-permissions-and-labels"></a>

If you want to set up your default dashboard when you log in so you aren’t automatically viewing the ThousandEyes Built-in one this can be accomplished provided you have the correct user access by clicking the **“...” options** menu or **ellipsis** pull down and selecting **Edit Dashboard** in the upper right corner of your dashboard as shown in the below screenshot:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-8bc93193fde71773eac99e998c76589a4c68a667%2Fdashboard-permissions-edit.png?alt=media)

Edit Dashboard Pull Down Menu Option

This makes the **Dashboard Details Pane** appear; which can be used to modify different settings like labels, account groups, and default time range as shown in the below screenshot:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-0f57e0710339941b70d787bc2646a36aa1574487%2Fdashboard-permissions-details.png?alt=media)

* **Account Group Visibility**: By default, this will be set to **Only current account group**. If you have other account groups that could benefit from your dashboard or want access to it you can share with all account groups or just specific ones using this selection.
* **View Settings**: Allows you to lock the dashboard down so it can only be visible to you. Which you may want to do while you are tuning or designing it or if it is something customized only for you. Additionally, you can set it as your default dashboard, and if you have the proper permissions set it as the account group default dashboard.
* Click the **Save Changes** button after you make changes to ensure they applied correctly.

Dashboard labels are a great way to quickly filter out a set of dashboards for troubleshooting. Some examples of ways to use them would be for dashboards that are for an application like Webex. You could have a dashboard dedicated to end-user experience using endpoint agents that your helpdesk uses, a dashboard showing Webex testing using enterprise agents for your branches and data center that your network and collaboration team use, and a dashboard with Internet Insights and Application Outages dedicated to Webex that everyone leverages. All these dashboards can share the same label of Webex and when you select it, they will be filtered to make it faster to navigate between dashboards for troubleshooting issues. Following is an example of a Webex dashboard label that will show up when you click the dashboard selection pull-down list:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-ca558f977ed4e30d0af2c7db1ce8772f3b0ed661%2Fdashboard-labels.png?alt=media)

* **Dashboards** pull down list
* **Custom Labels:** This example Webex is checked.

Another example could be that you have a critical business payment processing application with different layers of service, and you have enterprise agents monitoring from the inside to the edge which transits an internal load balancer, and externally have cloud agents monitoring it which transits an external load balancer. Additionally, there could be third party services that the application relies on, and different teams have their custom dashboards established to monitor the application internally versus externally versus the third party services. All the dashboards from these teams can be applied to the critical business payment application label allowing you to quickly filter and navigate between the different views.

To add a dashboard to a label, click the **“...” options menu** or **ellipses** in the upper right corner of the dashboard view and click **Edit Dashboard**. The Dashboard Details pane will appear as shown in the below screenshot:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-c702fd88856ac10a444967c1564da3629aaeef15%2Fdashboard-details.png?alt=media)

* **Label selection or Manage Labels:** You can associate your dashboard with an existing label, if you have any, or use the manage labels link to create a label.

### Save or Download a Dashboard Snapshot <a href="#save-or-download-a-dashboard-snapshot" id="save-or-download-a-dashboard-snapshot"></a>

#### Save a Dashboard Snapshot <a href="#save-a-dashboard-snapshot" id="save-a-dashboard-snapshot"></a>

Dashboard snapshots capture the data and all the metrics in the dashboard at that point in time and can be accessed in the future or shared with others, including in a ticket or chat so that the other person or team can see the same thing you are seeing. Click on the **camera icon** in the upper right on the dashboard page and it will create a drop-down list with a camera icon to **save a snapshot** of the dashboard as shown in the screenshot below:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-afa30125111fc01cc93d7a253a423c04cf1c30e1%2Fdashboard-save-snapshot.png?alt=media)

Dashboard - Save Snapshot

This opens the **Save a Snapshot** pane. It’s recommended to provide a meaningful name, so it can be referenced in the future. You will have to turn on link sharing to share it with others and copy the link otherwise it will only be available by logging into the ThousandEyes platform and viewing the snapshots directly in the **Sharing > Snapshots** menu. Following is an example of the Snapshot pane:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-2c6dc6c518517ab3561f35d61d779bf5f7dc990c%2Fdashboard-save-snapshot-options.png?alt=media)

Dashboard - Save Snapshot Options

* **Snapshot Name:** Provide a useful name for the snapshot for future reference like a ticket number for direct reference or information about the issue you’re troubleshooting and the date and time.
* **Link Sharing:** This is off by default, but you’ll need to toggle it to on in order to generate a unique link to the dashboard snapshot. **Note:** The link will not work untils you click the **Save and Share** button.
* **Copy button:** to copy the unique dashboard snapshot sharelink.
* **Save and Share:** This will save the dashboard snapshot and generate the sharelink which could take a few minutes.

You may want to quickly share a dashboard as a PDF or CSV with a coworker or other team which can be accomplished using the download icon as shown in the below image:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-9f38d11ecf32963e9a13d56517c32138fa15ae8b%2Fdashboard-download.png?alt=media)

### Schedule a Dashboard Snapshot <a href="#schedule-a-dashboard-snapshot" id="schedule-a-dashboard-snapshot"></a>

Now that you have a compelling dashboard visualizing the key metrics, you can raise awareness of the network's health and the applications. Imagine a scenario, where a network manager has a weekly meeting with branch managers who blame the network for application slowness. You can create a scheduled snapshot, and email it to them before the meeting so they can see and share the network's health combined with the application response time.

To schedule a dashboard snapshot click the **camera icon** in the upper right corner of the dashboard view and select the **clock icon** labeled **Schedule A Snapshot** as shown in the below screenshot:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-55d75158ab68b25ea379c4f885965c614b56f1e4%2Fdashboard-schedule-snapshot.png?alt=media)

Dashboard - Schedule Snapshot

The Schedule Snapshots pane will appear as shown in the below screenshot. Feel free to experiment with different options.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-22be1ce418dadd87d2440b95896e89ce00b61e79%2Fdashboard-schedule-snapshot-options.png?alt=media)

Dashboard - Schedule Snapshot Options

* **Snapshot Name:** Be sure to use a name that will be useful for the intended recipients.
* **Repeat Interval:** This will be how often the snapshot is created and sent out or saved.
* **Emails:** By default, this will show the email addresses of the users that are configured to access the ThousandEyes platform in your account group. If you need to configure the email to go to someone that doesn’t show up in the list, click the Edit Emails link and you can add them to the list.
