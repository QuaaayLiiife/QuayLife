# Best Practices for Choosing the Right Test Protocol for Cloud and Enterprise Agent Network Tests

Whenever possible, always use the protocol that is as close to the actual payload as possible to gain the most reliable results.

* Most of the time, this will be TCP.
* Use UDP for agent-to-agent tests if you want to simulate media traffic.
* Use ICMP as a fallback option if TCP or UDP don't work as expected.

Tests that run from Cloud and Enterprise agents (CEA) can use different protocols for testing:

* TCP and ICMP for all tests
* TCP, ICMP and UDP for agent-to-agent tests

It is not always clear when to use each. This article aims to explain the best practices in choosing this setting.

Every test in ThousandEyes consists of two parts: An end-to-end measurement, which determines the end-to-end packet loss and latency, and the path trace, which builds the path visualization. For full details please look at

Network Tests Explained

​

In general, it's always advisable to test with the same protocol that the application uses. What that means we will explain in the next sections.

### Protocol Choices for End-to-End Tests <a href="#protocol-choices-for-end-to-end-tests" id="protocol-choices-for-end-to-end-tests"></a>

The choices for the end-to-end tests are mostly mandated by the test type performed and what is being measured. (For a full description of available test types, see

[Tests](https://github.com/thousandeyes/docs/blob/prod/product-documentation/best-practices/product-documentation/internet-and-wan-monitoring/tests.md)

.) For example, an HTTP server test will use HTTPS as the end-to-end test metric, whereas a voice test will use RTP as the test protocol.

​

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-0c4c642c7e748a24f893671f2be3698a578f3b53%2Fproduct\_documentation\_best\_practices\_how\_to\_choose\_the\_right\_test\_protocol%20for\_cloud\_and\_enterprise\_agent\_tests\_1.png?alt=media)

​

The first test type where the user must make a choice is the agent to server test.

Agent to server tests can be performed using either ICMP or TCP.

If we are testing a specific application on our destination host, it's always advisable to use a TCP test to the application specific port. So, if we test an SSH server, we use TCP/22. If we are testing an SQL server we use TCP/1433, etc.

This approach gives us more information about the actual service health: We are not only testing if a host is responding, but also if the service port is open and accepting connections.

By using the same protocol and port as the actual payload, we also ensure that the network between the agent and host handles the test traffic the same as the production traffic. This will yield the most reliable measurements, whereas ICMP might be handled with lower priority as compared to TCP.

Sometimes there is no TCP service port that you can connect to – either because of firewall rules, or because there just isn’t any TCP port open on the host tested. If this is the case, ICMP can still give reachability, and path information.

Another test where the payload is user configurable is the agent-to-agent test. For this test we can choose between TCP and UDP.

Agent to Agent tests are very useful in testing how a network behaves for a specific application payload, for example voice and video traffic.

​

![](https://2360053865-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4QARF6s57qxMrOHDTZ%2Fuploads%2Fgit-blob-cbd2e3d2c0c90f4a72b78f3a774269c5d25e1c79%2Fproduct\_documentation\_best\_practices\_how\_to\_choose\_the\_right\_test\_protocol%20for\_cloud\_and\_enterprise\_agent\_tests\_2.png?alt=media)

​

Most voice and video traffic uses UDP as transport protocol. Given the connectionless nature of UDP, it's not possible to test UDP traffic without control over both source and destination. Using an agent-to-agent test, with UDP as transport, and the right port and QoS markings, allows you to test end-to-end voice and video performance.

This flexibility in protocol, port numbers and QoS marking allows us to carefully mimic applications on the network. See

[Agent-to-Agent Test Overview](https://github.com/thousandeyes/docs/blob/prod/product-documentation/best-practices/product-documentation/internet-and-wan-monitoring/tests/network-tests/agent-to-agent-test-overview.md)

for further information about agent to agent tests.

When choosing the protocol, consider the goal of the test: What kind of traffic are we evaluating on the network? Once we know that, we can choose the right protocol, port and additional settings. As always, the more closely you can mimic actual applications on your network, the more reliable and business-relevant the test results will be.

The default port number used for agent-to-agent tests, both for UDP and TCP, is 49153. Sometimes, the path visualization doesn't work as expected due to this port being blocked in firewalls between source and destination. If that happens, try to work with your firewall administrators to have this port opened. If that's not possible, find a port that is open between source and destination to ensure the best possible measurements.

### Protocol Choices for Path Trace <a href="#protocol-choices-for-path-trace" id="protocol-choices-for-path-trace"></a>

Now that we've explained the end-to-end measurement, we can discuss the second part of the testing, which is the path trace. For the path trace, there are two options: ICMP, and TCP. In general the same considerations apply for path trace as for the end-to-end test. Wherever possible, use TCP. The path trace traffic will be treated the same as the actual payload, giving the most reliable output of the path trace. If TCP doesn’t give the desired result, mostly because of misbehaving firewalls in the path, ICMP can be used as a fallback.
