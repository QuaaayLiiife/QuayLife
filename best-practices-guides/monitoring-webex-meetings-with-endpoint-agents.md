# Monitoring Webex Meetings with Endpoint Agents

The ThousandEyes - Webex collaboration provides visibility into the network health of Webex meetings, utilizing ThousandEyes Endpoint Agents to monitor the Webex experience and provide insights into call quality.

In this article, we’ll look at how to monitor Webex meetings by leveraging Endpoint Agents, Webex Cloud Agents, and the Webex Control Hub.

* Deploy ThousandEyes Endpoint Agents.
* Understand Webex architecture.
* Monitor Webex Web Zone with HTTP tests.
* Monitor Webex Meeting Zone with automated session tests (AST).
* Integrate with Webex Control Hub for advanced troubleshooting practices.
* Exclude any local connection issues.
* Use Webex Cloud Agents for monitoring UDP traffic.

For leveraging the endpoint monitoring, we recommend installing Endpoint Agents for all Webex users. ThousandEyes offers two ways to deploy Endpoint Agents.

​

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-6f09ffeb6d796441d62f872f8cf0000c5b45986d%2Finstallation.png?alt=media)

​

The second option, provide the download link to anyone with devices not managed by the IT team. The download link contains your Account Group token, which would automatically register the installed Agents to your Account Group.

Any new Endpoint Agents will consume an Agent license. So you’ll want to ensure you have unused licenses in your Account. The download link is valid provided the “Allow anyone with the link to download” option is enabled. To avoid over-subscription of licenses, limiting the users who have access to the link is recommended. In case you would like to limit access to this link, use “Generate new links” to refresh the link.

​

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-99f46960238f1483cec297cf105edc185bb2eb06%2Finstsallationlink.png?alt=media)

​

Once the Agent installation is complete, you will see the new Endpoint Agents under https://app.thousandeyes.com/endpoint/agent-settings/?section=agents including their associated status.

​

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-4ebefc26eb1722ba8855f19d988eab6a471a1f8d%2Flist.png?alt=media)

​

### Understand Webex Server Structure <a href="#understand-webex-server-structure" id="understand-webex-server-structure"></a>

Now that you have deployed Endpoint Agents to the end user's hosts, you can configure Webex performance monitoring. To plan the best tests, let’s look into the Webex meeting structure first.

Webex is a cloud-based service hosted in various Cisco-owned data centers and cloud service providers worldwide. As components are regionally hosted, this adds extra challenges to troubleshooting specific to Webex components.

​

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-48916d39dfabe98250a389e4d330f36229908b20%2Farchitecture.png?alt=media)

​

The Webex data center is logically divided into the Meeting Zone and the Web Zone. The Web Zone is responsible for what happens before and after a web meeting, along with scheduling, user management, billing, reporting, and streaming recordings. The Meeting Zone is responsible for switching the actual meeting once it is in progress between the endpoints and consists of two subsystems; the Collaboration Bridge (CB) and the Multimedia Platform (MMP).

When users click “Join the meeting” link of Webex, their browser launches to the specific Webex meeting page that indicates “Starting the meeting”. The meeting URL usually consists of {instance}.Webex.com/{meetingIdentifier}.

​

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-0ad5c2e0778fcefe8757fe288c1c88e449e3ebff%2Fstartmtg.png?alt=media)

​

At this stage, the client connects to the nearest configured “Web Zone” Data Center which is responsible for what happens before and after a web meeting. The Web Zone for an instance is always located in the primary data center, no matter where the client connects from, the client will connect to the same server. If the Web Zone is non-functional or inaccessible, the Webex meeting will not be able to launch and the below error message will pop up.

​

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-175463df5ca177c216ab289ce9065311267e236d%2Fglitch.png?alt=media)

​

