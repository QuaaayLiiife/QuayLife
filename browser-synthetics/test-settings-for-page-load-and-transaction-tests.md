# Test Settings for Page Load and Transaction Tests

This page addresses two test types that fall under Browser Synthetics: page load and transaction tests. These two test types are unique in that they emulate a browser's interaction with a website.

The content below supplements

[Working With Test Settings](https://docs.thousandeyes.com/product-documentation/internet-and-wan-monitoring/tests/working-with-test-settings)

and describes test configuration specifically for page load and transaction tests. You’ll need user permissions in ThousandEyes to create and edit test settings.

The test settings are available under **Cloud & Enterprise Agents** > **Test Settings** as shown below.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-58c75d92a6676c3674611137bfd13b5b1c0586d6%2Fbrowser-synth-test-config-accessing.png?alt=media)

1.  1\.

    Choose **Cloud & Enterprise Agents** > **Test Settings** and click **Add New Test**.
2.  2\.

    Choose **Web** as the Layer and then choose either **Page Load** or **Transaction** as the Test Type.
3.  3\.

    Complete the **Basic Configuration** and **Advanced Settings** tabs as needed. Most of the required defaults are already filled in.
4.  4\.

    Click **Run Once** to ensure that the test configuration is valid.
5.  5\.

    Click **Create New Test** to save and activate the test.

When you choose the test type, you can see all the view layers that will be enabled by your new test. If no name is specified, the Test Name uses the value in the URL field, along with a prepended protocol (**https://** by default).

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-be4736a7f5d8eca9bcb3b9142012110d46aff3f9%2Fbrowser-synth-test-config-choose-layer-type.png?alt=media)

The majority of the ThousandEyes test configuration settings are shared between page load and transaction tests, and many are common to all or most ThousandEyes test types. For commonly shared test layers such as Network and BGP, see

[Working With Test Settings](https://docs.thousandeyes.com/product-documentation/internet-and-wan-monitoring/tests/working-with-test-settings)

.

### Basic Configuration Tab: Page Load and Transaction <a href="#basic-configuration-tab-page-load-and-transaction" id="basic-configuration-tab-page-load-and-transaction"></a>

The basic test configuration is almost the same between page load and transaction tests. The figure below shows a page load test configuration.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-17c0571ec0abdc31ef68873b2776437488e22c27%2Fbrowser-synth-test-config-basic.png?alt=media)

The **Basic Configuration** settings are as follows:

* **URL** - Specify a domain to monitor using the format `http(s)://domain:port/path` for example **https://google.com**. If you type a simple domain like **google.com**, the prefix **https://** is automatically prepended.
* **Schedule** - Used if running this page load or transaction test from more than one ThousandEyes Agent. You can stagger the test launches so that the target server doesn’t identify the test as a security threat.
  * **Default** - Choose Default to launch all tests on all agents at the start of each test round if possible. If the test round specifies a 5-minute interval, choose Default to cause all agents to attempt to launch this test at the beginning of that 5-minute test interval. Note that tests will not necessarily execute at the beginning of the interval. Exactly when the test runs is a function of how many tests are assigned to the agent and the intervals and runtimes of those tests.
  *   **Round Robin** - Stagger the tests so that each agent launches the test on the same interval, but they don’t all start simultaneously. See

      [Using Round Robin Test Scheduling](broken-reference)

      for more information.
* **Page Load / Transaction Interval** - The test interval is the frequency with which the page load or transaction portion of this test will be run.
  *
    * 1 minute for page load test
    * 2 minutes for transaction test
* **HTTP Server Interval** - Page load test only. Set the test interval for the HTTP server portion of this page load test. It is recommended that you use the same interval to have a better product experience.
* **Agent (s)** - Choose one or more ThousandEyes Cloud Agents, or choose from the ThousandEyes Enterprise Agents that are available to your account. Both Cloud Agents and Enterprise Agents can be selected.
* **Alerts, Enable** - When the Enable box is checked, all the alert rules currently selected in the drop-down immediately below will be active for the test.
* **4 out of 6 Alert Rules Enabled** - Drop-down to quickly see which alert rules are associated with this test.
  * You can create, modify and delete alert rules using the **Edit Alert Rules** link.
  *   **Default**: A few built-in alert rules are automatically associated with new page load tests. You can de-select them, view the alert rule, or create your own alert rules as described in

      [Creating and Editing Alert Rules](https://docs.thousandeyes.com/product-documentation/alerts/creating-and-editing-alert-rules)

      .
* **Alert Suppression Windows** - This drop-down appears if you have any alert suppression windows configured under Alerts.

### Advanced Settings Tab, Page Load and Transaction <a href="#advanced-settings-tab-page-load-and-transaction" id="advanced-settings-tab-page-load-and-transaction"></a>

The **Advanced Settings** apply to both page load and transaction tests, except for a few items that are unique to page load tests, where noted.

Browser Options allows for additional fine-tuning of page load and transaction tests.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-a3b4d0b612314aa37805b1b4718e6956b6bb7668%2Fbrowser-synth-test-config-browser-options.png?alt=media)

