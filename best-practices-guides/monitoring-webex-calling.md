# Monitoring Webex Calling

The ThousandEyes - Webex collaboration expands the monitoring capability from Webex Meeting to include Webex Calling as well. This article outlines the best practices for monitoring Webex Calling functionality using Endpoint Agents, Enterprise Agents, and Webex Calling Cloud Agents.

* The Webex Calling architecture.
* How to identify the monitoring targets.
* Monitoring with Webex Cloud Agents.
* Alert and dashboard configuration options for call monitoring.

### Webex Calling Architecture <a href="#webex-calling-architecture" id="webex-calling-architecture"></a>

Webex Calling delivers a cloud-based phone system that allows users to dial in from IP phones or Webex apps through the internet. To learn more about configuring Webex Calling, see the

[Webex Calling Getting Started Guide](https://help.webex.com/en-us/article/nk1shtj/Get-Started-with-Webex-Calling)

.

Webex offers two calling solutions, based on a customer’s

[Calling Plan](https://pricing.webex.com/us/en/hybrid-work/calling/)

.

The Basic plan allows users to call anyone with a Webex account. For any users with Webex Meeting licenses, a **Call** button is available for making 1:1 calls to another Webex users’s account. As it doesn’t require any call services or routing, these type of calls use the Webex Meeting infrastructure instead of Webex Calling’s infrastructure.

For these users, the Webex application is the only available interface.

​

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-f312a6ab7150b89a9b3968b66dae7c73ac1d10b2%2F1.png?alt=media)

​

The Call (Professional) plan provides additional features beyond 1:1 calls, including allowing users to call any telephone number in a PSTN (public switched telephone network), providing voicemail services, call routing with extensions, and a phone menu. Each user needs to have their own phone number and location assigned in order to be able to initiate outbound calls.

Both the Webex application and registered VoIP devices can be used as the user interface.

​

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-c37b7c1ba9e6ec0496b52437b365aeb4864950d6%2F2.png?alt=media)

​

Incoming calls connect to Webex Calling cloud platform first, and are then routed to the local or international phone numbers via the pre-configured Local Gateway (CUBE) or PSTN Gateway, as shown in the topology diagram below:

​

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-4f5f038062f1bc9918e8de20e02ce973bbe2ca86%2Ftopology.png?alt=media)

​

The Webex client first sends a SIP (Session Initiation Protocol) call signaling using the TCP TLS connection via port 5062 or 8934 to the destination server. The Webex cloud will route the call to its destination, either to the PSTN or UCM (Cisco Unified Communications Manager Cloud) registered IP phones, or another Webex application user. Once the call session is established the Webex clients use a Secure RTP (Real-time Transport Protocol) connection for sending call media traffic via UDP port 5004, 19560-65535. This workflow applies to both call types.

### Identifying the Monitoring Targets <a href="#identifying-the-monitoring-targets" id="identifying-the-monitoring-targets"></a>

“Call on Webex” traffic is routed to the Webex Meeting data center based on the client geolocation. Therefore, the monitoring target could change based on the user’s network connection when users make a 1:1 call.

ASTs provide the network path for every single Webex call and meeting. In addition to the IP address, the destination node modal includes its network, ASN, and location.

This example shows a Webex call from Australia connected to the Webex Sydney data center (AS13445):

​

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-8844ac02d8ae3ee04595ce0953e31adc4fc8bf62%2Fpathvis.png?alt=media)

​

If the AST doesn't detect "Call on Webex", we recommend using the Webex Cloud Agents closest to the client geolocation.

On the other hand, “Premium Calling” doesn’t rely on the source network’s geolocation at all.

Instead, for every Calling user, it’s required to select a location and assigned phone number from the location. Webex will route the calls to the nearest data center from the pre-configured location country.

For example, the Webex user show below is configured for the location “Lima, Peru”. In this scenario, the default call routing is always to the nearest data center to Peru, regardless of where the call originates.

​

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-b33aa88a73845575ea60661a9af8244c977b076d%2F3.png?alt=media)

​

Webex Calling operates four regional platforms: North America, EMEAR, APJC (Japan) and APJC (Australia). Data and traffic are stored and processed within the regional platform. There are 8 data centers, listed below. We suggest monitoring the data centers from the nearest region.

For Webex Caller A above, the suggested data centers would be Chicago and Dallas.

| AMER             | EMEA               | APJC (AUS)           | APJC (JP)    |
| ---------------- | ------------------ | -------------------- | ------------ |
| Chicago, IL, USA | Frankfurt, Germany | Melbourne, Australia | Osaka, Japan |
| Dallas, TX, USA  | London England     | Sydney, Australia    | Tokyo, Japan |
| Montreal, Canada | ​                  | ​                    | ​            |
| Toronto, Canada  | ​                  | ​                    | ​            |

​

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-d885502d6118f562a1875c6a93221aa975f85362%2Fdc.png?alt=media)

​

### Monitoring with Webex Cloud Agents <a href="#monitoring-with-webex-cloud-agents" id="monitoring-with-webex-cloud-agents"></a>

Following the same approach of

