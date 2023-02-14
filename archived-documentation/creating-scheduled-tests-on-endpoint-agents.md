# Creating Scheduled Tests on Endpoint Agents

Endpoint Tests are tests run from

[Endpoint Agents](https://docs.thousandeyes.com/product-documentation/global-vantage-points/endpoint-agents/endpoint-agent-faq)

at regularly scheduled intervals. Customers can create HTTP Server tests and Agent-to-server tests. These tests run without user interaction, and run as long as an Endpoint Agent is online, providing data from remote workers, home workers and smaller branch offices.

This article provides information on creating and running Endpoint Tests, including the dynamic assignment of tests to Endpoint Agents. Unlike

[Cloud and Enterprise Agents](https://docs.thousandeyes.com/product-documentation/global-vantage-points#comparison-of-agent-types)

, Endpoints Agents are not typically online at all times. To address this issue and maximize the amount of data, test assignment to specific Endpoint Agents is dynamic.

The only prerequisite for running scheduled tests on an Endpoint Agent is the Endpoint Agent software version must be 0.96 or later. Versions prior to 0.96 will not be able to run scheduled tests.

In contrast to the

[original mode of Endpoint Agent operation](https://docs.thousandeyes.com/product-documentation/global-vantage-points/endpoint-agents/how-does-the-endpoint-agent-work)

where data collection is triggered by a user browsing with Chrome or Internet Explorer, scheduled Endpoint Tests do not require the browser extension for Endpoint Agent to be installed.

Creating a scheduled Endpoint Agent test consists of the following steps:

* Choose which Endpoint Agents, and how many, should perform the test
* Create a Label which includes the desired Endpoint Agents
* Assign the Label to your test and specify the maximum number of agents that may perform the test concurrently
* Select the test type, target, and interval
* Review advanced settings prior to completion

### Dynamic Agent Assignment Using Labels <a href="#dynamic-agent-assignment-using-labels" id="dynamic-agent-assignment-using-labels"></a>

In contrast to tests running on Cloud or Enterprise Agents where tests are assigned to agents statically, a scheduled Endpoint Agent test is assigned to Endpoint Agents using an Endpoint Label whose filter criteria match the Endpoint Agents.

Because Endpoint Agents are deployed on workstations that may frequently be offline, and because the network address, location and other characteristics of the host can change, test assignment is performed dynamically. Whenever an Endpoint Agent checks in with ThousandEyes, the criteria of each Endpoint Agent label are compared to the agent's information, such as network and geographic location. If the agent matches a label, any test configured with that label is assigned to the agent, up to a maximum of 10 tests.

If an Endpoint Agent does not check in for an hour, the agent is deemed offline, and the label assignment is removed. When the Endpoint Agent next successfully checks in, the label is re-assigned based on the configured filters.

When scheduled tests are assigned to execution slots, tests with a label that matches specifically to an agent are prioritized ahead of all other tests.

To create a new Endpoint Agent Label, head to the

[Agent Labels](https://app.thousandeyes.com/endpoint/agent-settings/?section=labels)

tab, under the Agent Settings page, and click on the **Add New Label** button:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-86fefc84c8611168f332dd7dbad233843a93b3bf%2Fproduct-documentation\_endpoint-agent\_creating-scheduled-tests-on-endpoint-agents-1.png?alt=media)

The new Endpoint Agent Label creation dialog will appear:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-51f0d355a2bdebead730d0d0f7f5bfc8b13f00c4%2Fproduct-documentation\_endpoint-agent\_creating-scheduled-tests-on-endpoint-agents-2.png?alt=media)

Enter the **Label Name** (1), select the **Label Color** (2) and use the **Filter** (3) setting to select the criteria that will determine which Endpoint Agents run a test with this Label. If multiple filters are selected, the Endpoint Agent must match all criteria (logical AND) in order to be assigned this Label.

On the right side of the dialog, there is an graph showing the number of Endpoint Agents matching the filter criteria in the last 24 hours (4). The graph can be refreshed with a click (5). Once you're satisfied with the Label configuration, click on the **Add New Label** button (6) to complete the Label creation process.

Once the Endpoint Agent Label has been configured, proceed to the test creation.

### Creating a Scheduled Test <a href="#creating-a-scheduled-test" id="creating-a-scheduled-test"></a>

(If you have not prepared your Endpoint Agent Label(s) yet, consult the section above on how to do that first. Once done, continue with scheduled Endpoint test creation here.)

Head to

[Endpoint Tests](https://app.thousandeyes.com/endpoint/test-settings/?tab=tests)

tab under the Test Settings page, and click the **Create New Test** button:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-9c567fc6772cbe761bd96e1b90f650d58e033333%2Fproduct-documentation\_endpoint-agent\_creating-scheduled-tests-on-endpoint-agents-3.png?alt=media)

Currently, two test types are available:

* Agent-to-server (Network Layer)

#### Creating an Agent-to-Server Test <a href="#creating-an-agent-to-server-test" id="creating-an-agent-to-server-test"></a>

In the scheduled Endpoint test creation dialog, choose **Network** layer (1) and **Agent to Server** test type (2):

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-5847098b044ca549d5f136bdea8c9dadc04d550e%2Fproduct-documentation\_endpoint-agent\_creating-scheduled-tests-on-endpoint-agents-4.png?alt=media)

In the **Basic Configuration** tab, the following configuration settings are available:

* **Test Name** (3): This optional parameter gives the test a name. When no name is provided, then the value from the Target field will be used as a test name.
* **Target** (4): Domain name or IP address
* **Protocol** (5): ICMP is currently the only available option.
* **TCP Connect** (6): Opens a TCP connection with a 10 second timeout and closes the connection if it was able to connect. Unsuccessful connections will count towards the TCP Connection Failures metric.
* **Interval** (7): How frequently this test will be run.
* **Agent Label** (8): Endpoint tests are dynamically assigned to Endpoint Agents through Labels. The helper graph (11) below indicates how many agents matching the Label were available throughout the last 24 hours. See the section on Label configuration above for details.
* **Alerts** (9): Select which alert rules will be enabled for the test by selecting them from the list in the drop-down. The Edit Alert Rules link allows you to create, modify and delete alert rules.
* **Max No. of Agents** (10): Specifies the maximum of agents within the Agent Label to run the test from.

Once you are satisfied with your test configuration, click on the **Create New Test** button (12) to complete the scheduled Endpoint test creation process. To see and understand the results, consult the "Viewing Results" section below.

#### Creating an HTTP Server Test <a href="#creating-an-http-server-test" id="creating-an-http-server-test"></a>

In the scheduled endpoint test creation dialogue, choose **Web** layer (1) and **HTTP Server** test type (2) to start creating a new HTTP Server test:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-ccb465175f0766151e98b285c2fbeaadec04da30%2Fproduct-documentation\_endpoint-agent\_creating-scheduled-tests-on-endpoint-agents-5.png?alt=media)