The Browser Options are as follows:

* **Screenshot / Enable** - Check box. You can disable screenshots for data privacy reasons without having to remove those lines from the transaction script. For example, if you are monitoring a HIPAA-compliant application you might want to disable screenshots that show patient identifying information.
*   **Browser Language**: Drop-down selector to choose the language/locale of the browser used during testing.

    When a visitor with a browser setting for a specific language/locale lands on a web site, that site can redirect them to the appropriate landing page that uses their preferred language. For example, if you are looking to test the Portuguese-language version of your site for visitors located in Brazil, or who have Portuguese selected as their preferred language, you can create a transaction test that runs on the default site for Portuguese.
* **Microphone and Camera / Allow or Block**: Button. Used for collaborative web applications such as Google Meet that may prompt the user for permission for the app to use the camera or microphone.
  * **Allow**: The ThousandEyes transaction or page load test will emulate a fake camera and microphone to be used in that application.
  * **Block**: Deny permission. Camera and microphone will not be available for the application.
* **Geolocation / Allow or Block**: Button. For web applications that require the user's location in order to test an area of the application, the target web application might request permission to use the location of the browser.
  * **Allow**: The ThousandEyes test provides the location of the ThousandEyes agent to be used for the test. Using the agent’s location provides data consistent with that vantage point.
  * **Block**: Denies permission to use geolocation.
*   **Page Loading Strategy**: This option lets you choose how long to wait to execute the webdriver command. The Page Loading Strategy gives you the option to execute the next action without waiting for all the elements on the page to load. For example, you might have a page or application where the DOM loads quickly, but because of JavaScript that modifies the page, or assets that take a long time to load, you might otherwise have to wait a long time before executing the next action on your transaction script.

    There are three major milestones for loading a web page: when the structure of the page (HTML) has been downloaded, when the major structural elements are present (DOMContent Loaded) and when images and other assets of the page have finished rendering (last contentful paint). You can see this in the page load waterfall charts: the "index.html" object shows when the HTML has finished downloading. The blue line denotes when the DOM content has loaded, and the red line in the waterfall shows when the page has fully loaded.

    Drop-down options as follows:

    * **Normal**. Wait for the entire page to load, meaning that HTML content and all resources have been downloaded and parsed before moving to the next action in the transaction test script.
    * **Eager**. Wait for the DOMContentLoaded event, meaning that HTML content is downloaded and parsed, and the document readiness state is “interactive”, before moving to the next action in the test script.
    * **None**. Wait only for HTML content to download. Once the HTML is downloaded, the test proceeds to the next action in the transaction test script.

#### Page Load or Transaction Timeout <a href="#page-load-or-transaction-timeout" id="page-load-or-transaction-timeout"></a>

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-9a6297cf33da59db2df6838486e497e5d7e487c0%2Fbrowser-synth-test-config-timeouts.png?alt=media)

The **Page Load Timing** settings are as follows:

*   **Timeout** - This is the overall page load or transaction test timeout setting. Note that there’s a separate timeout for the HTTP server portion of this test. Timeout is the number of seconds until the test type terminates due to inability to load the page in a page load test or to complete the script in a transaction test within the timeout time.

    Slider with a range 5 - 15 seconds. Timeout is equal to or larger than Target Time for View. Also note that the maximum timeout can change based on the interval selected in the basic settings.

    *
      * 10 seconds for page load tests. The maximum timeout value is either 0.25 \* interval (in seconds) or 60 seconds, whichever is lower.
      * 30 seconds for transaction tests. The maximum timeout value is either 0.5 \* interval (in seconds) or 180 seconds, whichever is lower.