In other words, the availability of Web Zone decides whether the client can launch the meeting, schedule the meeting, or access the Webex instance. Monitoring Webex Web Zone is very straightforward as every Webex instance uses the unique CNAME: {instance}.Webex.com, i.e. cisco.webex.com. Simply create a scheduled HTTP server test targeting https://cisco.Webex.com with Prefer TCP mode (SACK is recommended, see the explanation in

[this guide](https://docs.thousandeyes.com/product-documentation/end-user-monitoring/automated-session-test/configure-automated-session-tests#create-an-automated-session-test)

).

Webex Web Zone monitoring provides visibility into issues associated with the session initiation, such as ‘why my Webex meeting doesn’t connect?’, but not about the bridge quality.

​

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-43269676dec60155a0abbe66ab3133ca4e3392ad%2Fhttp.png?alt=media)

​

### Monitor Webex Meeting Zone <a href="#monitor-webex-meeting-zone" id="monitor-webex-meeting-zone"></a>

When you schedule a Webex meeting, session initiation traffic is sent to the Web Zone, but when a call is in progress, audio, and video traffic is directed to the collaboration, control and media servers in a completely different location. Meeting Zone data center hosting the ‘Collaboration bridge’ and ‘Multimedia Platform’ servers which are located globally and usually will connect to the one that is closest to the end user.

If you want to monitor Audio/Video traffic, you need to identify the MMP server. So how can this be accomplished? Unlike the Web Zone's data centers, the Media Zone's servers are hidden from the end users. Running a packet capture during Webex meetings, the destination address for “UDP” traffic will show the MMP server that serves the audio/video traffic. As you can see, Webex Client uses the random port for the source UDP port, and 9000 or 5004 for the destination UDP port.

​

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-ecfa17be0a75a81f19e1385f87ee241537c6d5f5%2Fpcap1.png?alt=media)

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-5dcb0d6f8e2d9e361bcb5393fd4de438d410498e%2Fpcap2.png?alt=media)

​

Based on the above packet capture, you can see 64.68.96.110 is the target MMP Webex server for this client's session. Though, troubleshooting using packet captures for every Webex session is not ideal for the lean IT team, the MMP servers are dynamic and could change depending on the end-user connection ie. VPN. Endpoint Automated Session Tests extended the ability to monitor this ‘moving target’ based on the actual audio/video traffic.

Create Automated Session Test under Endpoint Agent following

[this guide](https://github.com/thousandeyes/docs/blob/prod/product-documentation/best-practices/product-documentation/end-user-monitoring/automated-session-test/configure-automated-session-tests/README.md#create-an-automated-session-test)

. To achieve the best outcomes, we recommend to use the below configurations.

​

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-ec7c3f0494c4669dfc140b5ae209426e28c97ca2%2Fbasic.png?alt=media)

​

1.  1\.

    Select “Webex” for Target
2.  2\.

    Select “Auto-detect” protocol to allow Endpoint Agents automatically selecting best protocol for monitoring. Note: As UDP is not supported, TCP or ICMP would be selected.
3.  3\.

    Select “1 minute” interval to ensure the meeting sessions are consistently monitored
4.  5\.

    Select the number of Agents which covers all of end users using Webex client

Using this test configuration the Endpoint Agent will automatically detect the MMP server for the active Webex meeting and execute the test for the same targets in parallel. When the meeting concludes the tests will be shut down. In the event that the Endpoint’s host IP address changes, the Webex client changes the connection to the new server geogrphically assigned, then the test will also automatically change the target to the new IP address. In the below example, the Webex Client connected to 4 Webex servers on this round, and one of the paths clearly shows the forwarding loss.

​

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-76cc7f74a0782c3d2f47a060c73923bcf4a70292%2Fast1.png?alt=media)

​

Currently, AST only can be executed using TCP or ICMP, thus the end-to-end loss doesn't exactly correspond to the meeting’s audio/video quality but latency/jitter metrics are shown inline. The most useful information from AST is the network path that shows the node causing the loss as well as you can tell how many Endpoints have been affected by this node/hop.

