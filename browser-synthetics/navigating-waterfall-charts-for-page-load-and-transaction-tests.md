# Navigating Waterfall Charts for Page Load and Transaction Tests

ThousandEyes Page Load and Transaction tests provide a waterfall chart for insight into how a browser interacts with web page objects. This article explains how data is presented within waterfall charts.

ThousandEyes relies on Chromium, which prefers IPv6 if available, and otherwise falls back to IPv4. If you run browser synthetics tests on agents with “force IPv6” set as a policy, make sure that the target URL supports IPv6.

If the agent is set to force IPv6, but the target URL does not, you might see inconsistent DNS errors in the test view, where the “Transaction” or “Page Load” view layer looks successful, but the “HTTP Server” layer shows a DNS error.

This article contains screenshot views and instructions that reference “Classic” test views. ThousandEyes is in the process of introducing multi-service views that combine multiple test views into one multi-service view. See

[Multi-Service Views](https://docs.thousandeyes.com/product-documentation/internet-and-wan-monitoring/tests/multi-service-views)

for more information.

### What Is a Waterfall Chart? <a href="#what-is-a-waterfall-chart" id="what-is-a-waterfall-chart"></a>

A waterfall chart is a time-based representation of data that displays the relationship between events.

BrowserBot, the application that performs Page Load and Transaction tests, generates a **.har** file upon completion of each test. The **.har** file contains metrics about each object downloaded during the test. This information is then represented in the form of a waterfall chart.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-575353dead3ad3fcdc7436ef250823e5bc992046%2Fproduct-documentation\_tests\_navigating-waterfall-charts-for-page-load-and-transaction-tests-1.png?alt=media)

Properly understanding results requires familiarity with the test types, the Document Object Model, and the ThousandEyes user interface. An introduction to each is provided below.

### The Page Load Waterfall Display <a href="#the-page-load-waterfall-display" id="the-page-load-waterfall-display"></a>

Page Load tests are navigated using a timeline pane and an informational pane. Selecting a single agent, from the agent drop-down menu, enables a waterfall chart that documents each object loaded by the agent's browser.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-22a75cf8b4b3bc0d0d1431f47bc2b128ea9fda3a%2Fproduct-documentation\_tests\_navigating-waterfall-charts-for-page-load-and-transaction-tests-2.png?alt=media)

An explanation of how to navigate page load test results is

[available here](<../.gitbook/assets/using the page load view>)

.

### The Transaction Test Waterfall Display <a href="#the-transaction-test-waterfall-display" id="the-transaction-test-waterfall-display"></a>

Transaction tests are navigated using a timeline pane and an informational pane. Selecting a single agent, from the agent drop-down menu, enables a waterfall chart that documents each object loaded by the agent's browser.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-7b7ec3700e26aaee538afc0650ed24574b79bb28%2Fproduct-documentation\_tests\_navigating-waterfall-charts-for-page-load-and-transaction-tests-3.jpg?alt=media)

### The Document Object Model <a href="#the-document-object-model" id="the-document-object-model"></a>

Understanding waterfall charts requires familiarity with the Document Object Model.

Upon receiving a browser request for a web page, an HTTP server locates the site "Directory Index" file and provides an HTML formatted document to the requesting browser. HTML (HyperText Markup Language) instructs the browser regarding how information should be displayed.

The Document Object Model describes HTML structure as a series of objects called nodes. A diagrammed HTML document resembles an ancestral tree; hence the terms "parents" and "children" are used to describe the relationship between nodes. While some nodes, such as text and scripts, may be included within the root HTML document, others must include links to resources which a browser downloads separately.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-fbabe4541d844d57836d811ce335f3afa70b7940%2Fproduct-documentation\_tests\_navigating-waterfall-charts-for-page-load-and-transaction-tests-4.jpg?alt=media)

Downloaded objects, such as javascript and css files, may in turn reference other objects that the browser must download to prior to page load completion.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-4399eea5225c184d7ee5fbd21e9e1eb764bf8edd%2Fproduct-documentation\_tests\_navigating-waterfall-charts-for-page-load-and-transaction-tests-5.jpg?alt=media)

These objects are often sourced from multiple domains.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-bfc4fc1c1420218b9ff1433486aba942210ed26d%2Fproduct-documentation\_tests\_navigating-waterfall-charts-for-page-load-and-transaction-tests-6.jpg?alt=media)

Each Page Load Object requires an independently completed HTTP transaction.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-1370b897f2de743b700a118fa1104b0767bdfa18%2Fproduct-documentation\_tests\_navigating-waterfall-charts-for-page-load-and-transaction-tests-7.jpg?alt=media)

**Waterfall Charts provide metrics for the following HTTP transaction activities:**

**BLOCKED:** The time that a browser waits for an already established connection to become available. Web browsers are designed to allow a maximum number of concurrent connections per domain. Blocking time means that the browser is waiting for other requests to complete and represents the time that is spent before a request is sent because other requests are being handled.

**DNS**: The duration to resolve a domain record to an IP address. By default, Browserbot does not cache DNS records at startup.

**CONNECT:** The time to establish a TCP handshake with the Target Server.

**SSL:** The duration of SSL/TLS negotiation.

**SEND:** The duration in which the browser successfully sends a request to the server.

**WAIT:** The duration between the completion of a browser's SEND request and receipt of the first byte of a server's response.

**RECEIVE:** The time between the first byte of the server response to the last byte of the data payload.

**Aggregate Metrics include:**

**DOM LOAD TIME:** Transaction time from the beginning of the first object load to the end of the final object load.

**PAGE LOAD TIME:** The time from the initial request to when the page is fully rendered. Redirect time is taken into account when determining total page load time.

### Navigating the Page Load Waterfall Chart <a href="#navigating-the-page-load-waterfall-chart" id="navigating-the-page-load-waterfall-chart"></a>

The transaction test waterfall chart displays DOM load metrics for a target web page.

By default, the waterfall chart displays objects in chronological order. Selecting table headers will reorder rows by either Object Name, Domain, Response Code, Provider, Size, or Waterfall Chronology.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-00ca345ab32e32d6b180239149e701566136ad7f%2Fproduct-documentation\_tests\_navigating-waterfall-charts-for-page-load-and-transaction-tests-11.jpg?alt=media)

Hovering over a multi-colored download bar will display object and load metrics.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-1370b897f2de743b700a118fa1104b0767bdfa18%2Fproduct-documentation\_tests\_navigating-waterfall-charts-for-page-load-and-transaction-tests-7.jpg?alt=media)

Hovering over the blue and red load completion markers will display aggregate load metrics.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-6564339eae7100ee23ecc9c6fb2af3af45d1956d%2Fproduct-documentation\_tests\_navigating-waterfall-charts-for-page-load-and-transaction-tests-10.jpg?alt=media)

If "save object headers" was selected under the test's advanced settings, a link to view headers will be included within the Waterfall "Response Code" column.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-00ca345ab32e32d6b180239149e701566136ad7f%2Fproduct-documentation\_tests\_navigating-waterfall-charts-for-page-load-and-transaction-tests-11.jpg?alt=media)

Selecting a header link opens a light-box which includes both the Request and Response Headers.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-b2fa09a88c0d74ee146494e340b2786d7903eda9%2Fproduct-documentation\_tests\_navigating-waterfall-charts-for-page-load-and-transaction-tests-12.jpg?alt=media)

### Navigating the Transaction Test Waterfall Chart <a href="#navigating-the-transaction-test-waterfall-chart" id="navigating-the-transaction-test-waterfall-chart"></a>

The transaction test waterfall chart displays DOM load metrics for each page loaded during a transaction test.

By default, the waterfall chart displays objects in chronological order. Selecting table headers will reorder rows by either Object Name, Domain, Response Code, Provider, Size, or Waterfall Chronology.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-ae94cbb63e6e0a3a382057b2844b343ab6a821c6%2Fproduct-documentation\_tests\_navigating-waterfall-charts-for-page-load-and-transaction-tests-13.jpg?alt=media)

The Transaction test waterfall traverses multiple pages. A chronological view selector is used to focus on specific portions of the DOM load history.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-39946524daabb451f12b9ccb6d26713dcc991fcc%2Fproduct-documentation\_tests\_navigating-waterfall-charts-for-page-load-and-transaction-tests-14.jpg?alt=media)

Hovering over a multi-colored download bar will display object and load metrics.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-62d45021e0f378eda7f6e77bff9b1e73c0e30570%2Fproduct-documentation\_tests\_navigating-waterfall-charts-for-page-load-and-transaction-tests-15.jpg?alt=media)

Hovering over the blue and red load completion markers will display aggregate load metrics.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-ec313027a6552c7319fac61b5f5c1c73adfabebb%2Fproduct-documentation\_tests\_navigating-waterfall-charts-for-page-load-and-transaction-tests-16.jpg?alt=media)

If "save object headers" was selected under the test's advanced settings, a link to view headers will be included within the Waterfall "Response Code" column.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-d63941764b694983c012e62fcfc5e6509c06ace4%2Fproduct-documentation\_tests\_navigating-waterfall-charts-for-page-load-and-transaction-tests-17.jpg?alt=media)

Selecting the headers icon will open a light-box that includes both the Request and Response Headers.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-9899ef62a1e2530fce8e52da9319bef9a75fdb90%2Fproduct-documentation\_tests\_navigating-waterfall-charts-for-page-load-and-transaction-tests-18.jpg?alt=media)

In some cases, objects will not have Response Headers. One example of this is an object with the Cancelled designation. If there is no Response Code for an object, the word "Cancelled" is shown for an incomplete object. In the size field of the waterfall, a triangular logo with an exclamation point will appear and "Object Incomplete (cancelled)" will appear in the hover menu for that logo. Selecting the Header link will only show a Request Header. The Response Header section will not show information since there is none.
