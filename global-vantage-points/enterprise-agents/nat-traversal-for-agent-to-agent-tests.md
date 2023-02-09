# NAT Traversal for Agent-to-Agent Tests

An agent-to-agent test permits ThousandEyes users to monitor two endpoints and visualize the network path in both directions, which can mean faster, more accurate identification of problems than with an agent-to-server test. However, unlike an agent-to-server test, where the test target is typically intended to receive network traffic initiated by other hosts, in an agent-to-agent test often one or both agents cannot receive network traffic initiated by other hosts, either from the public Internet or from other network locations. Changes to network address translation (NAT), port address translation (PAT) and/or stateful packet filter (SPF, i.e. firewall) rules would normally be required to allow the test traffic.

To avoid the need for changes, ThousandEyes provides a NAT traversal feature, which allows the agent-to-agent test traffic to work in conjunction with typical NAT/PAT/SPF configurations. NAT traversal in the ThousandEyes platform is implemented through a proprietary method similar to NAT traversal methods described in IETF standards such as RFC 5382. Agents behind NAT devices will register with the ThousandEyes NAT traversal server in order to discover the agents’ NAT and PAT characteristics, then use the discovered information when performing agent-to-agent tests.

### When to Use NAT Traversal <a href="#when-to-use-nat-traversal" id="when-to-use-nat-traversal"></a>

If an agent-to-agent test fails with an error indicating that one or both agents cannot reach the opposite agent, NAT traversal is likely to be required. An agent requires NAT traversal if the following are true:

1.  1\.

    The Enterprise Agent is behind a NAT and/or PAT device

    Check the Agent Settings of the Enterprise Agent. If a Private IP address is present, the agent is behind a NAT, and will likely need NAT traversal for agent-to-agent tests. Port address translation will normally be done in conjunction with network address translation. Stand-alone port address translation is less common, but if you are port forwarding a public port to a different private port, then you will also need NAT traversal.
2.  2\.

    Inbound communication to the agent is blocked

    Your firewall/NAT device prevents communications initiated from the public Internet to the Enterprise Agent, and only allows the agent to initiate communications outbound to destinations on the public Internet.
3.  3\.

    Test **Direction** configuration

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-c89678a6cca7579ed95cf0bd6972df6b03aaeb85%2Fproduct-documentation\_enterprise-agents\_nat-traversal-for-agent-to-agent-tests-1.png?alt=media)

* The **Direction** selector on the agent-to-agent test is “Both Directions”, and the above two conditions are true for one or both Enterprise Agents
* The **Direction** selector is “Source to Target” and the above two conditions are true for the Target Enterprise Agent
* The **Direction** selector is “Target to Source” and the above two conditions are true for the Source Enterprise Agent

### Configuring NAT Traversal <a href="#configuring-nat-traversal" id="configuring-nat-traversal"></a>

Configure the NAT traversal feature by checking the **Behind a NAT** box under the agent's **Advanced Settings** tab on the **Settings > Enterprise Agents** page.

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-15945eda8f8b651ca83cc4bfc148966de1586f11%2Fproduct-documentation\_enterprise-agents\_nat-traversal-for-agent-to-agent-tests-2.png?alt=media)

**NOTE:** Because the NAT traversal feature is set on a per-agent basis (rather than a per-test basis) the NAT traversal feature will affect all agent-to-agent tests in which the agent participates.

When configured for NAT traversal, an Enterprise Agent will perform a NAT traversal compatibility check every five minutes, beginning when the agent contacts the ThousandEyes collector the first time after the **Behind a NAT** box on the Agent Settings is checked.

Note that the agent will contact the collector once per minute, and must first download the new configuration, perform the check and then wait for the next contact with the collector to upload results of the compatibility check. Thus, the results of the initial check may require up to two minutes to be displayed.

If the compatibility check determines that NAT traversal will not work for a particular agent, the check displays an error on the **Agent Settings** page, indicated by a red triangle icon, along with the following message:

**NAT Issues: NAT traversal not supported**

If the check fails, consult the requirements for NAT traversal in the following section.

### NAT Traversal Requirements <a href="#nat-traversal-requirements" id="nat-traversal-requirements"></a>

The requirements for NAT traversal to function properly are listed below.

