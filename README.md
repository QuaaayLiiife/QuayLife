# Getting Started

ThousandEyes is a network intelligence SaaS platform that allows users to run a variety of tests using global vantage points to monitor DNS resolution, browser response characteristics, detailed aspects of network pathing and connectivity, the status of network routing, and VoIP streaming connection quality.

This article provides an entry exercise for new users to get up and running with ThousandEyes, and to create their first test.

This exercise requires a ThousandEyes account with basic test creation permissions. If you have a user account, but do not have the required permissions, you can reach out to your ThousandEyes admin user for assistance. If you don't have a user account, or if you are unable to add test creation permissions to your existing account, you can create a trial account here:

[Sign up for a ThousandEyes Trial](https://www.thousandeyes.com/signup)

.

### Log in to the ThousandEyes Application <a href="#log-in-to-the-thousandeyes-application" id="log-in-to-the-thousandeyes-application"></a>

The default landing page in the ThousandEyes application is the **Views** page. If you are a new user, the app opens an onboarding wizard to walk you through the first steps. The wizard offers a smooth path to getting started with ThousandEyes. Choose a template to start monitoring one of the applications you use.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-37e65781623565fdbfa017164a8553bdb0c0b0d9%2Fgetting-started-plg-wizard-1.png?alt=media)

When the wizard finishes and you see **Setup completed successfully**, the UI is now populated with the results of your setup.

1.  1\.

    Click through the steps of the page tour.

    Explore the key elements of the **Views** screen:
2.  2\.

    On the **Dashboards** screen, click the selector and choose **Service Health Dashboard TEMPLATE**.
3.  3\.

    On the **Alert Rules** screen, check out the default
4.  4\.

    On the **Test Settings** screen, you'll see the results of the tests that the wizard configured for you.

    The default page load test includes information from lower-layer tests: HTTP server, agent-to-server, and BGP tests. For more information about these test types, see

The left-hand panel provides links to the key locations in the application:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-fdfb9e1d7e2e7030f5e901f7febaaaf4ed1fa945%2Fproduct-documentation\_getting-started\_readme-3.png?alt=media)