*   **Target Time for View** - Specifies the expected or “normal” timeout for the transaction or page load test. Influences color-coding legend on the test view **Map** tab for the page load or transaction view layer. If a test completion takes longer than this threshold, the test still runs but the results show in red instead of green.

    Slider with a range 1 - 30 seconds. Cannot exceed the Timeout.

    *
      * 10 seconds for transaction

The **HTTP Server Timing** settings are as follows:

*   **Timeout** - Slider with a range 5 - 60 seconds

    Seconds until the test type terminates due to an unresponsive target server. This is the HTTP server test timeout setting. Note that there’s a separate timeout for the page load portion of this test.

    Note that the HTTP server timeout cannot exceed the overall test timeout.

    **Default**: 5 seconds for page load and transaction tests
*   **Target Response Time** - Specifies the expected or “normal” timeout for the HTTP server portion of the page load or transaction test. Influences color-coding legend on the test view Map tab, for the HTTP Server view layer. If a test completion takes longer than this threshold, the test still runs but the results show in red instead of green.

    Slider with a range 100 - 5000 milliseconds.

    **Default**: 1000ms for page load tests; cannot exceed the HTTP Timeout.

#### Exclude Elements from Metrics and Waterfall <a href="#exclude-elements-from-metrics-and-waterfall" id="exclude-elements-from-metrics-and-waterfall"></a>

Use the exclude feature to exclude all objects from a domain, a sub-domain, or even specific objects such as very large images, for example \*.domain.com/very\_large\_logo.jpg.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-08c7210c4c10fa1e3fd4c0eb3f012e8a6c94b825%2Fbrowser-synth-test-config-exclude-url.png?alt=media)

*   **Exclude Domains / Object URLs**:

    Text entry. Ignore large page objects that you don’t care about that could be negatively impacting your page load times and raising false timeout alarms. Can also be used to block requests to third-party tracking tools.

Excluding domains or URLs can be helpful for ignoring third-party assets that are not important to your teams’ primary business objectives. Requests to blocked domains or objects appear greyed out in the waterfall and will not affect test metrics collected.

Note that entering a domain such as google.com only blocks the main domain (https://google.com). Blocking subdomains requires a wildcard, for example \*.google.com would block docs.google.com, maps.google.com and google.com itself.

Network layer test settings for page load and transaction tests are the same as for other test types, described in

[Working With Test Settings](https://docs.thousandeyes.com/product-documentation/internet-and-wan-monitoring/tests/working-with-test-settings)

.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-61fb6a83b57785fde113830fc4e306dff353ff92%2Fbrowser-synth-test-config-network.png?alt=media)

Use Proxy Settings to select a pre-configured setting from within ThousandEyes. You can view or configure these settings under **Cloud & Enterprise Agents** > **Agent Settings**, under the **Proxy Settings** tab. See

[Collecting Proxy Metrics](https://docs.thousandeyes.com/product-documentation/internet-and-wan-monitoring/tests/http-server-tests/proxy-metrics)

for more information.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-d9d3d724fa8d03f8273af3f94f5d87cbf93db486%2Fbrowser-synth-test-config-proxy.png?alt=media)

The TLS area lets you disable SSL verification for page load and transaction tests.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-6b2e345166ed90bbda541a2b5c9f1eba3a598716%2Fbrowser-synth-test-config-tls.png?alt=media)

The **TLS** settings are as follows:

*   **SSL Version** - Select the version of the SSL/TLS protocol to offer in the SSL Client Hello from the ThousandEyes Cloud or Enterprise Agent.

    This will set the maximum version of SSL/TLS that the connection can use, but a lower version may be negotiated by the server.

    Drop-down options are the following:

    * **SSLv3**: Use SSL version 3.0. No lower version can be negotiated.
    * **TLSv1.0**: The Agent will start the TLS negotiation at version 1.0.
    * **TLSv1.1**: The Agent will start the TLS negotiation at version 1.1.
    * **TLSv1.2**: The Agent will start the TLS negotiation at version 1.2.
    * **Auto**: The Agent will start the TLS negotiation at the highest version of TLS supported by its operating system. Currently the highest version is TLS 1.2 Contact ThousandEyes Customer Support if you require confirmation of the current version.
*   **Verify SSL Certificate** - Checkbox. Applies to both the HTTP view and to the page load or transaction view, for page load and transaction tests.

    By default, certificate-related errors will result in a test error. Uncheck this box to ignore certificate errors during SSL/TLS negotiation.

    If your page load and transaction tests have SSL verification disabled at the ThousandEyes Agent level, review your configuration and use the test-level setting going forward.