In the **Basic Configuration** tab, the following configuration settings are available:

* **Test Name** (3): This optional parameter gives the test a name. Where no name is provided, the value in the URL field will be used as the test name, prepended with a protocol ("http://" by default).
* **URL** (4): A URL, domain name or IP address, including the TCP port. If a domain name or IP address is used (i.e. protocol specification is not provided) then "http://" protocol is assumed.
* **Protocol** (5): ICMP is currently the only available option.
* **TCP Connect** (6): Opens a TCP connection with a 10 second timeout and closes the connection if it was able to connect. Unsuccessful connections will count towards the TCP Connection Failures metric.
* **Interval** (7): How frequently this test will be run.
* **Agent Label** (8): Endpoint tests are dynamically assigned to Endpoint Agents through Labels. The helper graph (12) below indicates how many agents matching the Label were available throughout the last 24 hours. For details, see the section about Label configuration above.
* **Alerts** (9): Select which alert rules will be enabled for the test by selecting them from the list in the drop-down. The Edit Alert Rules link allows you to create, modify and delete alert rules.
* **Max No. of Agents** (11): Specifies the maximum of agents within the Agent Label to run the test from.

Once you are satisfied with your test configuration, click on the **Create New Test** button (13) to complete the scheduled Endpoint test creation process. To see and understand the results, consult the "Viewing Results" section below.

Additionally, in the **Advanced Configuration** tab (11), the following configuration settings are available:

* **HTTP Server Timing** section:
  * **Timeout**: Seconds until the test terminates due to an unresponsive target server.
  * **Target Time for View**: Sets the color legend on the global map, and the corresponding font colors for the agent results table. For example, Response Time for an HTTP Server test sets the range of the legend from 0 seconds (green end) to 2x the Target Time for View (red end).
*
  * **Data Collection**: Check the box to collection Network metrics and perform Path Visualization.
* **HTTP Authentication** section:
  * **Username**: The username for the account being accessed by the HTTP request(s).
  * **Password**: The password for the account being accessed by the HTTP request(s).
  * **Scheme**: HTTP Basic Authentication or NTLM
*
  * **Request Method**: Select the HTTP request method - either GET or POST. If POST is selected, you may specify data in the POST Body field. The default is GET.
  * **SSL Version**: Select the version of the SSL/TLS protocol to offer in the SSL/TLS Client Hello. This will set the maximum version of SSL/TLS that the connection can use, but a lower version may be negotiated by the server. The options are the following:
    * SSLv3: Use SSL version 3.0. No lower version can be negotiated.
    * TLSv1.0: The agent will start the TLS negotiation at version 1.0.
    * TLSv1.1: The agent will start the TLS negotiation at version 1.1.
    * TLSv1.2: The agent will start the TLS negotiation at version 1.2.
    * Auto: The agent will start the TLS negotiation at the highest version of TLS supported by its operating system.
  * **Verify SSL certificate**: By default, certificate-related errors will result in a test error. Uncheck this box to ignore certificate errors during SSL/TLS negotiation.
  * **Custom Headers**: Enter one or more HTTP header strings in the form "\<stringname>: \<value>" (without quotes). Note the whitespace between the literal colon character and the placeholder \<value>.
  * **Override DNS**: Instead of using standard DNS resolution, allows you to specify the IP address to which the target's domain name will resolve. Useful for targeting a specific server within a cluster, or when testing HTTPS URLs which require a Server Name Indication (SNI) in the SSL/TLS negotiation that is different from the domain name-to-IP address mapping required to access the URL.
*
  * **Desired Status Code**: Sets the HTTP status code returned by the server that is defined as a successful test (i.e. no errors will be displayed in the test table results, no response code-based alerts generated etc.). By default, either a 200-level or 300-level status code is considered a successful return code. Uncheck this box and enter a response code in the field below to use a different expected response code.
  * **Verify Content**: Search the HTTP headers and body for text which matches the expression in the Verify Content field. The expression can be a literal text or a POSIX regular expression. If no match occurs, the test shows an error condition.
  * **Limit Download Size**: Load only the first number of kilobytes (kB) specified in the field below the Enable box. The result is not guaranteed to be exactly the number specified but can be slightly more, yet always within a few percent, or less as the size of the download is increased. Note that this function does not use an HTTP Range header, so the HTTP response code should not be affected (i.e. success is a 200 OK response, not a 206 Partial Content response).

Once you are satisfied with your test configuration, click on the **Create New Test** button (12) to complete the scheduled endpoint HTTP server test creation process. To see and understand the results, consult the "Viewing Results" section below.

### Frequently Asked Questions <a href="#frequently-asked-questions" id="frequently-asked-questions"></a>

**For HTTP Server test (Web layer), which protocol is used to collect network metrics in the included Network layer?** ICMP is currently the only protocol available.

**For Agent-to-Server test (Network layer), which protocol is used to collect network metrics?** ICMP is currently the only protocol available.

**How many tests can run on one Endpoint Agent?** There is a limit of ten (10) scheduled tests per agent.

**When is the test assignment recalculated?** Scheduling/test assignment is done at the time of agent check-in.

**How frequently does the agent perform the check-in?** The agent checks in with the platform once every 10 minutes.

**When is the agent removed from the test?** An Endpoint Agent is removed from a test if:

* the agent hasn’t checked in for 1 hour (for example, if a user puts the agent's laptop to sleep).
*   at the time of the check-in, the Label criteria is no longer met (e.g. changed location).

    If an agent is removed from the test, a new agent will be assigned to the test (if available, see next question).

**When one agent is removed from the test, which new agent will be assigned to the test and when?** The first agent that checks in and matches the Label criteria will be assigned to the test, provided that there are less than three tests currently assigned to it.

**How many ICMP packets are sent out to perform end-to-end network measurements (loss, latency, jitter)?** In one test round, each agent sends out 10 ICMP echo request packets per test to perform end-to-end network measurements.

**How many parallel path discoveries are performed by each agent?** In one test round, one path discovery is performed by an agent for each test.

**What happens if an agent does not check in for a while?** When the agent does not check in for one hour, it is disassociated from all Labels and removed from all tests. When the agent checks in again, matching label associations are re-established.

**Is there a limit to the amount of data Endpoint Agent retrieves in HTTP Server test?** Yes. If download size limit is not explicitly configured in test's advanced settings, Endpoint Agent will stop downloading content once 10MB of data is received.