​

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-6ab1e78a58cebef2e546157aa7e441d1bde8bee2%2Fast2.png?alt=media)

​

### Integrate with Webex Control Hub Troubleshooting <a href="#integrate-with-webex-control-hub-troubleshooting" id="integrate-with-webex-control-hub-troubleshooting"></a>

If you are the administrator of your Webex Organization instance, you can monitor the active or past meetings performance via Control Hub Troubleshooting tool (https://admin.Webex.com/diagnostic/meeting). Endpoint Agent AST data is integrated into Webex Control Hub to provide insights into the network path data. Refer to the

[Webex Control Hub integration guide](https://docs.thousandeyes.com/product-documentation/integration-guides/integration\_with\_webex\_controlhub.md)

to set it up.

Next, locate the meeting that you want to troubleshoot from either the “Live Meetings” tab or searching by Conference ID or Username under the “Meetings & Calls” tab.

​

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-54c335135cc4b92f5967f11872611132cb84464c%2Ftroubleshooting.png?alt=media)

​

From the meeting summary view, you can see each participant’s Audio / Video / Sharing’s Signal qualities in the timeline. Drilling down, if you click each participant’s tab, you can find the full metrics collected by Webex clients. If an Endpoint Agent was running on the same host, you will find the “Network Path” data, which was collected by the Endpoint Agent using AST.

The recommended steps to use this tool for troubleshooting is:

1.  1\.

    Spot dropped signals from the meeting view
2.  2\.

    Select the specific participants
3.  3\.

    Find the bad quality round, and click on Network Path
4.  4\.

    Find the network causing the forwarding loss

​

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-67e49587fdd95866b9e42e9b5cf3d88231bf3c9f%2Fhub.png?alt=media)

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-d4d83567b61e6b39e54e05fd889e391fd18c7b78%2Fnetpath.png?alt=media)

​

Please note this integration is limited to the voice over IP encoded sessions only. Traditional PSTN encoded voice won't show Network Path data.

​

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-e91378b543e19c2292a989f269060523b46ba833%2Fnopath.png?alt=media)

​

### Exclude Local Connection Issues <a href="#exclude-local-connection-issues" id="exclude-local-connection-issues"></a>

While Network path visualization is very helpful for diagnosing the issues on the ‘route’, quite often the local connection is the bottleneck. Wireless signal, gateway loss, VPN loss can contribute to the poor quality of a user’s meetings and it’s hard for a network test to isolate the issue. We recommend also leveraging the Agent View of the Endpoint Agent where you can correlate test data with the local host metrics in the same timeline. Please refer to the

[Agent View page](https://docs.thousandeyes.com/product-documentation/end-user-monitoring/viewing-data/single-agent-view.md)

for the navigation path and more detailed information. In the below case it’s clear that VPN loss is the culprit.

​

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-1bc4c7568cc01c67444657f18b5ac8d0af7a7351%2Fagentview.png?alt=media)

​

### Use Webex Cloud Agents for Monitoring UDP Traffic <a href="#use-webex-cloud-agents-for-monitoring-udp-traffic" id="use-webex-cloud-agents-for-monitoring-udp-traffic"></a>

Since Endpoint Agents are limited to TCP or ICMP monitoring, Enterprise and Cloud Agents allow UDP traffic monitoring through Agent to Agent tests. Moreover, ThousandEyes deployed Cloud Agents in the Webex Data Centers solely for monitoring the traffic into the Webex infrastructure. Once you find the target MMP server that serves your Webex clients, you can set up a UDP test from Enterprise Agent from the same network toward the Webex Cloud Agents located in the same data center.

In AST’s Path Visualization view, you can find the destination server’s location. In the below example, the next step will be testing to ‘Dallas Webex Cloud Agent’.

​

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-2392cc71cc7a3559b1b7cbb1f10abed6ba6c9f89%2Flocation.png?alt=media)

​