Authentication settings for page load and transaction test types are the same as for the HTTP server test type, with the exception of OAuth and NTLM:Negotiate. See

[Working With Test Settings](https://docs.thousandeyes.com/product-documentation/internet-and-wan-monitoring/tests/working-with-test-settings)

for information on the HTTP server test type.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-4f7490fa54b58fb68d1a8e87b0279aa19dbbf229%2Fbrowser-synth-test-config-http-authentication.png?alt=media)

HTTP request settings for page load and transaction tests include HTTP versions, redirects, browser versions, device emulation, and the use of custom headers.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-4f059f230f00f7e70e52f29a13f0b3da61543702%2Fbrowser-synth-test-config-http-request.png?alt=media)

The **HTTP Request** settings are as follows:

*
  * **Prefer HTTP/2** - Attempt HTTP/2 and fallback to HTTP/1.1 if HTTP/2 is not available.
  * **HTTP/1.1 only** - Send request(s) using HTTP/1.1 only, no attempt is made to utilize HTTP/2.
* **Follow Redirects / Enable** - Checkbox to enable redirects.
* **Device Emulation** - Drop-down options with these main device type categories. A range of options are available for different device type, including custom dimensions for each:
* **Device Emulation / pixel dimensions** - The browser display updates based on Device Emulation selection immediately above.
* **Device Emulation / portrait or landscape** - Icon. The browser display updates based on Device Emulation selection immediately above.
*   **User Agent** - The user agent normally refers to what your browser is sending in the `user-agent` heading. In this case it refers to what ThousandEyes sends when running this test.

    Drop-down options include various browser options for Windows and Mac OS. Chrome, Firefox, Internet Explorer, Edge, Safari. Options are:

    * Additional options for commonly used browsers
    * Choose **Custom** for other browsers not specified
*   **User Agent / Custom** - If **Custom** is selected immediately above, this text box populates with suggested text, which may show different versions based on recent software updates.

    For example, the suggested text might read something like this: “Mozilla/5.0 (X11; Linux x86\_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/80.0.3987.163 Safari/537.36”
*   **Agent ID Strategy** - Drop-down options for the identifier to use for the ThousandEyes Cloud or Enterprise Agent that is running this test. Options:

    * **Add x-thousandeyes-agent Header**: Identify ThousandEyes Agent HTTP requests by including the custom x-thousandeyes-agent: yes header to every request.
    * **Extend User Agent Header**: Identify ThousandEyes Agent HTTP requests by extending the user agent request header with the ThousandEyes Agent identifier string. Use if default ThousandEyes Agent header causes CORS issues.

    **Default**: Add x-thousandeyes-agent Header
* **Custom Headers** - Drop-down options. Use the plus sign to the right to add multiple entries. Options are:
* **Custom Headers / text** - Enter one or more HTTP header strings in the form `<stringname>: <value>`. Note the whitespace between the literal colon character and the placeholder `<value>`. When adding multiple headers, delineate between individual headers using a line break. The custom headers will be transmitted with the target page request (page load test) or each page request (transaction test) but not for objects within a page.

**Notes on Agent ID Strategy**

ThousandEyes adds one line to the HTTP request headers that identifies the HTTP request as coming from a ThousandEyes Cloud or Enterprise Agent. By default, that identifier is this string:

`x-thousandeyes-agent: yes`

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-cc384a3d7fa6d25fb66544c4647f6586f321448d%2Fbrowser-synth-test-config-agent-id-example.png?alt=media)

Sometimes the default agent identifier causes problems with cross-origin resource sharing on the target server.

[CORS](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS)

affects third-party HTML objects that might be fetched from another site. A third-party domain owner can choose not to allow sharing for requests containing unknown agent identifiers, which might cause all HTML objects from that domain to fail to load properly.

To get around this limitation, the alternative Agent ID strategy option **Extend User Agent Header:** appends the ThousandEyes Agent identifier string at the end of the line immediately above that (the line that begins with user-agent).

If the (ThousandEyes Agent) identifier string is removed from the User Agent text input while the Extend User Agent Header option is selected, the test configuration will not be valid and cannot be saved.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-7b33476d96e964ad3c9c0a6dcb742e87a951a190%2Fbrowser-synth-test-config-http-response.png?alt=media)

