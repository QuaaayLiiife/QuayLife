# New User FAQ

This Frequently Asked Questions document is meant to help answer general questions about the ThousandEyes platform and how to access it. Most answers are linked to other articles within the ThousandEyes documentation. If this article answers one of your questions, we encourage you to peruse other questions here to further your introduction.

*   ​

    [ThousandEyes](https://www.thousandeyes.com/)

    is a SaaS platform that allows you to run various tests to a target using various agents. Tests are created to track metrics that can be monitored using customizable Alert Rules which appear in the platform. Users can set up notification in these Alert Rules using email or some other form of integrated communication method.
* The ThousandEyes platform monitors DNS resolution, browser response characteristics, detailed aspects of network pathing and connectivity, the status of network routing, and VoIP streaming connection quality.
* Information about these different aspects of a network are portrayed in test results constructed from data collected by custom servers referred to as ThousandEyes agents. The agents examine a test target using methods developed by ThousandEyes which can be run as one-time only statistics or sampled over multiple intervals specified in customizable test configurations.
* Data collected can be reported to a Dashboard or in other forms to provide a comprehensive umbrella of intelligence about various areas of hybrid cloud and private networks. Network paths are represented in a Path Visualization that maps the route of your traffic. This map gives you detail analogous to a street view on a physical map and describes the characteristics of the nodes on each path.

**That’s great, but how do I use ThousandEyes?**

* Once you are logged in, you can create tests, work with agents and set up alerting or other reporting mechanisms.
* If your organization already has an account, contact your organization admin to add your user profile.

One quick way to begin is to construct a web test. To do this, you need access to the ThousandEyes Platform. When you click **+ Add New Test** in your account workspace, the selection defaults to a web HTTP server test.

**Why can’t I create a test?**

Certain users have permissions to use parts of the platforms. There are cases where users are given access to the platform to run a test prepared by an administrative level user. To have your permissions and Role reviewed communicate with the administrator of your ThousandEyes account

**How do I reset my password for the ThousandEyes platform?**

* Select **Forget password?**, and an email will be sent to the email address you used to log in to the platform.
* You will receive an email with the subject header "Password Reset". In some instances, this email may go to your spam folder, so look for it there if it does not appear to be sent before contacting support.
*   Our security standards require that the frequency of each password reset be every 24 hours. If for some reason a reset is required within a 24-hour window, contact ThousandEyes Support at this email address:

    \[email protected]

    .

**I forgot to activate my account and now the link activation expired. What are the steps to activate?**

*   If you are not listed in the platform, you may need to contact your ThousandEyes Account Admin and have them re-add your account. Otherwise, contact

    \[email protected]

    .

**I didn’t receive my password reset email.**

*   Before checking with

    \[email protected]

    , you may be able to find the password reset email in your spam folder. Look for an email with the subject header "Password Reset". There are times when this may occur. For more assistance, contact ThousandEyes Support.

**How do I delete my trial account before the 14-day trial?**

1.  1\.

    Log in to the ThousandEyes platform.
2.  3\.

    Under the **Organization Deletion** section, click **Delete**.

**How do I create my own agent?**

* You can deploy your own agent on hosts that you control.
* Agent deployment options are listed in a horizontal button menu.
* Each package type has its own corresponding installation steps, listed under an "Installation Guide" or listed as scripted commands. Three package type deployments that can get you started quickly are Appliance, Linux Package or Docker Agents. The three links below describe each of these in detail and give you the ability to deploy an agent as a host in Virtual Box, install the agent on a Linux server, or use Digital Ocean's solution to set up an agent as a Docker container.

**What operating systems are supported for Enterprise Agent deployments?**

* An _agent_ is a Linux server, running custom ThousandEyes software, that checks in with an agent collector to obtain instructions from the ThousandEyes platform. There are several types of agents to be aware of when using the platform.
* Enterprise Agents can be deployed by users of the platform to run tests.
* Cloud Agents are also be used for testing and are available for use by all customers from tier 2 and tier 3 data centers around the world.
* Another type of agent ThousandEyes employs is called an Endpoint agent which collects data about web browsing performance and network connectivity. Endpoint agents are installed on user workstations to obtain real-time User Experience metrics.
* To learn more about agents start in the documentation:

**There may be restrictions on using Cloud agents from outside my network. Is there a list of IP addresses I can access?**

*   Customers may need the IP addresses of ThousandEyes agents in order to construct firewall rules or similar filters. The ThousandEyes application program interface (API) provides the IP addresses of both Cloud Agents assigned to your organization and Enterprise Agents assigned to your account group. To query the ThousandEyes API use wget, cURL, a programming language which supports using RESTful APIs, or through a RESTful API client, such as

    [Postman](https://www.getpostman.com/)

    . For more information about the API:

**How do I decide what tests to use?**

* ThousandEyes tests various layers, including Web, DNS, Network, Routing and Voice. Within these layers are various test types.
* Different test types look at various parts of the online experience. Be aware that some tests referred to in this article might only available to specific types of account plans; all may not be visible.

**Where can I get an account group token?**

* The account group token is used to establish a unique connection with your Enterprise Agent and any specific account groups that a specific account user has on the ThousandEyes platform.

**How can I view the result of a test?**

* This area of the UI lists different test configurations. To view the results, click the stack icon in the 2nd column of the listing with the heading “Test Type”.
* Depending on whether the test is enabled or not, you will see data. A test is enabled if the checkbox under the "Enabled" column of a test listing is checked.
* If you want to see the result of a particular test that is not enabled, you can also run it once by clicking the name of the test and opening its details. The **Run Once** button at the bottom of the test detail lets you run one round of sampling. Enabling a test allows repeated sampling, depending on the "Interval" setting in the configuration detail. If, for example, a test has an interval set for 30 minutes in the basic Settings tab, clicking the "Enable" box will begin running the test every half hour. To understand tests in general, see the next FAQ entry on tests below.
*   To look at test results it is a good idea to be able to navigate the

    [View layouts](https://docs.thousandeyes.com/product-documentation/internet-and-wan-monitoring/viewing-data/)

    ​
*   To understand what metrics are being looked at look here, see

    [this article](https://docs.thousandeyes.com/product-documentation/internet-and-wan-monitoring/tests/thousandeyes-metrics-what-do-your-results-mean)

    .
* If you wish to test HTTP resource availability activity, choose a web test. With web-based tests, you can see if a web server is responding, what HTTP response codes are being passed, and whether the root object that you are browsing is reachable. For a more detailed view of what you are browsing, a web page load test shows the waterfall of elements that are reachable and the time it takes for each one to be received. It also shows errors related to individual components of the load. If there is a browsing action that has multiple steps, the best way to test this is with a web transaction test. The FTP server test tests access to an FTP site.
* Select the **Web** layer, then select the Web Test Type, URL, Interval to run your test at when it is Enabled, and Agents.
* If this is your first time creating a test, deselect the Alert Enable Box. Check further down in the FAQ on how to configure alerts. In the meantime, focus on creating a test.
* Create a new test by clicking **Create New Test**.

**What is a Web Transaction Test?**

* As mentioned in the previous answer, if there is a browsing action that has multiple steps, the best way to test this using ThousandEyes is with a Web Transaction test. If, for example, you want to check if a user can log in to a site and search for an item, the Transaction test can be used to build a predefined script.
* Transaction tests are powered by Selenium WebDriver to control the Chromium browser.
* If you are new to transaction testing or Selenium in general, you can build your first transaction using the ThousandEyes Recorder, where you walk the recorder through the steps. This is similar to building a Macro as you might in Microsoft Word. After you complete the steps, they can be imported into the test from the ThousandEyes Recorder.
* DNS tests provide the option to test resolution to a particular domain name server.
* DNS Server tests run queries against target servers.
* DNS Trace tests run queries against target DNS resource records.
* The DNSSEC Trace test measures worldwide validation of the keychain for the target DNS record from the bottom up. A DNSSEC query has a binary response.
* Set up a DNS server test by navigating to
  1.  3\.

      Select "DNS" in the layer category, then select the DNS test type, Domain, Interval to run your test, Agent and click **Look up Servers**. If this is your first time creating a test, deselect the Alert Enable box and create a new test.

**What does a network test accomplish?**

* Network testing looks at the state of a path from source to target IP. Network tests also measure networking from source to target then back using agents at the source and target location. The significant details of how data is gathered can be compared as follows:
  * Agent-to-Server Testing - ICMP based measurement: 50 ICMP echo request packets are sent out from the source agent to a Target IP. Data in the Echo reply responses to these requests is compared to produce latency and jitter metrics reported in the test result.
  * Agent-to-Server Testing - TCP based measurement: 50 TCP SYN packets are sent out from the source agent to a target agent. Data in the acknowledging SYN+ACK responses to these SYN requests are compared to produce metrics.
  * Agent-to-Agent Testing - TCP based measurement: These are made similar to Agent-to-Server tests with the addition of an initial Clock Synchronization benchmark measurement prior to the 50 probe packets being sent.
  * Agent-to-Agent Testing - UDP based measurement: This option differs from the A2A TCP option in how the Clock offset measurement is made
* In doing this a network test accomplishes the task of understanding the state of traffic from a source agent to some destination. The destination can be an IP address or if the path is being measured out to a target and back to the source agent, a second agent is used as a destination to enhance the accuracy of the measurement reported in the test result.
* The BGP Routing test shows routes between Autonomous Systems (ASNs) in a network.
* BGP Monitoring tracks routing changes, reachability, and updates. Discover local misconfigurations, peering changes, and route hijacks in the event those arise as well as understand routing between offices, data centers, and Cloud providers.
* BGP tests help identify networks most likely to contain the root cause of a routing issue using the BGP Visualization. Data on unreachable prefixes is collected and used to measure reachability.
* ThousandEyes monitors BGP network routes from both corporate and service provider networks, enabling you to act quickly on BGP local misconfigurations, peering changes and route hijackings.
* Private BGP routing monitors can also be used to discover routes from your enterprise network to prefixes that you originate or external applications and services. Newly announced and withdrawn routes are represented by red lines and dotted lines respectively in the visualization.
* To create a Routing Test, follow these steps:
  1.  3\.

      Select "Routing" in the layer category, then select the BGP test type, Name your test, Enter the Prefix and Monitors
* A Voice test looks at Voice over IP (VoIP) call quality and availability. Voice packets are sent as a continuous stream of evenly spaced packets. However, depending on the network path congestion a packet can take any path available which may be different from the other voice packets. As a result, packets may arrive at the destination at variable time and thus out of order. When you create a Voice test you have several options:
  1.  1\.

      You can test the handshake for a call using the SIP Server test. SIP stands for Session Initiation Protocol which is the signaling protocol for initiating, maintaining, and closing voice, video, and messaging application session.
  2.  2\.

      The Protocol for delivering audio and video over IP networks is called RTP. Real-Time Transport Protocol Stream tests can also be tested for.

**What is the difference between an Instant Test and Scheduled Test?**

* When a test is enabled it will use constituent agents selected to gather a test result at the intervals specified in a test configuration. The interval set in a test configuration is what schedules the data collection in a scheduled test result. An Instant test runs a test configuration once to troubleshoot problems without waiting for a scheduled test, or to validate a new test's configuration. In a test configuration the "Run Once" Button will start data collection of an Instant test and open the results in a new browser tab. Scheduled test results are viewed by clicking the layer icon which appears next to the Test Type in the short listing of the test.

**When I create a test, I noticed the resulting views are similar to other test results.**

* Yes, when you create any test that has a network measurement: Network, HTTP Server (with network measurements enabled), Page Load (with network measurements enabled), or DNS server (with network measurements enabled), you can usually see a BGP Route Visualization view. You can also see Path Visualization. Many views within ThousandEyes have similar layouts for that reason.

**Are there other ways to list tests, agents other than inside the platform?**

*   Yes, users can access their ThousandEyes data using the API. Run command-line tools to get JSON or XML output from our REST API endpoint. For a detailed cookbook with request examples, see the

    [ThousandEyes Developer site](https://developer.thousandeyes.com/)

    ​

**Can I recover a deleted test?**

* Yes, within 14 days a deleted test can be recovered from the test listing under **Cloud & Enterprise Agents > Test Settings > Tests**. On the right-hand side of the test listing, there is a trash can icon. Next to that the number of deleted tests is listed. Clicking those words opens a link to a recovery window listing deleted tests.

**Why can't a target for a test be edited after a test is created? I may want to correct or change it.**

* The reason the target in an existing test cannot be edited is to preserve data collected for each distinct target. If a test target was editable this would put two separate data sets into a single result. Making this into a new feature would mean an older result for a different target would be placed alongside data that is intrinsically unique from a result collected for either one that is mistyped or updated.
* Making this a feature would affect the integrity of any historical test results because the objects being tested don't match exactly. Different targets yield different results so they are kept separate with that intention in mind. Everything but the target in the test can be changed after a test is set up. That is why the only option for correcting or changing a test's target is to duplicate the configuration, keep what is there, then retype the target text.

**Some agents are reporting DNS resolution errors in my Web HTTP Test but I don't see errors on our DNS server.**

* Web HTTP testing performs several steps while validating browser response starting with DNS resolution. After that the test checks establishment of a 3 way TCP handshake to Connect, potentially negotiation of SSL, Sending the HTTP request, Receiving the HTTP Response and Verify and Validating the received response. During HTTP testing, Enterprise Agents will query the DNS server specified in the "/etc/resolv.conf" file. The DNS resolution test result is based on the local maps of each agent you have in a test so the resulting errors may vary from source to source shown in the Table view of your HTTP Server test result View. Comparatively, DNS Server tests will directly query a server specified in the test target (See the "DNS Servers" Field). DNS Trace tests query authoritative nameservers for each zone of the domain space starting at the root then at the Top-Level Domain (TLD) and so on until an authoritative answer is received. Common TLDs are familiar domains like .com, .net, .org, and so on.
* To learn more about the DNS Server and DNS Domain Trace views, see these articles:

**How do I configure alerts?**

**How often does a BGP Alert Condition clear?**

* BGP monitoring updates every 15 minutes.
*   ThousandEyes keeps every prefix that triggers an alert in its system for 7 days. The alert can be suppressed with an option to remove certain prefixes that would trip alerting. To suppress alerting during a maintenance period, see

    [Alert Suppression Windows](https://docs.thousandeyes.com/product-documentation/alerts/alert-suppression-windows)

    ​

**What form of notifications and integrated communications can be leveraged using alerts?**

* Alert Rules can be set up to notify you by email. This is done in the Notifications tab of an alert rule configuration dialog. Another form of notification is a webhook which makes an HTTP request (typically a POST) that will deliver data to an application. Webhooks are configured with a Name, URL, and can also contain a type of Authentication such as with a username/password, Token, or OAuth URL/Client ID credentials. Integrations can currently be configured to work with AppDynamics, Slack, PagerDuty, and ServiceNow.

**What is an Endpoint Agent?**

* The Endpoint Agent collects data about web browsing performance and network connectivity typically from a specific host. For more information about Endpoint Agents and Endpoint views, see these articles:

**How do I set up Endpoint Data collection?**

**After setting it up, where can I view Endpoint Agent Data?**

*   Endpoint Data can be browsed in the platform UI by selecting **Views > Endpoint Data**. There are several views within this area: Scheduled Test, Web, Network, Session Details, and Network Topology.

    [This article](https://docs.thousandeyes.com/product-documentation/global-vantage-points/endpoint-agents/data-collected-by-endpoint-agent)

    covers the data collected by the ThousandEyes Endpoint Agent.
* A more detailed view of Endpoint Agent Views are available in these articles:

**How does unit consumption work? How much does running a test cost?**

* ThousandEyes bills for scheduled tests and Instant Tests based on whether the test is run from a Cloud Agent or an Enterprise Agent. For agent-to-agent tests, ThousandEyes bills based on whether the target agent is a Cloud Agent or an Enterprise Agent. Any test run from or to a Cloud Agent will incur a cost in Units. When a test is run, the test's cost is deducted from the monthly Units purchased by the customer's organization, as specified in the customer's contract. Each month the account is reset to the number of Units that was contracted by the customer's organization.

**How do I deploy an Enterprise Agent behind a firewall?**

* When setting up an Enterprise agent behind a firewall, there are additional configurations that need to be done. Firewall rules must be set up to allow the agents to transmit and receive data with the ThousandEyes platform. Agents communicate with the platform using specific ports, so these must be whitelisted on the firewall. Articles related to this, and other items to consider in an agent networking configuration, are here:

**Can user logins be restricted to use SSO only?**

* Account users with the proper permissions can restrict logins via Single Sign-On or the ThousandEyes login page. These options are found in the Role-based Permissions Control Page. To find this page Navigate to the User icon on the upper right side of the platform browser view.
  1.  1\.

      Under the user icon, click **Account Settings**.
  2.  2\.

      Click the **Roles** tab. A listing appears in the Role-based Permission Control box.
  3.  3\.

      Under the label **All Permissions**, enter text to focus the listing by entering "login"
  4.  4\.

      Two permissions will be shown. Choose **Login via Single Sign-On** to allow this action.
  5.  5\.

      Uncheck **Login via ThousandEyes login page**.
*   To learn more about role-based access control, see

    [this article](https://docs.thousandeyes.com/product-documentation/user-management/rbac/role-based-access-control-explained)

    ​

**When I log in now, I get the following message:** _**Cannot Login Interactively**_ **What does this mean**?\*\*

*   That message means that your user profile does not have permissions to login interactively with email and password. You will need to login from the ThousandEyes SSO login page at

    [https://app.thousandeyes.com/login/sso](https://app.thousandeyes.com/login/sso)

    .
*   You can also add the "Login via ThousandEyes login page" permission to your user to login interactively. See

    [this article](https://docs.thousandeyes.com/product-documentation/user-management/rbac/role-based-access-control-explained)

    .

**An HTTP test is reporting a result with a 400 error code "Invalid Upgrade Request" in the HTTP Server View of the result. The link in the response code column of the table reads: "Connection: Upgrade. HTTP2-Settings; Upgrade: h2c". The target site is accessible via browser. What is going on?**

*   Changing the version of the HTTP request in the advanced settings tab of your HTTP server to "Prefer HTTP/2" will most likely remove this error from your test result. The reason is that the target URL may not support HTTP/2. Contact

    \[email protected]

    if you require additional assistance.

**A test result is reporting a 403 error. What might be the cause?**

* In general, 403 represents an HTTP status code that means the client does not have access to the target URL relating to some security issue. The client is not authorized to access the target URL. This could be for a number of reasons but two common examples could involve either requiring a valid client certificate or a restriction on the IP address for the source. In the case of the client certificate, check the text configuration for a client certificate. For a situation where there is an IP restriction, check if the agent being used in the test has an IP address that needs to be whitelisted.
*   Contact

    \[email protected]

    if you require additional assistance, or see the following articles for details on these circumstances.