1.  1\.

    Agent can contact ThousandEyes’ NAT traversal server

    Ensure that the agents can initiate outbound connections to **ntrav.thousandeyes.com** on destination TCP ports 9119 and 9120 when TCP is chosen as the protocol in the agent-to-agent test, and on TCP and UDP ports 9119 and 9120 when UDP is chosen.

    Failure of an agent to contact the ThousandEyes NAT traversal server will result in a test error message:

    **Failed to negotiate NAT traversal with (source/target) agent**
2.  2\.

    Symmetric NAT is an implementation of NAT in which outbound packets from the translated device a) have port address translation performed on the source ports, and b) the translated source port number is not constant for different destination IP address/port pairs (see

    [RFC 5382](https://tools.ietf.org/html/rfc5382)

    for formal definitions of types of NAT).

    For example, a client sends packets from source port 10000 to a server on port 80. The client’s firewall translates the source port to 50000. Immediately thereafter, the client sends packets from source port 10000 to another server (different IP address) on port 80. The firewall translates the source port to 50001. The NAT is symmetric, and will not work with NAT traversal.

    Symmetric NAT of an Enterprise Agent’s communication will result in a test error message:

    **Connection to (source/target) agent failed**
3.  3\.

    Firewall/NAT device(s) honor TCP keep-alives

    An agent configured to use NAT traversal registers with the ThousandEyes NAT traversal server using a long-lived TCP connection. The connection is kept open indefinitely using TCP keep-alives. This is done because the public port of this TCP connection is part of the registration data, and is given to other agents in order to send inbound agent-to-agent test traffic. The inbound test traffic uses the public port as the test traffic’s destination port (see the following requirement for TCP simultaneous open). If long-lived connections were not used, then it is possible that the public port would change over time. We do not want the public port number to change, since a change would be disruptive to the test, hence the requirement to support long-lived TCP connections.

    Most firewall and NAT devices will honor keep-alives. If NAT traversal fails, check your firewall or other NAT device to see if there are hard limits on the length of time a TCP connection can be maintained. Of course, reboots or other actions that clear the NAT and/or state tables of firewalls or NAT devices can disrupt a connection between agent and ThousandEyes NAT traversal server, as well.

    Failure of a firewall/NAT device to honor TCP keep-alives will result in a test error message:

    **Failed to negotiate NAT traversal with (source/target) agent**
4.  4\.

    Firewall/NAT device(s) support TCP simultaneous open (TCP-based tests only)

    When an agent-to-agent test uses TCP, the NAT traversal feature makes use of a TCP state called “simultaneous open”, which replaces the more common “three-way handshake” sequence of three packets (SYN packet sent, SYN-ACK received, ACK sent) with a four-packet sequence (SYN packet sent, SYN-ACK received on both ends). This allows both agents to initiate inbound traffic using the public port discovered in the registration with the NAT traversal server.

    Most firewall and NAT devices support TCP simultaneous open. NAT/firewall devices that do not support TCP simultaneous open will not work with NAT traversal for TCP-based agent-to-agent tests. UDP-based agent-to-agent tests do not have this requirement.

    Firewall/NAT devices that do not support TCP simultaneous open will result in a test error message:

    **Connection to (source/target) agent failed**
5.  5\.

    When using NAT on a target server via UDP, the target agent must have a public IP configured. During the NAT UDP test initialization, both agents will send packets to the ThousandEyes NAT traversal server. The server then examines the packets to determine which IP addresses to tell the agents to use. If an agent only has a private IP and is the target of the test (an agent-to-agent, RTP stream tests setup to use UDP), the ThousandEyes NAT traversal server will not provide the private IP of the packets it received to the source agent.

    This is expected behavior, and means that you cannot target an Enterprise Agent behind a NAT that does not have a public IP Address using UDP.

If an Enterprise Agent fails its NAT traversal compatibility check, or your agent-to-agent test fails to return data in one or both directions even when NAT traversal is configured on both Enterprise Agents, please check your firewall or NAT device logs for packets to the agent IP address and port configured for the agent-to-agent test, then contact the Customer Engineering team via email (

\[email protected]

) or via our in-app live support chat.

Consult the following RFC documents for additional background on NAT traversal:
