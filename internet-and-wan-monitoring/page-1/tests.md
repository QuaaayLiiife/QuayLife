# Tests

The ThousandEyes platform enables you to test networked assets that your organization owns, and test SaaS-based assets to which your organization subscribes.

This article walks you through all available ThousandEyes test types, enabling you to decide what test type best fits your monitoring intentions. A list of typical usage scenarios is provided for each test type.

### Classification of Agent Types <a href="#classification-of-agent-types" id="classification-of-agent-types"></a>

ThousandEyes collects data from various vantage points deployed around the internet and inside customer networks. For the most part, these vantage points are called "agents" - with a few exceptions outlined below. There are multiple types of agents available, each having a specific purpose:

*   **Cloud and Enterprise Agents** are hosts (or servers, if you will) containing ThousandEyes software capable of running

    [instant or scheduled](<../../.gitbook/assets/scheduled v s instant tests>)

    tests and

    [device discoveries](https://docs.thousandeyes.com/product-documentation/device-layer)

    . The main (and almost only) difference between Cloud and Enterprise Agents is who deploys and manages them - Cloud Agents are deployed by ThousandEyes, on many locations across the globe, instantly available for your new tests. Enterprise Agents, on the other hand, are deployed by you, our customer, in locations of your interest - your data centers, your branch offices, and so on.
* **Endpoint Agents** are your Windows or macOS workstations that have ThousandEyes Endpoint Agent software installed. These agents, whenever they are present in one of the defined networks, collect network and application layer performance data as your users are accessing websites or applications on configured domains. In addition to that, Endpoint Agents provide basic support for running scheduled tests. Pulse version of Endpoint Agents are also available dedicated to running scheduled tests, these can be installed on customer hosts.

There are two test types that are using different vantage points, not described above - routing layer test and DNS+ layer tests. Their vantage point specifics are outlined in the corresponding sections below. Regardless of the outlined data collection vantage point differences, tests from these two layers are listed in the Cloud and Enterprise Agent-Based Tests section below. Metrics calculated at various layers along with their significance are documented in

[ThousandEyes Metrics: What Do Your Results Mean?](https://docs.thousandeyes.com/product-documentation/thousandeyes-basics/thousandeyes-metrics-what-do-your-results-mean)

.

### Cloud and Enterprise Agent-Based Tests <a href="#cloud-and-enterprise-agent-based-tests" id="cloud-and-enterprise-agent-based-tests"></a>

ThousandEyes tests are classified into categories based on layers of operation, as shown in the following diagram:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-4a74a9f2510d2c1ebb3abc2873aae6edc9046732%2Fproduct-documentation\_tests\_guide-to-thousandeyes-test-types-1-3.png?alt=media)

Routing layer tests provide methods for collecting internet routing-related information.

This test type operates on the lowest fabric of the internet - the

[BGP routing](https://en.wikipedia.org/wiki/Border\_Gateway\_Protocol)

layer. Relevant BGP routing data is collected from ThousandEyes-provided BGP Monitors (a.k.a. "Public BGP Monitors"), from BGP peers that you connect to our infrastructure - the so-called

[Private BGP Monitors](https://docs.thousandeyes.com/product-documentation/thousandeyes-basics/inside-out-bgp-visibility)

, or both at the same time. Collected data is presented as

[BGP Route Visualization](<../../.gitbook/assets/using the bgp route visualization view>)

, a view that presents information in a cohesive manner, pointing out relevant events on the timeline and in the ASN graph. A BGP test also offers the ability to include prefixes covered by target prefix.

**Typical BGP Test Use Cases**

* Ensure network prefix reachability from multiple BGP vantage points on the internet.
* Detect and alert on BGP route leaks or BGP route hijacking.
* Validate and alert on active DDoS mitigation measures.
* Monitor presence and activity of multiple upstream network providers.
* Alert on unexpected path changes, unexpected upstream ASNs, route flapping, etc.

The following figure is showing BGP path change detected by the St. Petersburg public BGP Monitor, where the network path through ASN20485 is replaced by a path through ASN9002:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-4bbc2792f52b4dda8e66c1213b9ff73d88805c89%2Fproduct-documentation\_tests\_guide-to-thousandeyes-test-types-2.png?alt=media)

To get a sense of what interacting with collected BGP data feels like, you can review the contents of the test results depicted above interactively. To do so, visit this share-link:

[https://ascnkau.share.thousandeyes.com/](https://ascnkau.share.thousandeyes.com/)

.

An agent-to-server test measures network performance as seen from ThousandEyes agent(s) towards a remote server. The target could either be an IP address or a hostname. Measurements in an agent-to-server test combine parameters of both, forward and reverse paths. To measure direction-specific parameters an agent-to-agent test can be utilized.

**Typical Agent-to-Server Test Use Cases**

* Measuring network performance when accessing the target remote server from agents assigned to test.
* Understand network path changes between source to destination.
* Verification of target availability.
* Identify network degradation along the network path.
* Verify network management of DSCP, MTU, and optimization.
* Monitor ingress traffic load distribution across ISPs.

**Example Agent-to-Server Test Results:**

Below is the path visualization for a test targeting google.com. Restricted access to Google results in 100% packet loss from Cloud Agent Beijing, China (China Unicom). The red circles signify nodes with forwarding loss. Hovering over a specific node will provide a modal with detailed information.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-4990a01867237b03ea876d0d281558c778641f2a%2Fproduct-documentation\_tests\_guide-to-thousandeyes-test-types-3.png?alt=media)

An agent-to-agent test evaluates the performance of the underlying network between two physical sites. The source and target for performing measurements here are ThousandEyes agents and can be both a Cloud Agent, an Enterprise Agent or a combination of both. For more information, see the agent-to-agent test overview.

* Measure bi-directional network throughput.
* Measuring network connectivity characteristics between:
  * Regional branch offices connecting to data centers.
  * Regional branch offices connecting to IAAS cloud environments.
  * Data centers connecting to IAAS environments.
* Branch office to HQ network quality via VPN and so on.
* Detect packet dropping network nodes on the path between source to destination.
* Evaluating the return path by performing bi-directional testing. Measure network performance and throughput between locations.
* Compare end-to-end network performance and characteristics between the forwarding and return paths.
* Measuring network characteristics between data centers, offices, and cloud environments.
* Evaluate network connections for specific applications.
* Detect latency and loss along the network path.

**Example Agent-to-Agent Test Results**

The agent-to-agent test below depicts a connection error between Cloud Agent Wellington, New Zealand and Cloud Agent Johannesburg, South Africa.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-da1895cd05ace0271b0dc953f480cb00c471f9c8%2Fproduct-documentation\_tests\_guide-to-thousandeyes-test-types-4.png?alt=media)

Visit this

[share-link](https://poyrx.share.thousandeyes.com/)

to see an agent-to-agent test.

DNS Server tests provide record validation and service performance metrics. Upon selecting a specific domain and the servers to be queried, agents will run DNS and network layer performance metrics for all targeted servers. Complete information is available in

[Using the DNS Server View](https://docs.thousandeyes.com/product-documentation/thousandeyes-basics/using-the-dns-server-view)

.

* Alert on incorrect DNS Record Mapping.
* Measure DNS nameserver performance and availability.
* Monitor network performance between agents and target servers.
* Compare DNS results and performance from around the globe.
* Verify GSLB and GeoDNS performance.

**Example DNS Server Test Results**

The below example depicts an iterative query made to authoritative servers for google.com:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-0a10ece9dbffc18083c8e200071ca81e32827c8d%2Fproduct-documentation\_tests\_guide-to-thousandeyes-test-types-5.png?alt=media)

To get your hands dirty with a DNS Server test, visit this

[share-link](https://gpehi.share.thousandeyes.com/)

.

Large DNS zones are divided into various smaller child zones with each child zone having dedicated authoritative DNS servers. When a DNS request is made the parent zone will refer the request to authoritative DNS server in the child zone. In this scenario ensuring DNS requests are correctly pointed to authoritative servers by a parent server and also the authoritative server being correctly configured to assert authority becomes crucial. The DNS Trace test helps validate this critical delegation. A DNS Trace test will verify delegations from each parent zone to child zone.

* Verify the delegation of DNS records are being performed between parent and child zones as expected.
* Observe the DNS hierarchy of a target domain from various vantage points.

**Example DNS Trace Test Results**

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-c7d12c8f6f5666c18036c756caebef0e9166b7cc%2Fproduct-documentation\_tests\_guide-to-thousandeyes-test-types-6.png?alt=media)

Here is a

[sample test](https://ggjkirvg.share.thousandeyes.com/)

to see a DNS Trace test. Complete trace can be obtained by clicking **View Trace** link in the above screenshot.

During a DNS trace test, it is possible that a non-authoritative answer is received from a server in the path. The explanation below provides further details on what is happening and why.

Normally, a failed DNS Trace test terminates with the following error:

"Dead end for " + dnsName + " " + dnsType

;; ERROR: Dead end for login.microsoftonline.com A

This error is returned when:

1.  1\.

    an answer has not been received, and
2.  2\.

    no further referral data exists.

To successfully terminate a trace requires that the Answer section has one or more non-CNAME records, and the Authoritative Answer (AA) flag in the DNS header is set. Normally, when we have an answer, the answer comes from an authoritative nameserver which will set the AA flag. So, what happens when an answer is received, but it’s from an unconfirmed source?

We have observed that the Answer section can be populated by non-authoritative nameservers (spoofed or otherwise) without AA being set. In that situation, a different error message is returned. Whenever there is a non-zero Answer section that does not contain either a CNAME, or a record matching the type of the target record, you’ll see an error message similar to the following example:

;; ERROR: Server c.root-servers.net responded with AA flag unset (non-authoritative answer) for login.microsoftonline.com A

​

[DNSSEC](https://en.wikipedia.org/wiki/Domain\_Name\_System\_Security\_Extensions)

tests verify the digital signature of DNS resource records and hence validate the authenticity of resource records according to Domain Name System Security Extensions. A DNSSEC test adds security validation to a DNS trace test and complements it.

* Verify valid DNS signatures are being sent out along with DNS records.
* Validate DNS records based in DNSSEC.
* Observe the DNSSEC Trust Chain and Data Chain.

**Example DNSSEC Test Results**

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-82a0bbbe12460bca69c0937f48102b6c100425b0%2Fproduct-documentation\_tests\_guide-to-thousandeyes-test-types-7.png?alt=media)

Visit this

[share-link](https://eipqvw.share.thousandeyes.com/)

to get a sense of a DNS Trace test. Click **Details** to see the Trust Tree showing chain of trust and Data Chain showing actual resource records received during the test.

This set of tests touches on various Web technologies starting from the most basic measurement of availability of web server all the way up to performing precision transactions on a target. ThousandEyes also supports using

[Custom User-Agent Strings](<../../.gitbook/assets/custom user agent strings in a web test>)

for Web layer based tests. Watch

[Working with Web Tests](https://www.youtube.com/watch?v=Cht-ehtUaeQ)

to get up-to-speed with Web Layer tests quickly.

As the name suggests, an HTTP Server test measures the availability and performance of an HTTP service. Any HTTP service that is exposed to the internet (or intranet, if Enterprise Agents are deployed in your internal network) can be tested.

The HTTP Server test is performed as a series of steps (or phases):

1.  1\.

    **DNS**: The domain part of the test target URL is resolved to an IP address.
2.  2\.

    **Connect**: A TCP 3-way handshake is performed.
3.  3\.

    **SSL (optional)**: Security mechanisms are negotiated.
4.  4\.

    **Send**: An HTTP request is sent.
5.  5\.

    **Receive**: An HTTP response is waited for and received.
6.  6\.

    **HTTP**: The HTTP response code is validated.
7.  7\.

    **Content verification (optional)**: Verification of the received content is performed by matching it against a

    [regular expression](<../../.gitbook/assets/posix extended regular expression syntax>)

    .

Many aspects of HTTP Server testing can be configured to suit your individual or corporate testing requirements - various authentication protocols are supported, custom headers can be added, SSL options tweaked and so on.

When HTTP Server test detects an issue, the results pinpoint the phase of a request in which the issue occurred, helping to decrease your mean time to repair. To assist the analysis, information from lower layers is included in this test type, namely agent-to-server network and a BGP routing layers are readily available when looking for the root cause.

* Alert on the HTTP service availability or performance issues
* Effectively detect issues with HTTP services served from multiple data-centers concurrently
* Measuring CDN delivery speed, comparison to origin-only serving

**Example HTTP Server Test Results**

Here is an HTTP Server view for a test measuring the availability of the https://thousandeyes.okta.com/ service:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-4198198ef6b02cb375c6d3be0fb830036feae4ac%2Fproduct-documentation\_tests\_guide-to-thousandeyes-test-types-10.png?alt=media)

To interactively review the test results depicted above, visit the

[share link](https://bnleq.share.thousandeyes.com/)

and give it a go.

Page load tests use **te-chromium**, a browser based upon the Chromium browser codebase, to obtain in-browser site performance metrics. The metrics include the completed page load time and phase information for each DOM component. A complete explanation of how ThousandEyes presents DOM information is available here:

[Navigating Waterfall Charts for Page Load and Transaction Tests](https://docs.thousandeyes.com/product-documentation/browser-synthetics/navigating-waterfall-charts-for-page-load-and-transaction-tests)

. Instant page load tests provide a screenshot upon test completion, while scheduled page load tests provide screenshots when errors are recorded. A list of permitted content types is available in

[Permitted Content Types](https://docs.thousandeyes.com/product-documentation/browser-synthetics/page-load-tests/permitted-content-types-for-page-load-tests)

.

* Provide metrics regarding the in-browser use experience.
* Identify objects preventing or prolonging page load completion.
* Monitor performance across content providers.

**Example of Page Load Test Results**

Below is a page load test targeting

[Google](http://www.google.com/)

:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-797ef3fa92bc9047bf19325491cb8ef3ebb3ac9f%2Fproduct-documentation\_tests\_guide-to-thousandeyes-test-types-11.png?alt=media)

Transaction tests emulate user interactions with a website. This test performs a series of scripted steps - such as entering data into a form or clicking a button - and provides completion time and performance metrics obtained while performing scripted actions. Transaction tests use the Selenium WebDriver engine. Tests scripts are created using JavaScript, from the ThousandEyes Recorder IDE or within the test settings. You can set screenshots and markers at different points within the script to identify important points within the transaction workflow.

* Emulate common user interactions, such as completing a purchase.
* Alert on degradation of site performance.

**Example Transaction Test Results**

Below is a sample test that performs login and a search:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-20cd3903579773b42a636258bf52a9cab54f4877%2Fproduct-documentation\_tests\_guide-to-thousandeyes-test-types-20.png?alt=media)

For additional guidance on creating a Transaction test, see

A

[File Transfer Protocol](https://en.wikipedia.org/wiki/File\_Transfer\_Protocol)

server is an essential storage component of modern enterprises. This test supports FTP, FTPS, and SFTP protocols.

* Verify availability and performance of FTP server.
* Read, write, and list files within a user's directory.
* Verify SSH operation by selecting SFTP and performing a list test to any SSH enabled server.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-ca209dd98a415b30ef6fe289980d81c31ae65309%2Fproduct-documentation\_tests\_guide-to-thousandeyes-test-types-12.png?alt=media)

Visit this

[share-link](https://pewnnpen.share.thousandeyes.com/)

to get a sense of FTP Server tests.

Voice Layer tests look at whether a connection can be established (SIP), as well as testing the exchange of packets after the connection is made (RTP). SIP stands for Session Initiation Protocol and RTP is an acronym for Real-time Transport Protocol. These two actions enable Voice over IP connections. VoIP is a method for delivering voice communications and multimedia sessions over Internet Protocol (IP) networks. ThousandEyes provides a way to test the robustness and quality of these types of connections. Video tutorials:

[Working with Voice Tests](https://www.youtube.com/watch?v=KVFoHtHa\_1c)

and

[VoIP Monitoring with ThousandEyes](https://www.youtube.com/watch?v=KVFoHtHa\_1c)

.

A SIP Server test checks the availability of Session Initiation Protocol VoIP Server. Additionally, this test could be configured to perform SIP register. For more details, see

[Using the SIP Server View](<../../.gitbook/assets/using the sip server view>)

.

* Verifying performance of a VoIP SIP server.
* Confirming the ability to perform SIP Register with a target server.
* Identify the phase at which a SIP Register fails.
* Observe the SIP Register and Options request and response.

**Example SIP Server Test Results**

Here is a SIP Server test targeting an internal VoIP server.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-d3dd8a9e9682a362509e8fad47692e4e9b17da20%2Fproduct-documentation\_tests\_guide-to-thousandeyes-test-types-13.png?alt=media)

Here is a

[sample](https://puyxkx.share.thousandeyes.com/)

SIP Server test.

RTP Stream test measures the quality of Real-Time Protocol Voice stream between ThousandEyes agents acting as VoIP User Agents. For guidance on creating RTP Stream test, see

[RTP Stream Test Settings](<../../.gitbook/assets/rtp stream test settings>)

.

* Identify the node responsible for degraded RTP Stream.
* Analyze effects of BGP Route changes on RTP Stream.
* Measure call audio quality in terms of

**Example RTP Stream Test Results**

Here is an RTP Stream test between two Cloud Agents displaying Packet Delay Variation

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-54f7ebe3921470bf294f1149fe196d78763690ca%2Fproduct-documentation\_tests\_guide-to-thousandeyes-test-types-14.png?alt=media)

Check out this

[sample](https://khyxaxgy.share.thousandeyes.com/)

test to see an RTP Stream Test.

### Endpoint Agent-Based Tests <a href="#endpoint-agent-based-tests" id="endpoint-agent-based-tests"></a>

Endpoint Agent tests are classified in below manner:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-ddceb3266b98ab7b9c8f379e14081c83e6f48b80%2Fproduct-documentation\_tests\_guide-to-thousandeyes-test-types-16.jpg?alt=media)

Endpoint Agents record in-browser and network performance metrics whenever users navigate to monitored domains from monitored networks. Instructions on Endpoint Agent installation and configuration can be found in

[Configuring Endpoint Agent Setup](https://docs.thousandeyes.com/product-documentation/archived-documentation/configuring-endpoint-agent-setup)

.

An Endpoint Agent offers various views for unscheduled tests as below:

* Compare user experience across your organization.
* Identifying networks experiencing performance degradation.
* Identify DOM components affecting application performance.
* Identify network and wireless connectivity issues.

Below is a Browser Sessions view showing latency from an Endpoint Agent and visited domain details.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-5425468564765200b0b24df637c4a4596132050e%2Fproduct-documentation\_tests\_guide-to-thousandeyes-test-types-17-1.png?alt=media)

Visit this

[share-link](https://pkbaek.share.thousandeyes.com/)

to see an actual user sessions snapshot.

**Network - Agent to Server**

An agent-to-server test measures round-trip network performance between an agent and a remote server. The target may be either be an IP address or hostname.

* Measuring round-trip network performance from multiple vantage points.
* Monitor for, and comparing performance as a result of, network path changes.
* Verification of target availability.
* Identify network degradation along the network path.
* Verify network management of DSCP, MTU, and optimization.
* Monitor ingress traffic load distribution across ISPs.

**Example Agent-to-Server Test Results**

Here is an Endpoint-based agent-to-server test targeting

[thousandeyes.com](https://www.thousandeyes.com/)

with ICMP probing. The link highlighted in red is experiencing higher link delay.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-d85cff582e4328247925b15f5fc5bed79e800195%2Fproduct-documentation\_tests\_guide-to-thousandeyes-test-types-18-1.png?alt=media)

Visit this

[share-link](https://vlqwcxkz.share.thousandeyes.com/)

to see an Endpoint-based agent-to-server test.

An HTTP Server test measures the availability and performance of an HTTP service, whether public or private. HTTP server tests included network layer agent-to-server tests using either TCP or ICMP.

* Alert on HTTP availability and performance metrics by office or group of agents.
* Monitor web application performance from company workstations.

**Example HTTP Server Test Results**

Here is an Endpoint HTTP Server test on

[google.com](http://www.google.com/)

.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-ee41f6da96da75f2dc71034c42800aa6268e7ed7%2Fproduct-documentation\_tests\_guide-to-thousandeyes-test-types-19-1.png?alt=media)

Here is a

[sample](https://sibbhuzcd.share.thousandeyes.com/)

Endpoint HTTP Server test.

*   ThousandEyes also offers alert notification when a configured event occurs. See

    [How Alerts Work](https://docs.thousandeyes.com/product-documentation/alerts/)

    .