*   ​

    [Cloud and Enterprise Agents](https://docs.thousandeyes.com/product-documentation/global-vantage-points)

    allows you to manage all of your Cloud and Enterprise Agent settings, test settings, BGP monitors, and deep dive into the various data views available.
*   ​

    [Endpoint Agents](https://docs.thousandeyes.com/product-documentation/global-vantage-points/endpoint-agents)

    allows you to manage your end-user vantage points, configure test and agent settings, and review data.
*   ​

    [Devices](https://docs.thousandeyes.com/product-documentation/device-layer)

    allows users to configure monitoring of network devices, such as routers, switches, and access points.
*   ​

    [Internet Insights](https://docs.thousandeyes.com/product-documentation/internet-insights)

    is our collective intelligence product, that provides visibility into core Internet infrastructure and traces the impact of macro scale Internet events to individual users and enterprise networks at their edge devices.
*   ​

    [Dashboards](https://docs.thousandeyes.com/product-documentation/dashboards-and-reports/working-with-the-dashboard)

    is the default landing page for the ThousandEyes application. Use widgets to build out custom dashboards to show you exactly what you want to see, to ensure you have visibility into key infrastructure areas.
*   ​

    [Alerts](https://docs.thousandeyes.com/product-documentation/alerts/how-alerts-work)

    allows you to create and manage alert rules, suppression windows, and look through the list of active and historical alert events.
*   ​

    [Reports](https://docs.thousandeyes.com/product-documentation/dashboards-and-reports/)

    directs you to the main reports page, where you can navigate between pre-built or custom reports, and review historical reports.
*   ​

    [Sharing](https://docs.thousandeyes.com/product-documentation/tests/sharing-test-data)

    lets you share test data with users in other account groups, or outside of your organization.
*   ​

    [Account Settings](https://docs.thousandeyes.com/product-documentation/user-management/rbac/working-with-account-settings)

    is where you configure your user permissions, organization settings, and billing.

For assistance, use the question mark icon on the top navigation bar to access the help menu:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-76183122a1b06e5bd4c615e349ab1f5cf6b19ae7%2Fproduct-documentation\_getting-started\_readme-8.png?alt=media)

The help menu includes optimized links to the product documentation, develop reference material for API support, and page tours, as well as links to contact or chat with the ThousandEyes Customer Support team.

ThousandEyes provides several different test types that can be used for monitoring different parts of your network:

*   ​

    [BGP tests](https://docs.thousandeyes.com/product-documentation/tests/guide-to-thousandeyes-test-types#bgp-test)

    monitor the BGP routing layer, providing data on public and private BGP monitors.
*   ​

    [Agent-to-agent](https://docs.thousandeyes.com/product-documentation/tests/guide-to-thousandeyes-test-types#agent-to-agent-test)

    tests monitors the performance of the underlying network between two physical sites, using ThousandEyes vantage points at each location.
*   ​

    [Agent-to-server](https://docs.thousandeyes.com/product-documentation/tests/guide-to-thousandeyes-test-types#agent-to-server-test)

    tests measure network performance from a ThousandEyes vantage point to a remote server.
*   ​

    [DNS server](https://docs.thousandeyes.com/product-documentation/tests/guide-to-thousandeyes-test-types#dns-server-test)

    tests provide DNS record validation and service performance metrics.
*   ​

    [DNS trace](https://docs.thousandeyes.com/product-documentation/tests/guide-to-thousandeyes-test-types#dns-trace-test)

    tests verify delegations from parent zones to child zones.
*   ​

    [DNSSEC](https://docs.thousandeyes.com/product-documentation/tests/guide-to-thousandeyes-test-types#dnssec-test)

    tests verify the digital signature of DNS resource records.
*   ​

    [DNS+ domain](https://docs.thousandeyes.com/product-documentation/tests/guide-to-thousandeyes-test-types#dns-domain-test)

    tests provide metrics on DNS availability by querying open DNS resolvers.
*   ​

    [DNS+ server latency](https://docs.thousandeyes.com/product-documentation/tests/guide-to-thousandeyes-test-types#dns-server-latency-test)

    tests measure the total time taken to resolve a configured DNS record through authoratative name servers from ThousandEyes vantage points.
*   ​

    [HTTP server](https://docs.thousandeyes.com/product-documentation/tests/guide-to-thousandeyes-test-types#http-server-test)

    tests measure the availability and performance of an HTTP service.
*   ​

    [Page load](https://docs.thousandeyes.com/product-documentation/tests/guide-to-thousandeyes-test-types#page-load-test)

    tests monitor in-browser site performance metrics.
*   ​

    [Transaction](https://docs.thousandeyes.com/product-documentation/tests/guide-to-thousandeyes-test-types#transaction-test)

    tests emulate user interactions with a website to test performance.
*   ​

    [FTP server](https://docs.thousandeyes.com/product-documentation/tests/guide-to-thousandeyes-test-types#ftp-server-test)

    tests provide performance metrics on an FTP server.
*   ​

    [SIP server](https://docs.thousandeyes.com/product-documentation/tests/guide-to-thousandeyes-test-types#sip-server-test)

    tests check the availability of SIP VoIP servers.
*   ​

    [RTP stream](https://docs.thousandeyes.com/product-documentation/tests/guide-to-thousandeyes-test-types#rtp-stream-test)

    tests measure the quality of real-time protocol (RTP) voice streams between ThousandEyes vantage points acting as VoIP user agents.

Each test type produces a set of results and views based on the layers of data it interacts with. For example, an HTTP server test also includes network and routing data and views. The layers that a test type will interact with are referred to as **test nests**, and can be seen in the image below:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-595d7dcb2b084404032cfd2055024f6e9c608cb4%2Fproduct-documentation\_getting-started\_readme-7.png?alt=media)

For this example, an HTTP server test is the best test to configure. Follow the steps below to create the test:

1.  1\.

    In the left hand navigation panel, go to **Cloud and Enterprise Agents > Test Settings**, and click **Add New Test**.

    ![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-81a9c62036b5930fcfcf14932c71e1e5d814d7ac%2Fproduct-documentation\_getting-started\_readme-2-2.png?alt=media)
2.  2\.

    By default, the **Layer** field is set to **Web**, and the **Test Type** is set to **HTTP Server**. This exercise will use both these settings, so leave them as is.

For future test creation, the tests listed earlier in this document are broken into different layers, and can be found by navigating through the layer options.

1.  3\.

    **Optional**: Name the test. The test name should allow for easy identification / searching, and be unique where possible.

If no test name is added, the default name will be the URL provided in step four.

1.  4\.

    **Optional**: Provide a test description.

    This field is best used for a summary description to allow other users to quickly differentiate between similar tests.
2.  6\.

    ThousandEyes vantage points are lightweight Linux-based software agents that allow users to run a variety of layered monitoring tests. These vantage points can be divided into three types:

    * **Cloud Agents** are globally distributed vantage points deployed on servers maintained by ThousandEyes that all customers can use.
    * **Enterprise Agents** are vantage points deployed locally by customers in data centers, branch offices etc.
    * **Endpoint Agents** are vantage points deployed on end-user workstations.

    In this exercise, we will use Cloud Agents, as they provide the least friction to getting tests up and running. Open the **Agents** drop-down menu to select the vantage points to use for this test.

    Vantage points are grouped by region, and can be searched for using the search bar, or filtered by the built-in labels on the right hand side. For this exercise, we will use the following vantage points:

    * Cape Town, South Africa (Africa)
    * Seoul, South Korea (Asia)
    * Louisville, Kentucky (North America)
    * Brisbane, Australia (Oceania)
    * Rio de Janeiro, Brazil (South America)

    ![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-7f9c4e444a33014779f90ac20df6591a9ed84e0b%2Fproduct-documentation\_getting-started\_readme-4.png?alt=media)
3.  7\.

    For this test, we will leave the remaining settings as the default:

    * The **Interval** drop-down menu sets the cadence for how often the test should run.
    * The **Alerts** drop-down menu allows you to configure when the test should trigger notifications to users.
    * The **Advanced Settings** tab provides additional configuration options for the test.
4.  8\.

    The configured test should now look something like this:

    ![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-b424da04744ff20a34cfa48229b075f48332b348%2Fproduct-documentation\_getting-started\_readme-5-2.png?alt=media)

    To check that the test is configured correctly, you can click **Run Once** to run an instant test.

    Instant tests can be run to validate configuration or to troubleshoot issues immediately, rather than waiting for the next round of the scheduled test. The test will open in a new tab in the browser.
5.  9\.

    If you ran an instant test, close the tab and return to the test creation tab.
6.  10\.

    Click **Create New Test** to save the test configuration.

Now that the test is created, we can start reviewing the results as they come in.

You can navigate to the test results via one of two ways:

*   From the **Test Settings** page, click the stack icon (

    ![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-996b7cca3f6463f78ec03a581679c985a02964d3%2Fproduct-documentation\_getting-started\_readme-9.png?alt=media)

    ) beside the test type for the relevant test.
* In the left-hand navigation panel, navigate to **Cloud and Enterprise Agents -> Views**. Open the **Current Test** drop-down box in the top corner, and select the created test from the list.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-eaeed692678c2f533a7ddcf447389cf1fa7a241b%2Fproduct-documentation\_getting-started\_readme-6.png?alt=media)

The **Views** page provides a detailed look at a singular test, and all of the available data within it. In the top left, a drop-down menu displays the current test. In this example, only one test has been configured, so the current test will be the one configured above. When more tests have been configured, this drop-down can be used to navigate between the tests.

Beneath the drop-down menu is the main panel. On the left hand side, the various test views are listed, grouped by the appropriate layer. For this example test, the **HTTP Server** view is displayed, while the **Network Overview**, **Path Visualization**, and **BGP Route Visualization** views are also available:

*   The **Path Visualization** view allows you to visualize the path trace data between vantage points and target locations to identify problem areas in both the private and public network infrastructure. For more information, see

    [Using the Path Visualization View](https://docs.thousandeyes.com/product-documentation/thousandeyes-basics/using-the-path-visualization-view)

    .
*   The **BGP Route Visualization** view allows you to visualize how data is being routed across the internet, and troubleshoot issues that may be preventing packets from getting to their desired destination. See

    [Using the BGP Route Visualization View](https://docs.thousandeyes.com/product-documentation/thousandeyes-basics/using-the-bgp-route-visualization-view)

    .

On the right-hand side, the panel shows the primary view: the timeline. The timeline shows all the data collected over each test round, and updates as new test rounds complete. Sections of the timeline can be highlighted to focus on specific moments in time, allowing for deeper dives into the data to identify issues.

As a user moves across layers within or across tests, the timeline selection is preserved to aid the correlation of data.

Beneath the main panel, the secondary panel shows additional data about the tests run by each of the agents assigned to the test, broken into a series of tabs. The **HTTP Server** view has two tabs in the secondary panel:

* The **Map** tab displays the global position of each of the vantage points used for the test.
* The **Table** tab provides a more detailed collection of information about each of the agents.

Both the main panel and the secondary panel will update based on data selected in the other panel. For example, selecting the Munich, Germany agent on the map will update the timeline to only show data from that agent. The agent will remain selected when navigating to the **Table** tab, and will be highlighted in the table, until the user clicks away from, or changes, the selection.

Now that you have a working test, and are getting a feel for navigating the product, you can start diving into the more advanced options available. In order to operationalize ThousandEyes within your environment, we recommend the following:

*   Set up alerts based on your monitoring needs. Alerts can be fine-tuned based on the metrics that are important to your environment, and notifications can be sent directly through email, webhook, PagerDuty, Slack, and AppDynamics. For more information, see

    [How Alerts Work](https://docs.thousandeyes.com/product-documentation/alerts/how-alerts-work)

    .