The **HTTP Response** settings are as follows:

* **Desired Status Code / Default (2xx or 3xx)** - Check box
* **Desired HTTP status code of the response** - Use to set a custom status code, if Desired Status Code / Default is un-checked immediately above.

One reason to specify a custom HTTP status code is if you can’t run the test that you really want due to authentication challenges on the server side. In this case, even a “403 - forbidden” might constitute a success message, because it tells you that the target is still responding

*   **Verify Content / Enable** - Check box. If selected, a text box appears. Enter a POSIX Extended Regular Expression to match against the content of the response.

    Non-matching responses will be marked as errors.

    **Note**: the HTTP server portion of the test does not execute any JavaScript code, nor does it expand any CSS. It simply downloads the initial page and stops. It does not load anything that comes from other files. Therefore the content generated by JavaScript cannot be verified using a page load test. If you need to match JavaScript-generated content, use a transaction test instead.

Use this setting to suppress the capture and display of HTTP headers on the ThousandEyes platform.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-71a94991f06f9c81b4fc98d786b0439e199ea4c8%2Fbrowser-synth-test-config-http-headers.png?alt=media)

The **HTTP Headers** settings are as follows:

*   **Show HTTP headers in waterfalls** - If enabled, shows HTTP request and response header information for each object in the waterfall displays. You can view by clicking the \[Header] link in a waterfall row.

    De-select in order to suppress sensitive data that might otherwise be available in ThousandEyes.

### Additional Transaction Test Settings <a href="#additional-transaction-test-settings" id="additional-transaction-test-settings"></a>

The test settings for transaction tests are almost the same as for page load tests, with a few additional settings as described below.

#### Basic Configuration Tab, Transaction <a href="#basic-configuration-tab-transaction" id="basic-configuration-tab-transaction"></a>

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-8c87e21fda9ff9022e3f0de18c42176fbdaa5d95%2Fbrowser-synth-test-config-transaction-basic-01.png?alt=media)

All **Basic Configuration** settings are the same for a transaction test as for a page load test, except as noted below.

*   **Download the ThousandEyes Recorder** (shown first time only) - Link to download the ThousandEyes Recorder IDE. Use the Recorder to generate your own transaction scripts without having to write any code. See

    [ThousandEyes Recorder](<../.gitbook/assets/thousandeyes recorder>)

    for more information.
*   **Transaction Script** - Text window. Transaction tests execute custom Selenium WebDriver-based scripts written in JavaScript, to simulate user interactions with web page elements.

    **Default**: A skeleton transaction script is generated with the JavaScript functions necessary for ThousandEyes transaction tests.
* **Transaction Script / Icons** - Use the icons to insert special functions at selected points within your transaction test script.
  * **Hourglass** - Add sleep function which waits 5 seconds before proceeding to the next step in the script.
  * **Timer** - Adds a marker function to track script progress. Note that this can be changed from `markers.set` to `markers.start` and `makers.stop` to track a particular section.
  * **Screenshot** - Capture screenshot at a particular point in the script. You can temporarily disable screenshots without having to remove these lines from your script by un-checking the Screenshot | Enable checkbox under **Advanced Settings** tab, **Browser Options** section.
  *   **Key** - Add login credentials from the ThousandEyes Credentials Repository, available as a separate tab under Cloud & Enterprise Agents > Test Settings. See

      [Working With Secure Credentials](<../.gitbook/assets/working with secure credentials>)

      for more information.

#### Transaction Script Window <a href="#transaction-script-window" id="transaction-script-window"></a>

Transaction tests execute custom Selenium WebDriver-based scripts written in the JavaScript language to emulate user interaction with web page elements. There's a download link for the ThousandEyes Recorder as well.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-202ae76cc0664c063007a8bec51ad08a214c2530%2Fbrowser-synth-transaction-test-config-script.png?alt=media)

#### Advanced Settings Tab, Transaction <a href="#advanced-settings-tab-transaction" id="advanced-settings-tab-transaction"></a>

All of the items on the **Advanced Settings** tab for transaction test configuration are identical to the same settings as they appear for page load test configuration, with the exception of the default timeouts.

#### Some HTTP Server Test Options Not Available <a href="#some-http-server-test-options-not-available" id="some-http-server-test-options-not-available"></a>

The following test options that are available in the HTTP Server test type are not available in page load and transaction tests:

* HTTP Request method (can be used for basic API testing)