[Monitoring Webex Meetings](https://docs.thousandeyes.com/product-documentation/best-practices/monitoring-webex-meeting-with-cea)

, specially designated ThousandEyes Webex Cloud Agents can be used as the target agent of Agent-to-Agent and RTP tests for complete end-to-end connectivity from your network. For this purpose, we recommend deploying an Enterprise Agent on the same network where the Webex devices are deployed or the Webex applications are connected as the source agent.

An **Agent-to-Agent TCP Test** - between any applicable Enterprise Agents and the Webex Cloud Agent hosted within the same regional Data center. You should use (TCP) 5062 or 8934. This will measure the inbound performance of SIP call signaling traffic into the Webex Cloud. **In Session Path Trace** should be enabled. The DSCP value should be set to CS3 (DSCP 24).

​

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-95224502291096fe3b241ca5078e9e385adc8a7b%2Ftcp1.png?alt=media)

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-f6d5d348a4d4c53bf52cabaab6ab2837915b59ec%2Ftcp2.png?alt=media)

​

An **RTP Stream Test** - between any applicable Enterprise Agents and the Webex Cloud Agent hosted within the same regional Data center. You should use port 5004 or anything between 19560-65535. This will measure the inbound performance of media traffic into the Webex Cloud. The DSCP value for the Audio test should use EF (DSCP 46) and for the Video test should be set to AF41 (DSCP 34).

​

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-f84c01dac76b6b6acb9817d77d12e4facb4a0e78%2Frtp1.png?alt=media)

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-670adeef0b62f24aa8a2d685e206aab9c16e2b3a%2Frtp2.png?alt=media)

​

An **Agent-to-Agent UDP bidirectional Test** - between any applicable Enterprise Agents and the Webex Cloud Agent hosted within the same regional Data center. You should use port 5004 or anything between 19560-65535. This will help you understand simulated, bidirectional performance of call media traffic into the Webex Cloud environment. The DSCP value for Audio should use EF (DSCP 46) and for Video the value should be AF 41 (DSCP 34).

​

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-aa8129cede4bee264117d09086785dc9679a89b9%2Fudp1.png?alt=media)

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-c2ae6d55ca326628d24ca28f3491f36fc573d218%2Fudp2.png?alt=media)

​

### Alert and Dashboard Configuration Options for Call Monitoring <a href="#alert-and-dashboard-configuration-options-for-call-monitoring" id="alert-and-dashboard-configuration-options-for-call-monitoring"></a>

For agent-to-agent tests, the following alert conditions should be configured to capture any network issues, as high jitter can contribute to call quality issues like jumbled audio and should be further investigated.

* Latency > Dynamic 2 std deviations

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-85c12bd7c45284aeeb49b2ecfb2cd78e52e81f7f%2F4.png?alt=media)

For RTP tests, the following conditions should be alerted on to capture outstanding call degradation. In order to exclude the one-off outlier we recommend using the same agent with multiple occurrences:

* Packet Delay Variation > 2 standard deviation

​

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-cf1774031784555a2d958ead4d9a09faeb9101a4%2F5.png?alt=media)

​

Another key performance you should monitor is BGP, which is included in the RTP and agent-to-agent test. We recommend alerting for any AS changes of the Webex Data Centers as that would involve a routing change that consequently could result in latency and change in the call dynamics.

Start with the BGP Route Visualization layer in the test view and verify the current ASN of the target Cloud Agent. In the example below, the Frankfurt Webex Agent is using AS21534 (Adoption Technologies).

​

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-60dabb657057d78641265bf1e23bb632cbd9066a%2F6.png?alt=media)

​

Then, create an alert condition to catch the ASN change on the last hop from the original value as follows. We recommend using 10% of monitors to exclude the outlier monitors:

​

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-be5b1193f8bc185a43e382aabacfe45d9f38b0d3%2F7.png?alt=media)

​

Adding a dashboard can easily help visualize which Webex Calling location is affecting user call quality. The live widget Alert List / Test provides a quick overview of the test comparison and active alerts:

​

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-2eb2b955e26e7883b3c483b4250869fb90a82028%2F8.png?alt=media)

​

For the network test we recommend using the Color widget for each of the network metrics, and categorize the card by “Target Agent”. Since we only have eight locations, there is no need for grouping. This widget will tell you the location that has poor performance. In the example below, Frankfurt shows higher latency and jitter:

​

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-b2c29241ea1c739d52bcd778b922885fb51bf824%2F9.png?alt=media)

​

Then, you can use a Box and Whiskers or Line widget to monitor the specific location’s performance in the timeline. Make sure to use the Group by ‘Target Agent’ as your setting:

​

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-9207087f2ea1d4b2ed483137406d99a843ea6572%2F10.png?alt=media)

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-ed20ef2233f98b405d061feed07ef795aac668af%2F11.png?alt=media)

​

For the RTP tests, a multi-metric table is more useful to show the overall RTP performance. Use Test for Row, and each of the RTP metrics for columns as shown in the image below. In this example, you can see the Frankfurt location also shows the poor performance in context with the network test results:

​

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-44b2b5a2c8a4014aa7705bb49ff50723702618d9%2F12.png?alt=media)

​

A map widget, grouped by ‘Target Agent’ can also help to easily pinpoint the location of issues:

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-28f84e53aa46f5fa64aa8c86220bd7a6a4afd01f%2F13.png?alt=media)

Alert rules and dashboards are critical for active monitoring as they help to quickly isolate the actual issue in the Webex calls before the users report to your team. Cisco Webex also uses ThousandEyes for monitoring their infrastructure. Thus, when opening a TAC case, you can share the snapshot links from your test and dashboard with the Webex Support team and resolve issues faster.
